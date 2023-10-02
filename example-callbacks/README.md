---
description: >-
  Examples of successful callbacks. Callbacks are issued for both approved and
  refused transactions.
---

# Example Callbacks

### Refused Transaction Example

```json5
{
    "success": true,
    "state": "REFUSED",
    "trxID": "000000",
    "details": {
        "amount": 10.00,
        "currency": "USD",
        "clientReferenceID": "johndoe123xyz-test",
        "reason": "LIMIT EXCEEDED - Insufficient funds OR Insufficient funds/over credit limit",
        "additionalErrorCode": "51"
    },
    "time": "2023-00-00T00:00:00.000Z"
}
```

### Approved Transaction Example

```json5
{
    "success": true,
    "state": "APPROVED",
    "trxID": "352951",
    "time": "2023-07-08T04:28:43.623Z",
    "details": {
        "amount": 10.16,
        "currency": "USD",
        "CustomerWalletAddress": "0x87EA9703249dB472B596c278850DBC865f4548E1",
        "DigitalAssetStatus": "PROCESSING",
        "clientReferenceID": "johndoe123xyz-test"
    }
}
```
