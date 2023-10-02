# 3D Secure Webhooks

### Pending Transaction

```json5
{
    "success": true,
    "state": "PENDING",
    "trxID": "000000",
    "details": {
        "amount": 10.00,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
        "3D": true,
        "3DSecureURL": "https://<payment-url>"
    },
    "time": "2023-00-00T00:00:00.000Z"
}
```



Transaction notifications for 3D Secure transactions are issued once a client accesses the [`3DSecureURL`](broken-reference).

### Approved Transaction

<pre class="language-json5"><code class="lang-json5"><strong>{
</strong>    "success": true,
    "state": "APPROVED",
    "trxID": "000000",
    "details": {
        "amount": 10.00,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
    },
    "time": "2023-00-00T00:00:00.000Z"
}
</code></pre>

### Refused Transaction

```json5
{
    "success": true,
    "state": "DECLINED",
    "trxID": "000000",
    "details": {
        "amount": 10.00,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
        "reason": "51-LIMIT EXCEEDED",
        "additionalErrorCode": "51"
    },
    "time": "2023-01-01T00:00:00.000Z"
}
```
