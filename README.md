#Monetbil Android SDK

##How to set up Monetbil SDK
----------------------------

###Requirements

*   Android 2.0 or later.

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

First, we'll assume that you're going to launch the payment from a button,
and that you've set the button's `onClick` handler in the layout XML via `android:onClick="onMakePaymentPress"`.
Then, add the method as:

```java
public void onMakePaymentPress(View v) {

    // Your service key
    String service_key = "j9XjZzkFqjeL5fk34e1RNq98thRRwvYf";
    // Your service secret
    String service_secret = "oxr6Dyw80KlpJefIK7UyywXGHvkOM617wBBIXdZ1NTMWGZ9bSDyJmfX5oMI96204";

	// Initialize a payment
    PaymentRequest paymentRequest = new PaymentRequest(service_key, service_secret);
    paymentRequest.setAmount(1000); // Amount to be paid
	
    paymentRequest.setPayment_listener(MyPaymentListener.class);

	// Start a payment
    paymentRequest.startPayment(YourActivity.this);
}
```

Next, we'll write `MyPaymentListener` class to get the payment result.

###Processing payment result

To get the payment result, MyPaymentListener class needs to extends com.boorgeon.monetbil.PaymentListener. When a payment is completed, notification about that will be sent to the MyPaymentListener class that was defined in paymentRequest.setPayment_listener.

```java
package com.boorgeon.monetbil;

import android.content.Context;
import android.util.Log;

import com.boorgeon.monetbil.android.PaymentListener;
import com.boorgeon.monetbil.android.PaymentResponse;

public class MyPaymentListener extends PaymentListener {

    public MyPaymentListener(Context context) {
        super(context);
    }

    @Override
    public void onPaymentSuccess(PaymentResponse paymentResponse) {
        super.onPaymentSuccess(paymentResponse);

        Log.d("listener", "onPaymentSuccess");
    }

    @Override
    public void onPaymentFailed(PaymentResponse paymentResponse) {
        super.onPaymentFailed(paymentResponse);

        Log.d("listener", "onPaymentFailed");
    }

    @Override
    public void onPaymentWidgetClosed() {
        super.onPaymentWidgetClosed();

        Log.d("listener", "onPaymentWidgetClosed");

    }

}
```

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