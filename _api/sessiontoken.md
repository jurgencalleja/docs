---
title: /session token/
position_number: 20
type: post
description: Get session token

parameters:
  - name: merchantId
    Datatype: Integer(18)
    Mandatory?: mandatory
    Description: The identifier for the merchant in the IPG Gateway provided at on-boarding
  - name: password
    Datatype: String (64)
    Mandatory?: mandatory
    Description: The merchant’s password to the IPG Gateway provided at on-boarding
  - name: action
    Datatype: String (enum)
    Mandatory?: mandatory
    Description: Must be “TOKENIZE”
  - name: timestamp
    Datatype: Integer (13)
    Mandatory?: mandatory
    Description: milliseconds since 1970-01-01 00:00:00
  - name: allowOriginUrl
    Datatype: String (253)
    Mandatory?: mandatory
    Description: The merchant's URL that will make the Tokenize Request Cross-Origin Resource Sharing (CORS) headers will allow only this origin.
  - name: customerId
    Datatype: String (20)
    Mandatory?: optional
    Description: Customer identifier in merchant system. If the parameter is omitted or no value is provided, the IPG Gateway will generate a value, which will be returned in the Session Token Response - Processed (see section 1.2). The received or generated value is stored against the card token.
  - name: cardDescription
    Datatype: String (50)
    Mandatory?: optional
    Description: Free form text field for the merchant’s use that is used for reconciliation e.g. merchant’s internal card’s sequence id


left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/token?"> {
      Customer ID:hptest, Brand ID:897774000/, channel:ECOM, currency:GBP, country:GB, merchantId:897774, action:PURCHASE, amount:5, password:u16q9rZ02bW0jqTjxH8t, allowOriginUrl:*, timestamp:timestamp, paymentSolutionId:500, merchantNotificationUrl:https://ptsv2.com/t/v4w7q-1558948751/post, merchantLandingPageUrl:https://ptsv2.com/t/v4w7q-1558948751/post, forceSecurePayment:false, language:en, postCode (CIP):123456
      };
    title: jQuery
    language: javascript
right_code_blocks:
  - code_block: |2-
      {
          "result": "success",
          "resultId": "f52cc38a-7815-4f8c-8687-662cc63d56e9",
          "merchantId": "890490",
          "additionalDetails": {},
          "processingTime": 1000,
          "token": "96b7d82e-349f-4880-9b8a-928636437c75"
      }
    title: Response
    language: json
  - code_block: |2-
      {
          "result": "failure",
          "resultId": "bb248d1d-d657-4dbe-9f04-a279b384872c",
          "additionalDetails": {},
          "errors": [
            {
               "messageCode": "This field is required in [REQUEST]",
               "fieldName": "password"
            }
          ],
          "processingTime": 2
      }
    title: Error
    language: json
---