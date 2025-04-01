---
stoplight-id: cb46e29ea99a4
tags: [Accounts]
---

# Opening requirements

Each Account has its own set of requirements, listed below, that must be validated before the account can be opened. On top of the requirements below, adult parties (including the registered contact for a JISA, or parent / guardian for a SIPP) must also pass KYC checks.

<!-- theme: info -->
> These requirements are up to date as of 2025-03-28.

## GIA

Note that this is different to the opening requirements for a [corporate GIA](/docs/guides/cb46e29ea99a4-opening-requirements#corporate-gia).

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

For an adult member, the member must:

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

For a child member, the member must:

- Be a `Person`
- Have a forename
- Have a surname
- Be under 18 years old
- Have a nationality
- Not be a US national
- Not be a US tax resident
- Have at least one active UK address
- Have a `parentOrGuardian` party added to their account

Note that the parent or guardian must meet the requirements of the adult SIPP member above.

## Corporate GIA

To create a corporate GIA, the `productId` must be `prd-gia-corporate`.

The owner must:

- Be an `Organization`
- Have at least one active address
- Provide their country of incorporation
- Have a Legal Entity Identifier (LEI) if the organization plans to trade reportable instruments