---
title: Tokenize Card
position_number: 2
type: post
description: Tokenize a card  
 
parameters:
  - name: merchantId
    Datatype: Integer(18)
    Mandatory?: mandatory
    Description: The identifier for the merchant in the IPG Gateway provided at on-boarding.  This must be the same used in the related session token request.
  - name: token
    Datatype: String (40)
    Mandatory?: mandatory
    Description: Session Token received in the Session Token Response - Processed
  - name: number
    Datatype: String(100)
    Mandatory?: mandatory
    Description: The payment card number, primary account number (PAN), or simply a card number for the payment card being tokenised. The card number must be a single string of numbers, with no spaces, dashes or other characters
  - name: nameOnCard
    Datatype: String (150)
    Mandatory?: mandatory
    Description: Cardholder name as written on the payment card
  - name: expiryMonth
    Datatype: String (2)
    Mandatory?: mandatory
    Description: Card expiration month as a number, e.g. “04”.
  - name: expiryYear
    Datatype:  String (4)
    Mandatory?: mandatory
    Description: Card expiration year as a number, e.g. “2020”.
  - name: cardDescription
    Datatype: String (50)
    Mandatory?: optional
    Description: Free form text field for the merchant’s use that is used for reconciliation e.g. merchant’s internal card’s sequence id
  - name: startMonth
    Datatype: String (2)
    Mandatory?: conditional
    Description: Card issued month as a number, e.g. “04”. Condition - Only used for some card types. Required for Maestro; Optional for all other cards
  - name: startYear
    Datatype: String (4)
    Mandatory?: conditional
    Description: Card issued month as a number, e.g. “04”. Condition - Only used for some card types.  Required for Maestro; Optional for all other cards
  - name: issueNumber
    Datatype: String (2
    Mandatory?: conditional
    Description: Card issued month as a number, e.g. “04”.  Condition - Only used for some card types.  Required for Maestro; Optional for all other cards
 
left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/payment?"> {
      merchantId=111111, token=abcde12345abcde12345, number=4111111111111111, nameOnCard=NAME+OF+CARD+OWNER, expiryMonth=04, expiryYear=2020, cardDescription=Customer ID 123456
      };
    title: jQuery
    language: javascript
  
right_code_blocks:
  - code_block: |2-
      {
        "result": "success",
        "country": "GB",
        "resultId": "e086f9ad-6a78-4c56-b4e7-059764246811",
        "merchantId": "890490",
        "cardType": "400",
        "customerId": "testTokenize",
        "additionalDetails": {},
        "cardToken": "5512732598811111",
        "processingTime": 1000,
        "cardIssuer": null
        }
    title: Response
    language: json
  - code_block: |2-
      {
        "result": "failure",
        "resultId": "4e879e03-9ff1-481e-9611-b5155328a53f",
        "additionalDetails": {},
        "errors": 
        [
          {
          "messageCode": "This field is required in [REQUEST]",
          "fieldName": "number"
          }
        ],
      "processingTime": 8
      }
    title: Error
    language: json
---