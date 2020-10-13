---
layout: post
title:  "Indie Dev App Launch Checklist"
date:   2020-10-07 21:50:30 +0200
categories: android
---
This post will be a little different... <br />
I won't make this a secret - I am an indie developer. In my lifetime I have created probably around 35 apps.<br />
You can have a look at [my developer account](https://play.google.com/store/apps/dev?id=6178411479367698437) - right now I have closer to 10 apps since not all of them proved successful enough for me to keep supporting them.

After making all these apps I have found that some things worked for me and some didn't.<br />
In this post I will share all of the things I'm doing whenever launching an app.

Since there is a lot of things I want to talk about I will group them into two main categories
* App Implementation Practices - things that will make the user want to continue using the app
* ASO (App Store Optimization) - basically all of the things that will get users to install it in the first place

## Right Idea
So you might think you have an great and original idea for an app...<br />
First thing I would advise is to check out the potential competition - if there are already apps with similar functionality your app might not be a great success.<br />
However don't give up just yet, maybe the existing apps are limited or you have an idea on how to do things better - if that's the case I encourage you to turn your idea into an app!<br />
Don't get discouraged because the existing apps already have millions of downloads, if your app is better it will eventually surface, it will just take time depending on how saturated a given market is.

## App Implementation Practices
These are the things that I do for every project - usually at the start I will have an MVP (Minimum viable product) functionality and use below practices in order to increase overall app's quality.

### App Icon
The app icon is the first thing the user sees when he browses the Playstore. If it looks poor the user will be less likely to visit the Playstore listing and effectively install the app.

For a **Tool** type of an app I recommend choosing a [Material Design Icon](https://material.io/resources/icons/?style=baseline) along with primary app color for the background.<br />
For creation of the in-app launcher icon I am usually using [Image Asset Studio](https://developer.android.com/studio/write/image-asset-studio), since it already supports adaptive icons which are recommended for Android Oreo and above. <br />
For the Playstore listing itself I encourage you to use [Android Asset Studio](https://romannurik.github.io/AndroidAssetStudio/icons-launcher.html), this will allow you to add a nice-looking shadow to your app icon.

Now for a **Game** I would probably go with something more custom, if you have no graphic design skills you can probably pay someone couple of bucks to create the icon for you. For that you can use websites such as [Upwork](https://www.upwork.com) or [Freelancer](https://www.freelancer.com).

### Splash screen
Did you know that there is some time between app launch and when the user can start interacting with the user interface?<br />
It's called a **Cold Start** - a great way to give the appearance of faster loading time and to improve the UX is to show a splash screen during that time.
It doesn't have to be anything fancy - a simple centered app logo will do the trick.

It also requires very little effort to implement and you can learn how to do it [the right way here](https://medium.com/@shishirthedev/the-right-way-to-implement-a-splash-screen-in-android-acae0e52949a).

### Material Design User interface
No matter how good the app is if the UI is poor the users will be reluctant to use it.<br />
I'm a programmer so I know very little about design. Fortunately for us developers Google has created an [Material Design guide](https://material.io/) on how to build user interfaces. Whenever there is a piece of UI I need to develop I simply visit their website - they have covered most of the common use-cases that you will encounter.

### Dark theme
There are not many things that annoy me more than an app that doesn't support dark theme.<br />
Sometimes I'm using my phone during the evening and there it is, this one app that doesn't support dark theme - I am instantly blinded and lose sight for couple of seconds. Following my survival instincts I'm immediately uninstalling the aggressor.

You might think it is not that important but trust me on this, just do it.<br />
I wrote a couple of articles on how to add **Dark Theme** support to your app
* [App Dark Theme Support](https://androidexplained.github.io/ui/android/material-design/2020/09/24/dark-mode.html)
* [Webview Dark Theme Support](https://androidexplained.github.io/ui/android/material-design/2020/09/24/dark-mode-webview.html)

### Obfuscation
Now I don't care that you haven't used Proguard/R8 before - obfuscating your code requires so little effort, especially if your project is small, that there are literally no excuses for not doing it.

If your app gets successful you'll thank me for it later on - expect to have 15 clones on the store in no time. Obfuscation might not solve the problem entirely but at least it will discourage 90% of copycats out there.

Oh and did I mention it will also make your app smaller and faster?<br />
Yeah you get all that for a humble couple lines of code added to your `build.gradle`

~~~
buildTypes {
    release {
        minifyEnabled true
        shrinkResources true
        proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
    }
}
~~~
{: .language-gradle}

## ASO - App Store Optimization
After going through above practices you can be sure that your app is simply awesome. This doesn't mean we're finished yet. Since this is a new app the biggest problem you will face is getting users to notice it. Fortunately for you I will cover this as well.

### Store Listing
Store listing is basically what the user sees after going to your app details page on the Playstore.
It consists of the app description, screenshots, promo graphic etc.

#### Keywords
In order for your app to get discovered you need to use keywords relevant to your app functionality. <br />
The basic idea is to use the most important keywords in your app description **4-5 times**.
Additionally you can try to include one main keyword in your app name.<br />
When it comes to finding  the right keywords I use [KeywordTool](https://keywordtool.io/) & [SearchMan](https://searchman.com/), both have some limited functionality for free which should be enough for one app.

#### Screenshots
Play listing screenshots allow the user to see how your app looks like without actually installing it. <br />
Without graphic designer skills it is very hard to get this part right. However there are some free tools out there that can allow you to create a very nice screenshot graphics. <br />
I really recommend [App-mockup](https://app-mockup.com/android/#), in my opinion it is the best mockup tool out there for free.

### Landing Page
To increase your visibility on the web I recommend to creating an app landing page. <br />
Now as an indie developer it's natural that I don't like spending money on an app that might never become a success.
Don't worry, there are ways you can set up an landing page for free and without too much effort.<br />
You probably can find ways to do this on-line, personally I very much like using [Github Pages](https://pages.github.com/) along with [Jekyll](https://jekyllrb.com/). You can find many app landing page themes on [Jekyll Themes Website](https://jekyllthemes.io/jekyll-landing-page-themes).

### Marketing
After your app is released it will probably take some time till it shows up in any Playstore searches. To help it gain visibility faster we need to help it a little by posting the app all over the internet. <br />
The places that I always think about
* Forums & Subreddits relevant to your app or related to app development in general
* Answering questions on Quora & StackOverflow if there is a problem that your app solves
* Social media - I don't use it as much now since I've abused this way in the past and some of my friends delicately suggested that they are not fine with me annoying them with a new app each day

#### Localization
Now you may already have some userbase. If you see that you have a lot of users in some particular country you may want to localize your play store listing and the app itself to gain even stronger foothold in that location.
Currently for localization I'm using [app translation service](https://support.google.com/googleplay/android-developer/answer/3125566?hl=en) from Google Developer Console, however you might find it cheaper to use [Upwork](https://www.upwork.com) or [Freelancer](https://www.freelancer.com).

## Summary

After going through all that I can ensure you that you did almost all you can in order to ensure your app's success. The rest is in the hands of lady Fortune.

If there is one last thing I can advise it would be "not to put all eggs in one basket" - by releasing many apps you increase your chances of succeeding.

In this post we have learned what to focus on when releasing a new app.
