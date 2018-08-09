## Singing and API requests illustration

Please go to ExNow official website and visit “API” from the bottom of the home page to manage the apikey. Key means API accessing key, SecretKey is needed as a signature for users when sending request. (only visible when applying for API accessing)

Important: Do not reveal your 'AccessKey' and 'SecretKey' to anyone. They are as important as your password. 

### Components of a Query Request
ExNow requires that each API request formatted for Signature(except for market API), a legal request should contain the following:

api.exnow.com/private/v1 and follow with the method. 
For example:  api.exnow.com/private/v1/balance

AccessKeyId: The 'AccessKey' distributed by ExNow when you applied for APIKEY.

SignatureMethod: The hash-based protocol used to calculate the signature. This should be MD5. 
For example: MD5(Key_uersid_secretKey_time)


Timestamp: The time at which you make the request. Include timestamp in the Query request to help with prevent you if third parties intercepting your request.This is formatted in UTC time..


Required and optional parameters: Each action has a set of required and optional parameters that define the API call.This shows in the API reference.Important Reminder: Every param in a GET method should be included in signature calculation, and only AccessKeyId, SignatureMethod, SignatureVersion, Timestamp should be included in signature calculation for a POST method.

Signature: The calculated value that ensures the signature is valid and is not tampered.

### requests illustration
The access address of the exnow transaction： api.exnow.com/private/v1

The field 'Content-Type' in request header should be 'Content-Type:application/json' for a GET method.
Request parameter: Construct the request parameters according to each API interface.
Submit request: Use POST or GET method to send request to server.
ExNow processes the request and  returns data to users in JSON format after authentication check.
HTTPS is required.
Query asset details method order: query all accounts of the current user -> query the specified account balance
All of the trading pairs in ExNow are supported, new currency listing keep the official website up to date.

