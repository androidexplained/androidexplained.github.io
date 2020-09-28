---
layout: post
title:  "Webview Dark Theme Support"
date:   2020-09-24 21:50:30 +0200
categories: ui android material-design
---

In the previous post we've looked at how we can add **Dark Theme** support to our app.<br />
Full of hope you tried to test your app and everything went well until you stumble upon a **Webview...** <br />
By default **Webview** will assume **Light** theme version, breaking your dark theme user experience. <br /> <br />
Terrible, I know - fortunately for you I'm going to look at how to add **Dark Theme** support to **Webview** as well.

### Implementation
First of all you need to add `android.webkit` dependency into your project

`build.gradle`
~~~
dependencies {
    implementation "androidx.webkit:webkit:1.3.0"
}
~~~
{: .language-xml}

At the time of writing this post the latest stable version of `webkit` is `1.3.0`. <br />
It is worth noting that the **Dark Theme** support has been added with version `1.2.0`, before this version it was impossible to add **Dark Theme** support to **Webview.**

Next step would be to check whether **Webview** and **Android framework** on user's device supporting theming:

~~~
if (WebViewFeature.isFeatureSupported(WebViewFeature.FORCE_DARK)) {
  ...
}
~~~
{: .language-kotlin}

Please note that `WebViewFeature.FORCE_DARK` is only supported starting with **Webview** version **76**.
Unfortunately before that version there is no straightforward way to support the dark theming.<br />
If you own the contents displayed within the **Webview** you might want to implement your custom CSS themes and toggle them using `@JavascriptInterface` from your app. <br />

If `WebViewFeature.FORCE_DARK`is supported we can choose from three available options:
* `FORCE_DARK_OFF` - Disable dark theme, the content will be rendered in default Light Theme
* `FORCE_DARK_ON` - Enable dark theme, the content will be rendered in Dark Theme
* `FORCE_DARK_AUTO` - Enable dark theme based on the state of **parent** view  

Then we need to apply the setting using `WebSettingsCompat`

~~~
WebSettingsCompat.setForceDark(webView.settings, WebSettingsCompat.FORCE_DARK_ON)
~~~

That's all really, now when testing your app you should see a cool Dark Themed **Webview.**
