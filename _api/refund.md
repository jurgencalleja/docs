---
title: Refund Session token request
position_number: 6
type: post
description: The purpose of this document is to describe the REFUND API Operation to enable merchant developers to integrate their webpages with the IPG Gateway.  Refer to the IPG Gateway – 0 – Overview document for how this API Operation is used in the merchant processes. The IPG Gateway caters for full or partial refunds. More than one refund can be performed on a single transaction.  However, the refund amounts cannot exceed the original transaction amount. Refunds can only be performed on transactions with the status of CAPTURED.

parameters:
  - name: merchantId
    Datatype: Integer(18)
    Mandatory?: mandatory
    Description: The identifier for the merchant in the IPG Gateway provided at on-boarding.  This must be the same used in the related session token request.
  - name: password
    Datatype: String (64)
    Mandatory?: mandatory
    Description: The merchant’s password in the IPG Gatewayprovided at on-boarding
  - name: action
    Datatype: String(enum)
    Mandatory?: mandatory
    Description: Must be “REFUND”
  - name: timestamp
    Datatype: Integer (18)
    Mandatory?: mandatory
    Description: Milliseconds since 1970-01-01 00:00:00
  - name: allowOriginUrl
    Datatype: String (253)
    Mandatory?: mandatory
    Description: The merchant's URLthat will make the Auth/Purchase/VerifyRequest(see Section Auth/Purchase/Verify Request) Cross-Origin Resource Sharing (CORS)headers will allow only this origin
  - name: originalTxId
    Datatype: Integer (18)
    Mandatory?: optional
    Description: The IPG Gateway transaction Id of the transaction to be refunded. This will have been returned in the txId field of the Auth/Purchase Response – Processed (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)
  - name: originalMerchantTxId
    Datatype: String (50)
    Mandatory?: mandatory
    Description: The merchant’s original transaction identifier of the transaction to be refunded, that was provided in the merchantTxId field of the Auth/Purchase Session Token Request and Auth/Purchase Request (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)
  - name: agentId
    Datatype: String (18)
    Mandatory?: optional
    Description: Identifier of the merchant’s operator or agent on behalf of the end customer, if the operation is not performed by the merchant, and the merchant wants to track the operator who performed the transaction. Note - this is not the same as the operatorId or userAgent fields of the Auth/Purchase Session Token Request and Auth/Purchase/Verify Request (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)
  - name: amount
    Datatype: BigDecimal (10.2 or 10.3) BigDecimal (15.2 or 15.3
    Mandatory?: mandatory
    Description: The amount to refund. Can be less than or equal to the original transaction amount. Cannot be more than the original transaction amount
  - name: partialRefundComment
    Datatype: String (500)
    Mandatory?: optional
    Description: Free text field that allows a comments to be attached to the transaction record in the IPG Gateway

left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/payment?"> {
      action=REFUND&merchantId=167738&password=WcuQNsptvvd2ftu5MMhU&originalMerchantTxId=84Yf5iO28qFr3og8rWTo&amount=20&timestamp=1555494136820&allowOriginUrl=http://localhost:8083&originalTxId=11622150
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
        "cardToken": "5512732598811111",
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
        "errors": 
        [
          {
          "messageCode": "This field is required in [REQUEST]", "fieldName": "password" 
          }
        ],
      "processingTime": 4
      }
    title: Error
    language: json
---


---
