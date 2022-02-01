---
title: Build a App Complete
module: 4
---

# Complete Instructions <br />

### Create your first Cordova app

This guide shows you how to create a JS/HTML Cordova application and deploy them to various native mobile platforms using the cordova command-line interface (CLI). For detailed reference on Cordova command-line, review the CLI reference

### Installing the Cordova CLI
The Cordova command-line tool is distributed as an npm package.

To install the cordova command-line tool, follow these steps:

Download and install Node.js. On installation you should be able to invoke node and npm on your command line.

(Optional) Download and install a git client, if you don't already have one. Following installation, you should be able to invoke git on your command line. The CLI uses it to download assets when they are referenced using a url to a git repo.

Install the cordova module using npm utility of Node.js. The cordova module will automatically be downloaded by the npm utility.

### on OS X and Linux:
  $ sudo npm install -g cordova
On OS X and Linux, prefixing the npm command with sudo may be necessary to install this development utility in otherwise restricted directories such as /usr/local/share. If you are using the optional nvm/nave tool or have write access to the install directory, you may be able to omit the sudo prefix. There are more tips available on using npm without sudo, if you desire to do that.

### on Windows:
  C:\>npm install -g cordova
The -g flag above tells npm to install cordova globally. Otherwise it will be installed in the node_modules subdirectory of the current working directory.

Following installation, you should be able to run cordova on the command line with no arguments and it should print help text.

### Create the App
Go to the directory where you maintain your source code, and create a cordova project:

$ cordova create hello com.example.hello HelloWorld
This creates the required directory structure for your cordova app. By default, the cordova create script generates a skeletal web-based application whose home page is the project's www/index.html file.

### Add Platforms

All subsequent commands need to be run within the project's directory, or any subdirectories:

$ cd hello
Add the platforms that you want to target your app. We will add the 'ios' and 'android' platform and ensure they get saved to config.xml and package.json:

$ cordova platform add ios
$ cordova platform add android
To check your current set of platforms:

$ cordova platform ls
Running commands to add or remove platforms affects the contents of the project's platforms directory, where each specified platform appears as a subdirectory.

Note: When using the CLI to build your application, you should not edit any files in the /platforms/ directory. The files in this directory are routinely overwritten when preparing applications for building, or when plugins are re-installed.

### Install pre-requisites for building
To build and run apps, you need to install SDKs for each platform you wish to target. Alternatively, if you are using browser for development you can use browser platform which does not require any platform SDKs.

To check if you satisfy requirements for building the platform:

$ cordova requirements

### Requirements check results for android:
Java JDK: installed .
Android SDK: installed
Android target: installed android-19,android-21,android-22,android-23,Google Inc.:Google APIs:19,Google Inc.:Google APIs (x86 System Image):19,Google Inc.:Google APIs:23
Gradle: installed

### Requirements check results for ios:
Apple OS X: not installed
Cordova tooling for iOS requires Apple OS X
Error: Some of requirements check failed
See Also
Android platform requirements
iOS platform requirements
Windows platform requirements
Build the App
By default, cordova create script generates a skeletal web-based application whose start page is the project's www/index.html file. Any initialization should be specified as part of the deviceready event handler defined in www/js/index.js.

Run the following command to build the project for all platforms:

$ cordova build
You can optionally limit the scope of each build to specific platforms - 'ios' in this case:

$ cordova build ios

### Test the App
SDKs for mobile platforms often come bundled with emulators that execute a device image, so that you can launch the app from the home screen and see how it interacts with many platform features. Run a command such as the following to rebuild the app and view it within a specific platform's emulator:

$ cordova emulate android


Following up with the cordova emulate command refreshes the emulator image to display the latest application, which is now available for launch from the home screen:

Alternately, you can plug the handset into your computer and test the app directly:

$ cordova run android
Before running this command, you need to set up the device for testing, following procedures that vary for each platform.

### Add Plugins
You can modify the default generated app to take advantage of standard web technologies, but for the app to access device-level features, you need to add plugins.

A plugin exposes a Javascript API for native SDK functionality. Plugins are typically hosted on npm and you can search for them on the plugin search page. Some key APIs are provided by the Apache Cordova open source project and these are referred to as Core Plugin APIs. You can also use the CLI to launch the search page:

$ cordova plugin search camera
To add and save the camera plugin to package.json, we will specify the npm package name for the camera plugin:

$ cordova plugin add cordova-plugin-camera
Fetching plugin "cordova-plugin-camera@~2.1.0" via npm
Installing "cordova-plugin-camera" for android
Installing "cordova-plugin-camera" for ios
Plugins can also be added using a directory or a git repo.

NOTE: The CLI adds plugin code as appropriate for each platform. If you want to develop with lower-level shell tools or platform SDKs as discussed in the Overview, you need to run the Plugman utility to add plugins separately for each platform. (For more information, see Using Plugman to Manage Plugins.)

Use plugin ls (or plugin list, or plugin by itself) to view currently installed plugins. Each displays by its identifier:

$ cordova plugin ls
cordova-plugin-camera 2.1.0 "Camera"
cordova-plugin-whitelist 1.2.1 "Whitelist"
