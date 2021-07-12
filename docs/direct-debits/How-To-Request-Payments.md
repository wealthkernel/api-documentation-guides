---
tags: [Direct Debits]
---

# How To Create Payments

## Creating a Mandate
Before you can make any payments you have to first create a Mandate. To create a new mandate you must have already created a party and bank account. Since a mandate is merely an instruction to give authority to take payments, a mandate can be created without a portfolio or account being created first.

The bank account number and sort code must be able to pass a Modulus check including on sandbox environments. For test purposes you should use `55779911` as the account number and `20-00-00` as the sort code

Once you've met the prerequisites you can request a new mandate using the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates/post">Create Mandate API</a>.

When a mandate has been created it starts in a `Pending` state. You must wait until it has transitioned to an 'Active' status before you can start creating payments. It's also at this stage you would display the success page referred to in the [UI Guidelines](./Api-Access.md#page-3---success-screen). You can monitor this using the returned mandate Id against the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">Get Mandate API</a>.

The end user will receive an email, usually within an hour, of the mandate being create. This email have the mandate PDF attached to it.

> It's still possible for a mandate to fail after it's reached the Active state. If this happens, any payments created against the mandate will automatically be failed as well.

### Mandate Failures
When a mandate failure occurs, the reason will usually be returned on the mandate through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D/get">Get Mandate API</a>.

These are most commonly caused by incorrect bank account details. In this case the simplest solution is to create a new bank account against the party and try again to create a mandate using the new bank account id.

## Creating a Payment

You can create a payment either as a single one-off or as a recuring subscription. Before you can create either of these a mandate must have been created using the steps mentioned previously, and a portfolio must have also been created. The mandate must have an `Active` status before payments or subscriptions can be created.

> Payments are submitted to BACS daily at around 4pm. After this they cannot be cancelled.

### Single Payments
You can create single payments through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments/post">Create Payment API</a>. You can optionally provide a collection date, but this must be on or after the date returned from the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1mandates~1%7BmandateId%7D~1next-possible-collection-date/get">next possible collection date endpoint</a>. If a collection date is not specified, the payment will be collected as soon as possible.

You can monitor the status of the payment through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D/get">Get Payment API.</a> Depending on whether the payment has been submitted to BACS (See the note above) you can also <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D~1actions~1cancel/post">cancel</a> the payment.

### Subscriptions
A subscription is effectively a rule to describe when to automatically create single payments. Once created these payments behave like any other single payment and can be viewed through the <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1payments~1%7BpaymentId%7D/get">payments API</a>.

When <a href="/docs/api/docs/openapi/api.yaml/paths/~1direct-debits~1subscriptions/post">creating a Subscription</a>, you can specify an inteval of `Weekly`, `Monthly` or `Yearly`. For Monthly and Yearly intervals you can specify a `dayOfMonth` option and for Yearly you can also specify a `Month` for the payment date.

> `dayOfMonth` refers to the collection date, so the payment will be created prior to this date with the goal of the money being taken from the end users account on this day or the next working day.

Optionally you can also supply a `startDate` when creating a subscription. This controls when the subscription can start triggering payments. For example if you create a monthly subscription on the 2nd of the month, with the dayOfMonth set to the 15th, but then set the `startDate` to the 20th. Then the first payment would not be created until just before the 15th of the following month. Whereas omitted in the startDate would result in the first payment being created on the 15th of the same month.