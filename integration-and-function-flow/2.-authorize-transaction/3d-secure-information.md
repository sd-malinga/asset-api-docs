---
description: Refer to this page if you are enrolled in 3D Secure as a merchant
---

# 3D Secure Information

In order to process a transaction using 3D Secure, you must follow the following protocol as outlined on this page.

### Step 1: Configure Webhooks&#x20;

Using 3D Secure requires that you are set up to receive webhook notifications. This is because requests to authorize a transaction will return a `PENDING` state - the initial request will not have information on whether the transaction was approved or refused.&#x20;

In order to be notified on the state of a transaction, refer to the [webhook section of this guide](broken-reference). You can configure one or multiple multiple webhook endpoints to receive notifications.

Webhooks must be enabled because when using 3D Secure, any valid [Authorize Transaction](broken-reference) request is returned with the `PENDING` state, the response body will include a `3DSecureURL` field. See the following example:

{% code title="Authorize Transaction responses will have a PENDING state when using 3D Secure" %}
```json5
{
    "success": true,
    "state": "PENDING",
    "trxID": "000000",
    "details": {
        "amount": 10.13,
        "currency": "USD",
        "3D": true,
        "3DSecureURL": "https://<3DSecureURL>"
    },
    "time": "2023-01-01T00:00:00.000Z"
}
```
{% endcode %}

### Step 2: Configuring Requests

When interacting with this API, requests only require one additional field in the [Authorize Transaction](broken-reference) request to utilize 3D Secure. Requests to [get a quote](broken-reference) are identical with standard protocol and do not require modification.

As outlined on the Authorize Transaction page, 3D Secure requests must include the [`3D` object ](broken-reference)field with the `redirectURL` field nested inside. See below:

```json5
...
        3D: {
                redirectURL: "https://<redirect-url>"
        }
...
```

In the following steps, this guide will outline the purpose and use of the `3DSecureURL`, which is a field returned in the [Authorize Transaction](broken-reference) request. The purpose of the `redirectURL` as described in this step is a the destination where the `3DSecureURL` webpage will redirect to upon completing the 3DSecure operation.

### Step 2: `3DSecureURL`: Accessing the 3D Secure Environment&#x20;

The `3DSecureURL` field is a URL link to a webpage where the 3D Secure operation is performed on the client's device. As such, your integration must involve the client's device opening this webpage on their device to complete a transaction. You can open the `3DSecureURL` on a client device using a iFrame or similar imbedded html method to not disrupt the user experience.

### Important things to note:

**Any 3D transaction will not be submitted until the `3DSecureURL` webpage is opened on the client device.**

**`3DSecureURL` links are valid for 1 minute following the** [**Authorize Transaction**](broken-reference) **request.**

### Step 3: Receiving transaction responses via Webhooks

Once a client has successfully accessed the `3DSecureURL` webpage and completed a challenge if necessary, the transaction will be processed and you will receive the status of the transaction via webhooks - whether the transaction was approved or refused, etc. [Click here for more information on 3D Secure Webhooks.](broken-reference)

### Step 3b: Fetching transaction details via Get Details

You can also manually query transactions using the Get Details API. [Click here for more information regarding the Get Details endpoint.](broken-reference)
