---
layout: post 
title:  Android Material Design
---

<!-- links -->
[toolbar-doc]:https://developer.android.com/reference/android/support/v7/widget/Toolbar.html
[v7-support-library]:https://developer.android.com/tools/support-library/features.html#v7]:
[navigation-drawer-tutorial]:http://www.android4devs.com/2014/12/how-to-make-material-design-navigation-drawer.html
[navigation-drawer-google]:https://developer.android.com/training/implementing-navigation/nav-drawer.html
[android-developer-create-fragment]:http://developer.android.com/training/basics/fragments/creating.html#AddInLayout
[android-developer-actionbar]:http://developer.android.com/guide/topics/ui/actionbar.html

<!-- post start -->
See the new [Support Library v7 AppCompat][v7-support-library], which features a backwards compatible Toolbar
<!-- excerpt -->


<!-- First step-->

##Implement Gradle:

{% highlight xml %}
repositories {
  mavenCentral()
}

dependencies {
    compile 'com.android.support:appcompat-v7:22.0.0'
    compile 'com.android.support:cardview-v7:21.0.+'
    compile 'com.android.support:recyclerview-v7:21.0.+'
}
{% endhighlight %}


<!-- Second Step-->

##Apply theme:

Start by applying the Material theme to our Android application res->styles.xml. We will set two special attributes android:windowNoTitle and android:windowActionBar to tell Android we will be using a Toolbar instead of the Action Bar.



{% highlight xml %}
<style name="MyTheme" parent="@android:style/Theme.Material.Light.DarkActionBar">
    <item name="android:windowNoTitle">true</item>
    <!--We will be using the toolbar so no need to show ActionBar-->
    <item name="android:windowActionBar">false</item>

    <!-- Set theme colors from http://www.google.com/design/spec/style/color.html#color-color-palette-->
    <!-- colorPrimary is used for the default action bar background -->
    <item name="android:colorPrimary">#2196F3</item>
    <!-- colorPrimaryDark is used for the status bar -->
    <item name="android:colorPrimaryDark">#1976D2</item>
    <!-- colorAccent is used as the default value for colorControlActivated
         which is used to tint widgets -->
    <item name="android:colorAccent">#FF4081</item>
    <!-- You can also set colorControlNormal, colorControlActivated colorControlHighlight and colorSwitchThumbNormal. -->
  </style>
{% endhighlight %}


## Adding toolbar (goodbye action bar)

Toolbar is added in API 21. It is a generalization of the Action Bar pattern that gives you much more control and flexibility. Toolbar is a view in your hierarchy just like any other, making it easier to interleave with the rest of your views, animate it, and react to scroll events. You can also set it as your Activity’s action bar, meaning that your standard options menu actions will be display within it.

### Set toolbar in xml

{% highlight xml %}
<android.support.v7.widget.Toolbar xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:toolbar="http://schemas.android.com/apk/res-auto"
    android:id="@+id/toolbar"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:minHeight="?attr/actionBarSize"
    android:background="?attr/colorPrimary"
    toolbar:title="ToolBar"
    toolbar:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
    toolbar:popupTheme="@style/ThemeOverlay.AppCompat.Light">
</android.support.v7.widget.Toolbar>
{% endhighlight %}

Now you need to setup the toolbar inside your Activity. Since you want to use toolbar to replace ActionBar, your activity still have to be either AppCompatActivity or ActionBarActivity. Now, you need to assign the toolbar object to the view that you created in the XML file. 

{% highlight java %}
    toolbar = (Toolbar) findViewById(R.id.toolbar);
{% endhighlight %}

Next, call setSupportActionBar(toolbar) to set the toolbar to act as the ActionBar for this Activity.
{% highlight java %}
    setSupportActionBar(toolbar);
{% endhighlight %}

Now, you can control the menu item in your toolbar with overriding the two methods:

{% highlight java %}
 @Override
    public boolean onCreateOptionsMenu(Menu menu) {
        // Inflate the menu; this adds items to the action bar if it is present.
        getMenuInflater().inflate(R.menu.menu_activity__main, menu);
        return true;
    }

    @Override
    public boolean onOptionsItemSelected(MenuItem item) {
        // Handle action bar item clicks here. The action bar will
        // automatically handle clicks on the Home/Up button, so long
        // as you specify a parent activity in AndroidManifest.xml.
        int id = item.getItemId();

        //noinspection SimplifiableIfStatement
        if (id == R.id.action_settings) {
            return true;
        }

        if(id == R.id.action_search){
            return true;
        }

        return super.onOptionsItemSelected(item);
    }
{% endhighlight %}

For more information about actionbar or how to add item into the menu you can take a look at [android developer ActionBar][android-developer-actionbar].

##  Navigation Drawer
The navigation drawer is a panel that displays the app’s main navigation options on the left edge of the screen. It is hidden most of the time, but is revealed when the user swipes a finger from the left edge of the screen or, while at the top level of the app, the user touches the app icon in the action bar. [Here's more detail from android developer.][navigation-drawer-google]

### Initialize Navigation Drawer 
First, to start a navigation drawer, you have to initialize it in the XML file of the activity that you wish to implement it. In order to do that, you will have to use  XML tag android.support.v4.widget.DrawerLayout. For DrawerLayout, it should have two child views. The first child view contains the main content of the activity. The second child view contains the content of the navigation drawer. Below is the sample code for my main_activity xml that implements navigation drawer.

#### activity_main.xml

{% highlight xml %}
<android.support.v4.widget.DrawerLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/drawer_layout"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <!-- First Child: Main Content for activity -->
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical">

        <!-- Toolbar -->
        <include
            android:id="@+id/toolbar"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            layout="@layout/toolbar" />

        <!-- Content -->
        <FrameLayout
            android:id="@+id/container_body"
            android:layout_width="fill_parent"
            android:layout_height="0dp"
            android:layout_weight="1" />
    </LinearLayout>


    <!-- Second Child: Navigation Drawer content (using Fragment) -->
    <fragment
        android:id="@+id/fragment_navigation_drawer"
        android:name="com.mooqoo.app.materialdesignpractice.activity.FragmentDrawer"
        android:layout_width="@dimen/nav_drawer_width"
        android:layout_height="match_parent"
        android:layout_gravity="start"/>

</android.support.v4.widget.DrawerLayout> 
{% endhighlight %}

I use fragment for my navigation drawer because I want to customize my drawer and fragment provide that flexibility. To add a fragment inside xml, simply just use the fragment tag and use the name attribute to specify the Fragment class that you created. I have already created a Fragment class called FragmentDrawer, therefore my sample code looks like this:

{% highlight xml %}
<fragment
    android:id="@+id/fragment_navigation_drawer"
    android:name="com.mooqoo.app.materialdesignpractice.activity.FragmentDrawer"
    android:layout_width="@dimen/nav_drawer_width"
    android:layout_height="match_parent"
    android:layout_gravity="start"/>
{% endhighlight %}

While fragments are reusable, modular UI components, each instance of a Fragment class must be associated with a parent FragmentActivity. However, since you are using the v7 appcompat library, your activity should instead extend ActionBarActivity, which is a subclass of FragmentActivity.

Note: When you add a fragment to an activity layout by defining the fragment in the layout XML file, you cannot remove the fragment at runtime. If you plan to swap your fragments in and out during user interaction, you must add the fragment to the activity when the activity first starts, as shown in the next lesson. For more information, [check out android developer on creating fragment][android-developer-create-fragment]

If you want more information on how to setup the navigation drawer you can check it out [here][navigation-drawer-tutorial].








