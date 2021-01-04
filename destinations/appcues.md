---
description: Step-by-step guide to send your event data from RudderStack to Appcues
---

# Appcues

[Appcues](https://www.appcues.com/) is a popular product marketing platform that makes it easy for you to deliver scalable user experiences and accelerate your business growth. With Appcues' cutting-edge growth platform, you can effectively monitor your customers' product behavior, and design personalized customer experiences and in no time.

RudderStack supports sending your event data to Appcues from our native web SDKs, to help you understand your customers better.

## Getting Started

Before configuring your source and destination on the RudderStack, please check whether the platform you are sending the events from is supported by Appcues. Please refer the following table to do so:

| **Connection Mode** | **Web** | **Mobile** | **Server** |
| :--- | :--- | :--- | :--- |
| **Device mode** | **Supported** | - | - |
| **Cloud mode** | - | - | - |

{% hint style="info" %}
To know more about the difference between Cloud mode and Device mode in RudderStack, read the [RudderStack connection modes](https://docs.rudderstack.com/get-started/rudderstack-connection-modes) guide.
{% endhint %}

Once you have confirmed that the platform supports sending events to Appcues, perform the steps below:

* From your [RudderStack dashboard](https://app.rudderstack.com/), add the source and select **Appcues** from the list of destinations.

{% hint style="info" %}
Please follow our guide on [How to Add a Source and Destination in RudderStack](https://docs.rudderstack.com/how-to-guides/adding-source-and-destination-rudderstack) to add a source and destination in RudderStack.
{% endhint %}

* Name your destination, and click on **Next**. You should be able to see the following screen:

![Connection settings for Appcues destination](../.gitbook/assets/appcues.png)

* Enter the relevant details and click on **Next** to complete the setup. To get the **API Key** & **Account ID** field, please login to Appcues and navigate to **Settings** - **Account**. Here, copy the values of both your API key and the Account ID.

{% hint style="info" %}
You need to make an `identify` call before making any call to Appcues.
{% endhint %}

## Identify

The `identify` call is used to uniquely identify a user in Appcues. For more information on the `identify` call, please refer to the [RudderStack API Specification](https://docs.rudderstack.com/rudderstack-api-spec) documentation.

A sample `identify` call looks like the following snippet:

```javascript
rudderanalytics.identify("userId", {
  name: "John Doe",
  title: "CEO",
  email: "name.surname@domain.com",
  company: "Company123",
  phone: "123-456-7890",
  state: "Texas",
  rating: "Hot",
  city: "Austin",
  postalCode: "12345",
  country: "US",
  street: "Sample Address",
  state: "TX",
});
```

The above call is directly passed on to Appcues via its `Appcues.identify(userId,[properties])` call.

## Track

A `track` call lets you track custom events as they occur in your web application. For more information on the `track` call, please refer to the [RudderStack API Specification](https://docs.rudderstack.com/rudderstack-api-spec) documentation.

A sample `track` call looks like the following:

```javascript
rudderanalytics.track("Clicked button", {
  color: "red",
  buttonText: "Get started",
});
```


