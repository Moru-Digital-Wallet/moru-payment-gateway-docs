## Server Verification

Once the transaction is completed in the client side, you need to initiate the api call from your server to moru server api to verify the status of the transaction.

This is a `mandatory step` in process transaction as only this step will ensures about the status of the transaction.

## 1. Check Payment

You need to send POST request to `check-payment` api inorder to get the status of the transaction.

API

- `url`: `https://test.moru-gateway.pnpl.com.np/gateway/v1/check-payment`
- `method` : `POST`
- `body`:
  - `secret_key`: `<secret key>`
  - `tnx_identifier`: `moru_txn_identifier` or `transaction_id`

Description

`moru_txn_identifier` : Moru unique transaction identifier which is received in response after payment is success.
`transaction_id` : Your unique transaction identifier which you send when initiating the transaction

## Payment Response

```json
{
  "data": {
    "amount": 10.0,
    "complete": true,
    "created_at": "2021-08-04 18:50:38",
    "external_txn_identifier": "abc",
    "extra_data": {
      "item": "laptop"
    },
    "id": 12,
    "moru_txn_identifier": "1ae23e65f4f5",
    "source_type": "Internal",
    "state": "Completed"
  },
  "meta": {}
}
```

## Going to Production

In production the api url is to be updated by:

` https://api.payment-gateway.moru.com.np/gateway/v1/check-payment`
