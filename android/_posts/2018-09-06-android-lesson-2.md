---
layout: post
title:  "Lesson 2 - Recycler Views and UI"
date:   2018-09-06
published: false
---

Material Design:
Material Design is a compromise between flat, minimalist design (like Microsoft's Metro design) and older designs focused on real world objects (making buttons look glossy and realistic) by expanding on the "card motif."
Android Studio encourages the default Material Design pattern with built in Views like CardViews, icons, and more.

Scalable Vector Graphics (SVGs):
One way to implement Material Design is through Scalable Vector Graphics, or svg. SVG images store xml that essentially defines the outline of an image as a function, making it effectively infinite resolution.
Android Studio comes with a large suite of Material Design svg icons. To add one, right click the res->drawable folder and select New->Vector Asset.
Text uses SVG, so it appears sharp no matter how large.

Common Libraries:
Palette - a library to extract and use colors from images
Glide - a library to load very large images or images from a URL
CardView - the basic item in Material design
You can add dependicies for these in build.gradle

Javascript Object Notation (JSON):
Javascript object notation is a very common way of structuring data, and the way objects are stored in Javascript.
Kind of like a combination of dictionaries / HashMaps and arrays
With RecyclerViews, JSON are an alternative way of storing your data.

JSON Properties:
- JSON objects are signified by { } and JSON arrays are signified by [ ].
- Use key value pairs, a key is always a string and a value is either an int, string, boolean, float, another JSON object, or another JSON array
- In Javascript if this object is called response, response.abilities[0].ability.name returns the name of the first ability
- In Java - response
              .getJSONArray("abilities")
              .getJSONObject(0)
              .getJSONObject("ability")
              .getString("name")

When working with JSON...
- Don't use as a data structure - put it into an arraylist / hashmap of objects as soon as possible
- Don't mess up the key names - the compiler will not complain and you'll end up with a vague error
- https://jsonformatter.curiousconcept.com is your friend, it will help you visualize the JSON well so you can figure out what keys you need to access

Making Lists in Android:
Briefly, Lists in Android work by extending the Adapter class, which you attach to your actual View.
The Adapter class essentially maps your data to a custom view, which would most likely have its own layout file. 
You can also override methods relating to what to do when the dataset changes.

This avoids redundancy because we don’t want to make a million views that are exactly the same.
It preserves modularity because we can change how many, which order, and even which kind of Views show up.
It also abstracts away a lot of the complex code that went into creating RecyclerViews.

We want to reuse views so that loading 1000 emails into a single list won't slow down your phone.
Only the Views displayed on the screen load, and they get deleted once they’re off the screen.

Introducing...RecyclerViews!
- Recycling the Views is done by default
- Not attached to a specific Layout, can change the LayoutManager of the RecyclerView
- Has animations for common actions

RecyclerViews also support fancy things like horizontal lists, grid lists, animations, and much more.
ListViews are used if you're making a widget, but they're pretty similar to RecyclerViews in terms of code.



Let's say we were implementing an adapter for a simplified version of the Gmail app.

Custom View:
The first thing we would need to do is design a row view layout file to define what we want the layout of each email to look like.
- Try to use a CardView as the parent View instead of ConstraintLayout
- Make sure to make the parent View wrap_content so each item doesn't take a full page

Row Model Class:
Typically the data will always be of the same structure, so we can use a class like this:
class Email {
	String imageUrl;
	String title;
	String body;
	String description;
}

Email Recycler View Adapter:
We connect a list of Email items to the row_views using an Adapter like this:

class MyAdapter extends RecyclerView.Adapter<MyAdapter.ViewHolder> {
	ArrayList<Email> emails;
	MyAdapter(ArrayList<Email> emails) {
    this.emails = emails;
	}
	@Override
	ViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
    return ViewHolder(LayoutInflater.from(parent.context).inflate(R.layout.row_view,parent,false));
	}
	@Override
	void onBindViewHolder(ViewHolder holder, int position) {
		holder.bind(position);
	}
	@Override
	int getItemCount() { return emails.size(); }
	
  class ViewHolder extends RecyclerView.ViewHolder {
		TextView title;
		...
		ViewHolder(View v) {
      super(v);
      title=(TextView) findViewById(R.id.title);
      ...
    }
		void bind(int position) {
			title.setText(emails.get(position).title);
			...
		}
	}
}

"ViewHolder" is the class representing our own defined View that acts as a container for our row_view.xml
"getItemCount" gets the number of items in the list
"onCreateViewHolder" returns a custom ViewHolder with our row view
  - Uses a LayoutInflater to "inflate" the xml file into a View object in our code
  - You can override getItemViewType to map some positions to a different view type (an integer), and maybe inflate a different layout file depending on that 
"onBindViewHolder" puts data about the different emails into the view holder
  - Typically, you will have a bind method in your ViewHolder to bind a certain data point to your row, use the position argument to index into your data source

Attaching an adapter:
Now, we can initialize this adapter in our activity.
MyAdapter adapter = new MyAdapter(this, emails);
RecyclerView recyclerView = (RecyclerView) findViewById(R.id.rv);
recyclerView.setLayoutManager(new LinearLayoutManager(this));
recyclerView.setAdapter(adapter);

Updating an adapter:
Once you set your adapter, changing the data won't actually update the RecyclerView!
To let the RecyclerView know that the data set has changed, use adapter.notifyDataSetChanged()
  - Do not set the adapter again
  - notifyDataSetChanged will update the whole thing, but if you just want to add a single thing / a few items / remove one thing / update one thing, etc, there are more specific methods you can use, like notifyItemInserted, notifyItemRemoved, notifyItemRangeInserted, notifyItemChanged, etc.
Changing the layout manager will work at runtime normally
