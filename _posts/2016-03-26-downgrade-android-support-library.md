---
layout: post
title:  Downgrade Android Support Library
---

<!-- links -->
[support_library]:https://dl-ssl.google.com/android/repository/support_r23.0.1.zip

<!-- post start -->

### How to downgrade your android support library in just a few steps

There will be times when you will want to downgrade your android support library due to compatibility issue. When that happens, you will want to downgrade your support library back to which ever version that supports it. Android Studio did not have any tool that can do this for you so you will have to do it manually on your own.

<!--excerpt-->

<!-- content -->
You can downgrade your support library is just a few basic steps:

1.  download the support library that you want to downgrade.   
    **e.g.** [download][support_library] support library for version 23.0.1

2.  decompile the support library and replace the support directory in $ANDROID_HOME/extras/android/

3.  go to $ANDROID_HOME/extras/android/m2repository/com/android/support/{LIBRARY_YOUR_WANT_TO_DOWNGRADE}   
    **e.g.** I want to downgrade **support-v4** library, so I go to **$ANDROID_HOME/extras/android/m2repository/com/android/support/support-v4**

4.  open up **maven-metadata.xml** and remove the latest support library info   
    **e.g.** If I want to downgrade to 23.0.1, then I will need to delete the version info after 23.0.1 and change the release info to 23.0.1

5.  remove all folder after the version you want to downgrade   
    **e.g.** If I want to downgrade to 23.0.1, then I will need to delete the version after 23.0.1

6.  go to another library {*LIBRARY_YOUR_WANT_TO_DOWNGRADE*} and do steps 3~5 until all the library you want to downgrade are done

7.  clean project and run project again
