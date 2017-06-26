# Monetbil Android SDK

Accept Mobile Money in your Android app https://www.monetbil.com/.
This SDK makes it easy to add In-App Purchase to your mobile apps.

## How to set up Monetbil SDK

### Requirements

*   Android 2.0 or later.

### Download the SDK

https://github.com/Monetbil/monetbil-android-sdk/raw/master/monetbil.aar

### Add the SDK to Your Android Studio project

```android
File -> New -> New Module -> Import .JAR/.AAR and choose `monetbil.aar`
```
### Gradle

You'll need to modify your app/build.gradle file. Add the following (in the dependencies section):

```gradle
dependencies {
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.android.support:support-v4:23.0.0'
    compile 'com.android.support:cardview-v7:23.0.0'
    compile 'com.android.support:design:23+'
    compile 'com.patrickpissurno:ripple-effect:1.3.1'
    compile 'com.squareup.picasso:picasso:2.5.2'
    compile project(':monetbil')
}
```

## Payment integration

When the user decides to make a purchase, you will initialize Monetbil SDK and whenever the payment is completed, your application will be notified using your implementation of the `PaymentListener` class, this will be done even if the app is not currently running.

### Making a payment

First, we'll assume that you're going to launch the payment from a button,
and that you've set the button's `onClick` handler in the layout XML via `android:onClick="onMakePaymentPress"`.
Then, add the method as:

1. Get your "service_key" and "service_secret" from the [Dashboard](https://www.monetbil.com/services)
2. Build & start real payment

```java
public void onMakePaymentPress(View v) {

    String service_key = "j9XjZzkFqjeL5fk34e1RNq98thRRwvYf";
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

### Processing payment result

To get the payment result, `MyPaymentListener` class needs to extends `com.boorgeon.monetbil.android.PaymentListener`. When a payment is completed, notification about that will be sent to the `MyPaymentListener` class that was defined in `paymentRequest`.

```java
package com.boorgeon.monetbil;

import android.content.Context;
import android.content.Intent;
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

        String transaction = paymentResponse.getTransaction_UUID();
        String item_ref = paymentResponse.getItem_ref();
        String payment_ref = paymentResponse.getPayment_ref();
        String msisdn = paymentResponse.getMsisdn();
        int amount = paymentResponse.getAmount();
        boolean success = paymentResponse.isSuccess();

        Intent intent = this.getIntent();
        intent.putExtra("transaction", transaction);
        intent.putExtra("item_ref", item_ref);
        intent.putExtra("payment_ref", payment_ref);
        intent.putExtra("msisdn", msisdn);
        intent.putExtra("amount", amount);
        intent.putExtra("success", success);

        this.startActivity(YourPaymentSuccessActivity.class);
    }

    @Override
    public void onPaymentFailed(PaymentResponse paymentResponse) {
        super.onPaymentFailed(paymentResponse);

        Log.d("listener", "onPaymentFailed");

        String transaction = paymentResponse.getTransaction_UUID();
        String item_ref = paymentResponse.getItem_ref();
        String payment_ref = paymentResponse.getPayment_ref();
        String msisdn = paymentResponse.getMsisdn();
        int amount = paymentResponse.getAmount();
        boolean success = paymentResponse.isSuccess();
		
        Intent intent = this.getIntent();
        intent.putExtra("transaction", transaction);
        intent.putExtra("item_ref", item_ref);
        intent.putExtra("payment_ref", payment_ref);
        intent.putExtra("msisdn", msisdn);
        intent.putExtra("amount", amount);
        intent.putExtra("success", success);

        this.startActivity(YourPaymentFailedActivity.class);
    }

    @Override
    public void onPaymentWidgetClosed() {
        super.onPaymentWidgetClosed();

        Log.d("listener", "onPaymentWidgetClosed");

    }

}
```

### Download the sample app on Google Play Store

https://play.google.com/store/apps/details?id=com.boorgeon.monetbil.android.sdkdemo

## Screenshots

![Image](https://www.monetbil.com/assets/img/monetbil-android-sdk-example.gif)

If you have any questions or need help, do not hesitate to contact us at [support@monetbil.com](https://www.monetbil.com/contact/support/?referral=github)

## License

Please refer to this repo's [LICENSE](LICENSE).
