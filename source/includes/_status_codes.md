# Status codes

The Teezily Plus API uses the following HTTP status codes:

HTTP Status Code | Meaning
---------------- | -------
200 | Ok
204 | Ok -- No content
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The following ressource requested is forbidden.
404 | Not Found -- The specified ressource could not be found.
405 | Method Not Allowed -- You tried to access a ressource with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The ressource requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many ressources! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
