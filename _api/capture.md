---
title: Capture
position_number: 10
type: post
description: Capture operation

#Document Purpose
#The purpose of this document is to describe the CAPTURE API Operation to enable merchant developers to integrate their webpages with the IPG Gateway.  Refer to the IPG Gateway – 0 – Overview document for how this API Operation is used in the merchant processes.
#A CAPTURE API Operation is required after an AUTH Request, not a PURCHASE Request.
#Transaction Status
#All transactions that can be captured have the status SET_FOR_CAPTURE, which means the payment is authorised, through the AUTH/PURCHASE/VERIFY – API Operation (see IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Direct API or IPG Gateway – 2 – AUTH-PURCHASE-VERIFY – Hosted Payment Page, as appropriate to the integration method)).
#The successful CAPTURE API Operation will set the transaction status to CAPTURED.
#A CAPTURE API Operation can be unsuccessful for two reasons
#•	The transaction status is set to ERROR if there was an error in the API Operation
#o	usually the result of a communication error between the customer browser and the IPG Gateway
#•	The transaction status is set to DECLINED if
#o	the card payment was refused by the acquirer, or
#o	the 3DS authentication failed
#A failure response is sent.
#Funds Transfer
#The transfer of funds from the customers’ accounts to the merchant account is not instantaneous.
#The IPG Gateway CAPTURE API Operation flags transactions for batch processing later in the day, according to the acquirers’ requirements. This batch process informs the acquirer that the funds should be transferred.
#The actual transfer of funds is performed by the acquirer.
#This delay allows for the VOID API Operation (see IPG Gateway – 4 - VOID) to be performed before the CAPTURE API Operation.
#Only the full authorised amount of the transaction can be captured, based on the amount authorised in the AUTH API operation.  Partial captures are currently not supported.
#Full or Partial Captures
#The IPG Gateway caters for full or partial captures.  If the full amount is not captured the residual amount is released to the cardholder.  Multiple partial captures are not currently catered for.

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
    Description: Must be “CAPTURE"
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
  - name: amount
    Datatype: BigDecimal (10.2 or 10.3) BigDecimal (15.2 or 15.3)
    Mandatory?: mandatory
    Description: The amount to capture. Can be less than or equal to the original transaction amount. Cannot be more than the original transaction amount
  - name: result
    Datatype: String (40)
    Description: Will always be “success” or "failure"
  - name: merchantId
    Datatype: Integer (18)
    Description: The merchantId value received in the Session Token Request (section 1.1)
  - name: token
    Datatype: String (40)
    Description: The Session Token that is a one-time use, hexadecimal string. The Session Token that must only be used for the Capture Request (see Section 2.1). Session tokens are valid for 3600 second (1 hour) after which they expire. Any requests with expired session tokens will be rejected
  - name: resultId
    Datatype: String (40)
    Description: Hexadecimal string that is to be used in any support request calls
  - name: processingTime
    Datatype: Integer (6)
    Description: The time in seconds for the process to complete
  - name: additionalDetails
    Datatype: Array
    Description: Not used – will always be “{}” or not included
  - name: errors
    Datatype: String Array
    Description: List of issues


    left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/token?"> {
          merchantId=1111111&password=klw74U6yt40mNo&originalTxId=123456789&originalMerchantTxId=XYZ123456789ABC&allowOriginUrl=www.merchantsite.com&action=CAPTURE&timestamp=1249751864238&agentId=brian01&amount=120
      };
    title: jQuery
    language: javascript
right_code_blocks:
  - code_block: |2-
      {
        "result":"success",
        "merchantId":1111111,
        "token":"abcde12345abcde12345",
        ”resultId”:”fghij67890fghij67890”,
        “processingTime”: 2



      }
    title: Response
    language: json
  - code_block: |2-
      {
        "result":"failure",
        "merchantId":1111111,
        "errors":[ { "messageCode": "This field is required in [REQUEST]", "fieldName": "password" } ],
        “processingTime”: 4


      }
    title: Error
    language: json
---