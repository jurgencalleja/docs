---
title: Void
position_number: 8
type: post
description: 1	Session Token API Operation


parameters:
  - name: merchantId
    Datatype: Integer(18)
    Mandatory?: mandatory
    Description: The identifier for the merchant in the IPG Gateway provided at on-boarding. 
  - name: password
    Datatype: String (64)
    Mandatory?: mandatory
    Description: The merchant’s password in the IPG Gatewayprovided at on-boarding
  - name: action
    Datatype: String(enum)
    Mandatory?: mandatory
    Description: Must be “VOID"
  - name: timestamp
    Datatype: Integer (18)
    Mandatory?: mandatory
    Description: Miliseconds since 1970-01-01 00:00:00
  - name: allowOriginUrl
    Datatype: String (253)
    Mandatory?: mandatory
    Description: The merchant's URLthat will make the Auth/Purchase/VerifyRequest(see Section Auth/Purchase/Verify Request) Cross-Origin Resource Sharing (CORS)headers will allow only this origin
  - name: originalTxId
    Datatype: Integer (18)
    Mandatory?: optional
    Description: The IPG Gateway transaction Id of the transaction to be voided. This will have been returned in the txId field of the Auth/Purchase Response – Processed (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)
  - name: originalMerchantTxId
    Datatype: String (50)
    Mandatory?: mandatory
    Description: The merchant’s original transaction identifier of the transaction to be voided, that was provided in the merchantTxId field of the Auth/Purchase Session Token Request and Auth/Purchase Request (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)
  - name: agentId
    Datatype: String (18)
    Mandatory?: optional
    Description: Identifier of the merchant’s operator or agent on behalf of the end customer, if the operation is not performed by the merchant, and the merchant wants to track the operator who performed the transaction Note - this is not the same as the operatorId or userAgent fields of the Auth/Purchase Session Token Request and Auth/Purchase/Verify Request (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)

left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/payment?"> {
        merchantId=1111111&password=klw74U6yt40mNo&originalTxld=1234&originalMerchantTxId=12345&allowOriginUrl=www.merchantsite.com
      };
    title: jQuery
    language: javascript
  
right_code_blocks:
  - code_block: |2-
      {
        "result": "success",
        "resultId": "85034083-22dd-49ff-9906-495098c42501",
        "merchantId": "167738",
        "additionalDetails": {},
        "processingTime": 33,
        "token": "72102985-5a92-4cde-a51b-9459d37d97a9"

        }
    title: Response
    language: json
  - code_block: |2-
      {
        "result": "failure",
        "resultId": "99392fc1-bcd9-4fb0-8838-7dc37256cb51",
        "additionalDetails": {},
        "errors": [
        { "messageCode": "This field is required in [REQUEST]", "fieldName": "password" }
        ],
        "processingTime": 4

      }
    title: Error
    language: json
---
---