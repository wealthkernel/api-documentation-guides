---
tags: [Webhooks]
---

# Local testing

## Tunnelling traffic to your local machine

To test out webhooks locally without deploying an application to an environment or exposing your test environments to the Internet, you can use ngrok, a free service which tunnels internet traffic to your local environment. 

Download ngrok [here](https://ngrok.com/download), then follow their getting started guide.

## Configuring webhooks through the portal

Once you’re up and running with ngrok, you’ll need to configure our webhooks as follows:

1. Generate a secret in the portal and save its value for later
2. Create subscription in the portal, using the URL provided by ngrok

Ensure ngrok is running and forwarding traffic to the port on which your local application is running.

You can then send the test event by clicking the button in admin portal or sending an API request
The request will be sent to your local application via ngrok, where you can:

1. Handle the event
2. Return a 200
3. Check the signature
4. Perform any business logic based on the new information you have received
