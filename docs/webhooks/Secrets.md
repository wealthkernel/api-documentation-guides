# Secrets

We sign our webhooks using a secret, to prove that it is WealthKernel sending you requests, and not a third party. You can generate this secret through our portal. The secret will only be shown to you once, and is not retrievable, so make sure you record it at this point. The secret should be stored securely.

The value is the same for all subscriptions and event types, and consists of a series of cryptographically strong bytes encoded into base64. It is not possible to receive webhooks without first generating a secret.

Secrets expire after 3 months, however you may have up to two active secrets concurrently, allowing you to continue to receive webhooks without any downtime. The expiration time of your secret can be viewed through our portal at any time.

Secrets can be disabled, should the need arise, for example if your secret becomes compromised. If you disable your only secret, all webhook traffic will stop until a new secret is generated.

## Using a secret to verify a webhook

On every webhook request there is a header called `X-Webhook-Signature`. It is composed of a timestamp and at least one HMAC (hash-based message authentication code). A signature header looks like this:
```
t=16485552000000000,v1=d7021975861ff5baf2ca05913dce24ff7d03a51be8cb2fdd11c2e761b95650c4,v1=6a4c3ab16a3c8327c52408be0f006b5f5b71f5c11847cd055824ce90f6370c1f
```

The process for verifying the webhook using the signature is:

First, split the header down into its component pieces using comma (`,`) as a delimiter. Each component is a key-value pair, delimited by equals (`=`). The timestamp can be identified by the `t=` key. The HMAC(s) can be identified by a scheme key, e.g. `v1=`.

Next, concatenate the value of the timestamp element to the end of the body of the webhook request. Compute the HMAC with SHA-256 as the hash function, using your secret as the key, and the concatenated value as the message. Get the HEX encoding of the genereated HMAC.

Lastly, check if the timestamp is within your tolerance (to protect from replay attacks). Compare the HEX encoded HMAC(s) from the first step to the HEX encoded HMAC(s) you have generated. Note that if you have multiple secrets you might need to compare more than one HMAC.

<!-- theme: info -->
> A constant time string comparison here is recommended