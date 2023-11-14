---
tags: [IP Allow Listing]
---

# FAQs

## 1. At what point is traffic filtered?

We filter IP traffic after you've authenticated. This means that requests to our authentication endpoints (`/connect/token`) are not filtered at all. This is due to the fact that, until you are authenticated, we don't know who is sending traffic to us. Once you've successfully received an access token and start sending requests to other endpoints, we will filter your requests and return a 403 Forbidden when the remote IP is not in the allow list.

If you are testing the IP allow list functionality in sandbox, ensure you do something like the following after your allow list is implemented:

1. First, get an access token from `https://auth.sandbox.wealthkernel.io/connect/token`
2. Make a request to an authenticated endpoint, such as `https://api.sandbox.wealthkernel.io/parties`
3. Observe that you get a 2xx response - if you get a 403 Forbidden, it is likely something isn't quite right with the IP allow list configuration.

## 2. What types of IPs do you support?

We support both IPv4 and IPv6, and you can give us a list of IPs or a range.

## 3. What if we don't have an allow list?

By default, if you don't have an allow list, we will serve any remote IP making requests to us which has a valid access token.
