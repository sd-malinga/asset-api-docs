---
description: >-
  Authorize a payment for a given quote. The final step for processing a
  transaction. Requires that you've already obtained a quote that's still
  active.
---

# 2. Authorize Transaction

**POST Request to {Endpoint}/pay/submitTransaction**

_submitTransaction_ can only be called once a quote has been generated and is active, meaning that [the quote](broken-reference) was generated within 10 minutes of the request to authorize a payment.

When a payment is authorized for a given quote, the user's billing information is processed for the orderTotal amount generated in getQuote.

## Request Information

### JSON Body Parameters:

<table><thead><tr><th width="214.33333333333331">Parameter</th><th width="102">Type</th><th width="444.6666666666667">Details</th></tr></thead><tbody><tr><td><code>token</code></td><td>String</td><td>Quote token generated in <a href="broken-reference">step 1.</a></td></tr><tr><td><code>ipAddress</code></td><td>string</td><td>User's ip address</td></tr><tr><td><strong><code>client</code></strong></td><td>Object</td><td><a href="./#user-json-object">Click here for user object details</a></td></tr><tr><td><strong><code>contact</code></strong></td><td>Object</td><td><a href="./#contact-json-object">Click here for contact object details</a></td></tr><tr><td><strong><code>billingAddress</code></strong></td><td>Object</td><td><a href="./#billingaddress-json-object">Click here for billingAddress object details</a></td></tr><tr><td><strong><code>paymentData</code></strong></td><td>Object</td><td><a href="./#paymentdata-json-object">Click here for paymentData object details</a></td></tr><tr><td><strong><code>3D</code></strong></td><td>Object</td><td><strong>(REQUIRED FOR 3D)</strong> <a href="./#3d-json-object">Click here for 3D object details</a></td></tr></tbody></table>

### JSON Body Interface:

<pre class="language-typescript"><code class="lang-typescript"><a data-footnote-ref href="#user-content-fn-1">{</a>
    token: string,
    ipAddress: string,
    client: {
        first: string,
        last: string,
        referenceID?: string,
        cryptoAddress?: string
    },
    contact: {
        email: string,
        phone: string,
    },
    billingAddress: {
        address: string,
        addressLine2?: string,
        city: string,
        state: string,
        postalCode: string,
        country: string,
    },
    paymentData: {
        cardNumber: string,
        monthExpire: string,
        yearExpire: string,
        cvv: string,
    },
    3D: {
        redirectURL: string
    }
}
</code></pre>

### `client` JSON Object:

<table><thead><tr><th>parameter</th><th width="96">Type</th><th>Details</th><th>Test Value</th></tr></thead><tbody><tr><td><code>first</code></td><td>String</td><td>Payee card number</td><td>"4111111111111111"</td></tr><tr><td><code>last</code></td><td>String</td><td>Payee full name</td><td>"John Doe"</td></tr><tr><td><code>referenceID</code></td><td>String</td><td>(<strong>Optional</strong>) Customer Reference ID to associate client with order - will be provided in responses and callbacks. <strong>Maximum of 25 characters.</strong></td><td>"johndoe123xyz-test"</td></tr><tr><td><code>cryptoAddress</code></td><td>String</td><td>(<strong>Optional</strong>) Client's EVM cryptocurrency wallet public address. If no is provided, the platform will generate a public address and private key on behalf of the client. </td><td>"0x0000000000000000000000000000000000000000"</td></tr></tbody></table>

### `contact` JSON Object:

<table><thead><tr><th>parameter</th><th width="96">Type</th><th>Details</th><th>Test Value</th></tr></thead><tbody><tr><td><code>email</code></td><td>String</td><td>Client email address</td><td>"john@doe.com"</td></tr><tr><td><code>phone</code></td><td>String</td><td>Client phone number. <strong>Include country code, separated from the phone number with a space.</strong></td><td>"+1 1234567890"</td></tr></tbody></table>

### `billingAddress` JSON Object:

<table><thead><tr><th>parameter</th><th width="96">Type</th><th>Details</th><th>Test Value</th></tr></thead><tbody><tr><td><code>address</code></td><td>String</td><td>Client's billing address</td><td>"123 Main St"</td></tr><tr><td><code>addressLine2</code></td><td>String</td><td>(Optional) 2nd billing line</td><td>"Apt 1A"</td></tr><tr><td><code>city</code></td><td>String</td><td>Card's billing city</td><td>"New York"</td></tr><tr><td><code>state</code></td><td>String</td><td>Billing state (Two characters)</td><td>"NY"</td></tr><tr><td><code>country</code></td><td>String</td><td>Billing country (Two characters)</td><td>"US"</td></tr><tr><td><code>postalCode</code></td><td>String</td><td>Postal code</td><td>"10001"</td></tr></tbody></table>

### `paymentData` JSON Object:

<table><thead><tr><th>parameter</th><th width="96">Type</th><th>Details</th><th>Test Value</th></tr></thead><tbody><tr><td><code>cardNumber</code></td><td>String</td><td>Payee card number</td><td>"4111111111111111"</td></tr><tr><td><code>monthExpire</code></td><td>String</td><td>Two digit month expire</td><td>"02"</td></tr><tr><td><code>yearExpire</code></td><td>String</td><td>Four digit year expire</td><td>"2025"</td></tr><tr><td><code>cvv</code></td><td>String</td><td>Card CVV</td><td>"123"</td></tr></tbody></table>

### `3D` JSON Object:

<table><thead><tr><th>parameter</th><th width="96">Type</th><th width="217">Details</th><th>Test Value</th></tr></thead><tbody><tr><td><code>redirectURL</code></td><td>String</td><td><strong>(REQUIRED FOR 3D SECURE)</strong> URL where client is redirected after 3D Secure operation is performed on client device</td><td>"https://google.com/"</td></tr></tbody></table>

### Example JSON Body:

```json
{
    "token": "wPJTIbahJxweGUbSw13jjJsGAw4",
    "ipAddress": "127.0.0.1",
    "client": {
        "first": "John",
        "last": "Doe",
        "referenceID": "johndoe123xyz-test"
    },
    "contact": {
        "email": "john@doe.com",
        "phone": "+1 1234567890"
    },
    "billingAddress": {
        "address": "123 Main St",
        "addressLine2": "Apt 1A",
        "city": "New York",
        "state": "NY",
        "postalCode": "10001",
        "country": "US"
    },
    "paymentData": {
        "cardNumber": "4111111111111111",
        "monthExpire": "02",
        "yearExpire": "2025",
        "cvv": "123"
    },
    "3D": {
        "redirectURL": "https://google.com/"
    }
}
```

## Response Information

There are 4 possible categories of responses for this request. You can determine the category by referring to the `state` field. The categories are the following:

1. **Approval**&#x20;
   * Completed transactions. Digital Asset is actively being generated.
2. **Refused**
   * Transactions that have been declined/refused. Responses will include refusal reasons in the `reason` field and also potentially provide additional error codes in the `additionalErrorCode` field.
3. **Pending (FOR 3D TRANSACTIONS ONLY)**
   * Pending transactions are neither refused nor accepted. Merchants can receive [webhook notifications](broken-reference) and also the [Get Details API](broken-reference) to access the finalized status of a transaction once a customer completes the necessary tasks associated with 3D Secure. If the response includes the `3DSecureURL` field, the customer must access the webpage via a browser. [For more information on using 3D Secure, click here.](broken-reference)
4. **Error**
   * A problem has occurred with the request. You can utilize information in the `error` field response to troubleshoot the error. Additionally, refer to the [Error Code Table](broken-reference) to identify errors by their HTTP status code.&#x20;

### Successful Responses:

#### Approval Response Example

```typescript
{
    "success": true,
    "state": "APPROVED",
    "trxID": "000000",
    "time": "2023-01-01T00:00:00.000Z",
    "details": {
        "amount": 10.00,
        "currency": "USD", 
        "CustomerWalletAddress": "0x0000000000000000000000000000000000000000",
        "DigitalAssetStatus": "PROCESSING",
        "clientReferenceID": "johndoe123xyz-test"
    }
}
```

#### Refused Response Example

```json
{
    "success": true,
    "state": "REFUSED",
    "trxID": "000000",
    "details": {
        "amount": 10.02,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
        "reason": "CARD EXPIRED",
        "additionalErrorCode": "33"
    },
    "time": "2023-01-01T00:00:00.000Z"
}
```

Refused transactions will include a `reason` field in the `details` object, which will provide information with regards why a transaction was refused.&#x20;

#### Pending[^2] Response Example (3D Secure)

```json
{
    "success": true,
    "state": "PENDING",
    "trxID": "000000",
    "details": {
        "amount": 10.13,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
        "3D": true,
        "3DSecureURL": "https://<3DSecureURL>"
    },
    "time": "2023-01-01T00:00:00.000Z"
}
```

### Error Responses

Error responses will have `"state": "ERROR"` along with a HTTP status code that is between 400 and 600. Refer to the [Authorize Transaction Error Codes](broken-reference) page for more information.

```json
{
    "success": false,
    "state": "ERROR",
    "time": "2023-07-03T20:58:46.343Z",
    "reason": "Date creation error: Invalid month: 0220",
    "additionalErrorCode": "5"
}
```

[^1]: 

[^2]: 
