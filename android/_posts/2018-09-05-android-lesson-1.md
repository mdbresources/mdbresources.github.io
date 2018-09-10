---
layout: post
title:  "Lesson 1 - Getting Started"
date:   2018-09-05
published: false
---

*Notes taken by Shreya Reddy and formatted by Aayush Tyagi*

# Java Review
In order to learn Android development, you'll need to know Java. Although we won't go over everything Java related, we'll go through a quick refresher.

## Data Types

### Declaring Variables

In Java, variables are declared by stating the type and then the name of the variable, and they are assigned with `=` and then the value you want to assign to it. Variables do not change types! For example,
```java
int yearInt = 2017;
String str = null;
float gpa = 4.20f;
String year = "2017";
year = yearInt; // does not compile, can't assign int to String
year = "2016";
char c;
c = 'a';
```

### Primitive Data Types
Primitive data types store raw data in a fixed amount of space, and are always lowercase in Java. Examples include
- `int` / `long` for integer values (Ex. `12` / `15L`)
- `float` / `double` for decimals (Ex. `4.20f` / `0.0`)
- `boolean`
- `char`
- other ones that are hardly used (`byte`, `short`)

Other non primitive data types are all children of the `Object` class, and do not directly store the values they represent (they store an address that points to the value.) As a result, using the `==` operator will usually not work, and values are instantiated to `null`, which doesn't point to anything. Attempting to invoke a method on a `null` value will raise a `NullPointerException`, or NPE.

## Methods

All functions belong to a class, so we call them methods. Methods must be called from an instance of a class unless they are specifically marked as `static`. Static methods must be called from the class itself (like `Math.round()`), and effectively do not belong to the object.

Example of a method in Java:
```java
class Adder {
    public static int addOne(int x) {
        return x + 1;
    }
}
...
Adder.addOne(3); // returns 4
```
## Loops
There are three types of loops in Java:
```java
for (int i = start; i < end; i += 1) {
    //do stuff
}
for (Object obj : objList) {
	//do stuff to obj
}
while (condition) {
	//do stuff
}
```

## Classes
Classes are a model for a new type of object that you want to work with. Classes can be children of other classes, and can be parents of others. All classes are children of the `Object` class and therefore have the methods `hashcode()` and `toString()`. Here is an example of a simple class:
```java
class Rectangle extends Shape {
	int width;
	int height;
	public Rectangle(...) {...}
	public int getWidth ...
	public int getHeight ...
	@Override
	public int getArea ...
}
```
### Objects
Objects are instances of the classes. While the above class is just an idea or template of a Rectangle, we can create a our own `Rectangle rect` with its own properties. 
```java
Rectangle rect = new Rectangle(3, 4);
rect.getArea(); // returns 12
```

### Anonymous Classes
Sometimes you want to extend an abstract class or interface for just a single object in Java (something very common in Android). These are called anonymous classes and have their own unique syntax.
```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    void onClick(View view) {
        // do stuff
    }
});
```

# Basic Git
## What is Git?
Git is a solution for version control - the idea that to prevent errors, development code should be kept separate from working code to prevent bugs. It also makes collaboration much easier in larger codebases. Despite its similarities to Google Drive, Git is not an offline storage solution, and should never be treated as one.

In version control, there is typically a master, prod, or release branch (a version of your codebase) that only contains ready to deploy features. You can branch off of this to add your own features or work on bugs, so that you can mess around while the working version of the app still exists and (more importantly) people can work on their own features in parallel.

Once you're done with your code and you think it's good to put (or *merge*) into master, you have two options:
1. Push your code to master - you may get a merge conflict which you have to manually resolve, but Git can handle minor changes.
2. Make a pull request - ask for someone to review it and when everyone's good to go, you or someone else with write access can merge it in.

Git also allows you to manage versions on a single branch too, every time you push something to Github, it's stored as a diff, only remembering the changes you made from the last version (or *commit*). You can revert to any commit at any time, a useful feature if you make a mistake.

## Github
Serves as a remote location for your git "repository". You can add collaborators, write a wiki, check branches, and manage pull requests from here. Typically employers will check your Github, so it's good to have your projects on Github even if you're working solo and don't need version control. It's not a Google Drive alternative so you shouldn't (though you can) edit code on Github.

Common Commands:
- `git init`
  - Enables git commands in the current directory and all subdirectories
- `git remote add origin https://github.com/...`
  - Adds a remote location for your code called "origin" linking to the given URL. Doesn't actually interact with it here.
- `git clone (-b branchName) https://github.com/...`
  - Clones the code at the URL's master branch. To clone a specific branch, use the -b
- `git checkout (-b) branchName`
  - Creates and enters a new branch with your current changes with name "branchName". If the branch already exists, ignore the -b
- `git add -A`
  - Saves the state of your code and makes it ready to commit
- `git commit -m "first commit"`
  - Commits the changes with message "first commit." Commits are accessible even when more are pushed on top, so use useful messages.
- `git push origin branchName`
  - Pushes the commit to the specific remote at the specific branch. Push often to your branch to avoid losing code! You can also push to master, though it's better to make a pull request through Github.
- `git pull origin master`
  - Pulls the code from master into your current code. If you're working on a feature that someone else has edited, you will have to pull and resolve any conflicts to get that code. 

# Intro to Android
This part will be more of a walkthrough, and we assume that you already have the latest version of Android Studio up and running. Make sure that you're able to run the demo app - a lot of times errors will pop up prompting you to install things, but they provide links for you to do so. If you run into anything unexpected, Google and StackOverflow are your friends!

Create Android Project
- Name it whatever you want
- Pick a unique package name if you plan on launching your app on the store
- Target API: Default is API 15 - Ice Cream Sandwich to support older phones
- Create an empty activity
  - Generates MainActivity.java (view controller with Java) and activity_main.xml (layout file)
- Manifest file defines the different activities (like screens) within your app and lets you decide which activity to label your MainActivity that you launch when the app first opens
- "java" folder is where all of your Java code for activities, services, etc.
- "res" folder is where all of your resources lie for layout files, images, audio, icons, strings, etc.
- build.gradle file has all of your app's dependencies on external libraries and APIs
- Use autocomplete to find views and methods you can use in your activity

Views:
A view is an abstract class representing an item the user can see on the screen, like a regular text field, button, image, switch, etc. Views have properties like text and color.
Some Views are containers for other Views, like a dropdown menu or a scrolling list.
In Android Studio, editing any layout file will show common Views on the left of the visual editor.
Ex. TextView, ImageView, RecyclerView, CardView, FloatingActionButton

Programmatically Updating Views:
View v = findViewById(R.id.viewId);
v.setOnClickListener(new OnClickListener() {//autofill});
((TextView) findViewById(R.id.text)).setText("Hello");

Layouts:
A specific View that defines how the Views contained will be arranged
ConstraintLayout
The standard layout for all uses. Views are constrained to each other in a variety of ways to allow for dynamic and sensible layouts
"RelativeLayout" is an outdated version of this
LinearLayout
All Views are organized either horizontally or vertically. Nice and simple, with the added functionality of evenly spacing the Views to fill up the space
GridLayout
CoordinatorLayout

Layout Files:
Layout files are XML files that describe how Views will be initialized. It is possible to create them in the Java files, but typically the layout files are in the res folder.
Android Studio has a handy visual editor that lets you add Views to your layout file and edit their starting properties, but sometimes it's faster to edit in the XML.

Activities:
For now, you can think of an activity as essentially one screen in Android (this gets more inaccurate the more you learn about Android), and typically corresponds to one layout file. This is where we handle the logic for the screen. 
In addition to what happens while you're in this Activity, there are also several methods called at different points in the lifecycle.

Activity Lifecycle:
Note that when an Activity starts, onCreate(), onStart(), and onResume() are all called before it starts running.
<Insert graphic>

Intents:
Intents represent actions that can leave the Activity and do something else. With an Intent, you can do many things, such as
- Open a new Activity (in your app or another)
  - Before executing the Intent, you can add data, or "extras" to it
- Open an Activity, get data, and return to your Activity
  - For example, to take a picture
- Start background services or broadcast data

Contexts:
A context is usually passed into a method that needs to know what the current Activity is, like an Intent.
Every Activity is a Context, so if you're defining a method within an Activity and need the Context, you can just use the keyword this.
If you're within an anonymous class / object, "ActivityName.this" will be needed to clarify which class it refers to.

Intent Methods:
Intent i = new Intent(this, OtherActivity.class);
i.putExtra("age", 5);
startActivity(i); //also startActivityForResult
int weight = getIntent().getExtras().getInt("age");
