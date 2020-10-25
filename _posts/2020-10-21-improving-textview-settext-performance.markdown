---
layout: post
title:  "Improving TextView setText performance"
date:   2020-10-21 21:50:30 +0200
categories: android ui
---

In previous post we have looked at how we can improve performance when working with **TextView** and **Spannable**.

In this post we will explore ways to make setting of text on **TextView** faster.

If you look at the source code of `setText` method you can see that it does a lot of heavy lifting - there is measuring, drawing and object allocations, all of which run on the main thread. <br />
That is why setting a large amounts of text on a **TextView** might result in UI stutters and hangs, not the smooth experience the user expects.

Fortunately for us there is something that can help us to remediate that - [PrecomputedText](https://developer.android.com/reference/android/text/PrecomputedText), in this post we will look at how we can use it to improve **TextView** performance.

## PrecomputedText

In simple terms **PrecomputedText** is a text object that contains both the text and layout measurements. When we use it to set text on a **TextView** no further layout calculations are required which is why it will be faster.

### TextView

In order to create **PrecomputedText** we need to pass the text and **TextMetricsParams** of the target **TextView** to `PrecomputedTextCompat.create` method.
Since it does heavy text layout measurements its best to call it from a background thread.

In the below code snippet we can see a full example using [Kotlin coroutines](https://github.com/Kotlin/kotlinx.coroutines)

~~~
private fun TextView.setTextAsync(text: String) {
    val textView = this
    lifecycleScope.launch {
        val params = TextViewCompat.getTextMetricsParams(textView)
        val precomputedText = withContext(Dispatchers.Default) {
            PrecomputedTextCompat.create(text, params)
        }
        TextViewCompat.setPrecomputedText(textView, precomputedText)
    }
}
~~~
{: .language-kotlin}

Now I haven't measured the performance differences myself.
However according to [Google](https://android-developers.googleblog.com/2018/07/whats-new-for-text-in-android-p.html) measuring text can take up to 90% of the time required to set the text.<br />
Thanks to the above code snippet we can do all of that in the background without blocking the main thread.

### EditText
Since **EditText** is a thin layer on top of **TextView** you might expect the above to work on **EditText** as well.
Well you are wrong.

**PrecomputedText** appears to work only with **TextView** and **StaticLayout**. You might try to use **EditText** with the above code snippet but the result will be exactly like calling `setText`.

Looking at the source code of **TextView** there is a check in the `setText` method

~~~
if (type == BufferType.EDITABLE || getKeyListener() != null
        || needEditableForNotification) {
            ...
        }
~~~
{: .language-kotlin}

If the `type` is `BufferType.EDITABLE` (**BufferType** used by **EditText**) then the `precomputedText` will not be used.

Thanks for reading! <br />
In this post we have learned have to make `setText` method of **TextView** faster!
