# Secrets

We sign our webhooks using a secret, to prove that it is WealthKernel sending you requests, and not a third party. You can generate this secret through our portal. The secret will only be shown to you once, and is not retrievable, so make sure you record it at this point. The secret should be stored securely.

The secret is the same for all subscriptions and event types, and consists of a series of cryptographically strong bytes encoded into base64. It is not possible to receive webhooks without first generating a secret.

Secrets can be disabled, should the need arise, for example if your secret becomes compromised. If you disable your only secret, all webhook traffic will stop until a new secret is generated.

## Secret expiration

Secrets expire after 3 months, however you may have up to two active secrets concurrently, allowing you to continue to receive webhooks without any downtime. The expiration time of your secret can be viewed through our portal at any time.

The webhook signature header will contain one or multiple HMAC (hash-based message authentication code) values, depending on the number of active secrets at a given time. If you have two active secrets and one of them expires, from that point you will only receive one HMAC in the signature. If all secrets expire you will stop receiving webhooks.

We recommend to have one active secret and generate a new one when the expiration date of the secret gets close.

## Using a secret to verify a webhook

On every webhook request there is a header called `Webhook-Signature`, which is composed of:
* A timestamp in [UNIX seconds](https://en.wikipedia.org/wiki/Unix_time) prefixed by `t=`.
* A HMAC for each secret and scheme prefixed by `v{scheme}=`. (e.g. `v1=`). The only valid signature scheme at the moment is `v1`, but new schemas might be added in the future.

A signature header with two HMACs looks like this:
```
t=164855520,v1=d7021975861ff5baf2ca05913dce24ff7d03a51be8cb2fdd11c2e761b95650c4,v1=6a4c3ab16a3c8327c52408be0f006b5f5b71f5c11847cd055824ce90f6370c1f
```

The process for verifying the webhook using the signature is the following:

1. Split the header down into its component pieces using comma (`,`) as a delimiter. Each component is a key-value pair, delimited by equals (`=`). The timestamp can be identified by the `t=` key. The HMAC(s) can be identified by a scheme key, e.g. `v1=`.
1. Concatenate the value of the timestamp element to the end of the body of the webhook request.
1. Compute the HMAC with SHA-256 as the hash function, using your secret as the key (keep in mind the secret is base64, so you will need to decode it first), and the concatenated value as the message (if you need to get the raw bytes of the concatenated string use UTF-8 as the encoding).
1. Get the hexadecimal encoding of the genereated HMAC.
1. Compare the hexadecimal encoded HMAC(s) from the first step to the hexadecimal encoded HMAC(s) you have generated. Check if the timestamp is within your tolerance (to protect from [replay attacks](https://en.wikipedia.org/wiki/Replay_attack))

Note that if you have multiple secrets you might need to compare more than one HMAC.

<!-- theme: info -->
> A constant time string comparison here is recommended to avoid [timing attacks.](https://en.wikipedia.org/wiki/Timing_attack)

Here's the pseudocode to verify a webhook signature with one HMAC:
```
signature = getRequestHeader("Webhook-Signature")
body = getRequestBody()
secretBase64 = getSecret()
secretDecoded = decodeBase64(secretBase64)

signatureSplitByComma = signature.Split(",")
timestamp = signatureSplitByComma[0].Split("t=")[1]
signatureHmac = signatureSplitByComma[1].Split("v1=")[1]

content = concatenate(body, timestamp)
contentHmac = getHmacSha256(content)
contentHmacHexadecimal = toHexadecimal(contentHmac)

isVerified = equals(signatureHmac, contentHmacHexadecimal)
```