---
layout: post
title:  "Website debugging on Android"
date:   2020-09-24 21:50:30 +0200
categories: android
---

I know this might not be strictly related to android development but hopefully some of you might find this post useful as well.<br />
As a person who has to deal with websites a lot I often struggled to find a way check to out my website on android phone while I'm away from my computer.<br />
In this post I will try to describe how we can debug websites from your android phone.<br />

Now I've found two ways you can perform web debugging on Android:
* Chrome Developer Tools
* HTML/CSS Website Inspector app

### Chrome Developer Tools
While it is possible to use Chrome Developer tools on your mobile phone, unfortunately it requires the phone to be connected to your computer.<br />
While you can use the same set of tools as on Desktop I wasn't very satisfied with this solution, since it wouldn't work while I'm away from my computer.

For more details on how you can use Chrome Dev Tools on Android I refer you to the [official tutorial](https://developers.google.com/web/tools/chrome-devtools/remote-debugging)

### HTML Website Inspector
It is worth noting that this solution doesn't offer as much options as Chrome Dev Tools do, however you can use the app whenever you want without being connected to your PC.<br />
I wasn't expecting a full feature-set either, since most desktop apps on mobile usually have simplified functionality.

Okay so now let's go through what you can do with `HTML Website Inspector`


When you launch the app you can see it is essentially a browser.

<img src="{{site.baseurl}}/images/html-website-inspector.png">

Now in order to inspect a particular element you need to tap on the **hand** icon as outlined on the above screenshot. <br />
After that all you have to do is to tap the element which html you want to preview.<br />
In my case I went with **Images** link on the top.

<img src="{{site.baseurl}}/images/html-website-inspector-2.png">

Now you will be presented with a text field allowing you to edit given HTML. <br />
I will now change link to from **Images** to **Bananas** and apply it to the page using **Up-Arrow** icon in the toolbar.

<img src="{{site.baseurl}}/images/html-website-inspector-3.png">

That's it! You've just edited your first HTML on Android!<br />

The application also offers the following functionality:
* Editing of full website source
* Viewing desktop version of the website
* Listing all types of HTML Elements
* Injecting simple javascript one-liners
<br />

In this post we've covered how you can edit HTML of any website on your Android phone.
