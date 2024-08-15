---
tags: [Inbound Transfers]
---

# Inbound transfer basics

## What is an inbound transfer?

This is a transfer of funds from an existing account with another provider into a portfolio managed by WealthKernel.

Currently we only support ISA, JISA and SIPP transfers, however in future we will be supporting others, such as GIA transfers.

The inbound transfer will pass through the following stages:

```mermaid
stateDiagram-v2
    [*] --> Pending: Request
    Pending --> Submitted
    Pending --> Cancelled
    Submitted --> Pending: Revision Requested
    Submitted --> Rejected
    Submitted --> Cancelled
    Submitted --> Accepted
    Accepted --> Transferring: Begin transfer
    Accepted --> Cancelled
    Transferring --> Transferred: Transferred assets received
    Transferred --> Completed
    Completed --> [*]
```

State | Explanation
---------|----------
 Pending | The inbound transfer has been requested, it can still be edited and WealthKernel will not process the inbound transfer until you submit it. 
 Submitted | The inbound transfer has been submitted to WealthKernel to be processed and requested from the ceding provider. 
 Accepted | The inbound transfer has been accepted by the ceding provider. 
 Transferring | The funds for the inbound transfer have been sent by the ceding provider to the portfolio managed by WealthKernel. 
 Transferred | The funds for the inbound transfer have been received and are available in the portfolio managed by WealthKernel.
 Completed | The inbound transfer has been completed.
 Rejected | The inbound transfer has been rejected by WealthKernel. The reason will be communicated in the status history entry.
 Cancelled | The inbound transfer has been cancelled.

## Status history

For each status change that an inbound transfer goes through, we create a status history entry on the resource with a timestamp and an optional reason (populated for rejections and requests for more information).

## Requesting an inbound transfer

To [request an inbound transfer](https://docs.wealthkernel.com/docs/api/c0641cdcaad59-request-an-inbound-transfer) through our API, you must provide us with the details of the account that you would like to transfer (there are specific requirements for each type of transfer, that can be found on the relevant transfer type guide page). We have a list of known ceding providers that can be queried by transfer type. If the ceding provider is not one that is known by us, you can provide the name and address.
Each inbound transfer request must satisfy the following requirements:

- The portfolio referenced on the inbound transfer request must be Active.
- The account that the portfolio is under must be Active.

There are a few things to be aware of when providing client data:

- Any addresses that we capture should be as they are registered with the ceding provider.
- The estimated transfer amount does not have to be exact.

Once the resource has been created, it will be in the Pending status and WealthKernel will not process the inbound transfer until you submit it. The reason for this is that you may need to upload a document for the ceding provider. Some ceding providers require a signed form, and so you can choose to provide one at the start of the process or we will ask for one later on if the ceding provider requires one.

> Whilst the inbound transfer is in Pending, you can patch certain details on the resource.

## Attaching a document to an inbound transfer

To attach a document to an inbound transfer, firstly you need to [provide the document metadata](https://docs.wealthkernel.com/docs/api/a19c0afc799f2-add-document-metadata) and after you will be able to [upload your document contents](https://docs.wealthkernel.com/docs/api/ab300f280c6b4-add-document-contents) to the document resource.

Documents can only be attached to a Pending inbound transfer, and you cannot submit the inbound transfer if a document is missing contents.

## Submitting an inbound transfer

When all information (including documents) is attached to the inbound transfer, you need to [submit it to WealthKernel](https://docs.wealthkernel.com/docs/api/2d2c732382f2a-submit-inbound-transfer) to be processed.

After submission we validate the inbound transfer to check that the portfolio and account exist, and that the account type is valid for the account that is being transferred. If the information is valid, we will request the transfer from the ceding provider.

If the ceding provider accepts the transfer request, we will move the inbound transfer to the Accepted status.

However, if the inbound transfer fails our validation or the ceding provider rejects our request we move it back to `Pending` if we need more information or we move it to `Rejected` if it is not recoverable. You will be able to see the reason in the status history entry.

> If the inbound transfer is moved back to Pending, you can update the resource again.

## After the inbound transfer is accepted

Once an inbound transfer is Accepted, the ceding provider will begin to liquidate the account (if this is required) and once that is complete, they will send the funds to the portfolio managed by WealthKernel.

Once we receive notification that that has happened, the inbound transfer will move to the Transferring status.

Once we receive the money and it is available in the portfolio, we will move the inbound transfer to Completed.

## Cancelling an inbound transfer

You can [cancel an inbound transfer](https://docs.wealthkernel.com/docs/api/197b558519290-cancel-inbound-transfer) that is Pending, Submitted or Accepted. The inbound transfer will be immediately moved to Cancelled if the inbound transfer was Pending. However, if it is not in Pending, it will not immediately move to Cancelled as we may need to request cancellation from the ceding provider, and it may be the case that they have already begun the transfer of the funds and can’t cancel it. 
In the case where we can´t cancel the inbound transfer, we will communicate the reason by adding a new status history entry.

## Webhooks

To allow you to respond more quickly to changes on inbound transfers, we expose webhooks that you can consume. You can find out more about using webhooks on our [webhooks guide](../webhooks/Getting-Started.md), or look at our main API documentation to see the structure of each of the inbound transfer webhooks.

| Event Type | Description |
|------------|------------:|
| `inbound_transfers.inbound_transfer_requested` | Notification that a new inbound transfer has been requested. The inbound transfer will be in the `Pending` status. |
| `inbound_transfers.inbound_transfer_submitted` | The inbound transfer has been submitted to WealthKernel. The inbound transfer will be in the `Submitted` status and will be validated. |
| `inbound_transfers.inbound_transfer_revision_requested` | The inbound transfer needs more information or changes before it will be accepted. The transfer has been moved back to the `Pending` status. |
| `inbound_transfers.inbound_transfer_rejected` | The inbound transfer failed validation and is not recoverable. To continue, a new inbound transfer will need to be created. This inbound transfer will be in the `Rejected` status. |
| `inbound_transfers.inbound_transfer_accepted` | Validation has passed and the ceding provider has accepted the inbound transfer. The inbound transfer will be in the `Accepted` status. |
| `inbound_transfers.inbound_transfer_transferring` | The ceding provider is now in the process of sending WealthKernel the assets. The inbound transfer will be in the `Transferring` status. |
| `inbound_transfers.inbound_transfer_transferred` | WealthKernel has received the assets and they are now in the client's portfolio. The inbound transfer will be in the `Tranferred` status. |
| `inbound_transfers.inbound_transfer_completed` | The transfer has completed successfully and is now in the `Completed` status. |
| `inbound_transfers.inbound_transfer_cancelled` | The inbound transfer was cancelled and is now in the `Cancelled` status. |
| `inbound_transfers.inbound_transfer_cancellation_rejected` | We received a request to cancel the transfer, but it is already too late and we cannot cancel the transfer anymore. The inbound transfer's status has not changed. |

### Typical inbound transfer lifecycle

Usually an inbound transfer will follow the below lifecycle and you should receive webhooks in this order. This assumes it is not cancelled or rejected.

| What happened | Updated account status | Webhook event |
| ------------- | ---------------------- | ------------- |
| Inbound transfer is requested | `Pending` | `inbound_transfers.inbound_transfer_requested` |
| The transfer is submitted to us | `Submitted` | `inbound_transfers.inbound_transfer_submitted` |
| The ceding provider has accepted the transfer | `Accepted` | `inbound_transfers.inbound_transfer_accepted` |
| Assets are being transferred to WealthKernel | `Transferring` | `inbound_transfers.inbound_transfer_transferring` |
| The assets have been received and moved into the client's portfolio. | `Transferred` | `inbound_transfers.inbound_transfer_transferred` |
| The inbound transfer is complete. | `Completed` | `inbound_transfers.inbound_transfer_completed` |
