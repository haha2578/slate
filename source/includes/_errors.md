# Errors

The Codia API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
402 | PaymentRequired -- Your credit is insufficient.
403 | Forbidden -- The api requested is hidden for administrators only.
404 | Not Found -- The specified api could not be found.
405 | Method Not Allowed -- You tried to access an api with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
429 | Too Many Requests -- You're requesting too many images! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
