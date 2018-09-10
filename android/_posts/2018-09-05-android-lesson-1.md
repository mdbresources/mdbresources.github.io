---
layout: post
title:  "Lesson 1 - Getting Started"
date:   2018-09-05
published: false
---

*Java Basics:*
Primitive Data Types: Different from other classes - don’t have methods, can’t be null, don’t extend the master Object class
- int / long for integer values (Ex. 12 / 15L)
- float / double for decimals (Ex. 4.20f / 0.0)
- boolean
- char
- other ones that are hardly used (byte, short)

Declaring Variables: Different from other classes - don’t have methods, can’t be null, don’t extend the master Object class
int year = 2017;
String str = null;
float gpa = 4.20f;
String year = "2017";
- reassigning a value with a different type to variable "year" will not compile
char c;
c = ‘a’;

Arithmetic Operators: Unlike some languages, separation between integers and decimals
5 / 2 returns 2
5 / 2. returns 7.0
'a' + 2 returns 'c'
"Hello, " + "World"

Methods: All functions belong to a class, so we call them methods
Example of a method in Java:
public static int addOne(int x) {
	return x + 1;
}

Loops: There are 3 types
for (int i = start; i < end; i += 1) {
	//do stuff
}
for (Object obj : objList) {
	//do stuff to obj
}
while (condition) {
	//do stuff
}

Classes: A definition of a new type of object you want to work with. All classes extend Object.
class Rectangle extends Shape {
	int width;
	int height;
	public Rectangle(...) {...}
	public int getWidth ...
	public int getHeight ...
	@Override
	public int getArea ...
}

Anonymous Classes: Sometimes you want to extend an abstract class just to use it once in Java (very common in Android). These are anonymous classes.
new AsyncTask(...) {
	@Override
	Void doInBackground ...
}.execute()

*Basic Git*
What is Git?
Git is a solution for version control - the idea that to prevent errors, development code should be kept separate from working code to prevent bugs. It also makes collaboration much easier in larger codebases.
Despite its similarities to Google Drive, Git is not an offline storage solution, and should never be treated as one.

Version Control:
- Typically a "master" or "prod" branch (a branch is a version of your code) that only contains ready to deploy features
- Collaborators branch off a master to work on some feature
- Two options once finished
  - Push the code to master - might get merge conflict, have to manually resolve
  - Submit a pull request
- Allows people to work on different features at the same time, just pull from master regularly to keep up to date

Github:
Serves as a remote location for your git "repository". You can add collaborators, write a wiki, check branches, and manage pull requests from here.
Typically employers will check your Github, so it's good to have your projects on Github even if you're working solo and don't need version control.
It's not a Google Drive alternative so you shouldn't (though you can) edit code on Github.

Common Commands:
git init
  - Enables git commands in the current directory and all subdirectories
git remote add origin https://github.com/…
  - Adds a remote location for your code called "origin" linking to the given URL. Doesn't actually interact with it here.
git clone (-b branchName) https://github.com/…
  - Clones the code at the URL's master branch. To clone a specific branch, use the -b
git checkout (-b) branchName
  - Creates and enters a new branch with your current changes with name "branchName". If the branch already exists, ignore the -b
git add -A
  - Saves the state of your code and makes it ready to commit
git commit -m "first commit"
  - Commits the changes with message "first commit." Commits are accessible even when more are pushed on top, so use useful messages.
git push origin branchName
  - Pushes the commit to the specific remote at the specific branch. Push often to your branch to avoid losing code! You can also push to master, though it's better to make a pull request through Github.
git pull origin master
  - Pulls the code from master into your current code. If you're working on a feature that someone else has edited, you will have to pull and resolve any conflicts to get that code. 

*Android Demo:*
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
