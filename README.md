# FeedAd Android SDK Demo App

This application shows how to configure and integrate the FeedAd Android SDK into an Android App.


## Getting started

If you want to run the application you have to set your client token first. Either:
- Open `app/src/main/res/values/config_feedad.xml`. Uncomment and replace the `feedad_client_token` with your token.
  After adding it to the xml file delete the marked config block inside `app/build.gradle`.
- Add the following to your 'local.properties' file: `feedad.clientToken=your client token`.

You can find your client token within the FeedAd admin panel.


## App Structure

The app consists of a single activity that features a navigation drawer menu.
When selected, each menu item will replace the main content frame of the activity with a fragment
showing a different kind of integration method of the SDK.

There are code comments inside each file that describe the integration. For in-depth explanations
of the FeedAd SDK please refer to the SDK's documentation page. 


### SDK Initialization

The following files show how to integrate & initialize the FeedAd SDK:
- `app/build.gradle`: SDK repository and dependency notation.
- `app/src/main/java/.../App.java`: SDK initialization
- `app/src/main/res/values/config_feedad.xml`: SDK configuration


### Ad requests

The following files show how to include FeedAds into your layout and how to request an ad:
- `app/src/.../SimpleIntegrationFragment.java`: The simplest form of integration by just adding a view to your layout.
- `app/src/.../ScrollViewIntegrationFragment.java`: Demonstrates that a FeedAdView also works within a classic scroll view.
- `app/src/.../RecyclerViewIntegrationFragment.java`: Shows how to integrate FeedAd into a heterogeneous recycler view.
- `app/src/.../AdvancedIntegrationFragment.java`: Shows how to integrate FeedAd based on Listener responses.


## FeedAd Mediation examples

The demo app includes examples of custom mediation using DFP, AppLovin MAX and AdMob.
If you want to run those examples within the demo app your need to configure each framework to serve ads to the demo app.

### DFP Configuration

In DFP create a Custom Event with the following config:
- Class name: `com.feedad.demo.dfp.FeedAdDfpCustomEventBanner`
- Parameter: `a FeedAd placement id`

After adding the Custom Event to a delivery you have to add the DFP ad unit id to the demo app:
- Either uncomment the ad unit id line inside the `config_dfp.xml` file and set your ad unit as a value.
- Or add a line `dfp.unitId=your-ad-unit` to the `local.properties` file.

Make sure that the ad size specified for your creative matches the size of the DFP example banner.
Otherwise DFP will not load the Custom Event creative.


### AppLovin Configuration

Before this example will work, you will have to configure your FeedAd client token. (See "Getting Started")

The app shows how to use FeedAd with AppLovin banner, interstitials, and native ads.
Look at the following files to see the different parts of the integration:

- app/build.gradle: The dependencies for AppLovin and the FeedAd AppLovin plugin
- AppLovinMAXIntegrationFragment.java: The example code that shows how to integrate FeedAd into AppLovin.
- config_applovin.xml: The ad unit IDs for AppLovin.

Read the [documentation](https://docs.feedad.com/android/mediation_networks/applovin/) for examples on how to configure FeedAd in AppLovin's dashboard.

### AdMob Configuration

To test AdMob Native Custom Event integration inside the demo app:

1. Create an app inside the AdMob console.
2. Create an advanced native ad
3. Add a new `Custom Event` using:
    - Class Name: `com.feedad.demo.admob.AdMobFeedAdNative`
    - Parameter: `your-feedad-placement-id`
4. Configure the demo app to use the AdMob ids:
    - Either uncomment the app id and ad unit id lines inside the `config_admob.xml` file and set your app id and ad unit as their values.
    - Or add the lines `admob.appId=your-app-id` and `admob.unitId=your-ad-unit` to the `local.properties` file.

If you want to integrate AdMob Native Custom Events into your app you should be safe to copy & paste the majority of the AdMob example classes:

1. Copy `AdMobFeedAdNative.java` along with all other package-private classes inside the `com.feedad.demo.admob` package into your app.
2. Integrate the native ads into your ad response logic as shown inside the `AdMobIntegrationFragment`.
