---
description: >-
  Get Details allows you to reference an existing previous transaction and
  obtain it's details.
---

# 3. Get Details (Optional)

## **POST Request to {Endpoint}/pay/getDetails**

### **JSON Body Parameters:**

<table><thead><tr><th width="146.33333333333331">Parameter</th><th>Type</th><th>Details</th></tr></thead><tbody><tr><td>trxID</td><td>String</td><td>trxID provided in response to the payment authorization request.</td></tr></tbody></table>

### JSON Body Request Example:

```json
{
    "trxID": "111111"
}
```

### JSON Success Response (Status Code 200)

```json
{
    "success": true,
    "data": {
        "trxID": "364856",
        "subtotalAmount": 10.01,
        "totalAmount": 10.02,
        "state": "FINALIZED",
        "mintHash": "0xd883e6c1a39e6b5d217a1a0c34178edbd835110227c7da0a94d8344ddb07b70c",
        "mintDate": "2023-07-24T20:16:16.631Z",
        "address": "0x87EA9703249dB472B596c278850DBC865f4548E1"
    }
}
```
