# Rate limits

> Once throttles the API will return the following JSON:

```json
{
  "error": {
    "key": "throttled",
    "message": "Request was throttled. Available in 59 seconds."
  }
}
```

The API enforces rate limits on the amount of requests that can be made. a 429 HTTP status code will be returned if throttled. Currently available rate is returned in response headers.

Time period | Call limit |
----------- | ---------- |
1 minute | 60 calls

#### Response header example

`x-tzy-limit: 40`

<!--
  ### HTTP Response
  Slate JS Scroller issue as we miss an H2 (##), we hardcode it in HTML
-->
<h3 id="rate-limits-http-response">HTTP Response</h3>


Parameter | Type | Description |
--------- | ---- | ----------- |
error.key | String |
error.message | String |