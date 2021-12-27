# Rate limits

> Once throttles the API will return the following JSON:

```json
{
  "status": "error",
  "message": "Request was throttled. Available in 59 seconds.",
  "error": {
    "key": "throttled",
    "status_code": 429,
    }
}
```

The API enforces rate limits on the amount of requests that can be made.

Time period | Call limit | 
----------- | ----- | 
1 minute | 60 calls

### HTTP Response

Parameter | Type | Description |
--------- | ---- | ----------- |
status | String |
message | String |
error.key | String |
error.status_code | String |
error.message | String |