---
layout: post 
title:  Android RecyclerView
---

<!-- links -->
[android-developer-recyclerview]:https://developer.android.com/reference/android/support/v7/widget/RecyclerView.html

<!-- post start -->
The RecyclerView widget is a more advanced and flexible version of ListView. This widget is a container for displaying large data sets that can be scrolled very efficiently by maintaining a limited number of views. Use the RecyclerView widget when you have data collections whose elements change at runtime based on user action or network events.

The RecyclerView class simplifies the display and handling of large data sets by providing:

1. Layout managers for positioning items
2. Default animations for common item operations, such as removal or addition of items

You also have the flexibility to define custom layout managers and animations for RecyclerView widgets.
<!-- excerpt -->

To use the RecyclerView widget, you have to specify an adapter and a layout manager. 

<!-- Define Layout -->

## Define Layout 
The following code example demonstrates how to add the RecyclerView to a layout:

``` 
<!-- A RecyclerView with some commonly used attributes -->
<android.support.v7.widget.RecyclerView
    android:id="@+id/my_recycler_view"
    android:scrollbars="vertical"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```

<!-- Define Data -->

## Define Data
Just like ListView, a RecyclerView needs an adapter to access its data. Therefore, before we create an adapter, let us create the data that we can work with. 

<!-- Create Adapter -->

## Create Adapter
The adapter provides access to the items in your data set, creates views for items, and replaces the content of some of the views with new data items when the original item is no longer visible. To create an adapter, extend the RecyclerView.Adapter class. 

To create an adapter that a RecyclerView can use, you must **extend RecyclerView.Adapter**. This adapter follows the view holder design pattern, which means that you need to define a custom class that **extends RecyclerView.ViewHolder**. This pattern minimizes the number of calls to the costly findViewById method.

The following code example shows a simple implementation for a data set that consists of an array of strings displayed using TextView widgets:


<!-- LayoutManager -->

## Use LayoutManager
A layout manager positions item views inside a RecyclerView and determines when to reuse item views that are no longer visible to the user. To reuse (or recycle) a view, a layout manager may ask the adapter to replace the contents of the view with a different element from the dataset. Recycling views in this manner improves performance by avoiding the creation of unnecessary views or performing expensive findViewById() lookups.

RecyclerView provides these built-in layout managers:

* LinearLayoutManager shows items in a vertical or horizontal scrolling list.
* GridLayoutManager shows items in a grid.
* StaggeredGridLayoutManager shows items in a staggered grid.
To create a custom layout manager, extend the RecyclerView.LayoutManager class.

<!-- Implementation -->

## Implement
Once you have added a RecyclerView widget to your layout, obtain a handle to the object, connect it to a layout manager, and attach an adapter for the data to be displayed:


{% highlight java %}
public class MyActivity extends Activity {
    private RecyclerView mRecyclerView;
    private RecyclerView.Adapter mAdapter;
    private RecyclerView.LayoutManager mLayoutManager;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.my_activity);
        mRecyclerView = (RecyclerView) findViewById(R.id.my_recycler_view);

        // use this setting to improve performance if you know that changes
        // in content do not change the layout size of the RecyclerView
        mRecyclerView.setHasFixedSize(true);

        // use a linear layout manager
        mLayoutManager = new LinearLayoutManager(this);
        mRecyclerView.setLayoutManager(mLayoutManager);

        // specify an adapter (see also next example)
        mAdapter = new MyAdapter(myDataset);
        mRecyclerView.setAdapter(mAdapter);
    }
    ...
}
{% endhighlight %}

<!-- Handle Click Action -->

## Handle Click Action
The standard implementation of RecyclerView does not have an onItemClick implementation. Instead they support touch events by adding an OnItemTouchListener through the addOnItemTouchListener method of RecyclerView class.


<!-- Animation -->

## Animation