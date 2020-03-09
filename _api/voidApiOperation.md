---
title: VOID API Operation
position_number: 9
type: post
description: VOID API Operation

parameters:
  - name: result
    Datatype: String(40)
    Description: Will always be “success” if processed and "failure" if error
  - name: merchantId
    Datatype: Integer(18)
    Description: The merchantId value sent in the Session Token Request 
  - name: action
    Datatype: String (enum)
    Mandatory?: mandatory
    Description: Will always be “VOID”
  - name: originalMerchantTxId
    Datatype: String (50)
    Description: The merchant transaction identifier of the transaction that was refunded
  - name: originalTxId
    Datatype: Integer (18)
    Description: The IPG Gateway transaction Id of the transaction refunded sent in the Session Token Request (section 1.1)
  - name: amount
    Datatype: BigDecimal (15.2 or 15.3)
    Description: The transaction amount refunded sent in the Session Token Request (section 1.1)
  - name: currency
    Datatype: String (enum)
    Description: The transaction ISO alpha-3 currency code, as defined in the ISO 4217 standard, used in the original and refund transactions
  - name: customerId
    Datatype: String (20)
    Description: The IPG Gateway customer identifier used in the original and refund transactions
  - name: pan
    Datatype: String (100)
    Description: The customer account value/number used in the original and the refund transactions.  For payment card transactions this is the IPG Gateway Card Token.
  - name: brandId
    Datatype: Integer(18)
    Description: The brandId value for the original and the refund transaction
  - name: paymentSolutionId
    Datatype: Integer(18)
    Description: The paymentSolutionId value used in the original and refund transactions
  - name: Status
    Datatype: String(enum)
    Description: The status of the transaction in IPG Gateway -
#Status	Condition
#VOID	If “VOID” successful
#ERROR	If an error was returned by the payment process
  - name: errors
    Datatype: String(400)
    Description: Any errors that occurred during the successful processing of a transaction
  - name: resultId
    Datatype: String(40)
    Description: Hexadecimal string that is to be used in any support request calls
  - name: processingTime
    Datatype: Integer (18)
    Description: The time in seconds for the process to complete
  - name: additionalDetails
    Datatype: Array
    Description: Not used – will always be “{}” or not included

    left_code_blocks:
  - code_block: |-
      $ .post("https://apiuat.test.boipapaymentgateway.com/token?"> {
          merchantId=1111111&token=fghij67890fghij67890
      };
    title: jQuery
    language: javascript
right_code_blocks:
  - code_block: |2-
      {
        “result”:”success”,
        "resultId": "4fd9f223-bb1a-4879-a6e6-81a10b53bdca",
        "merchantId":111111,
        "originalMerchantTxId":"abc123",
        "originalTxId":123,
        "amount":12.50,
        "currency":"GBP",
        "customerId":"mgn456",
        "action":"VOID",
        "pan":"45ae201ghy23498FjMj701",
        "brandId":3,
        "paymentSolutionId":500,
        ”status”:”VOID”,
        "additionalDetails": {},
        "processingTime": 948


      }
    title: Response
    language: json
  - code_block: |2-
      {
        "result": "failure",
        "resultId": "308802f2-224d-44f5-b256-8d9443a72770",
        "additionalDetails": {},
        "errors": [
        { "messageCode": "This field is required in [TOKEN]", "fieldName": "amount" }
        ],
        "processingTime": 173


      }
    title: Error
    language: json
---