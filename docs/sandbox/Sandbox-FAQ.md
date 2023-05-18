---
tags: [Sandbox]
---

# Sandbox FAQ

## What is Sandbox?

Sandbox is our pre-production environment that you will use as part of your onboarding process. 

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

Orders you create will automatically move into a `Matched` state roughly 30 seconds after creation, at which time the `Buy`/`Sell` transaction will be booked into the Portfolio for that day. The transaction will then automatically move into a `Settled` state roughly 60 seconds later.

We do not currently create orders in Sandbox for portfolio setups that will be managed by us. If you need some orders created for your testing then please raise a service desk ticket and we will try to help.

#### Production

If your portfolios are managed by us, we will be placing orders for your portfolios.

Be aware that orders will usually not match until after 3pm on the day they were created, and typically not settle until 2 days after they were created. This will vary by ISIN.

### Prices & Securities

Currently not all of the securities we have set up in Production are mirrored into Sandbox. If you require a specific security for testing purposes, please create a service desk ticket.

Similarly, we do not have up to date prices in Sandbox, and the ones that are generated each day stay the same for each ISIN.

### Fees

#### Sandbox

Fee accrual and charging is manual in sandbox. If you would like to test out fees in Sandbox please contact your tenant manager. 

To test in sandbox we will need the ID of the fee portfolio that you have set up and the accrual strategy details that have been agreed upon with your tenant manager. There also needs to be enough cash present in the portfolio, which you can ensure by making a deposit or creating orders if the portfolio's mandate is execution only. Typically we will simulate this for the previous month but let your tenant manager know if you want a different period.

#### Production

In production this process is automated.