# Building a Hybrid App in Android and Ember

### Table of Contents
[Introduction](#introduction)
[Getting started](#getting-started)
[Dev tool usage](#dev-tool-usage)
[Working with your first Cordova Plugin](#working-with-your-first-cordova-plugin)
[Accelerometer display component](#accelerometer-display-component)
[Extending the app](#extending-the-app)


### Introduction
In this module you will go behind a simple 'Hello World' app and interact with some of the native device features that Cordova gives you access too. It assumes you have completed the basic setup, configuration, and installation of Cordova, Android, and Ember as the [previous tutorial](../hybrid-app-part1/README.md) discussed.

### Getting Started
Start by getting your development environment setup. For this tutorial, we will use the Android emulator we setup last time. If you want, you can replace the emulator portions with your actual Android device and use ADB.

#### Running the livereload ember cordova server
Begin by starting the live-reload ember server. Change into your code repository and issue the following command:

```bash
corber serve --platform=android --verbose
```

If all goes well you should see a terminal running ember (leave it running).
![Corber live reload](assets/README-5e7bd.png)

#### Starting the Android Emulator
Since we are working with command line tools, lets configure our environment to allow us to launch the emulator from command line.

Make sure the following is in your path, (linux/mac paths shown below).

```
export JAVA_HOME=`/usr/libexec/java_home`
export ANDROID_HOME=~/Library/Android/sdk
export PATH=${PATH}:$ANDROID_HOME/platform-tools:$ANDROID_HOME/tools
```

check to make sure the android tools are accessible from the command line using the command:

```bash
android
```
if so, chances are you are good!

Now, open a new shell (power shell or CMD if windows), navigate to your code repository, and launch the emulator.

```bash
corber proxy run android --emulator
```
> Note this assumes you created an AVD in android in the previous exercise. If not you need to create one using the `avd manager`

Once your app launches, you should see your app running in the emulator

![Ember app running in the emulator](assets/README-bb226.png)

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

![Chrome inspect](assets/README-fdd24.png)

Clicking 'inspect' will give you a full visual + console toolset that you can use to interact directly with the running app.

![Chrome inspect](assets/README-caa26.png)

Pretty neat!

[Top](#table-of-contents)

### Working with your first Cordova Plugin
Lets get started with really using Cordova. The beauty of the platform is that it exposed native libraries to webviews in native wrappers. Let's explore our first plugin.

#### Adding the plugin
In the shell used to launch your emulator do the following.

Now lets tell cordova to add a plugin to our app. In the new terminal type:

```bash
corber plugin add cordova-plugin-device-motion
```

Once this completes, rebuild your app and send the apk to the emulator.

```bash
corber build --platform=android
corber proxy run android --emulator --nobuild
```
> Note that anytime you modify the native container (i.e. the android part) by adding or removing plugins, you will need to rebuild and relauch the app. You can leave the corber live reload server open as you rebuild.

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

![Empty Template](assets/README-b55bb.png)

#### Making it actually work
Now that we have some basic markup, we need to tell our ember component where to get its data from. This involves connecting the component to the cordova plugin data via the cordova API. Essentially we want our component to work as shown in the following diagram.

![Component Architecture](hybrid-app-tutorial-part2/component-architecture.png)
> The runloop is a function that will be responsible for invoking the Cordova API and getting and updating the current values of x, y, and z.

To implement this, lets modify our component code in ```/app/components/accelerometer-display.js```

> Raw code below

```js
import Component from '@ember/component';
import { later } from '@ember/runloop';

export default Component.extend({
  x: 0,
  y: 0,
  z: 0,
  on: true,
  init(){
    //begin logging accelerometer data once the component launches
    this._super(...arguments);
    this.updateAccelData(this)

  },
  updateAccelData(component){
    later(function(){
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

There is a lot here, so lets unpack it. The first few lines setup some basic variables for storing the x, y, and z parameters. The 'on' variable is a boolean that indicates when to stop the run loop. The init method initializes the run loop by forcing it to run whenever the ember component first loads, but waiting until the component has rendered (i.e. 'on init'). The meat of the component is in the `updateAccelData` function. This updateAccelData method runs every 100ms and invokes the navigator.accelerometer method as outlined in the [cordova API](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-device-motion/index.html#navigatoraccelerometergetcurrentacceleration): (please review this method before proceeding). Specifically, the function invokes the accelerometer and then stores x, y, and z back into the component. At the end, the function will decide to 'loop' again if ```on``` is still true. You could extend this by adding a button to turn this feature on or off.

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

Since we edited the libraries in the ember app, we need to rebuild and re-run the app in our emulator:

```bash
corber build --platform=android
corber proxy run android --emulator --nobuild
```

#### Template Code
First open your template code in `./app/templates/components/accelerometer-display.hbs`
edit it to the following to add our chart component in.

```hbs
Accelerometer X value: {{x}}<br>
Accelerometer Y value: {{y}}<br>
Accelerometer Z value: {{z}}<br>

{{time-series-chart lineData=accelHistory}}
```
This tells the chart library that our lineData is in a variable called 'accelHistory'. It doesn't exist yet, but we are about to create it.

#### Component Code
Now open your component code `./app/components/accelerometer-display.js` and modify it to the following, adding an array of data points and code to update the array as new points come in.

> Raw code below

```js
import Component from '@ember/component';
import { later } from '@ember/runloop';
import { A } from '@ember/array';

export default Component.extend({
  x: 0,
  y: 0,
  z: 0,
  on: true,
  accelHistory: A(),
  init: function(){
    //begin logging accelerometer data once the component launches
    this._super(...arguments);
    this.updateAccelData(this)

  },
  updateAccelData: function(component){
    later(function(){
      //wrapper to preserve binding satistfaction
      try {
        //invoke cordova accelerometer Plugin and get accelerometer data
        navigator.accelerometer.getCurrentAcceleration(function (acceleration) {//success callback
            console.log('acceleration setvars called');
            component.set('x', acceleration.x);
            component.set('y', acceleration.y);
            component.set('z', acceleration.z);
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

Now instead of just overwriting X, Y, and Z when the next point comes in, we are pushing those values into an array of 50 time points. When the array gets full, we shift off the first three points (x, y, z for a single time t) and add on the new ones. Pretty nifty.

#### Time to test it out
I've added another dandy gif of the graph. Test it out yourself!

![With graph](hybrid-app-tutorial-part2/accelerometer-graph.gif)

[Top](#table-of-contents)

### Integrating other Cordova Plugins
You can apply the same logic used for Accelerometer to other Cordova Plugins. The typical corber workflow is

1. Install the cordova plugin using `corber plugin add <name of plugin>`
1. Create an ember component to handle the data and manage the interaction with the plugin
1. Add the component somewhere in your App's template code
1. Invoke the Cordova API (Typically `navigator.<name of plugin>`) in your component code according to the documentation and update the component variables tracking the data accordingly.

#### Try it
Work with someone else in the class and add a feature to your app to use another component. Pick from one of the components listed in the [cordova docs](https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-battery-status/index.html)

When you've integrated it, fork this repo and edit hybrid-app-tutorial-part2.md to include your directions (below in this section) and make a pull request to add in your own directions to use other features. This way everyone can benefit!

### Student Contributions
The following plugin module directions are submitted by previous students in the course.
> Note the code may be geared towards previous versions of corber (when it was still ember-cordova) and/or previous versions of ember/ember cli.

#### Authors

(your names go here)

#### Plugin Name (which plugin did you look at?)

(Provide a link to the plugin and briefly describe it)

#### Usage

(your instructions go here)

#### Authors
Gabi Wethor

#### Plugin Name (which plugin did you look at?)
Cordova Plugin Battery Status
https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-battery-status/index.html
#### Usage
Hey guys :)
#### 1. Install Cordova Plugin
```bash
ember cdv:plugin add cordova-plugin-battery-status
```

#### 2. Generate Ember Component
```bash
ember generate component battery-display
```

#### 3. Edit the following files:
#### 3a. application.hbs
Calls the battery-display component.
```
 Battery Status
 {{battery-display}}
```
#### 3b. battery-display.hbs
Calls the level variable from the battery-display.js file. I included a % because the battery status needs to display as a percentage.
```
 Battery Level: {{lvl}} % <br>
```
#### 3c. battery-display.js
Declaring our variables and utilizing the navigator to call the current battery status. Then multiplied by 100 to convert to a whole number.
```
 import Ember from 'ember';

export default Ember.Component.extend({
  lvl: 0,
  on: true,
  startLogging: function(){
      var component = this;
      this.onBatteryStatus(component);
  }.on('init'),
  onBatteryStatus: function (component) {
     navigator.getBattery().then(function(battery){
     component.set('lvl', battery.level * 100);
     });
	}
});
```
#### Author
Jeff Dempsey

#### Plugin Name (which plugin did you look at?)
Device Orientation - https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-device-orientation/index.html
This plugin gives access to the device compass to give a heading in degrees.

#### Usage
1. Install plugin [ember cdv:cordova plugin add cordova-plugin-device-orientation]
1. Write necessary files to process and display data.

2a. /app/templates/application.hbs
> Calls out to orientation-display component to place its template here.
> Code:

```hbs
{{orientation-display currHead=heading}}
```

2b. /app/templates/components/orientation-display.hbs
>Sets up the template within application.hbs and calls the javascript file to fill the {{heading}} value in degrees. Basically copied the format from in-class accelerometer example.
>Code:

```hbs
Orientation Heading: {{heading}}<br>
```

2c. /app/components/orientation-display.js
> Queries Cordova for current device heading, in degrees, every 100ms. Since I'm new to all this, I again largely copied the format of the js file for the accelerometer-display.

> Code:

```javascript
import Ember from 'ember';

export default Ember.Component.extend({
  heading: null,

  //Begin collecting heading data
  startLogging: function(){
    var component = this;
    this.get('updateHeading')(this);
  }.on('init'),
  updateHeading: function(component){
    Ember.run.later(function(){
      try {
        navigator.compass.getCurrentHeading(function(heading) {//if successful
          component.set('heading', heading.magneticHeading);
          console.log('Compass heading:');
          console.log(heading);
        }, function(error){//if error
          console.log('Compass heading error.');
          console.log(error);
        });
      } catch (error) {
        console.log('Compass heading error.');
        console.log(error);
      }
      component.get('updateHeading')(component);
    }, 100); //run after 100ms, recurses to effectively run every 100ms
  }
});
```

#### Authors
James Percival

#### Plugin Name (which plugin did you look at?)
cordova-plugin-contacts[https://www.npmjs.com/package/cordova-plugin-contacts]
Interesting plugin that allows the adding, viewing, and searching of contacts.

#### Usage
1. Install the plugin [ember cdv:plugin add cordova-plugin-contacts]
1. Generate the files [ember generate component contacts-display]
1. Edit the neccesary files:

3a. /app/templates/application.hbs

> Calls out to the contacts-display component to place its template here.

> Raw code below

```hbs
  {{contacts-display}}
```
3b. /app/templates/components/contacts-display.hbs

>Sets up its template inside application.hbs and then calls out to the javascript file to fill in {{q}} and {{w}}. Had to use the pre-wrap/pre-line style in order to preserve and display the newlines.

> Raw code below

```hbs
  Total Number of Contacts: {{q}}<br>
  Names:Numbers
  <div style="white-space: pre-wrap;">{{w}}</div>
```
3c. /app/components/contacts-display.js

>Queries Cordova and asks for an array of contact objects. We then list the number that was returned, their name, and finally their phone number. We then update q and w accordingly with the above information. Bad variable names... I know... This was all just messing around with it and once it worked I left it alone.

> Raw code below

```js
  import Ember from 'ember';
  export default Ember.Component.extend({
    q:0,
    w:"",
    startLogging: function(){
        //begin logging accelerometer data once the component launches
        var component = this;
        this.hi2(component);
    }.on('init'),
    hi2: function(component){
      var fields = [navigator.contacts.fieldType.displayName, navigator.contacts.fieldType.name];
      navigator.contacts.find(fields, function(contacts){
        component.set('q',contacts.length);
        var nameToNumStr = "";
        contacts.forEach(function(ele){
          nameToNumStr += ele.name.givenName+':'+
            ele.phoneNumbers[0].value+'\n';
        });
        console.log(nameToNumStr);
        component.set('w', nameToNumStr);
      });
    }
  });
```

#### Authors
Vaibhav Ingle

#### Plugin Name (which plugin did you look at?)
cordova-plugin-geolocation[https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-geolocation/index.html]
This plugin provides information about the device's location, such as latitude and longitude.
Note: This plugin only works if you serve the app from a secure url. In order to do so you
will need to setup the ember-cli to serve the index.html from an https domain. The following link guides you through the process of generating your own self signed ssl certificate:
https://devcenter.heroku.com/articles/ssl-certificate-self

#### Usage
1. Install the plugin [ember cdv:plugin add cordova-plugin-geolocation]
2. Generate the files [ember generate component geolocation-display]
3. Edit the neccesary files:

3a. /app/templates/application.hbs

>This calls the geolocation-display component.

> Raw code below

  ```hbs
Cordova Plugin For Geolocation

{{geolocation-display }}
  ```
3b. /app/templates/components/geolocation-display.hbs

>This template takes values from javascript file and assigns the values to the lat and lng.

> Raw code below

```hbs
Latitude value: {{lat}}<br>
Longitude value: {{lng}}<br>
```

3c. /app/components/geolocation-display.js

>This javascript Queries Cordova and accepts a Position object, which contains the current GPS coordinates. Then the variables
lng,lat and alt are updated with the current GPS coordinates.

> Raw code below

```javascript
import Ember from 'ember';

export default Ember.Component.extend({
  lng: 0,
  lat: 0,
  alt: 0,

  on: true,
  startLogging: function(){
    //begin logging geolocation data once the component launches

    var component = this;
    this.computeGPS(component);

  }.on('init'),
  computeGPS: function(component){
    Ember.run.later(function(){
      //wrapper to preserve binding satistfaction
      try {
        //invoke cordova geolocation Plugin and get geolocation data
        navigator.geolocation.getCurrentPosition(function (position) {//success callback
            //console.log('acceleration setvars called');
            component.set('lng', position.coords.longitude);
			console.log(position.coords);
            component.set('lat', position.coords.latitude);
            component.set('alt', position.coords.altitude);


        }, function (error) {//error callback

            console.log(error);
        });
      }
      catch(err){
        console.log('error: '+err);
      }
      if(component.get('on')){
        //keep running
        component.computeGPS(component); //recurse
      }

    }, 10000);//run ever 10000ms
  }
});
```

#### Author
Gib Filter

#### Plugin Name (which plugin did you look at?)
Media - https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-media/index.html

This plugin provides the ability to record and play back audio files on a device.

#### Usage
1. Install plugin [ember cdv:cordova plugin add cordova-plugin-media]
2. Create new componenent in ember for our view [ember generate component gif-mash]
3. Update Files

3a. /app/templates/application.hbs
> Call our new component from the main application
> Code:

```hbs
.gif mashup machine!
{{gif-mash}}
```

3b. /app/templates/components/gif-mash.hbs
>Set up the gif-mash home screen
>Code:

```hbs
<br>
URL of .gif: {{input value=gifUrl}}<br>
URL of music: {{input value=musicUrl}}<br>

{{#if isPlaying}}
	<button {{action "stopMus"}}>Stop!</button>
	<img src={{gifUrl}}>
{{else}}
	<button {{action "playMus" musicUrl}}>Play!</button>
{{/if}}
```

3c. /app/components/gif-mash.js
> Background stuff for the gif-mash

> Code:

```javascript
import Ember from 'ember';

export default Ember.Component.extend({
	isPlaying: false,
	my_media: null,
	genMash: null,
	loadCode: null,
	musicUrl: "http://www.midiworld.com/download/4726",
	gifUrl: "http://i1090.photobucket.com/albums/i363/scooterr98/Icons/170422_dancing_banana.gif",
	apiUrl: "https://is.gd/create.php?format=simple&url=",
	ajax : function(getIt) {
		return Em.$.ajax({url: getIt});
	},

	actions: {
		playMus : function (musUrl) {

			this.my_media = new Media(musUrl,
				 // success callback
		        function () {
		            console.log("playAudio():Audio Success");
		        },
		        // error callback
		        function (err) {
		            console.log("playAudio():Audio Error: " + err);
		            console.log(err);
		        });

		   	//play the song
			this.my_media.play();
			//set playing to true, to toggle the view in the template
			this.set('isPlaying', true);
		},
		stopMus : function () {
			//stop music, toggle the is playing
			this.my_media.stop();
			this.my_media.release();
			this.set('isPlaying', false);
		},
	}

});
```

#### Authors

Glenn Anderson

#### Plugin Name (which plugin did you look at?)

Dialogs & Network Information

#### Usage

#### 1. Install Cordova Plugin
```bash
cordova plugin add cordova-plugin-network-information
cordova plugin add cordova-plugin-dialogs
```

#### 2. Generate Ember Component
```bash
ember generate component network-display
```

#### 3. Edit the following files:
#### 3a. application.hbs
Calls the network-display component.
```hbs
 Networking Status
 {{network-display}}
```
#### 3b. network-display.hbs
````hbs
You are using a {{networkType}} network <br>
{{notification}}
````
#### 3c. network-display.js
````javascript
import Component from '@ember/component';
import { later } from '@ember/runloop';

export default Component.extend({
  networkType: 'Unknown Network',
  notification: 'No notification',
  on: true,
  init: function() {
    this._super(...arguments);
    this.checkConnections(this);
  },
  checkConnections: function(scope) {
    later(function() {
      let newNetworkState = navigator.connection.type;
      if(newNetworkState !== scope.get('networkType')){
        if(scope.get('networkType') !== 'Unknown Network') {
          navigator.notification.alert(
            'Your connection type has changed. You are now using ' + newNetworkState + '.',
            scope.alertDismissed,
            'Connection Changed',
            'Ok'
          );
        }
        if(newNetworkState !== 'wifi') {
          scope.set('notification', 'Offline');
        }
        else {
          scope.set('notification', 'Online');
        }
      }

      scope.set('networkType', newNetworkState);

      if(scope.get('on')){
        scope.checkConnections(scope); //recurse
      }
    }, 100);
  },
  alertDismissed: function(scope) {

  }
});

````

#### Authors

Dan Lucier

#### Plugin Name (which plugin did you look at?)

Dialogs - https://cordova.apache.org/docs/en/latest/reference/cordova-plugin-dialogs/

This plugin provides the ability to access and customize native dialog boxes.

#### Usage

#### 1. Install plugin
```bash
corber plugin add cordova-plugin-dialogs
```

#### 2. Generate Ember files

##### 2a. Generate Ember application template
```bash
ember generate template application
```

##### 2b. Generate Ember component
```bash
ember generate component dialogs-display
```

#### 3. Edit necessary files

##### 3a. Edit /app/templates/application.hbs
Although this app will be presenting pop-up display boxes, any text in this file will be shown on the screen in the background.
```hbs
Demo: cordova-plugin-dialogs
<br />Methods used:
<br />navigator.notification.prompt
<br />navigator.notification.confirm

{{dialogs-display}}
```

##### 3b. Edit /app/templates/components/dialogs-display.hbs
This display is intended for QA testing only.
```hbs
<!-- This display is for QA testing only
Comment out the below lines prior to final deployment -->
<br />Player's Name: {{playerName}}
<br />Number To Guess: {{numGuess}}
<br />Player Guess: {{playerGuess}}
```

##### 3c. Modify /app/components/dialogs-display.js
This app implements the prompt and confirm methods of the dialogs plugin as a simple number guessing game.
```javascript
import Component from '@ember/component';

export default Component.extend({
  playerName: 'Player One',
  numGuess: 0,
  playerGuess: 0,
  init(){
    this._super(...arguments);
    this.introduction(this)
  },

introduction(component){
  navigator.notification.prompt(
    "Please, enter your first name", //Introduction - prompt message
    function setPlayerName (results){ //Introduction - prompt callback
      component.set('playerName', results.input1);
      navigator.notification.confirm(
        "Would you like to play a game?", //Greetings - confirm message
        function( index ) { //Greetings - confirm callback
          switch( index ) {
            case 1: //Greetings - if button one was pressed
              component.numberGuessGame(component);
              break;
            case 2: //Greetings - if button two was pressed
              break;
          }
        },
        "Greetings " + component.get('playerName'), //Greetings - confirm title
        ["Yes", "No"] //Greetings - confirm button text
      );
    },
    "Introduction", //Introduction - prompt title
    ["Hello!"], //Introduction - prompt button text
    ""
  );
},

numberGuessGame(component){
  component.set('numGuess', Math.floor((Math.random() *10) +1)); //randomly set number to be guessed
  navigator.notification.prompt(
    "What is your guess?", //Number Guess Game - prompt message
    function playerGuess (results){ //Number Guess Game - prompt callback
      component.set('playerGuess', results.input1);
      //Correct Player Guess
      if (component.get('playerGuess') == component.get('numGuess')){
        navigator.notification.confirm(
          "Would you like to play again?", //Correct Player Guess - confirm message
          function( index ) { //Correct Player Guess - confirm callback
            switch ( index ) {
              case 1: //Correct Player Guess - if button one is pressed
                component.numberGuessGame(component);
                break;
              case 2: //Correct Player Guess - if button two is pressed
                break;
            }
          },
          "Congratulations!! " + component.get('numGuess') + " is the number I was thinking of!", //Correct Player Guess - confirm title
          ["Play Again", "Exit"] //Correct Player Guess - confirm button text
        );
      }
      else {
        //Incorrect Player Guess
        navigator.notification.confirm(
        "Better luck next time!", //Incorrect Player Guess - prompt message
        function( index ) { ////Incorrect Player Guess - prompt callback
          switch ( index ) {
            case 1: //Incorrect Player Guess - if button one is pressed
              component.numberGuessGame(component);
              break;
            case 2: //Incorrect Player Guess - if button two is pressed
              break;
          }
        },
        "Sorry, the number I was thinking of is " + component.get('numGuess') + ".", //Incorrect Player Guess - prompt title
        ["Play Again", "Exit"] //Incorrect Player Guess - prompt button text
      );
    }
  },
  "I'm thinking of a number between 1 and 10...", //Number Guess Game - prompt title
  ["Guess"] //Number Guess Game - prompt button text
  );
},

});
```

##### 3d. Modify /app/tmeplates/dialogs-display.hbs
This modification is just to completely comment out the display.
```hbs
<!-- This display is for QA testing only
Comment out the below lines prior to final deployment
<br />Player's Name: {{playerName}}
<br />Number To Guess: {{numGuess}}
<br />Player Guess: {{playerGuess}} -->
```

[Top](#table-of-contents)

### Next time we explore vulnerabilities and exploitations in hybrid apps.

#### License
<a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-sa/4.0/88x31.png" /></a><br /><span xmlns:dct="http://purl.org/dc/terms/" property="dct:title">CYBER8480 and related works</span> by <a xmlns:cc="http://creativecommons.org/ns#" href="http://faculty.ist.unomaha.edu/mlhale" property="cc:attributionName" rel="cc:attributionURL">Matt Hale</a> are licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nc-sa/4.0/">Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License</a>.
