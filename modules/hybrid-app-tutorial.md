# Building a Hybrid App in Android and Ember

### Table of Contents
[Introduction](#introduction)  
[Installing Android, Android Studio, Ember, and Cordova](#installing-cordova-and-ember)

### Introduction

Hybrid apps are what you get when web apps and native apps have a baby. The core limitation of web apps in mobile environments is there inability to access native device features (e.g. photo libraries, keyboard functions, and bluetooth capabilities - to name a few). The core strength of web apps is their ability to be deployed cross-platform. That is, a web app is the same for Android as it is for iOS or Windows phone. This means developers can iterate much quicker without the need to develop stand alone siloed code for different platforms. 

On the flip side, native apps have all of the tight control of mobile operating system and hardware capabilities, but at the cost of being developed in platform specific languages and paradigms. This measn that developers supporting multiple native apps must individually change each code base if they wish to put out an update to their app.

Hybrid apps get the best of both worlds - access to native features, while still being built as a cross-platform web-app. How does this work you ask? Well hybrid apps operate in a native platform-specific 'container.' This native container provides API access to native features to a web app core (where the majority of the app lives). So developers can write one app and just map it to many containers. 

The content of this lesson explores these concepts and helps you build your first cross-platform hybrid app using Apache Cordova and Ember JS.

Our entire setup uses Free and Open Source Software (FOSS). When using FOSS, respect its copyright and license restrictions. These obligations and rights are typically conveyed in a LICENSE file.

[Top](#table-of-contents)

### Installing Cordova and Ember
#### Foreword

This guide assumes you have already installed git (github desktop for windows users) and npm. The guide also assumes both of these packages are available at the command line (or in a power shell). If you do not meet this requirement, see [installing git on mac/windows](https://desktop.github.com/) or (for linux) just:

```
sudo apt-get install git
```

To install node and npm (the node package manager), visit [https://nodejs.org/en/](https://nodejs.org/en/)
#### Installing Cordova

Apache Cordova is a framework that contains a number of native wrappers (containers) that map hardware and operating system features from various vendors (android, ios, etc) to what are called ```webviews```. Webviews are essentially mini-browser windows that re-use the browser capabilities built into mobile operating systems to render HTML, CSS, and Javascript. Cordova allows this view to access approved device features. To get started:

```
npm install -g cordova
```
<script src="https://raw.githubusercontent.com/apache/cordova-docs/master/www/docs/en/dev/guide/platforms/android/index.md"></script>
#### Installing Ember
Since we will be building our app in Ember, lets also install the Ember CLI you worked with before in sec. web dev.

```
npm install -g ember-cli
```

Now you should be able to interact on the command line and see the cordova and ember build tools functioning:

```
cordova help
```

![cordova](hybrid-app-tutorial/cordova-cli-running.png)
> If you dont see content similar to this, check to ensure your cordova install worked

```
ember help
```

![ember](hybrid-app-tutorial/ember-cli-running.png)
> If you dont see content similar to this, check to ensure your ember install worked.

#### Creating a new ember project

Lets start an empty ember project that we can use to demo the app. We will modify this later (and track its changes on github).
> I suggest you first create a new folder somewhere where you'd like to store the files, then cd into that directory

```
ember new hybridapp
```

![ember new project](hybrid-app-tutorial/ember-new-project.png)
> This may take a few minutes

Create a new repo on github by visiting [https://github.com/new](https://github.com/new). Give it a name, I named mine CYBR-hybrid-app-code so I could share it with all of you. You can call yours simply ```hybridapp``` if you like.

![new repo](hybrid-app-tutorial/new-repo.png)

Lets switch back to our shell and commit the code to our new github repo
```
cd hybridapp
git status
git remote add origin <your repo url goes here>
git push -u origin master
```

#### Installing an ember addon to make ember and cordova play nice
There is a handy ember addon (built by [@poetic](https://github.com/poetic/ember-cli-cordova) and [@isleofcode](https://github.com/isleofcode/ember-cordova)) that makes cordova cli and ember cli seamlessly (and I mean really seamlessly) work together. Lets install it.

```
ember install ember-cordova
```

[Top](#table-of-contents)

####



#### License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER8480</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.