---
layout: post
title: Android - NFC Basics
---

<!-- links -->
[android-offical-doc]:https://developer.android.com/guide/topics/connectivity/nfc/index.html
[android-nfc-basics]:http://developer.android.com/guide/topics/connectivity/nfc/nfc.html
[tutorial-points-nfc]:http://www.tutorialspoint.com/android/android_nfc_guide.htm
[tutsplus-nfc]:http://code.tutsplus.com/tutorials/reading-nfc-tags-with-android--mobile-17278
[example-write-tag]:https://shanetully.com/2012/12/writing-custom-data-to-nfc-tags-with-android-example/
[android-nfc-tech-list]:http://developer.android.com/reference/android/nfc/tech/TagTechnology.html


<!-- post start -->
Near Field Communication (NFC) is a set of short-range wireless technologies, typically requiring a distance of `4cm or less` to initiate a connection. NFC allows you to share small payloads of data between an NFC tag and an Android-powered device, or between two Android-powered devices.
<!-- excerpt -->

### Terms and Definition
- **NDEF**: An NDEF(NFC Data Exchange Format)is a light-weight binary format, used to encapsulate typed data. It is specified by the NFC Forum, for transmission and storage with NFC, however it is transport agnostic.
- **NDEF Record**: An NDEF Record contains typed data, such as MIME-type media, a URI, or a custom application payload. 
- **NDEF Message**: An NDEF Message is a container for one or more NDEF Records.

### Android-powered devices with NFC simultaneously support three main modes of operation:

1. **Reader/writer mode**, allowing the NFC device to read and/or write passive NFC tags and stickers.
2. **P2P mode**, allowing the NFC device to exchange data with other NFC peers; this operation mode is used by Android Beam.
3. **Card emulation mode**, allowing the NFC device itself to act as an NFC card. The emulated NFC card can then be accessed by an external NFC reader, such as an NFC point-of-sale terminal.

### Android Manifest

Always remember to add permission when your code required some specific hardware.

{% highlight java %}
<uses-permission android:name="android.permission.NFC" />
{% endhighlight %}

If your app requires NFC to work, then you can add uses-feature so device without NFC won't be able to install it. 

{% highlight java %}
<uses-feature
    android:name="android.hardware.nfc"
    android:required="true" />
{% endhighlight %}

### Availability

Always check the device to see if it supports the required hardware when the app is launched. Sometimes the hardware component is not required, so you will have to check it when the app start up.

{% highlight java %}
mNfcAdapter = NfcAdapter.getDefaultAdapter(this);
if(mNfcAdapter==null) {
    Toast.makeText(this,"NFC is not supported with this device.", Toast.LENGTH_SHORT).show();
    finish();
}
{% endhighlight %}

Decide what you need to do when you found out the specific hardware is not supported with the device. In the above case, the app just exit with a Toast message.

Next, you need to check if NFC is currently enabled. If not, we will want to enable it.

{% highlight java %}
if(!mNfcAdapter.isEnabled()) {
    updateLog("NFC is disabled.");
    enableNFC();
} else {
    updateLog("NFC is enabled");
}
{% endhighlight %}

Unfortunately, there's no way to enable NFC by code. It must be done by user. Therefore, all you can do is to start an activity that launch the NFC setting(or wireless setting based on the device api level) so the user can enable it directly.  

{% highlight java %}
private void enableNFC() {
    //if current api level is 16 or above: use ACTION_NFC_SETTINGS
    if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.JELLY_BEAN) {
	    startActivityForResult(new Intent(Settings.ACTION_NFC_SETTINGS), 0);
    } else {
	    startActivityForResult(new Intent(Settings.ACTION_WIRELESS_SETTINGS), 0);
    }
}
{% endhighlight %}

### Discover NFC tag

[ACTION_NDEF_DISCOVERED vs ACTION_TECH_DISCOVERED][android-nfc-basics] 

### Read and write NFC Tag

It is usually a good practice to access NFC tags (or in general any IO operations) in a separate thread.
