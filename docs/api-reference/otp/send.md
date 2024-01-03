# Send OTP
Contiguity aims to make communications extremely simple and elegant. In doing so, we're providing an OTP API to send one time codes - for free (no additional charge, the text message is still billed / added to quota)

?> Contiguity supports 33 languages for OTPs, including `English (en)`, `Afrikaans (af)`, `Arabic (ar)`, `Catalan (ca)`, `Chinese / Mandarin (zh)`, `Cantonese (zh-hk)`, `Croatian (hr)`, `Czech (cs)`, `Danish (da)`, `Dutch (nl)`, `Finnish (fi)`, `French (fr)`, `German (de)`, `Greek (el)`, `Hebrew (he)`, `Hindi (hi)`, `Hungarian (hu)`, `Indonesian (id)`, `Italian (it)`, `Japanese (ja)`, `Korean (ko)`, `Malay (ms)`, `Norwegian (nb)`, `Polish (pl)`, `Portuguese - Brazil (pt-br)`, `Portuguese (pt)`, `Romanian (ro)`, `Russian (ru)`, `Spanish (es)`, `Swedish (sv)`, `Tagalog (tl)`, `Thai (th)`, `Turkish (tr)`, and `Vietnamese (vi)`

!> OTPs expire after 15 minutes. Upon successful OTP verification, the otp_id is invalidated

`POST /otp/new`

#### Parameters

- `to` (string, required): Recipient's phone number.
- `language` (string, required): Language for OTP message (e.g., `en` for English).
- `name` (string): Your app's name (e.g. "Your [name\] token is...") 

#### Headers

- `Authorization`: Used for authentication, specify it as `Token YOUR_TOKEN`
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

#### Example request
```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "+1234567890",
    "language": "en",
    "name": "Contiguity"
}' \
  https://api.contiguity.co/otp/new
```

#### Response Format

JSON response includes:

- `message` (string): Result message.
- `crumbs` (object): Additional request info.
- `otp_id` (string): ID of the generated OTP.

#### Example Response

```json
{
  "message": "OTP sent successfully",
  "crumbs": {
    "plan": "free",
    "quota": 3,
    "type": "sms",
    "ad": true
  },
  "otp_id": "abc123xyz"
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Sending failed or internal errors occurred.

?> _The `name` parameter is optional, it customizes the message to say "Your \[name] code is ..."_