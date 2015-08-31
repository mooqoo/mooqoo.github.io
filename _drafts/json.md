---
layout: post
title: Json 
---
<!-- links -->
[json_to_models]: https://guides.codepath.com/android/Converting-JSON-to-Models
[gson_tutorial_1]: http://www.studytrails.com/java/json/java-google-json-parse-json-to-java.jsp
[gson_tutorial_2]: http://kylewbanks.com/blog/Tutorial-Android-Parsing-JSON-with-GSON




Gson uses the name to match the json property to the java field. There are two ways to convert json to java. @SerializedName("") annotation denotes that the property name does not match the field name in our JSON. If both names do match, there is no need for the annotation.

Using the com.google.gson.Gson class. Create a new instance of this class and use the method public <T> T fromJson(String json, Class<T> classOfT). classOfT is the java object to which the json is to be converted to.
The other way is to use the com.google.gson.GsonBuilder class. This class allows setting up certain features, such as - allowing null serialization or setting up custom serializing policies. Create a GsonBuilder, apply the features and then obtain the Gson class from the builder.

[link1][gson_tutorial_1] [link2][gson_tutorial_2]

