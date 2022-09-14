R8 is a tool that is used to shrink, secure, and optimize Android applications. It uses proguard rules to change the behavior of application. We tend to confuse R8 with proguard. They are similar but have some slight differences.

R8 is already available to use in android gradle version 3.2.+

What R8 is :-</B><br>
R8 shrinking means reducing application size to a smaller size. Basically, we reduce the size of the dex files of the application.

<B>How R8 differs from proguard :-</B><br>
R8 has higher Kotlin language support as compared to proguard. Proguard is mainly used by applications developed using Java.
Usually, the R8 compiler is much faster than the proguard compiler. This makes R8 more efficient. Also, the build time for R8 is shorter.
Steps involved in R8 compiler

App code--->javadoc--->Java ByteCode--->R8---->Optimized Dalvik bytecode
Steps involved in Progurad 
App code--->javadoc--->Java ByteCode--->proguard---->Optimized Java bytecode---->dex---->Optimized Dalvik bytecode

In terms of shrinking, R8 is more effective than proguard. It can shrink an app by 10%, whereas proguard can cut it by 8%.
Proguard applies 520 peephole optimizations compared to R8 which is very less 10.

<B>Enabling R8 in your project:-</B><br>
  android {
    buildTypes {
        release {
            minifyEnabled true
            shrinkResources true
        }
    }
  }

In cases where you want to optimize your code intensively and minimize it, add the following in gradle.properties:<br>
<B>android.enableR8.fullMode = true</B><br>

<b>How is R8 used to shrink, optimize and secure Android applications?</B><br>

Shrink->R8 will remove all unused classes, functions, and variables. Also, it removes all resources that you added to your project but were never used.Moreover it removes all unused resources in libraries and SDKs being used in app.

Optimization->When you shrink your app, you optimize your code. R8 will check, rewrite, and rearrange your code to improve code efficiency. It also disposes dead code that may be present.

Security->To provide security, R8 provides code obfuscation. This means that it will take all class names, variables, and functions in your app and they will be renamed to short unreadable names before building the release version of the app.

<b>Proguard rules and @keep annotation:-</B><br>
R8 uses the proguard rules to optimize your code. It is not always advisable to rename all class names due to various reasons. But, R8 may delete a piece of code that your app actually requires. This may be because R8 did not check your code correctly.

Following lines can be used to restrict R8 from modifing specific classes in proguard-rules.pro

It will exclude whole class from Obsfuscation and shrinking.
- keep class ClassName

It will exclude some specific function of class from Obsfuscation and shrinking.
- keep class ClassName { fun myFunction() }

It will exclude all classes available in this directory from Obsfuscation and shrinking.
-keep class com.example.bean.**

Moreover you can restrict class from R8 operations by using @keep annotatuion on class name

<b>Why we need to restrict R8 :-</b><br>
As discussed earlier R8 changes the names of classes and variables in process of obsfucation. Therefore it could case some issues where we are using java reflection of classes.

i.e MainActivity::class.java

It can also cause issues in data classes where we can parse json to objects without using @Serialized(""). If variable name is changed then we will not be able to parse json therefore best practice is to use @Serialized("") while parsing.



