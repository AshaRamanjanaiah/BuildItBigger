# JokeTelling App

In this project, I have create an app with multiple flavors that uses
multiple libraries and Google Cloud Endpoints. The finished app will consist
of four modules. A Java library that provides jokes, a Google Cloud Endpoints
(GCE) project that serves those jokes, an Android Library containing an
activity for displaying jokes, and an Android app that fetches jokes from the
GCE module and passes them to the Android Library for display.

## Why this Project

As Android projects grow in complexity, it becomes necessary to customize the
behavior of the Gradle build tool, allowing automation of repetitive tasks.
Particularly, factoring functionality into libraries and creating product
flavors allow for much bigger projects with minimal added complexity.

## What did I Learn?

I have learnt the role of Gradle in building Android Apps and how to use
Gradle to manage apps of increasing complexity. I have learnt to:

* Add free and paid flavors to an app, and set up your build to share code between them
* Factor reusable functionality into a Java library
* Factor reusable Android functionality into an Android library
* Configure a multi project build to compile your libraries and app
* Use the Gradle App Engine plugin to deploy a backend
* Configure an integration test suite that runs against the local App Engine development server

## Install

To run this app:

Run a local instance of the GCE server. 

In order to do that you need to install the Cloud SDK:

https://cloud.google.com/sdk/docs/

Once installed, follow the instructions in the Setup Cloud SDK section at:

https://cloud.google.com/endpoints/docs/frameworks/java/migrating-android

Note: do not follow the rest of steps in the migration guide, only the Setup Cloud SDK.

Start or stop your local server by using the gradle tasks.

Once your local GCE server is started you should see the following at 
[localhost:8080](http://localhost:8080)

<img src="https://raw.githubusercontent.com/GoogleCloudPlatform/gradle-appengine-templates/77e9910911d5412e5efede5fa681ec105a0f02ad/doc/img/devappserver-endpoints.png">

Now you are ready to install and run the app. 


## How Did I Completed this Project?

### Step 0: Starting Point

This project contains an activity with a banner ad and a button that purports to tell a
joke. The banner ad was set up following the instructions here:

https://developers.google.com/mobile-ads-sdk/docs/admob/android/quick-start

You may need to download the Google Repository from the Extras section of the
Android SDK Manager.

### Step 1: Create a Java library

Created a Java library that provides jokes. Create a new
Gradle Java project either using the Android Studio wizard, or by hand. Then
introduced a project dependency between my app and the new Java Library.

Make the button display a toast showing a joke retrieved from your Java joke
telling library.

### Step 2: Create an Android Library

Created an Android Library containing an Activity that will display a joke
passed to it as an intent extra. Wired up project dependencies so that the
button can now pass the joke from the Java Library to the Android Library.

### Step 3: Setup GCE

This next task will be pretty tricky. Instead of pulling jokes directly from
our Java library, I have set up a Google Cloud Endpoints development server,
and pull our jokes from there. 

Before going ahead I had to be able to run a local instance of the GCE 
server. In order to do that I had to install the Cloud SDK:

https://cloud.google.com/sdk/docs/

Once installed, I have followed the instructions in the Setup Cloud SDK
section at:

https://cloud.google.com/endpoints/docs/frameworks/java/migrating-android

Note: I did not follow the rest of steps in the migration guide, only
the Setup Cloud SDK.

Started or stopped my local server by using the gradle tasks as shown in the following
screenshot:

<img src="/FinalProject/GCE-server-gradle-tasks.png" height="500">

Once your local GCE server is started you should see the following at 
[localhost:8080](http://localhost:8080)

<img src="https://raw.githubusercontent.com/GoogleCloudPlatform/gradle-appengine-templates/77e9910911d5412e5efede5fa681ec105a0f02ad/doc/img/devappserver-endpoints.png">

Now I'm ready to continue! 

Introduced a project dependency between your Java library 
and my GCE module, and modified the GCE starter code to pull jokes from my Java library. 
Created an AsyncTask to retrieve jokes using the template included int these 
[instructions](https://github.com/GoogleCloudPlatform/gradle-appengine-templates/tree/77e9910911d5412e5efede5fa681ec105a0f02ad/HelloEndpoints#2-connecting-your-android-app-to-the-backend). 
Made the button kick off a task to retrieve a joke, 
then launch the activity from my Android Library to display it.


### Step 4: Add Functional Tests

Added code to test that Async task successfully retrieves a non-empty
string. For a refresher on setting up Android tests(Esspresso Idling).

### Step 5: Add a Paid Flavor

Added free and paid product flavors to the app. Removed the ad (and any
dependencies you can) from the paid flavor.

### Step 6: Add Interstitial Ad

Followed these instructions to add an interstitial ad to the free version.
Ad will be displayed after user hits the button, but before the joke is shown.

https://developers.google.com/mobile-ads-sdk/docs/admob/android/interstitial

### Step 7: Add Loading Indicator

Added a loading indicator that is shown while the joke is being retrieved and
disappears when the joke is ready. The following tutorial is a good place to
start:

http://www.tutorialspoint.com/android/android_loading_spinner.htm

### Step 8: Configure Test Task

To tie it all together, created a Gradle task that:

1. Launches the GCE local development server
2. Runs all tests
3. Shuts the server down again
