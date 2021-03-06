---
layout: post
title:  "Improving TextView & Spannable Performance"
date:   2020-10-12 21:50:30 +0200
categories: android ui
---

You probably encountered **Spannables** at some point in your android journey but just to remind you, they are used in order to apply styling to text.

A fact that you might not have known is that there are a lot of span types such as
* [ForegroundColorSpan](https://developer.android.com/reference/android/text/style/ForegroundColorSpan)
* [ImageSpan](https://developer.android.com/reference/android/text/style/ImageSpan)
* [ClickableSpan](https://developer.android.com/reference/android/text/style/ClickableSpan)
* and [many more &hellip;](https://developer.android.com/reference/android/text/style/package-summary)

In this article we will look at how to use **Spannables** in a more optimized way!
### The Problem
In one of my apps named [HTML/CSS Website Inspector](https://play.google.com/store/apps/details?id=web.dassem.websiteanalyzer) I've had to implement a search feature - the user could search through website's source code and a given query would be highlighted.<br />
In order to highlight search results I've decided to use [BackgroundColorSpan](https://developer.android.com/reference/android/text/style/BackgroundColorSpan).

The problem that I encountered was that updating **Spannable** on search query change was very slow and caused UI lags.<br />
This was probably because I was working with a lot of text - the website's source code can sometimes be massive. In order to view source code of **google.com** you can simply type `view-source:https://www.google.com/` in **Chrome** browser address bar. And yes that's a lot of text!

It appears that the below code was the one to blame
~~~
editText.setText(updatedSpannable)
~~~
{: .language-kotlin}

On every search query change I would update `editText` using `setText` method passing my updated **Spannable** string which caused UI hangs. <br />

### The Solution
But worry not, there is a more optimal way to do this.

But first some explanation, whenever we call `setText` there is a lot happening behind the scenes - measuring, drawing and extra objects are being created.<br />
In order to improve performance we basically can't call it too often and we don't need to really - here is how we can work with **Spannable** and use `setText` method only once.

First we need to set the text as **Spannable** to `editText`
~~~
editText.setText(spannableString, BufferType.SPANNABLE)
~~~
{: .language-kotlin}

After that whenever we need to edit a **Span** we can simply retrieve it from `editText` by calling

~~~
val spannable = editText.text as Spannable
~~~
{: .language-kotlin}

Any changes to the Spannable object will automatically be reflected in the UI - in my case `editText`. <br />
That's it! No need to call `setText` again!

In this post we have learned how to use **Spannables** in a more optimized way.
