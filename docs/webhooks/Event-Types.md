# Event types

Depending on your needs, you may only need a subset of all the events we offer. To make this easy to manage, you can opt in to only the event types you need. You can choose these in our dashboard, and use them in your code to determine any action you need to take.

This is an excerpt of a request to demonstrate how event types are included in the webhook request.

```json
{
[...],
"eventType": {
    "name": "webhooks.test",
    "version": 1
},
[...]
}
```

The name of an eventType is broken down into the namespace name and local name, separated by a full stop (`.`).

The eventType also contains a version, which allows us to update an eventType without breaking your integration. Should you wish to work with the new version of this event, you can then manage the transition between two versions of the event at your convenience.

Note that if you are subscribed to two versions of the same webhook you may wish to only process one of them. You can use the `eventId` to determine if they are the same event.
