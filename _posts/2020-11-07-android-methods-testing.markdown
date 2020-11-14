---
layout: post
title:  "Unit Testing objects with Android API references"
date:   2020-10-21 21:50:30 +0200
categories: android testing
---

In an ideal world every class in the old codebase would be ready for testing - the dependencies would be provided via the constructor, there would be no Android APIs used inside Presenters...<br />
Sorry to wake you up just now but you're not living in an ideal world... <br />
The Global pandemic is a thing and people are writing code like there is no tomorrow!

In this article we will talk about what you can do when encountering **Android API** classes inside objects under test.

## Refactor
The best solution and the one that needs to be considered first is trying to refactor the class itself.
Having **Android API** classes in objects that need to be unit tested is usually a code smell - references to **Android SDK** should, in most circumstances, reside in a given **View** class (**Fragment/Activity**).

If you're familiar with **MVP** or **MVVM** architecture you probably know that **ViewModels** and **Presenters** should not need to know about details of showing the UI.
This allows for a separation of concerns and more testable, easier to understand code.

So in most cases you should try to refactor the code so that it doesn't contain any Android framework references.
It shouldn't be too hard and you will thank me later on.

## Workaround
As I mentioned earlier we're not living in the ideal world and in some circumstances you won't be able to refactor the class itself.<br />
I remember that at one point in my career I was tasked with improving the test coverage of our codebase.
Despite argumentation management did not allow for refactoring, they just wanted to improve testing coverage fast, probably so it looks good on slides.<br />
In these cases well... you need to suck it up and get your hands dirty!

For the purpose of the article I will use a very simple **MainViewModel** class along with **android.util.Base64** reference.

~~~
import android.util.Base64

class MainViewModel : ViewModel() {

    private val mode = Base64.DEFAULT

    fun encodeData(text: String): ByteArray {
        return Base64.encode(text.toByteArray(), mode)
    }
}
~~~
{: .language-kotlin}

The unit test will look like the following

~~~
import java.util.Base64

internal class MainViewModelTest {

    private val mainViewModel = MainViewModel()

    @Test
    fun `test encoding`() {
        val text = "text"
        val encodedText = mainViewModel.encodeData(text)
        val decodedText = String(Base64.getDecoder().decode(encodedText))

        assert(text == decodedText)
    }
}
~~~
{: .language-kotlin}

Now if you try to run the code you might see the following errors

~~~
java.lang.NullPointerException: Base64.encode(text.toByteArray(), mode) must not be null
~~~
{: .language-kotlin}

or

~~~
java.lang.NoClassDefFoundError: android/util/Base64
~~~
{: .language-kotlin}

That happens because tests don't have access to Android framework classes. <br />
Now lets see whether there is something we can do to fix the error without refactoring **MainViewModel**.


### Create local version of the Android API reference
As mentioned by default the test throws an error when some code under test is not available.
However we can workaround this by simply creating our local version of the class that will return what we want.

In our case the missing class is **android.util.Base64** and its **encode** method.

Therefore we can simply create **Base64** class inside `android.util` package which we will place under test directory.

~~~
package android.util;

public class Base64 {

    public static byte[] encode(byte[] input, int flags) {
        return java.util.Base64.getEncoder().encode(input);
    }
}
~~~
{: .language-kotlin}

Now the test will pass since the class will be available.
That's it!

In this article we've learned what to do when encountering Android API references inside objects under test.
