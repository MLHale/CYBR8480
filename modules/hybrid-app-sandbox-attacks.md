# Building a Hybrid App in Android and Ember

### Table of Contents
[Introduction](#introduction)  
[Getting started](#getting-started)  



### Introduction
In this module you will go behind a simple 'Hello World' app and interact with some of the native device features that Cordova gives you access too. It assumes you have completed the basic setup, configuration, and installation of Cordova, Android, and Ember as the [1st tutorial](hybrid-app-tutorial.md) discussed. It also assumes you have completed the [previous tutorial](hybrid-app-tutorial-part2.md) 

### Getting Started
Start by getting our development environment setup. For this tutorial, we will use the Android emulator we setup last time. If you want, you can replace the emulator portions with your actual Android device and use ADB.

#### Starting the Android Emulator
open a new shell (power shell or CMD if windows), navigate to your code repository, and launch the emulator.

```
cd ./hybridapp/
ember cdv run --platform=android --emulator
```
#### Running the livereload ember cordova server
Once the emulator is launched, you can start serving the live-reload ember server using the following command:

```
ember cdv:serve --platform=android --verbose
```

If all goes well you should see a terminal running ember (leave it running):

![ember running](hybrid-app-tutorial-part2/ember-server-running.png)

and then upon opening the app, the app running in the emulator:

![ember running in emulator](hybrid-app-tutorial-part2/ember-server-running2.png)

[Top](#table-of-contents)

### Dev tool usage

#### Android Tools
Before we get started lets launch some dev tools. First and foremost, launch the Android emulator controls by clicking the '...' shown below. This will launch a panel of various controls that we can use to simulate GPS, accelerometer, and other types of data.

![android-controls](hybrid-app-tutorial-part2/android-controls.png)

This will launch a window that should resemble this:

![android-controls](hybrid-app-tutorial-part2/android-controls2.png)

We will use this later to simulate some accelerometer activity.

#### Chrome Dev tools 
This may be surprising to you, but the chrome dev tools we all know and love work with Android! Think about it, your app is really a fancy web app living in a native wrapper. Chrome is smart enough to talk to Android device browsers - so it can talk to Cordova Webviews too!

To inspect our app, open a new chrome window and type the following:
```
chrome://inspect/#devices
```

You should see something like this:

![Chrome inspect](hybrid-app-tutorial-part2/chrome-inspect.png)

Clicking 'inspect' will give you a full visual + console toolset that you can use to interact directly with the running app.

![Chrome inspect](hybrid-app-tutorial-part2/chrome-inspect2.png)

Pretty neat!

[Top](#table-of-contents)

### Working with your first Cordova Plugin
Lets get started with really using Cordova. The beauty of the platform is that it exposed native libraries to webviews in native wrappers. Let's explore our first plugin. 

#### Adding the plugin
Stop the ember cdv:serve command running in the original shell you opened (ctrl + c), open up a new shell and navigate to your ember project.

```bash
cd ./hybridapp/
```

Now lets tell cordova to add a plugin to our app. In the new terminal type:

```bash
ember cdv:plugin add cordova-plugin-device-motion
```
Once this completes, rebuild your app and send the apk to the emulator.

```bash
ember cdv run --platform=android --emulator
```

Now with the app running in the emulator, switch back to the first terminal and re-run the ember livereload server.
```bash
ember cdv:serve --platform=android --verbose
```

[Top](#table-of-contents)

### Accelerometer display component
Lets create a new component that will be responsible for displaying accelerometer data as it comes in.
```bash
ember generate component accelerometer-display
```

open up and edit the ```/app/templates/application.hbs``` template to look like the following:

> raw code below

```hbs
Demo Cordova Plugins For Days

{{accelerometer-display currX=x currY=y}}

```
Now open the new component ```/app/templates/components/accelerometer-display.hbs``` and modify it to the following:

```hbs
Accelerometer X value: {{x}}<br>
Accelerometer Y value: {{y}}<br>
Accelerometer Z value: {{z}}<br>
```

Saving your code you should see:

![Empty Template](hybrid-app-tutorial-part2/template-only.png)

#### Making it actually work
Now that we have some basic markup, we need to tell our ember component where to get its data from. This involves connecting the component to the cordova plugin data via the cordova API. Essentially we want our component to work as shown in the following diagram.

![Component Architecture](hybrid-app-tutorial-part2/component-architecture.png)
> The runloop is a function that will be responsible for invoking the Cordova API and getting and updating the current values of x, y, and z.

To implement this, lets modify our component code in ```/app/components/accelerometer-display.js```

> Raw code below

```js
import Ember from 'ember';

export default Ember.Component.extend({
  x: 0,
  y: 0,
  z: 0,
  on: true,
  startLogging: function(){
    //begin logging accelerometer data once the component launches

    var component = this;
    this.updateAccelData(component)
    
  }.on('init'),
  updateAccelData: function(component){
    Ember.run.later(function(){
      //wrapper to preserve binding satistfaction
      try {
        //invoke cordova accelerometer Plugin and get accelerometer data
        navigator.accelerometer.getCurrentAcceleration(function (acceleration) {//success callback
            console.log('acceleration setvars called');
            component.set('x', acceleration.x);
            component.set('y', acceleration.y);
            component.set('z', acceleration.z);
            console.log("accel vals: x: "+ acceleration.x+ " y: "+acceleration.y+" z: "+acceleration.z+" t: "+ Date.now());
        }, function (error) {//error callback
            console.log('error: ' + error);
        });
      }
      catch(err){
        console.log('error: '+err);
      }
      if(component.get('on')){
        //keep running
        component.updateAccelData(component); //recurse
      }

    }, 100);//run ever 100ms
  }
});
```

There is a lot here, so lets unpack it. First, lines 4-7, setup some basic variables for storing the x, y, and z parameters. The 'on' variable is a boolean that indicates when to stop the run loop. Lines 8-14 initialize the run loop, but waiting until the component has rendered (i.e. 'on init'). The meat of the componet is in lines 15-39. This updateAccelData method runs every 100ms and invokes the navigator.accelerometer method as outlined in the [cordova API](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-device-motion/index.html#navigatoraccelerometergetcurrentacceleration): (please review this method before proceeding). Sepcifically, the function invokes the accelerometer and then stores x, y, and z back into the component. On lines 33-36, the function will decides to 'loop' again if ```on``` is true. 

#### Testing it out
Once you've saved the new code, try playing around with it using the Android controls. I started by 'sliding down' and turning off rotate display functionality on the emulated phone.

![Turn off rotate](hybrid-app-tutorial-part2/turn-off-rotate.png)

With rotate display off, I opened the Android emulator tools and started rotating the phone to get some readings.

![Testing accelerometer](hybrid-app-tutorial-part2/android-rotate-capture.gif)

[Top](#table-of-contents)

### Extending the app
Just for kicks, lets extend this app and add a time-series chart from [http://opensource.addepar.com/ember-charts/#/time-series](http://opensource.addepar.com/ember-charts/#/time-series). We can store accelerometer data into an array of previous points and then graph them.

```bash
ember install ember-charts
```

#### Template Code
First open your template code ./app/templates/components/accelerometer-display.js
edit it to the following to add our chart component in. 

```hbs
Accelerometer X value: {{x}}<br>
Accelerometer Y value: {{y}}<br>
Accelerometer Z value: {{z}}<br>

{{time-series-chart lineData=accelHistory}}
```
This tells the chart library that our lineData is in a variable called 'accelHistory'. It doesn't exist yet, but we are about to create it.

#### Component Code
Now open your component code ./app/components/accelerometer-display.js and modify it to the following, adding an array of data points and code to update the array as new points come in.

> Raw code below

```js
import Ember from 'ember';

export default Ember.Component.extend({
  x: 0,
  y: 0,
  z: 0,
  accelHistory: [],
  on: true,
  startLogging: function(){
    //begin logging accelerometer data once the component launches

    var component = this;
    this.updateAccelData(component);
    
  }.on('init'),
  updateAccelData: function(component){
    Ember.run.later(function(){
      //wrapper to preserve binding satistfaction
      try {
        //invoke cordova accelerometer Plugin and get accelerometer data
        navigator.accelerometer.getCurrentAcceleration(function (acceleration) {//success callback
            //console.log('acceleration setvars called');
            component.set('x', acceleration.x);
            component.set('y', acceleration.y);
            component.set('z', acceleration.z);

            //update history, maintain 50 points max
            var history=component.get('accelHistory');
            if(history.length === 150){
              history.shiftObject();//shift an x off
              history.shiftObject();//shift a y off
              history.shiftObject();//shift a z off
            }
            var t = Date.now();
            var newXPoint = {time: t, label: 'x', value: acceleration.x};
            var newYPoint = {time: t, label: 'y', value: acceleration.y};
            var newZPoint = {time: t, label: 'z', value: acceleration.z};
            history.addObjects([newXPoint, newYPoint, newZPoint]);
            //console.log("accel vals: x: "+ acceleration.x+ " y: "+acceleration.y+" z: "+acceleration.z+" t: "+ Date.now());
        }, function (error) {//error callback
            console.log('error: ' + error);
        });
      }
      catch(err){
        console.log('error: '+err);
      }
      if(component.get('on')){
        //keep running
        component.updateAccelData(component); //recurse
      }

    }, 100);//run ever 100ms
  }
});

```

Now instead of just overwriting X, Y, and Z when the next point comes in, we are pushing those values into an array of 50 time points. When the array gets full, we shift off the first three points (x, y, z for a single time t) and add on the new ones. Pretty nifty. 

#### Time to test it out
I've added another dandy gif of the graph. Test it out yourself!

![With graph](hybrid-app-tutorial-part2/accelerometer-graph.gif)

[Top](#table-of-contents)

### Integrating other Cordova Plugins
You can apply the same logic used for Accelerometer to other Cordova Plugins. The typical ember-cordova workflow is

1. Install the cordova plugin using ember cdv:plugin add <name of plugin>
1. Create an ember component to handle the data and manage the interaction with the plugin
1. Add the component somewhere in your App's template code
1. Invoke the Cordova API (Typically ```navigator.<name of plugin>```) in your component code according to the documentation and update the component variables tracking the data accordingly.

#### Try it
Work with someone else in the class and add a feature to your app to use another component. Pick from one of the components listed in the [cordova docs](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-battery-status/index.html)

When you've integrated it, fork this repo and edit hybrid-app-tutorial-part2.md to include your directions (below in this section) and make a pull request to add in your own directions to use other features. This way everyone can benefit!

### Student Contributions
The following plugin module directions are submitted by previous students in the course. 

#### Authors 
(your names go here)
#### Plugin Name (which plugin did you look at?)
(Provide a link to the plugin and briefly describe it)
#### Usage
(your instructions go here)

[Top](#table-of-contents)

### Next time we explore vulnerabilities and exploitations in hybrid apps.

#### License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER8480</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
