---
layout: post
title: JSON in Android
---
<!-- links -->
[mooqoo_gson-json]: https://github.com/mooqoo/Gson-Json
[json_org]: http://json.org/
[android_dev__jsonobject]: http://developer.android.com/reference/org/json/JSONObject.html
[android_dev__jsonarray]: http://developer.android.com/reference/org/json/JSONArray.html
[github_gson]: https://github.com/google/gson

<!-- What is Json -->

What is JSON
------------
JSON is short for JavaScript Object Notation. It is an open standard syntax that uses human readable text to transmit or store data. Due to its simplicity and readability, JSON is an ideal data-interchange language and it is widely used among people. For more information about json [please check out the official website][json_org].
<br /><br />

<!-- Json format -->

JSON Data Format
----------------
JSON data structure is actually very straight forward. It is based upon **JSON Object**, **JSON Array**, and **JSON Value**.  

**JSON Value:**   
A JSON value can be one of the following:  

-	A number (integer or floating point)
-	A string (in double quotes)
-	A Boolean (true or false)
-	A JSON array (in square brackets)
-	A JSON object (in curly braces)
-	null

**JSON Object:**  
A JSON object is just an *{ "name": value }* pair which is surrounded by **curly braces** and it is separate by a **colon**. JSON names require double quotes and value is the JSON Value we define above. Below are some examples:  

-  { "name_number": 345 }    		
-  { "name_string": "string_A" } 	
-  { "name_boolean": true }    	
-  { "name_null": null } 
-  { "name_array":  [ 3, 5, 10 ] } 
-  { "name_object": { "name": value } } 
   
**JSON Array:**   
An JSON array is an *ordered collection of values* which is surrounded by **brackets** and if there are multiple values, it is separate with **comma**. Below are some examples:  

-  [ ]					
-  [ 3, 5, 4 ]			
-  [ "string" ]			
-  [ true, false ]		
-  [ { name_1: value_1 },
	 { name_2: value_2 },
	 { name_3: value_3 } ]			

***Note:**   
- It will be common to have nested JSON Array and JSON Object.  
<br /><br />

<!-- Json in Android -->

JSON in Android
---------------
In order to send and receive JSON data with android, we will have to know how to: 

-  convert java class to JSON data 
-  parse JSON data and create java class

Android provide a few different classes that let you do that. The one I am going to mention is [JSONObject][android_dev__jsonarray] and [JSONArray][android_dev__jsonarray]. To convert java class to JSON data, you first have to identify the field that you are interested and what type of data it is. Then you will have to create an empty JSONObject and manually add each field in with the key/value pair. Below is the sample code from my [github project: Gson-Json][mooqoo_gson-json]:

{% highlight java %}  
//Create JSONObject for dataset
public static JSONObject toJSONObject(Dataset dataset) {
    try {
        //Creating JSONObject for album
        JSONObject jsonObj = new JSONObject();
        jsonObj.put("album_id", dataset.album_id);
        jsonObj.put("album_title", dataset.album_title);
        //convert datasetImages into JSONArray
        JSONArray jsonArray = new JSONArray();
        for(AlbumImages albumImage:dataset.images)
            jsonArray.put(toJSONObject(albumImage));
        //put JSONArray into JsonObject
        jsonObj.put("images", jsonArray);
        return jsonObj;
    } catch(JSONException ex) {

    }
    return null;
}
{% endhighlight %}

This looks okay with a small amount of JSON data, but this will be a lot of work as the size of your JSON data gets larger and larger. Now, let see what it is like to parse the JSON data. Once again, we will need to get the value one by one from the JSONObject and add it to our java object. Below is another sample code from my [project][mooqoo_gson-json].

{% highlight java %}  
//Create Dataset object from JSON
public static Dataset fromJSON_toDataset(String json) {
    try {
        Dataset dataset = new Dataset();
        JSONObject jsonObject = new JSONObject(json);
        dataset.album_id = jsonObject.getString("album_id");
        dataset.album_title = jsonObject.getString("album_title");

        JSONArray jsonArray = jsonObject.getJSONArray("images");
        List<AlbumImages> images = new ArrayList<AlbumImages>();
        for(int i=0; i<jsonArray.length(); i++)
            images.add(fromJSON_toAlbumImages(jsonArray.getJSONObject(i).toString()));
        dataset.images = images;

        return dataset;
    } catch(JSONException ex) {

    }
    return null;
}
{% endhighlight %}

As you can see, this will be very frustrating when you have a certain amount of JSON data. Therefore, I want to recommend another library instead. It is called [Gson][github_gson], and it is created by Google. 
<br /><br />

<!-- Gson library -->

Gson
----
[Gson][github_gson] is a Java library that can be used to convert Java Objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object. The advantage of using GSON is that it can use the Object definition to directly create an object of the desired type. Gson uses the name to match the json property to the java field. @SerializedName("") annotation denotes that the property name does not match the field name in our JSON. If both names do match, there is no need for the annotation.   
   
### Setting up Gson
Setting up the Gson library is very simple.   
Add the following line to the gradle dependency:

{% highlight java %} 
	compile 'com.google.code.gson:gson:2.3.1'
{% endhighlight %}

### Using Gson
In order to use Gson, we have to create a Gson instance:

{% highlight java %} 
//setup Gson/Gson builder
GsonBuilder builder = new GsonBuilder();
Gson gson = builder.create();
{% endhighlight %}

Now, if we want to convert java object to json, all we need to do is call the toJson method with the object we want to convert as input:
{% highlight java %} 
	String json = gson.toJson(album);
{% endhighlight %}

Vise versa, if we want to parse a json, all we need to do is call the fromJson method with the json string and the Object class that we wish to parse to:
{% highlight java %} 
	Albums album = gson.fromJson(json, Albums.class);
{% endhighlight %}

