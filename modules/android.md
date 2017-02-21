### Creating an Android App
I am a firm believer in not reinventing the wheel. Android is a well documented framework that has a variety of solid content (slides and tutorials). This lab uses open source materials from [@vogella](https://github.com/vogellacompany).

### First task
Go to [http://www.vogella.com/tutorials/Android/article.html](http://www.vogella.com/tutorials/Android/article.html) and follow the step-by-step instructions provided to create your first native Android app. The app the guide has you build is a temperature converter that converts to and from farenheit and celcius.

Ultimately you app should end up looking like:

![Final app](http://www.vogella.com/tutorials/Android/img/xtemperature96.png.pagespeed.ic.Qf89ajp3Vp.webp)

#### Using git
As you follow along with the Vogella tutorial, make regular git commits and push those commits to github. You can setup android studio to work with git directly, following the instructions here: [https://www.londonappdeveloper.com/how-to-use-git-hub-with-android-studio/](https://www.londonappdeveloper.com/how-to-use-git-hub-with-android-studio/), or you can use git from a terminal launched in the folder you create your Android project in.

Make sure to push your final code to the github repo you create and **share it with me via slack** when you are done.

### Second Task
Once you complete the basic how-to tutorial. Take a look at the various available options available to you [http://www.vogella.com/tutorials/android.html](http://www.vogella.com/tutorials/android.html). Notice there is a nice step-by-step tutorial for virtually everything you will need to know about Android programming. If you find that you need a particular class, feel free to read up about the class and see it in use.

### Third Task
Lastly, Android development doesn't need to happen in a vacuum. There are numerous resources available to the enterprising developer that prevent you front needing to start from scratch. I've collected a few resources here that I think you mind beneficial. Please look over and familiarize yourself with what they have to offer.

### Resources
* [Android Developer API portal](https://developer.android.com/guide/index.html). I would be remiss to not list the official docs first in this list. There are lots of good conceptual and programmatic examples on the offical docs. Check them out.
* [Google samples](https://github.com/googlesamples) is a collection of actual android app examples that has been put together by Google. These examples illustrate different application architectures, samples for interacting with certain APIs or resources, and even some wearable applications compatible with Android Wear products. Since they are compiled by google, they are up-to-date and mostly well documented.
* [Glide](https://github.com/bumptech/glide) is a library for image loading and caching that helps simplify the task of getting images into your apps.
* [RxJava](https://github.com/ReactiveX/RxJava) and [RxAndroid](https://github.com/ReactiveX/RxAndroid) are two libraries that make writing Android apps more like writing web apps. They specifically provide so-called 'reactive extensions' that act like callbacks. These libraries vastly simplify writing applications that have multiple collaborating components that need to routinely talk to each other. Just like Ember.js simplifies the process of binding data to components and sending and receiving data between them - so too does RxJava and RxAndroid.
* [Retrofit](http://square.github.io/retrofit/) is an HTTP-client that you can use in your Android apps to send/receive data to/from a RESTFul API. Think of Retrofit as the Android equivalent of AJAX. It is way simpler to use a library like this than to manually implement a REST client from scratch.
* [AChartEngine](https://github.com/ddanny/achartengine) is, as its name indicates, a nice charting library that can help you create and present a range of different data diagrams (line, pie, area, bar, time, doughnut, etc charts). 
* [ORMLite](http://ormlite.com/), [Active Android](http://www.activeandroid.com/), and [Sugar ORM](http://satyan.github.io/sugar/index.html) are all different Object-relational-mappings that are analogous to Django Models or Ember data. They all provide an abstraction layer that sits atop the Android SQL stack and allow you to deal with first class objects at a model or schema level instead of writing database queries and tables 'by hand'. Don't underestimate how important this is for large applications.
*[Dagger 2](https://github.com/google/Dagger) Dagger is Google's answer to dependency injection. It specifically addresses a class of problems associated with declaring components. The base Android architecture doesn't do a good job of handling components that involve other components. Think of Dagger as a framework for simplifying component connection declaration. If you don't use it in this class - it isnt the end of the world, but know that it is here.
* [Scripting Layer for Android (SL4A)](https://github.com/kuri65536/sl4a) is a plugin that enables Android developers to launch and run various scripts (Python, Javascript, Shell, etc). It is a fork of a former project by the same name [https://github.com/damonkohler/sl4a](https://github.com/damonkohler/sl4a). SL4A can be helpful if you just need to do some work and you don't want to deal with the horrible semantics of Java to get it done. 
