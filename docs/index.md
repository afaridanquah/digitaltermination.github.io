# Overview
Digital Termination API allows you to send and receive funds accross africa through simple RESTful APIs.

* Programmatically send and receive high volume of transactions anywhere in the world.
* Build apps that scale with the web technologies that you are already using.
* Send SMS with low latency and high delivery rates.
* Receive SMS for free using SMS-enabled local numbers in countries around the world.
* Only pay for what you use, nothing more.


# Requirements
* PHP 5.5.0
* To use the PHP stream handler, allow_url_fopen must be enabled in your system's php.ini.
* To use the cURL handler, you must have a recent version of cURL >= 7.19.4 compiled with OpenSSL and zlib.

# Client Libraries
We maintain a set of officially support client libraries which make integrating and using the Zeepay APIs significantly easier.
Code examples for any of these client libraries can be seen by selecting your language of choice from the top right of the window.

## Authentication
All authentication is handled through OAuth2 authentication.

To connect to our system kindly send an email to the team via [something@myzeepay.com](something@myzeepay.com).
Someone from the team will set you up.

## Errors
The API uses standard HTTP response codes to indicate success, failure and everything inbetween. The various codes we return are outlined on the right side.

All errors should be returned in the form of JSON along with a message which explains the issue in plain english. When a validation error occurs return the name of the field which is invalid one by one, so if you forgot to include two fields, only the name of the first field will be returned.

### HTTP Status Codes

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The Zeepay requested is hidden for administrators only.
404 | Not Found -- The specified Zeepay could not be found.
405 | Method Not Allowed -- You tried to access a Zeepay with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The Zeepay requested has been removed from our servers.
429 | Too Many Requests -- You're requesting too many Zeepay Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.


## Methods

### Auth
OAuth access tokens also permit client-side API requests. All request sent must contain the access_token.
Below is a guide on how to get the access token.

Endpoint: [test.digitaltermination.com/oauth/token](https://test.shop.digitaltermination.com/oauth/token)
```curl
# Curl
curl -X POST \
  http://test.digital.test/oauth/token \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'Postman-Token: 6773dea8-fb4c-4794-8427-432b769ecd76' \
  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \
  -F grant_type=password \
  -F client_secret=your secret  \
  -F client_id= your client id \
  -F username=bee@gmail.com \
  -F password=your password
```
### Validate Mobile Wallet


### Payout

* METHOD: POST

Params | Data Type | Options | Description
---------- | ------- | -------- | ----------
sender_first_name | String | Required | First Name of Sender
sender_last_name | String | Required | Last Namae of Sender
sender_country | String | Required | Sender Country
receiver_first_name | String | Required | Receipient First Name
receiver_last_name | String | Required | Receipient First Name
receiver_msisdn | String | Required | Receipient Mobile Number Account
receiver_country | String | Required | Receipient Country
amount | Decimal | Required | Amount To Pay
address | String | Required | Address of Receipient
receiver_currency | String | Required | Receipient Currency
mno | String | Optional | Mobile Number Operator (MTN,TIGO,AIRTEL,VODAFONE,ZEEPAY)
transaction_type | String | Optional | (CR (For Credit))
extr_id | String | Required | Your Unique Reference
service_type | String | Required | Wallet,Pickup

* Sample Codes

Endpoint: [test.digitaltermination.com/api/payout](https://test.shop.digitaltermination.com/api/payout)
```curl
# CURL
curl -X POST \
  https://test.digitaltermination.com/api/payouts \
  -H 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOjIsImlzcyI6Imh0dHBzOi8vc2hvcC5kaWdpdGFsdGVybWluYXRpb24uY29tL2FwaS9hdXRoIiwiaWF0IjoxNTIyNDQ1NzMwLCJleHAiOjE1MjI0NDkzMzAsIm5iZiI6MTUyMjQ0NTczMCwianRpIjoiSlZ3N0VxRmVnWlFhUm90MCJ9.WHfOIqmfdvJ01kn3Hl9oIsh974XGv40SpV-lAO4XtOM' \
  -H 'Cache-Control: no-cache' \
  -H 'Postman-Token: 398e8abb-6d48-4389-a124-0a5a54818eed' \
  -H 'content-type: multipart/form-data; boundary=----WebKitFormBoundary7MA4YWxkTrZu0gW' \
  -F sender_first_name=Test \
  -F sender_last_name=Name \
  -F sender_country=UK \
  -F receiver_first_name=Kofi \
  -F receiver_msisdn=233541859113 \
  -F receiver_country=GH \
  -F amount=1.00 \
  -F 'address=Box 2662' \
  -F receiver_currency=GHS \
  -F mno=MTN \
  -F receiver_last_name=Stephen \
  -F transaction_type=CR \
  -F extr_id=11111111129994 \
  -F service_type=Wallet
```
