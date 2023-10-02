# Simulating Refused Transactions

In the sandbox environment, you can simulate various refused responses by utilizing various refusal codes for the client first name, and the string `"TEST_PROGRAM"` for the client last name as shown:

```json5
...

"client": {
        "first": "<Refusal-Code>",
        "last": "TEST_PROGRAM",
},

...
```

| Refusal Code | Value                        |
| ------------ | ---------------------------- |
| REFUSED4     | HOLD CARD                    |
| REFUSED5     | REFUSED                      |
| REFUSED8     | APPROVE AFTER IDENTIFICATION |
| REFUSED13    | INVALID AMOUNT               |
| REFUSED15    | INVALID CARD ISSUER          |
| REFUSED17    | ANNULATION BY CLIENT         |
| REFUSED28    | ACCESS DENIED                |
| REFUSED33    | IMPOSSIBLE REFERENCE NUMBER  |
| REFUSED34    | CARD EXPIRED                 |
| REFUSED38    | SECURITY CODE EXPIRED        |
| REFUSED41    | LOST CARD                    |
| REFUSED43    | STOLEN CARD, PICK UP         |
| REFUSED51    | LIMIT EXCEEDED               |
| REFUSED55    | INVALID SECURITY CODE        |
| REFUSED56    | UNKNOWN CARD                 |
| REFUSED57    | ILLEGAL TRANSACTION          |
| REFUSED62    | RESTRICTED CARD              |
| REFUSED63    | SECURITY RULES VIOLATED      |
| REFUSED75    | SECURITY CODE INVALID        |
| REFUSED76    | CARD BLOCKED                 |
| REFUSED85    | REJECTED BY CARD ISSUER      |
