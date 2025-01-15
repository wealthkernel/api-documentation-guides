---
tags: [Outbound Transfers]
---

# Sandbox Simulation

## Requesting an outbound transfer

To request an outbound transfer, you will need to contact us and provide us the account ID you'd like to transfer out. There is currently no API to request an outbound transfer.

## Simulation flow

In sandbox, when an outbound transfer is requested it will automatically go through the usual statuses due to simulation. We have 30 second delays between status changes to allow you to fetch the resource while it is still in the individual statuses and inspect what it would look like. 

There are also simulated documents, but note that these will not look like the documents received in production and are just placeholders.