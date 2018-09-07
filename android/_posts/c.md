# The Row View
- first design the layout for your little row
- under the layout folder in the resources
- in the code, you can create model classes 

# Demo
- start with an empty activity, MainActivity, standard stuff
- have to add dependencies for recyclerview and cardview
  - make your layouts for row_view
    - wrap_content and stuff
- recyclervie
  - setlayoutmanager
  - setadapter
  - make your adapter class, extends RecyclerView.Adapter<VH>
    - you make your own VH class which should extend RecyclerView.ViewHolder
  - make constructor, which takes in context and (potentially) data, and sets it to instance variable
    - context used for displaying images
  - three methods
    - getItemCount is how long the list is, just do `data.size()` or something
    - onBindViewHolder
      - lmao what's a viewholder
      - add all the pertinent views
      - put in the data from the item at the given position into the given viewholder
    - onCreateViewHolder
      - `LayoutInflater.from(context).inflate(R.layout.row_view, parent, false);`
  - so what it does
    - set the adapter
    - get number of items
    -
