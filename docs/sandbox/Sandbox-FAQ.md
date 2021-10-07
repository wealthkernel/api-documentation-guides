---
tags: [Sandbox]
---

# Sandbox FAQ

## What is Sandbox?

Sandbox is the name for our pre-production environment that you will likely use as part of your onboarding process. You will be given an API key and potentially access to Admin Portal.

## How should I use it?

You can use it in a number of different ways. When onboarding, you will likely be wanting to creates Parties, Accounts and Portfolios and then fund them to test the API.

We have also seen some customers use it to do their integration testing.

## Are there any differences between Sandbox and Production?

Yes, in a number of areas outlined below.

### Deposits

#### Sandbox

Deposits will automatically move into a `Matched` state roughly 30 seconds after creation, at which time the `Deposit` transaction will be booked into the Portfolio for that day

#### Production

Once created, it may take some time for the client (your user) to deposit the money. Once we have received the money, it will then be matched at the earliest available opportunity. Because of these steps, the process could potentially take days

### Withdrawals

#### Sandbox

Once a withdrawal is created, fees (if any) will be charged and then the requested withdrawal will automatically be paid out. This process from start to finish should take roughly one minute, with pause between charging any fees and then paying out the money requested.

<!-- theme: danger -->

Due to how fast you can request withdrawals (multiple in one day), you can end up in a state where you withdraw into negative cash. This cannot happen in production.

#### Production

Once a withdrawal is created, there can be a multi day process of selling down the holdings in a portfolio to cover the amount of money requested by the withdrawal.

### Valuations

#### Sandbox

Valuations for Portfolios are always generated at the same time each day. This occurs at 8AM (UTC).

#### Production

Due to the nature of the platform, we may not generate valuations at the same time each day. Generally valuations for all portfolios should be available by 9AM (GMT) but this is not guaranteed.

### Orders

#### Sandbox

Depending on your portfolio's mandate type, portfolios may be managed by us which means we will be placing the orders for the portfolios. We do not currently do this in sandbox. If you require this for testing, please raise a service desk ticket and someone will be able to help you.

#### Production

If your portfolios are managed by us, we will be placing orders for your portfolios.

### Prices & Securities

Currently not all of the securities we have set up in Production are mirrored into Sandbox. If you require a specific security for testing purposes, please create a service desk ticket.

Similarly, we do not have up to date prices in Sandbox, and the ones that are generated each day stay the same for each ISIN.

