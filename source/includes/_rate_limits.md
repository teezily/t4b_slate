# Rate limits

> Once throttled the API will return the following JSON:

```json
{
  "errors": [
    {
      "code": "RateLimitError",
      "title": "Too Many Requests",
      "detail": "Your requests exceeded the rate of 60 by period of 60 seconds."
    }
  ]
}
```

The API enforces rate limits on the amount of requests that can be made. a 429 HTTP status code will be returned if throttled. Currently available rate is returned in response headers.

Time period | Call limit |
----------- | ---------- |
1 minute | 60 calls

### Response header

`X-Tzy-Limit: 60`
