---
tags: [IP Allow Listing]
stoplight-id: de106d6bed233
---

# IP Allow Listing

IP allow listing will ensure that when we receive your API requests, we only accept them from your IP addresses. This means that even if your API access is compromised, we will only allow requests from your infrastructure. This is an excellent security feature which ensures that you are the only one with access to your data. We support both ipv4 and ipv6 ranges, so if you have more than one IP then it isn't a problem. Note We also offer IP allow listing for Dashboard, so that only your users can access your clients' data.

## Pre-requisites

Before requesting an IP allow list with us, make sure you have considered the following:

1. Are your IPs static? You need to ensure the IPs you give us will not change frequently, otherwise you risk losing access to our APIs and dashboard.
2. Do you know what your IP is when sending public traffic to us?
3. In the case that something goes wrong during allow list set-up, are you prepared for a brief outage? Setting up the allow list will block any traffic outside of the expected IP range. If the IP range is incorrect, you could end up having an outage.

## Set up

To begin setting up IP allow listing, you should contact your customer success manager and provide the following information:

1. Which environment(s) you want to be IP allow listed
2. The set of IPs (or the IP range) we should accept requests from
3. Whether it is for the API, Dashboard, or both.