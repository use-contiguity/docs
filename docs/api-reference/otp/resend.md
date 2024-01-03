# Resend OTP
`POST /otp/resend`

#### Parameters

- `otp_id` (string, required): ID of the OTP to be resent.

#### Headers

- `Authorization`: Used for authentication, specify it as `Token YOUR_TOKEN`
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

#### Example request
```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "otp_id": "abc123xyz"
}' \
  https://api.contiguity.co/otp/resend
```

#### Response Format

JSON response includes:

- `message` (string): Result message.
- `resent` (boolean): If it was resent or not.

#### Example Response

```json
{
  "message": "OTP resent successfully."
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Sending failed or internal errors occurred.