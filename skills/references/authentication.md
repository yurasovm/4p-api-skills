# Authentication

The 4Partners API uses token-based authentication via the `X-Auth-Token` header.

## Getting a Token

### Via Email + Password

```http
POST https://api.4partners.io/v1/auth/sign-in
Content-Type: application/json

{
  "email": {
    "email_address": "your@email.com",
    "password": "your-password"
  }
}
```

Response:
```json
{
  "result": {
    "user": {
      "access_token": "ff69d01342da85a3fd80a81868e574c7..."
    }
  }
}
```

### Via Phone (SMS code)

```http
POST https://api.4partners.io/v1/auth/sign-in
Content-Type: application/json

{
  "phone": {
    "country_code": "+7",
    "value": "9111111111"
  }
}
```

Then confirm with the received code:

```http
POST https://api.4partners.io/v1/auth/confirm
Content-Type: application/json

{
  "confirmation_id": "phone:123456789",
  "confirmation_code": "1234"
}
```

## Using the Token

Add the token to every request as a header:

```http
X-Auth-Token: your-access-token-here
```

## Environment Variable

Store the token in environment variable `FOURPARTNERS_AUTH_TOKEN` and read it at runtime. Never hardcode tokens in source code.

## Token Masking (Display)

When showing the token to users, mask it:
- Show first 6 + last 4 characters: `ff69d0...74c7`
- Never show the full token
