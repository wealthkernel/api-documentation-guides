# Secrets

We sign our webhooks using a secret, to prove that it is WealthKernel sending you requests, and not a third party. You can generate this secret through our portal. The secret will only be shown to you once, and is not retrievable, so make sure you record it at this point. The secret should be stored securely.

The value is the same for all subscriptions and event types, and consists of a series of cryptographically strong bytes encoded into Base 64. It is not possible to receive webhooks without first generating a secret.

Secrets expire after 3 months, however you may have up to two active secrets concurrently, allowing you to continue to receive webhooks without any downtime. The expiration time of your secret can be viewed through our portal at any time.

Secrets can be disabled, should the need arise, for example if your secret becomes compromised. If you disable your only secret, all webhook traffic will stop until a new secret is generated.
