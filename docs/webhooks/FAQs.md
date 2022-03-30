# Webhooks FAQs

## Do you guarantee ordered events?

We do not guarantee in order events, so you’ll need to consider how to deal with receiving events that are out of order. 

## How many times will you deliver a webhook?

In order to guarantee that each webhook request is delivered at least once while remaining performant, it is possible that a webhook request may be delivered more than once. 

## How can I handle a webhook delivered more than once?

We provide an idempotency key as a header on each request, which we advise you utilise to ensure you do not process the same event more than once.