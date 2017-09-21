---
layout: post
title: How to change text and theme of Google Sign-In button in Android?
subtitle: ""
date: 2017-09-20T14:37:00.000Z
author: Shobhit Puri
header-img: img/posts/google-signin-button/google-signin-button-bg.png
comments: true
tags: [ CodeMonkey ]
published: true
---

### Index
- <a href="#quick-summary">Summary</a><br>
- <a href="#requirements">Requirements</a><br>
- <a href="#introduction">Introduction</a><br>
- <a href="#usage">Library Usage</a><br>
- <a href="#library-options">Library Options</a><br>
- <a href="#why-a-library">Why a library?</a><br>
- <a href="#source-code-and-sample-android-application">Source Code / Sample App</a><br>

### Quick Summary
In this post, I will show you how to change the text on Google's Sign-In button using standard `android:text` attribute, which is missing from the Google's <a href="https://developers.google.com/android/reference/com/google/android/gms/common/SignInButton" target="_blank">SignInButton</a>. I'll also show you, how you can switch between dark and light button themes. At the end of the post, a ready to use small Android library in included along with a sample application to try the same. 

### Requirements
* Android Studio.
* `compileSdkVersion 25` and `buildToolsVersion "25.0.3"`. This is what the sample app is using. You can change the values in the `build.gradle`, to use the SDK version you have installed.
* `minSdkVersion` supported is `16`.

### Introduction
Do you want to provide localization for the Google Sign-In button? Maybe you want to change the default "Sign In" text to "Sign in with Google". Or you want switch between "Sign in with Google" and "Sign up with Google" text based on whether it is a sign-in or sign-up flow. As you might already know, to set the text on an Android `Button`, you can use `android:text="{string}"` attribute in your layout XML. If you want to do the same for Google Sign-In, this attribute is not available. On Stackoverflow, there are obviously <a href="https://stackoverflow.com/questions/18040815/can-i-edit-the-text-of-sign-in-button-on-google" target="_blank">questions</a> which have been asked for this problem. Most of the existing answers were hacks at the time of writing. 

Follow along as I show you how you can use a very small library, created using <a href="https://developers.google.com/identity/sign-in/android/custom-button" target="_blank">Google's recommended way to customize the SignInButton</a>, that will enable you to use `android:text` attribute to set any text on the button. The library also enables you to change the theme of the button to light or dark easily.
    
### Usage

1. Add the following to your `app` module level `build.gradle` file:

        dependencies {
            // To include this library.
            compile 'com.shobhitpuri.custombuttons:google-signin:1.0.0'
        }

2. In your XML Layout, have the following:

        <RelativeLayout
            ...
            xmlns:app="http://schemas.android.com/apk/res-auto">
        
            <com.shobhitpuri.custombuttons.GoogleSignInButton
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:layout_centerInParent="true"
                android:text="@string/google_sign_up"
                app:isDarkTheme="true" />
        </RelativeLayout>

### Library Options
If you notice the XML, there are two attributes:
- `app:isDarkTheme="{Boolean}"` : This is to enable you to switch between the light (gray-white) theme and the dark (blue) theme for the button. The library handles changing the text color, background color and color change on button press based on Google's recommended guidelines.

- `android:text="{string}"`: This sets the text on the custom button.

Light Theme (White)        |  Dark Theme (Blue)
:-------------------------:|:-------------------------:
![Google Sign-In Light]({{site.baseurl}}/img/posts/google-signin-button/GoogleSignInLight.png)  |  ![Google Sign-In Dark]({{site.baseurl}}/img/posts/google-signin-button/GoogleSignUpDark.png)


### Why a library?
"Why create a library for this? Aren't there already tons of libraries already?", you would say. This library was result of the issues I faced when trying to set text on the `SignInButton`. I don't like using hacks and since you are here, this far in the article, I would assume you don't either. If the underlying implementation of Google's `SignInButton` changes, the hack would break. The ideal Google recommended solution from the documentation is to create a custom button as mentioned on <a href="https://developers.google.com/identity/sign-in/android/custom-button" target="_blank">Customizing the Sign-In Button.</a>It specifies the [branding guidelines](https://developers.google.com/identity/branding-guidelines#sign-in-button) which includes using custom icons and images for the button, setting specific text size, paddings and other do's and don'ts for the logo.

As you can see the ideal solution involves some extra work. Instead of creating a custom button just for my usage, I wanted to write some re-usable code, which I can drag and drop in any of my projects and it would work out of the box. That's why I decided to create a small 3.93 KB library, so that anyone facing this issue need not spend time implementing a custom solution and can get the custom Google Sing-In button working in no time.

### Source Code and Sample Android Application
You can find the implementation of the library and a sample Android application that is using the library here: <a href="https://github.com/shobhitpuri/custom-google-signin-button" target="_blank">https://github.com/shobhitpuri/custom-google-signin-button</a>. Feel free to give any feedback on the article or library. If you come across any issues, you are more than welcome to create an issue or open a pull request.

***Note: The images used in this article are trademark of Google. They have been just used for instructional purposes.***
