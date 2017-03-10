---
published: true
comments: true
layout: post
title: Automatically update Chrome via Jamf Pro
---

It's always good to be up-to-date, especially with [vulnerabilities](https://bugs.chromium.org/p/project-zero/issues/detail?id=1011) being publicised on a regular basis, and people like the [CIA](https://wikileaks.org/ciav7p1/) and NSA hacking *everything*. It will keep your InfoSec team happy too!

Updating apps in Jamf Pro isn't the easiest thing to do (at least until version 10 is released, with Patch Management built in!). So I wanted to find a way to automate it. Yes, Chrome should automatically update itself, but users disable automatic updates or just never restart their browser, so there are still some older versions of Chrome out there.

The method we started using at first worked, but needed some manual intervention (See the script [here](https://www.jamf.com/jamf-nation/third-party-products/files/770/google-chrome-install-update)). It downloads and installs the latest Chrome DMG from Google - they have a hidden static URL that always provides the current version. Then we create a Smart Group in Jamf Pro that targets all Macs that have Google Chrome installed where the version is not like *insert latest version number*. Every time Google update Chrome, we would need to update that version number (which is fairly often) and it's something my team and I would rather not have to do!

As this method does work for us, I thought I'd build on it, and automate the version part. So I created an Extension Attribute called 'Chrome Version'.

![]({{site.baseurl}}/images/Screen%20Shot%202017-03-08%20at%2021.02.19.png)

It works by checking a [site](http://omahaproxy.appspot.com) where Google keeps all of the Chrome version history, finds the latest, stable, macOS version number and saves it to a variable. It then inspects the Google Chrome.app/Contents/Info.plist on the Mac the script is running on, and gets the version number. If the two versions are the same, it updates the EA with 'Latest', if they do not match it outputs 'Old'.

![]({{site.baseurl}}/images/Screen%20Shot%202017-03-08%20at%2021.09.53.png)

Find the Extension Attribute code below:

{% gist b819019a2c4dbde7dbdbecc8f78f39b3 %}

Next, I made a Smart Group targeting all Macs where *Chrome Version* = *Old* (this may take some time to populate initally, as the computers need to check in and do an Inventory Update first). Now all we need to do is create a Policy targeting the Smart Group to update Chrome!

![]({{site.baseurl}}/images/Screen%20Shot%202017-03-08%20at%2021.27.21.png)

The Policy simply runs the script below, on all Macs in scope.

{% gist 980acccde324da79c6cfd24472c3ee4d %}

Google Chrome is now up to date on all of our Macs :)

I am going to start posting more scripts I have used in Jamf to my [GitHub](https://github.com/LewisLebentz), so check it out!

*Update:* [mm2270](https://www.jamf.com/jamf-nation/users/1927/mm2270) from Jamf Nation kindly shared an alternative bash script which you could use instead of the Python one I wrote. This one uses curl and awk instead. You can find the Jamf Nation post [here](https://www.jamf.com/jamf-nation/discussions/23323/how-to-update-chrome-automatically#responseChild141302) and the code below:

{% gist 7a9ef796e5ada363da5eae011ae7e96d %}
