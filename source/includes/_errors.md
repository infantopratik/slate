# Errors

We are trying to use conventional HTTP response codes wherever possible to indicate the success or failure of an API request. In general: Codes in the 2xx range indicate success. Codes in the 4xx range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.). Codes in the 5xx range indicate an error with Involvio's servers.

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid, ofter due to missing a required parameter.
401 | Unauthorized -- Your involvio access token is not valid.
404 | Not Found -- The requested resource could not be found.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
