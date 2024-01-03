# Verify OTP
`POST /otp/verify`

#### Parameters

- `otp_id` (string, required): ID of the OTP.
- `otp` (integer / string, required): OTP to verify.

#### Headers

- `Authorization`: Used for authentication, specify it as `Token YOUR_TOKEN`
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

#### Example request
```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "otp_id": "abc123xyz",
    "otp": "123456"
}' \
  https://api.contiguity.co/otp/verify
```

#### Response Format

JSON response includes:

- `message` (string): Result message.
- `verified` (boolean): Indicates whether the OTP was successfully verified.

#### Example Response

```json
{
  "message": "OTP Verified",
  "verified": true
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Verifying failed or internal errors occurred.