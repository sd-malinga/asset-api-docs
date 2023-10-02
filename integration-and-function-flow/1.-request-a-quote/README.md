---
description: Request a quote on an order.
---

# 1. Request a Quote

## POST Request to {Endpoint}/pay/getQuote

**Calling getQuote only requires two body parameters in the JSON format. MerchantID is associated with the storefront that is the merchant.**

<table><thead><tr><th width="166.66666666666666">Parameter</th><th width="124">Type</th><th>Details</th></tr></thead><tbody><tr><td><strong>merchantID</strong></td><td>String</td><td>Merchant Username for given merchant</td></tr><tr><td><strong>amount</strong></td><td>Number</td><td>Order Amount in USD</td></tr></tbody></table>

## JSON Body Request Example:

```json
{
   "merchantID": "1234567890",
   "amount": 100.00
}
```

## JSON Success Response (Status Code 200)

```json
{
    "success": true,
    "subTotal": 100,
    "fee": 6.00,
    "total": 106,
    "token": "gVVikeun9DzqEX3FOFlwOyVvq",
    "tokenExpire": "2020-01-01T00:00:00.000Z"
}
```

### JSON Response Body:

<table><thead><tr><th width="170.66666666666666">Parameter</th><th width="135">Type</th><th>Details</th></tr></thead><tbody><tr><td>success</td><td>Boolean</td><td>true if request is successful</td></tr><tr><td>subTotal</td><td>Number</td><td>The requested order amount</td></tr><tr><td>fee</td><td>Number</td><td>The fee amount for the given merchant</td></tr><tr><td>total</td><td>Number</td><td>The summation of the subtotal and fee. Amount to be charged by the card when authorized.</td></tr><tr><td>token</td><td>String</td><td>Quote token, used as a parameter when authorizing a payment.</td></tr><tr><td>tokenExpire</td><td>Date/String</td><td>The expire time for the quote</td></tr></tbody></table>

### Information regarding tokens:

Tokens are active for 10 minutes following the time they’ve been created (600 seconds). Merchants should consider this and make repetitive requests to getQuote, **if needed**, to ensure that when a payment is authorized, there is an active quote that is associated with that order. [Requests to authorize a transaction](broken-reference) with an expired quote will revert.&#x20;



**See the following page for error & status codes associated with requesting a quote.**
