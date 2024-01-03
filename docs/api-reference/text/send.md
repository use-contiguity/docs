# Send text
As long as you provided Contiguity a valid token, and provide valid inputs, sending texts will be a breeze. Various text parameters can be configured in the [Dashboard](https://contiguity.co/dashboard/texts) such as selecting what number a message comes from, if Contiguity sends messages from the nearest area code, and more.

?> Note: Contiguity expects the recipient phone number to be formatted in E.164. You can attempt to pass numbers in formats like NANP, and the SDKs will try their best to convert it. The API will also attempt to do so. If conversion fails, it will throw an error!

`POST /send/text`

#### Parameters

- `to` (string, required): Recipient's phone number.
- `message` (string, required): Content of the message.

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
    "message": "Hello, this is a test text message."
}' \
  https://api.contiguity.co/send/text
```

#### Response Format

JSON response includes:

- `message` (string): Result message.
- `crumbs` (object): Additional request info.
- `Other` (any): Contiguity may provide additional JSON such as `otp_id` (string) 

#### Example Response

```json
{
  "message": "Successfully sent",
  "crumbs": {
    "plan": "payg",
    "quota": 12,
    "type": "sms",
    "ad": false
  }
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Sending failed or internal errors occurred.