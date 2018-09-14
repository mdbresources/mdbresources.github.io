---
layout: post
title:  "Lesson 0 - Setting Up Your Environment"
date:   2018-09-02
published: false
---
# Installing Android Studio
lol figure it out b

# Running your first app
Close any projects you might have open and you should arrive at this screen:


<img src="../assets/000.png" width="500" />


Click on Start a new Android Project and you should arrive here:

<img src="../assets/001.png" width="500" />

At this screen, you can name it anything you want, but pick a reasonable (and unique!) package name if you plan on launching the app to the app store. Make sure to deselect the "Kotlin support" checkbox if you're planning on following along in Java.

After this, you'll see another screen asking you to pick your minimum version of Android, and if you click "Help me choose" you'll see a distribution chart.


<img src="../assets/002.png" width="500" /> <img src="../assets/003.png" width="500" />

Choosing these is a bit up to you, since as the distribution screen will show you, newer versions of Android support more features that will make your life easier as a developer, but also support fewer devices. I would recommend 19 if you're looking to support the most people, 21 if you want a lot more features than 19 but not support everyone.

On the next "Add an Activity to Mobile" screen select "Empty Activity" and finish making the app. Try to run the app by clicking the play button up over here

<img src="../assets/006.png" width="500" />

The app will first have to build into something executable by your Android device (which is what the hammer represents), and will probably not be able to build initially since you have to install the Software Development Kit (SDK) depending on what version of Android you're targeting. Essentially, if something is blue in your error log and prompts you to install something, just do what it says!

If you don't have a device to run the default app on, the run screen will have a link to the Virtual Device manager, where you can create and use virtual devices. Once you have the default "Hello, world!" app running, you're ready to move on.

# Android File Structure
If you've created the project successfully, you'll be greeted with this file tree on the left (make sure you're viewing it in "Android" mode and not "Project" mode, as specified in the dropdown at the top.)

<img src="../assets/005.png" width="500" />

It might seem daunting at first, but you only have to worry about the directories expanded in the screenshot above!

## manifests
The manifest file defines the different activities (like screens) and broadcast receivers within your app and lets you decide which activity to label your MainActivity that you launch when the app first opens. You also add your permissions that you want to give to the app, like internet or storage.

## java/packagename
This is where you store all your Java / Kotlin code, and effectively where all the source code of the app goes. Currently, there should be one Java file here called MainActivity. To create an Activity, DO NOT create a Java file. You should right click the packagename folder, go to New, and select New Activity, since this will do extra stuff like create a default layout file and register it in the manifest.

## res
The `res` folder is where all visual resources and other assets are stored like layout files, images, audio, icons, strings, fonts, etc. The files in here are typically in XML, a language remniscient of HTML. Don't worry, it's not really a new language you have to learn! All the files are linked to Java using a special reference library called `R`.

The drawable folder is where images are stored. They recieve a unique id that can be referenced with `R.drawable.filename`, but it's also possible to reference them using a string value for the filename (although this involves receiving the above id, which is an integer value.) To add some default icons, right click the drawable folder

The layout folder describes how all of our screens / parts of screens should be laid out. These can also be referenced by `R.layout.layoutname`, but are more deeply linked with their associated java files. To see what I mean, in MainActivity.java you can find the line
```java
setContentView(R.layout.activity_main);
```
and in activity_main.xml you can find the line
```xml
tools:context="packagename.MainActivity"
```

For the values folder, you shouldn't add files directly to this folder, but instead add to the existing files. Similar to the other folders, Strings in strings.xml can be referenced with `R.string.stringname` in Java and `@string/stringname` in XML. These files are used to be able to reference values that may change depend on who's using the app: for example, you might want user facing strings to be in a different language depending on the user's default language, and you might want dimensions to be different for tablets. It's good practice to save these values in their corresponding files regularly.

## gradle
Gradle is used to compile the app together and link together the Java and res folders. It also links together external libraries and APIs (including most of the core Android libraries!)

# Using Android Studio
There's several important features of Android Studio that need to be covered before we can get started writing any code. 

## General Shortcuts
These are shortcuts that can generally be used throughout the app. Any instance of `Ctrl` should be replaced with Command for Macs.

### Ctrl + Click
This will generally take you to the declaration of whatever you are clicking. This is useful if you're looking at a method or variable, and you're not sure where to find it to see what it does. If you're at the definition, this is also useful since it shows all the places where the method / variable is being referenced. 

### Alt + Enter
Many times, Android Studio will recognize that something is wrong, but will be reasonably confident that it knows how to fix it. For example, if a red variable is underlined in white (it needs to be imported), highlighted yellow (potentially causing bugs / is bad practice), grayed out (it's never used) then 

### Other useful things
- Refactor (rename all instances of) a variable with right click -> refactor -> rename
- Ctrl + \[ to go back to wherever your cursor was before
  - Ctrl + \] to move it forward
- Ctrl + O to search through Java files
- Ctrl + / to comment out with single line comment(s)
  - Ctrl + Shift + / to comment out with multiline comment
- Ctrl + F to search in file
  - Ctrl + Shift + F to search in all files
- Ctrl + R to find and replace in file
  - Ctrl + Shift + R to find and replace in all files

## Layout Stuff

### Asset Studio

### Constraint Layout editor

## Java Stuff

## Other Tools

### Logcat

### Version Control


