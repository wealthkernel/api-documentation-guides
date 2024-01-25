---
stoplight-id: wd4h0w1bl31lb
---

# US Withholding Tax

When a non-US resident invests in US shares, the US government mandates a tax charge on any income received from those shares. The tax charge will be dependent on the tax residency of the customer making the investment. 

To ensure the customer pays the correct amount of tax, they can complete a W-8 BEN form. 

The W-8 BEN form is a declaration by the customer and includes information such as their personal details and tax residency. The form remains active until the end of the third calendar year after the form is signed (i.e. if the form is signed in January 2024, it is valid until 31st December 2027). At this point a customer will need to complete a new form to benefit from reduced rates of withholding tax.

WealthKernel provides a service for Tenants which will generate all of the required information to complete the W-8 BEN form to be presented to a customer. If all of the information presented to a customer is correct, the customer can attest to the information. Tenants can submit a customer's attestation which will create a PDF copy of the W-8 BEN form with a digital signature of the customer. The customer can access a copy of the W-8 BEN form should they require for their records. 

```mermaid
sequenceDiagram
    participant C as Customer
    participant T as Tenant
    participant W as WealthKernel
    C->>T: Selects a US Share or model containing a US Share to buy
    T->>W: Requests draft W-8 BEN for customer
    W->>T: Provides draft with customer data required for attestation
    T->>C: Presents information to customer
    C->>T: Attests to information
    T->>W: Confirmation of customer attestation
    W->>W: Log information 
    W->>W: Generate and store PDF
opt  
    T->>C: Displays option to download a PDF copy of the W-8 BEN
    C->>T: Selects to view the PDF 
    T->>W: Request W-8 BEN PDF
    W->>T: PDF returned
    T->>C: Display W-8 BEN PDF document to party
end
```