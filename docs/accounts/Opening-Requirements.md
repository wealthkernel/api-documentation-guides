---
stoplight-id: cb46e29ea99a4
tags: [Accounts]
---

# Opening requirements

Each Account has its own set of requirements, listed below, that must be validated before the account can be opened.

<!-- theme: info -->
> These requirements are up to date as of 2021-09-27

## GIA

Note that this is different to the opening requirements for a [corporate GIA](docs/guides/cb46e29ea99a4-opening-requirements##corporate-gia).

The owner must:

- Be a `Person`
- Have a forename
- Have a surname
- Be older than 18 years old
- Have a nationality
- Have a valid NINO
- Be a UK tax resident
- Not be a US National
- Not be a US tax Resident
- Have an email address
- Have at least one active UK address
- Specify their employment status (and industry, if employed)
- Provide their expected annual income
- Provide their sources of wealth

## ISA

The owner must:

- Be a `Person`
- Have a forename
- Have a surname
- Be older than 18 years old
- Have a nationality
- Have a valid NINO
- Be a UK tax resident
- Not be a US national
- Not be a US tax resident
- Have an email address
- Have at least one active UK address
- Specify their employment status (and industry, if employed)
- Provide their expected annual income
- Provide their sources of wealth
- Not have an existing ISA

## JISA

The registered contact must:

- Be a `Person`
- Have a forename
- Have a surname
- Be older than 18 years old
- Have a nationality
- Have a valid NINO
- Be a UK tax resident
- Not be a US national
- Not be a US tax resident
- Have an email address
- Have at least one active UK address

The child must:

- Be a `Person`
- Have a forename
- Have a surname
- Be younger than 18 years old
- Have a nationality
- Not be a US national
- Not be a US tax resident
- Have at least one active UK address
- Not have an existing JISA

## SIPP

<!-- theme: warning -->
> SIPPs are currently in a private beta. If you wish to access them, please contact your account manager for more details

The member must:

- Be a `Person`
- Have a forename
- Have a surname
- Be older than 18 years old
- Have a nationality
- Have a valid NINO
- Be a UK tax resident
- Not be a US national
- Not be a US tax resident
- Have an email address
- Have at least one active UK address
- Specify their employment status (and industry, if employed)
- Provide their expected annual income
- Provide their sources of wealth

## Corporate GIA

To create a corporate GIA, the `productId` must be `prd-gia-corporate`.

The owner must:

- Be an `Organization`
- Must have at least one active address
- Must provide their country of incorporation
- If the organization plans to trade reportable instruments, an LEI identifier is also required.