---
tags: [Inbound Transfers]
---

# Sandbox simulation

In sandbox there is some functionality that is designed to simulate the flow in production. The time frames in production may be days, however in the simulation time is compressed so that the whole flow (from Pending to Completed) takes minutes.

## Normal flow simulation

After an inbound transfer has been submitted to WealthKernel for processing, the simulation takes over and begins to transition the inbound transfer through the statuses. The interval between each of the state transitions is 30 seconds.

## Simulating a request for more information

If you would like to simulate a request for more information(for example the ceding account reference was not found by the ceding provider) you can do so by setting the ceding provider reference to `TRIGGER_PENDING`. Once you submit the inbound transfer to WealthKernel for processing, after 30 seconds we will move the inbound transfer back to Pending.

You can then update the inbound transfer and resubmit.

## Simulating a cancellation rejection

If you would like to simulate a cancellation request being rejected you can do so by setting the ceding provider reference to `TRIGGER_CANCELLATION_REJECTION`.

Once you request cancellation of the inbound transfer, after 30 seconds we will set cancellation requested back to false.
