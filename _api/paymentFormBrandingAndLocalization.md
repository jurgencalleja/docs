---
title: Payment Form Branding & Localisation
position_number: 5
type: post
description: However, the Hosted Payment Form is loaded, it is possible to customise the Hosted Payment Form to match the design and branding of the merchant’s webpage. The merchant must provide the IPG Gateway with the CSS and image files.  Sample files can be supplied on request.  The customised CSS file must be delivered to the IPG Gateway Support Team for review and sign off to ensure code integrity and security.  The files will be loaded to the merchant’s configuration in the IPG Gateway.
#description: Localisation - Merchants will present different languages on their website.  The Hosted Payment Page should reflect the language being viewed by the customer.
#description: The language used in the Hosted Payment Form is determined by the value provided in the language parameter in the Session Token Request (section 1.1).
#description: If IPG Gateway does not support the requested language the default will be Spanish.  However, to ensure the language is supported, the merchant should contact IPG Gateway Support Team to have the language added to the IPG Gateway suite.
#description: Appendix A	UAT Trigger Values
#des: When integrating with the IPG Gateway in the User Acceptance Testing (UAT) environment, certain amount values in the Session Token Request (section 1.1) can be used to elicit status and error messages.  This facility is provided to merchants so that testing can be confirmed against these expected errors.
 
parameters:
  - Amount: 0.00
    Status: SUCCESS
    Error message: {none}
  - Ammount: 0.01
    Status: SUCCESS
    Error message: {none}
  - Amount: 0.02
    Status: SUCCESS
    Error message: {none}
  - Amount: 0.03
    Status: ERROR
    Error message: Refer to card issuer
  - Amount: 0.04
    Status: ERROR
    Error message: Refer to card issuer, special condition
  - Amount: 0.05
    Status: ERROR
    Error message: Invalid merchant
  - Amount: 0.06
    Status: SUCCESS
    Error message: {none}
  - Amount: 0.07
    Status: ERROR
    Error message: Pick-up card
  - Amount: 0.08
    Status: ERROR
    Error message: Do not honor
    
---
