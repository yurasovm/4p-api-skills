# Base URLs

## Production

```
https://api.4partners.io/v1
```

All skill endpoints are relative to this base URL.

## OpenAPI Specification

Full machine-readable API spec:

```
https://api.4partners.io/v1/doc/index.json
```

## Rate Limits

| Resource | Limit |
|---|---|
| Rubric | 600 requests/minute |
| Brand | 600 requests/minute |
| Rubric Brand | 600 requests/minute |
| Info | 600 requests/minute |
| Source Store | 600 requests/minute |
| Ai | 600 requests/minute |
| Article | Standard limits apply |

When rate limit is exceeded, the API returns `429 Too Many Requests` with reset time in the response body.

## Site Variations

Many endpoints require a `{variation}` parameter. Use `"default"` for the main locale. Other variations (e.g., `en`, `ru`, `de`) correspond to site locale codes.

To list all available variations for a site:

```http
GET /article/site-variations-library
X-Auth-Token: your-token
```
