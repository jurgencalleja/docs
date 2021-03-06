---
title: AUTH/PURCHASE/VERIFY API Operation
position_number: 4
type: post
description: AUTH/PURCHASE/VERIFY API Request

parameters:
  - name: merchantId
    Datatype: Integer(18)
    Mandatory?: mandatory
    Description: The identifier for the merchant in the IPG Gateway provided at on-boarding
  - name: token
    Datatype: String (40)
    Mandatory?: mandatory
    Description: Session Token received in the Session Token Response - Processed
  - name: freeText
    Datatype: String (200)
    Mandatory?: optional
    Description: A free text field for use by the merchant that is returned in the Transaction Result Call (see IPG Gateway - 6 - TRANSACTION RESULT CALL), can be used if not supplied in the Session Token Request
  - name: customerId
    Datatype: String (20)
    Mandatory?: conditional
    Description: Customer identifier in the merchant system, or the value generated by the IPG Gateway in a previous original payment transaction using the payment card or method. The value is used to validate that the payment card token is for the correct customer.  If the customerId value is not the same held against the payment card token in the IPG Gateway database a Auth/Purchase/Verify Response – Not Processed (section 2.4) is returned. This must be the value supplied in or by the TOKENIZE API Operation.  The value is used to validate that the payment card token is for the correct customer.•	Mandatory for payment cards method •	Must not be supplied if quickSale = TRUE •	Optional for alternative payment methods. If the parameter is omitted or no value is provided for a first time use of the payment card, the IPG Gateway will generate a value, which will be stored internally against the payment method and returned in the Auth/Purchase/Verify Response – Processed (section 2.3). Condition- Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored.
  - name: customerIPAddress
    Datatype: String (39)
    Mandatory?: conditional
    Description: Customer IP address from where purchase is made. Only IPv4 supported Condition - Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored
  - name: fraudToken
    Datatype: String (50)
    Mandatory?: optional
    Description: Antifraud token. If an antifraud tool has been executed before an analysis identifier is required by payment acquirer. Mandatory for transactions conducted in LATAM countries, and only when the merchant wishes the transaction to be conducted as direct integration (server-to-server), as opposed to browser-redirection based integration.
  - name: paymentSolutionId
    Datatype: Integer (18)
    Mandatory?: conditional
    Description: Payment solution identifier in the IPG Gateway. Condition- Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored.
  - name: setOneClickValueSettingForCard
    Datatype: Boolean
    Mandatory?: optional
    Description: If TRUE flags that the cardholder wishes to save the card stored in the specinCreditCardToken parameter for future OneClick transactions. Must be TRUE if the payment card is to be saved. Note - the card will only be available for use as a OneClick Payment Method, if the current transaction is successful.  Otherwise, the payment card will not be available in the future.  The customer will have to make another transaction that is successful.
  - name: specinCreditCardCVV
    Datatype: String(5)
    Mandatory?: conditional
    Description: Credit card CVV, if payment solution is credit card through the ECOM channel. Condition - Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored.
  - name: specinCreditCardToken
    Datatype: String (100)
    Mandatory?: conditional
    Description: The payment card token received in the TOKENIZE API Operation, see IPG Gateway – 1 – TOKENIZE Condition - Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored
  - name: specinCreditCardToken
    Datatype: String (100)
    Mandatory?: conditional
    Description: The payment card token received in the TOKENIZE API Operation, see IPG Gateway – 1 – TOKENIZE Condition - Mandatory, if not received in the Session Token Request (section 1.1), otherwise ignored
  - name: ipPlanId
    Datatype: String (7)
    Mandatory?: optional
    Description: The Plan ID of the chosen Instalments Plan. If not included in the context of Instalments Plans, the API Operation will be treated as a normal single purchase transaction. Only used by merchants from the EVO MX Sales Channel




left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/token?"> {
         merchantId=1111111&token=abcde12345abcde12345}
    title: verify request
    language: javascript
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/token?"> {“result”:”success”,"merchantId":111111,"merchantTxId":"abc123","txId":"123","acquirerTxId":"0009312","amount":12.50,"currency":"GBP","customerId":"mgn456","action":"PURCHASE","pan":"45ae201ghy23498FjMj701","brandId":3,"paymentSolutionId":500,"freeText":"Added+10%+discount+on+the+item","language":"en","acquirerAmount":16.7,"acquirerCurrency":"EUR","paymentSolutionDetails":{“authCode”:"1234"},”status”:”NOT_SET_FOR_CAPTURE”}
    title: redirection response
    language: javascript
right_code_blocks:
  - code_block: |2-
      {
          "result": "redirection",
          "merchantId": "111111",
          "merchantTxId":"abc123",
          "txId":"123",
          "redirectionUrl":"https://mpi.bank.com/123123123-abc-123123123"
      }
    title: Redirection
    language: json
  - code_block: |2-
      {
          "result": "failure",
          "resultId": "7433a8d6-caea-40e6-a6eb-90c11dad61b",
          "additionalDetails": {},
          "errors": [
            {
               "messageCode": "field.nonempty",
               "fieldName": "action"
            }
          ],
          "processingTime": 2
      }
    title: Error
    language: json
---