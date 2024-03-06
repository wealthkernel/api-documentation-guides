---
tags: [Bank Accounts]
---

# Bank Account FAQs

# Why has a bank account stayed in the `Pending` state?

Bank accounts may sit in the `Pending` state for slightly longer than usual if our automatic verification has failed. In this scenario, manual intervention is required to verify that the bank account belongs to the party.

# When can I add deposits from a bank account?

You can add deposits via our API as soon as a bank account is added - even if it is still in the `Pending` state. However, when the cash reaches us, we will not match it to the party's portfolio until verification is complete and the bank account is in the `Active` state.

Please note that attempting to add a Direct Debit mandate while the bank account is still `Pending` is not possible, as a bank account must be verified before permission can be given to take payments from the bank account. Therefore, funding using Direct Debit payments will require an `Active` bank account.

# What does it mean if a bank account is suspended?

If a bank account is in the `Suspended` state, one or more checks on the bank account have failed. Until we resolve the issues with these checks, we will not match cash and deposits cannot be added using our API. 
