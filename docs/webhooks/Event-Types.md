# Event Types

Depending on your needs, you may only need a subset of all the events we offer. To make this easy to manage, you can opt in to only the event types you need. You can choose these in our portal, and use them in your code to determine any action you need to take.

This is an excerpt of a request to demonstrate how event types are included in the webhook request.

```json
{
[...],
“eventType”: {
    “name”: “test”,
    “version”: 1
},
[...]
}
```

Within the name of the event is the concept of a namespace to give a more consistent view of what is happening in our system. For example deposit.deposit_settled, which generally refers to a resource that exists on the WealthKernel API, e.g. Parties.

The eventType also contains a version, which allows us to update an eventType without breaking your integration. Should you wish to work with the new version of this event, you can then manage the transition between two versions of the event at your convenience.
