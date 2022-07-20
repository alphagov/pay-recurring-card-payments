# Recurring card payments

> :warning: This feature and guidance is part of a private beta so may be subject to change. For general help using Pay please refer to [Pay's documentation](https://docs.payments.service.gov.uk/) or [contact support](https://www.payments.service.gov.uk/support/) if you have questions.

GOV.UK Pay is adding support for recurring card payments  (also known as automatic card payments). Public sector services will be able to set up agreements with their users so that they can repeatedly charge for services provided on an ongoing basis.

Once a user gives permission, the amount can be automatically deducted on a prearranged schedule e.g daily, monthly, annually until a user chooses to end the agreement. 

This space documents the conceptual model and API interface to allow your service to set up and start processing recurring payments with GOV.UK Pay. This will rely on tokenisation provided by the underlying PSP in use (currently Worldpay or Stripe) to securely store the card numbers on your behalf. Our team is here to support your service getting started.

## Getting started

To start building a recurring card payments integration with your service, [contact support](https://www.payments.service.gov.uk/support/) to enable the features for your existing Sandbox account.

With recurring features enabled, you can start integrating with: 

- [common recurring paying user journeys](./2022-07-13/taking-recurring-payments/Journeys.md)
- [creating and setting up agreements for your users](./2022-07-13/taking-recurring-payments/Agreements.md)
- [taking recurring payments](./2022-07-13/taking-recurring-payments/Payments.md) and [get notified about their results](./2022-07-13/webhooks/README.md)
- [managing recurring payments in the admin tool](./2022-07-13/taking-recurring-payments/Management.md)


## Beta membership
The organisations taking part in this beta and adopting recurring payments are:

* Department for Work and Pensions
* Foreign, Commonwealth & Development Office
* Environment Agency
* Scottish Social Services Council / Care Inspectorate
* Stoke Council

If you are interested in joining the private beta and using recurring card payments [contact us](https://www.payments.service.gov.uk/support/).
