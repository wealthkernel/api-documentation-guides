---
stoplight-id: 1wglbgxw55w7x
---

# US Withholding Tax FAQs

## How can a W-8 BEN form be submitted?

An endpoint is available to request draft information required to complete a form for a given party. The information can be displayed to the customer, accompanied by an attestation that the information is correct. 

On submission of the attestation to WealthKernel, a PDF copy of the W-8 BEN will be generated which can be accessed by a separate endpoint. 

## What if the W-8 BEN draft has incorrect information?

If any information in the draft request is incorrect, this should be updated separately and a new request generated. 

## Once the party has attested the W-8 BEN has the correct information, when does the W-8 BEN become valid?

Assuming all of the information is correct, the W-8 BEN form will become active at the point the party attests to the information. A digital signature will be generated with a timestamp of when the party confirmed the information. 

## What happens when the W-8 BEN form expires?

The form will last until the end of the third calendar year after it was initially signed (i.e. if the form is signed in January 2024, it will expire on 31st December 2027). 

## What happens if the details of the party changes?

If a change in circumstances results in the information contained within an active W-8 BEN form incorrect, the underlying party should submit a new form. 

## What tax residencies do you support for submitting W-8 BENs through the API?

Currently only UK tax residents can submit the W-8 BEN form via the API. 

## Can I submit a W-8 BEN-E form via the API?

Currently only the W-8 BEN form (for individuals) can be submitted via the API.

## Is a W-8 BEN form required for each account a customer holds?

No. Only one form is required for a customer no matter the number of accounts held. 
