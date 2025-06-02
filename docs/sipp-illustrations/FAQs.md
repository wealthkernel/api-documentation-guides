---
stoplight-id: 26cgp5wk2wbxx
tags: [SIPP Illustrations]
---

# Illustrations FAQs

## Does the illustration service support drawdown illustrations?

At present, the illustration service only supports accumulation illustrations. Illustrations for drawdown and drawdown transfer will be added in the future. 

## Does the illustration service support fee tiering?

Yes, fee tiers can be accommodated, as per the example in the API documentation.

## Is it possible to add adviser, DFM and product provider charges in one illustration?

Yes, this combination of fees can be added, as per the example in the API documentation. 

Adviser fees can be added into the adviser section of the API request. DFM and product provider fees can be added into the 'provider' section of the API request.

## Is it possible to include more than one transfer?

Yes, more than one transfer can be included on a single illustration if required. The example illustration in the API documentation shows how this can be requested. 

## Can the raw data of the illustration be accessed?

At present only the illustration document can be retrieved along with the inputs used for the illustration.

##  Is it possible to edit an existing illustration?

If a variation of an illustration is required, a separate request will need to be made to the illustration service.
