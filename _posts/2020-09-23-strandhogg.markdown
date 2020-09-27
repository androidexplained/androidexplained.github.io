---
layout: post
title:  "Strandhogg Vulnerability"
date:   2020-09-23 21:50:30 +0200
categories: security android malware
---

Mobile malware becomes increasingly difficult to protect against, with hackers trying more subtle approaches to gain access to user's phone or steal his data.
Probably we have all heard stories of someone we know that got hacked loosing access to his accounts and even money.<br>
One of the vulnerabilities that became very popular recently is called Strandhogg.
Its name comes from an [Viking tactic consisting of coastal raids]. <br>

Essentially the vulnerability allows the malicious app to show a screen on top of a legitimate app. This means that the unaware user could potentially grant malicious app permissions or enter credentials trying to log in to his favorite service.
More technically speaking the malicious app would display its own custom `Activity` on the top of other app. This activity could try to trick the user into thinking it is legitimate by matching the user interface with the target application.

At the time of writing there are two versions (1.0 & 2.0) of the vulnerability which I will talk about in more detail below.

## Strandhogg 1.0

### How does it work?
First version of Strandhogg is based on application manifest attribute called `taskAffinity`.
The malicious app sets the attribute of its `Activity` to match the package name of the target application.
Then the attacker can use manifest attribute called `allowTaskReparenting` set to true or add flag `Intent.FLAG_ACTIVITY_NEW_TASK` to activity launching intent.

When the activity is launched the above steps trick the system into thinking that the malicious `Activity` is belonging to the target app. After its launched it will be displayed on top of the target application.

### Android versions affected
According to [Promon] (security company which found the vulnerability in the first place) most of the popular apps are at risk.
As for the system versions affected it appears that all of them are vulnerable, this including Android 10.

### How can one protect against it?
[Promon] has came up with its solution protecting against vulnerability called Shielder SDK.
We can also protect against it setting the `taskAffinity` of the application in the manifest to an empty string. This however could have an UX side-effects - it is worth checking how your application behaves in the android recents screen. Potentially the application could display every activity as a separate window - in order to fix that one can use combination of `excludeFromRecents` and `documentLaunchMode` manifest attributes.

Google claims that it is effectively able to protect users against it, after all the malicious app needs to declare uncommon manifest attributes - when such attributes are detected the app would be removed from Google Play.
However this doesn't protect against apps from sources other than Google Play.

## Strandhogg 2.0

### How does it work?
Second version of the vulnerability has been classified by Google as a vulnerability with critical severity (CVE-2020-0096).
This version is much more dangerous since it cannot be detected so easily - it relies on runtime code execution which is much harder to detect.

It works by exploiting `Context.startActivities` API using the following activity-launching intents:
* First intent launches the target application - the intent needs to contain `Intent.FLAG_ACTIVITY_NEW_TASK`
* Second intent is the one doing the attack. Potentially the corresponding activity would match the target application's UI to trick the user
* Third intent works as a distraction, ensuring that user does not become suspicious of the target application being launched - this intent would also contain the `Intent.FLAG_ACTIVITY_NEW_TASK` flag

After creation of the above intents they're passed into `startActivities` method.
The same scenario happens as with Strandhogg 1.0, the malicious application is able to display the activity from the second intent on the top of the legitimate app.

### Android versions affected
According to [Promon] all versions up to Android 9 included are affected

### How can one protect against it?
As with Strandhogg 1.0 one can use [Promon] product called Shielder SDK.
Alternatively the protection involves adding `singleTask` or `singleInstance` attributes to every public activity of your app (activity that can be launched by other apps - either one that contains `intent-filter` or has the `exported` attribute set to `true`).
This can also have undesired side-effects, make sure to thoroughly test your application when applying this fix.

Resources:
<https://promon.co/>

[Viking tactic consisting of coastal raids]: https://en.wikipedia.org/wiki/Strandh%C3%B6gg
[Promon]: https://promon.co/
