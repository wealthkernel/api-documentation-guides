---
tags: [Direct Debits]
---

# How To Request Payments

## Creating a Mandate
Before you can make any payments you have to first create a Mandate. To create a new mandate you must have already created a party and bank account. A mandate is only an instruction to give authority to take payments. As such you can create a mandate without creating a portfolio or account first.

The bank account number and sort code used to create the mandate must be able to pass a Modulus check. To test on sandbox, you should use `55779911` as the account number and `20-00-00` as the sort code.

Once you've met the prerequisites you can request a new mandate using the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates/post">Create Mandate API</a>.

When you create a mandate it starts with the `Pending` status. You cannot create payments until it has transitioned into an `Active` status. It's also at this stage that you would display the success page referred to in the [UI Guidelines](./Api-Access.md#page-3---success-screen). You can monitor this using the returned mandate Id against the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">Get Mandate API</a>.

The end user will receive an email, usually within an hour, of the mandate being created. This email has the mandate PDF attached to it.

> It's still possible for a mandate to fail after its reached the `Active` state. If this happens, any payments created against the mandate will fail as well.

### Mandate Failures
When a mandate failure occurs, the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">mandate resource</a> will usually include a reason.

These are most commonly caused by incorrect bank account details. In this case the simplest solution is to create a new bank account against the same party. Using the id of the newly created bank account, try creating the mandate again.

## Creating a Payment

You can create a payment either as a single one-off or as a recurring subscription. You must have created a portfolio and mandate before you can create a payment or subscription. The mandate must also be `Active`. Multiple payments and subscriptions or a mixture of both can all be raised against a single mandate.

> Payments are submitted to BACS daily at around 4pm. After this they cannot be cancelled.

### Single Payments
You can create single payments through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments/post">Create Payment API</a>. You may specify a collection date. This must be on or after the date returned from the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D~1next-possible-collection-date/get">next possible collection date endpoint</a> endpoint. If a collection date is not specified, the payment will be collected as soon as possible. If the collection date is not a working day, then the payment will be taken on the next working day.

You can monitor the status of the payment through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D/get">Get Payment API</a>. You can also <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D~1actions~1cancel/post">cancel</a> the payment before it has been submitted to BACS (See the note above).

Once created, a payment will pass through several states as outlined below.

|Status|Description|
|------|-----------|
|Pending|The payment has been created|
|Collecting|The payment has been submitted to BACS for approval. It cannot be cancelled at this point|
|Collected|The payment has been collected from the end users bank account|
|Completed|The payment has been received and allocated to the chosen portfolio|
|Failed|The payment was rejected within the banking system|
|Cancelled|The payment was cancelled at the intention of the API user|

### Recurring Subscriptions
A Subscription is a schedule definition describing when to generate payments. Once created these payments behave like any other single payment. As such you can manage it through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D/get">payments APIs</a>. After a Subscription starts it will continue generating payments until <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1subscriptions~1%7BsubscriptionId%7D~1actions~1pause/post">paused</a> or <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1subscriptions~1%7BsubscriptionId%7D~1actions~1cancel/post">cancelled</a>.

When <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1subscriptions/post">creating</a> a Subscription, you can specify an interval of `Monthly` or `Yearly`. Some optional request properties are only valid for certain intervals. If the request does not include any of these properties, the first payment will be taken at the earliest opportunity.

|Interval|Description|
|--------|-----------|
|Monthly|Can optionally specify a `dayOfMonth` when creating. |
|Yearly|Can optionally specify a `dayOfMonth` and/or `month` when creating|

You should consider inspecting the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D~1next-possible-collection-date/get">next available collection date</a> on the mandate. This will let you predict when a created subscription will generate its first payment. It's particularly helpful when using the `dayOfMonth` property. `dayOfMonth` can be between 1-28. Or you can specify -1 to signify that the payment should be take on the last working day of the month.

> `dayOfMonth` refers to the collection date. This is when the money will be taken from the user's account (or the next working day). The payment will be created in the system before this date.

Optionally, you can also supply a `startDate` when creating a subscription. This controls when the subscription can start triggering payments. For example if you create a monthly subscription on the 2nd of the month, with the `dayOfMonth` set to the 15th, but then set the `startDate` to the 20th. Then the first payment would not be created until just before the 15th of the following month. Whereas omitting the `startDate` would result in the first payment being created on the 15th of the same month.

### Payment Failures
As with mandates, if a payment fails then the reason will usually be returned on the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D/get">Payment resource</a>.