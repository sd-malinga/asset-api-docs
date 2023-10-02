# Testing Webhooks

## **POST Request to {Endpoint}/merchant/testWebhook**

Use this endpoint to simulate webhooks. Once enrolled in receiving webhooks, you can configure the request body to simulate either a [successful](broken-reference) or [failure (refund)](broken-reference) notification.

#### Header Configuration

| Header Parameter | Type   |                             |
| ---------------- | ------ | --------------------------- |
| apiKey           | String | API key provided by Support |
| content-type     | String | application/json            |

#### Body Configuration

<table><thead><tr><th width="214.33333333333331">Parameter</th><th width="171">Type</th><th width="354.6666666666667">Details</th></tr></thead><tbody><tr><td>merchantUserID</td><td>String</td><td>Merchant username/ID. Same as used in <a href="broken-reference">step 1.</a></td></tr><tr><td>success</td><td>boolean</td><td>Set to <code>true</code> for simulating successful order notifications. Set to <code>false</code> for simulating unsuccessful order notifications.</td></tr></tbody></table>

If the request is successful, meaning that you are properly enrolled in receiving webhooks, a successful response (status 200) will mean that a webhook notification was sent to your endpoint(s).

```json
{
    "success": true
}
```

If you are not actively enrolled in receiving webhooks, you will receive a request such as the following:

```json
{
    "success": false,
    "error": "Merchant is not enrolled in webhooks. Contact support to enroll."
}
```
