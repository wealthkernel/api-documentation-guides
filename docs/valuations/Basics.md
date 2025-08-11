---
tags: [Valuations]
---

# Valuations

A valuation is the breakdown of the value of cash and holdings in a portfolio at the close of its date.

## Concepts

- Valuations are made available on a T+1 basis.
- Valuations are designed to give a value at close on the valuation's date. For more realtime data, [Balances](../balances/Basics.md) should be used.
- The `changedAt` property on a valuation shows the time that the most recent update to that valuation occurred.

## Examples

On 2025-01-01 a deposit is made to prt-1. This deposit will first be reflected in valuation prt-1-20250101. This valuation will be calculated early in the morning (UTC) on 2025-01-02.

On 2025-01-03 a transaction in prt-1 is booked with the timestamp 2025-01-01 12:00:00. This will cause a refresh of the valuation for both prt-1-20250101 and prt-1-20250102.

## Keeping in sync

 In order to keep your valuation data up to date, the following strategy is recommended:

1. Retrieve valuations and store the latest `changedAt` property. You may want to provide a `startDate`.
1. Schedule a job at your desired update frequency, e.g. every hour.
1. Retrieve valuations again, providing the `changedAt` property from step 1 in the `updatedSince` query parameter.