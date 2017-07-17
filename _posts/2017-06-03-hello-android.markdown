---
layout: post
title:  "Hello Android"
date:   2017-06-03 21:13:10 -0400
categories: android intro
---
# What?
Android is the most used operative system running in phones, tablets, watches, TVs and even cars around the world. The Android platform enables us to make apps that can be delivered on those devices.

# How?
Android apps can be developed using Android Studio, and IDE made specifically for this purpose. You can download android studio from this [link](https://developer.android.com/studio){:target="_blank"}.

# Why?
Android devices usage is always increasing, and you can pour your creativity delivering awesome apps that can reach a domain the regular computer doesn't, so why wouldn't you want to be part this?

# Create a new project
After installing Android Studio (if you had any issues follow this [link](http://lmgtfy.com/?q=how+to+install+android+studio){:target="_blank"}), when you open it you will see this window.

![Welcome to Android Studio](/downloads/hello-android/hello-android-1.png)

To create a new Android project click on `Start a new Android Studio project` and we will see the new project wizard, here we define the application name, and the company domain.

![New Android Studio project wizard](/downloads/hello-android/hello-android-2.png)

Then click next to set the minimum SDK level.

![Choose minimum SDK level](/downloads/hello-android/hello-android-3.png)

Finally we can add an activity which is a screen in the app defined as a unit of interaction like choosing a song in a playlist in a music app, showing details of a recipe in a cake recipe app or adding a new task in a to-do app. So we can choose the activity template.

![Choose first activity template](/downloads/hello-android/hello-android-4.png)

And set its name.

![Define first activity name](/downloads/hello-android/hello-android-5.png)

After clicking `Finish` we can see the project structure being built and after a few moments we get to see Android Studio with our new project open for the first time.

![Newly created Android Studio project](/downloads/hello-android/hello-android-6.png)

Here we can see the three main areas of Android Studio, the toolbar at the top, the project panel to the left and the code editor to the right.

In the project panel are the project folders, where the main folders are `manifests` a folder containing manifest files where metadata related to the app is defined, `java` where the app logic is defined and `res` where all the non-code resources like layouts, strings and media reside.

# Run the app
To execute the app click the green play button in the toolbar. After that we need to choose the device (physical or virtual) in which we will deploy the app. By now there're no devices so we'll create a new virtual device.

![Run app](/downloads/hello-android/hello-android-7.png)

# Create an Android Virtual Device (AVD)
Select the device and click next.

![Select virtual device](/downloads/hello-android/hello-android-8.png)

Download the system image and click next.

![Select system image](/downloads/hello-android/hello-android-9.png)

Check Android Virtual Device configuration and click finish.

![Finish AVD configuration](/downloads/hello-android/hello-android-10.png)

Then our new AVD is available, so now we can use it, so we click OK to run the app on the android emulator.

![Use new AVD](/downloads/hello-android/hello-android-11.png)

# Try
And ta-da! the app is running in the emulator, we see the title `Hello` which we defined when created the project and a view that says `Hello World!`, but where is this last one defined?

![Hello World](/downloads/hello-android/hello-android-12.png)

# Edit
When our project was just created, Android Studio had two files open, the `MainActivity.java` file, where the activity logic is defined and the `activity_main.xml` file, which is the activity layout.

When we open `activity_main.xml` we see the Design view of the layout where we can drag and drop UI elements on it and edit things in a more visual way.

![Layout design view](/downloads/hello-android/hello-android-13.png)

We can click the TextView that holds the text Hello World! in the middle of the layout and we'll see a new panel at the right showing that element's properties, then if we set the TextView -> text attribute to "Hello Android", we can see in the design view that the text at the center has changed.

![Edit TextView](/downloads/hello-android/hello-android-14.png)

# Try again
And if we run the app again we will be that change reflected in the emulator as well.
![Test change in emulator](/downloads/hello-android/hello-android-15.png)

We created a new Android project, edited it a bit and deployed it to a virtual device, cool!

Now stay tuned for more :D
