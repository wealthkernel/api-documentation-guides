# Testing

To enable you to check you have set up your infrastructure correctly, we offer a test event type. This can be triggered via our portal or API and does not contain any information pertaining to a resource, just the following:

```json
{
  “eventId”: ”whevt-abc123”,
  “eventType”: {
      “name”: “webhooks.test”,
      “version”: 1,
  },
  “payload”: {
      
  }
}
```

You can view the status of webhook requests in our portal, including the HTTP status code we received.

Webhooks are also available to try out on our sandbox environment. 

If you want to receive webhooks locally, you can use a service such as ngrok to make your local endpoint accessible publicly, see [here](../webhooks/Receiving-Webhooks.md) for more information.

You may wish to disable the subscription for this event when you are finished.
