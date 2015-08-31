---
layout: post 
title:  Android Service vs IntentService
---

<!-- links -->
[android-developer-service]:https://developer.android.com/reference/android/app/Service.html
[android-developer-intentservice]:https://developer.android.com/reference/android/app/IntentService.html
[stack-service-vs-intentservice]:http://stackoverflow.com/questions/7771323/what-is-the-difference-between-an-intent-service-and-a-service
[android-developer-boundservice]:http://developer.android.com/guide/components/bound-services.html

<!-- post start -->
A Service is an application component representing either an application's desire to perform a longer-running operation while not interacting with the user or to supply functionality for other applications to use. Note that services, like other application objects, run in the main thread of their hosting process. This means that, if your service is going to do any CPU intensive (such as MP3 playback) or blocking (such as networking) operations, it should spawn its own thread in which to do that work. 

<!-- excerpt -->

## Service
Each service class must have a corresponding < service > declaration in its package's AndroidManifest.xml. Services can be started with Context.startService() and Context.bindService().

## Lifecycle

## Permission

## Creating a bound service
A bound service allows components (such as activities) to bind to the service, send requests, receive responses, and even perform interprocess communication (IPC). A bound service typically lives only while it serves another application component and does not run in the background indefinitely. 

A bound service is an implementation of the Service class that allows other applications to bind to it and interact with it. To provide binding for a service, you must implement the onBind() callback method. This method returns an IBinder object that defines the programming interface that clients can use to interact with the service.

Multiple clients can connect to the service at once. However, the system calls your service's onBind() method to retrieve the IBinder only when the first client binds. The system then delivers the same IBinder to any additional clients that bind, without calling onBind() again.

When creating a service that provides binding, you must provide an IBinder that provides the programming interface that clients can use to interact with the service. There are three ways you can define the interface:

1. Extending the Binder class
2. Using a Messenger
3. Using AIDL(Android Interface Definition Language)

Since AIDL is a more complicated implementation and most application should not use this approach so I won't be talking about it.



### Extending the Binder class

### Using a Messenger




