# Errors

The Scriptdrop Delivery API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- Request not authorized.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a route that's not allowed.
406 | Not Acceptable -- You requested a format that isn't supported.
429 | Too Many Requests -- You've hit your request limit. Retry in a few moments.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.

