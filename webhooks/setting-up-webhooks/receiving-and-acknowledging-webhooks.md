# Receiving and Acknowledging webhooks

When a HTTP request is sent to your endpoint, this notification will come in the form of a post request. You should acknowledge the requets by responding to the request with status 200.&#x20;

If a request is not responded to/acknowledged within 30 seconds following notification, a consecutive webhook request will be sent to your endpoint. The second request will come 5 seconds after the initial request. After this second request, no further requests will be made with regards to the given transaction. Again, the 2nd request is only issued if the first request is not acknowledged.

See the following pages to understand the format of the webhook notifications. They will follow the same format as the typical responses to the [submitTransaction](broken-reference) request.

#### To practice/simulate how webhooks will behave with your server/application, you can use the [testWebhook](broken-reference) endpoint on the following page to receive sample webhooks to your endpoint from the sandbox enviroment. This feature is not available in production.
