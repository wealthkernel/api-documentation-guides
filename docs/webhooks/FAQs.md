# Webhooks FAQs

## Do you guarantee ordered events?

We do not guarantee in order events, so you’ll need to consider how to deal with receiving events that are out of order. 

## How many times will you deliver a webhook?

We guarantee at least once delivery within our retry policy, so it is possible that a webhook request may be delivered more than once.

## How can I handle a webhook delivered more than once?

We provide an idempotency key as a header on each request, which we advise you utilise to ensure you do not process the same event more than once.

## What happens with events after I disable a subscription?

When a subscription is disabled, it stops receiving events, including any ongoing retry requests due to transient HTTP error codes. If you re-enable a disabled subscription, it will only receive new events.