# Take a recurring payment

You can take recurring payments even when the paying user is not present. 

Your service will supply an agreement identifier for an agreement that your user has provided card details and consent for.

- [Creating an agreement](./Agreements.md#creating-an-agreement)
- [Setting up an agreement](./Agreements.md#setting-up-an-agreement)

## Creating a recurring payment

The existing `/v1/payments` API is used to process recurring payments.

For creating recurring payments: 

- no `return_url` is required as the user is not present
- no `next_url` will be returned

| Body parameter  | | Description |
| ------------- | ------------- | ---- |
| `authorisation_mode`  | Optional  | Specify how GOV.UK Pay should authorise this payment. For recurring payments this be `agreement`. The default value is `web`.  |
| `agreement_id`  | Optional  | The agreement identifier that should be used to authorise the payment. The agreement provided must be in the `active` state.  |

For a full description of the current payments API see [Creating a payment](https://docs.payments.service.gov.uk/making_payments/#creating-a-payment).

### Example request
```json
{
  "amount": 1000,
  "reference": "SERVICE-PAYMENT-REFERENCE",
  "description": "Green garden waste July 2022",
  "authorisation_mode": "agreement",
  "agreement_id": "cgc1ocvh0pt9fqs0ma67r42l58"
}
```

### Example response
```json
{
  "amount": 1000,
  "description": "Green garden waste June 2022",
  "reference": "SERVICE-PAYMENT-REFERENCE",
  "state": {
    "status": "created",
    "finished": false
  },
  "payment_id": "a01vhg8efe47gfvhkbjh78erl4",
  "payment_provider": "sandbox",
  "created_date": "2022-07-13T11:00:22.334Z",
  "return_url": "https://your.service.gov.uk/completed",
  "agreement_id": "cgc1ocvh0pt9fqs0ma67r42l58",
  "authorisation_mode": "agreement",
}
```

Unlike one-off web payments, the card details to authorise the payments are already provided by the agreement.

The payment will be queued to be taken by GOV.UK Pay. This can be immediate but can also take some time, your service can [receive webhook messages](../webhooks/README.md#receiving-webhook-messages) to be notified when the payment has succeeded.

### Example recurring payment journey (success)
```mermaid
 sequenceDiagram
 participant Service
 participant GOV.UK Pay
 Service ->> GOV.UK Pay: Create recurring payment
 Note over Service,GOV.UK Pay: POST /v1/payments
 Note over Service,GOV.UK Pay: "authorisation_mode": "agreement"
 Note over Service,GOV.UK Pay: "agreement_id": "xxx"
 GOV.UK Pay ->> Service: Webhook: Payment started
 GOV.UK Pay ->> GOV.UK Pay: Authorise payment
 Note over GOV.UK Pay,GOV.UK Pay: Success
 GOV.UK Pay ->> Service: Webhook: Payment successful
 GOV.UK Pay ->> GOV.UK Pay: Capture payment
 Note over GOV.UK Pay,GOV.UK Pay: Success
 GOV.UK Pay ->> Service: Webhook: Payment captured
 ```

### Example recurring payment journey (rejected)
```mermaid
 sequenceDiagram
 participant Service
 participant GOV.UK Pay
 Service ->> GOV.UK Pay: Create recurring payment
 Note over Service,GOV.UK Pay: POST /v1/payments
 Note over Service,GOV.UK Pay: "authorisation_mode": "agreement"
 Note over Service,GOV.UK Pay: "agreement_id": "xxx"
 GOV.UK Pay ->> Service: Webhook: Payment started
 GOV.UK Pay ->> GOV.UK Pay: Authorise payment
 Note over GOV.UK Pay,GOV.UK Pay: Declined
 ```

## Managing recurring payments
Recurring payments taken with the `agreement` `authorisation_mode` can be managed exactly the same as existing GOV.UK Pay payments.
* [Refunding payments](https://docs.payments.service.gov.uk/refunding_payments/)
* [Report on a payment](https://docs.payments.service.gov.uk/refunding_payments/)