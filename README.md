#Monetbil Android SDK

##How to set up Monetbil SDK
----------------------------

###Requirements

*   Android SDK version 8 (Android 2.2) or later.

###Download the SDK

https://github.com/Monetbil/monetbil-android-library/raw/master/monetbil.aar

###Import the SDK to your Android Studio project

```android
File -> New -> New Module -> Import .JAR/.AAR and choose monetbil.aar
```

###Gradle

You'll need to modify your app/build.gradle file. Add the following (in the dependencies section):

```gradle
dependencies {
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.android.support:support-v4:23.0.0'
    compile 'com.android.support:cardview-v7:23.0.0'
    compile 'com.android.support:design:23+'
    compile 'com.github.traex.rippleeffect:library:1.3'
    compile 'com.squareup.picasso:picasso:2.5.2'
    compile project(':monetbil')
}
```

##Payment integration
----------------------------


###Making a payment


License
--------

    Copyright 2013 Serge NTONG.

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.