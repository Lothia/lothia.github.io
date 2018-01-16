---
layout: post
title: "How to get rid of Firefox's newtab page on Ubuntu"
tags: [firefox, privacy]
comments: false
---
Firefox installs some global extensions to directories like `/usr/lib/firefox/browser/features`, turning them on for every user on the PC. These are hidden in Firefox’s extension page and some of these can’t be turned off. 
This will use `dpkg-divert`, so it is only for distributions like **Debian** and **Ubuntu**, which use `apt`.


The reason I’ll use `dkpg-divert` is to make the change persistent, the changes will not be lost on Firefox upgrade.

Check if extensions are there;
~~~sh
ls /usr/lib/firefox/browser/features/
activity-stream@mozilla.org.xpi       #The newtab page
onboarding@mozilla.org.xpi            #Welcome thingie
firefox@getpocket.com.xpi             #Pocket
shield-recipe-client@mozilla.org.xpi  #Shield experiment addon
followonsearch@mozilla.com.xpi        #Search telemery
aushelper@mozilla.org.xpi
e10srollout@mozilla.org.xpi
screenshots@mozilla.org.xpi
formautofill@mozilla.org.xpi
webcompat@mozilla.org.xpi
~~~
I’ll disable the commented ones.

Switch to root;
~~~sh
sudo -i
~~~
Create a directory to hide the extensions;
~~~sh
mkdir /usr/lib/firefox/browser/features/hidden
~~~
Divert an extension;
~~~sh
dpkg-divert --rename --divert /usr/lib/firefox/browser/features/hidden/activity-stream@mozilla.org.xpi --add /usr/lib/firefox/browser/features/activity-stream@mozilla.org.xpi
Adding 'local diversion of /usr/lib/firefox/browser/features/activity-stream@mozilla.org.xpi to /usr/lib/firefox/browser/features/hidden/activity-stream@mozilla.org.xpi'
~~~
Now none of the users on the PC will see the newtab page, they’ll see a good old blank new tab. You should divert the other extensions too.

To remove the diversion
~~~sh
dpkg-divert --rename --remove /usr/lib/firefox/browser/features/activity-stream@mozilla.org.xpi
~~~
