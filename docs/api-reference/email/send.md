# Send email
As long as you provided Contiguity a valid token, and provide valid inputs, sending emails will be a breeze. Various email parameters can be configured in the [Dashboard](https://contiguity.co/dashboard/emails) such as tracking, where emails come from, and more.

`POST /send/email`

#### Parameters

- `to` (string, required): Recipient's email address.
- `from` (string, required): Sender's name.
- `subject` (string, required): Email subject.
- `body` (string, required): Email content.
- `contentType` (string, required): Content type (either `html` or `text`).
- `cc` (string): CC email address (only 1 is supported as of now).
- `replyTo` (string): Reply-to email address.

#### Headers

- `Authorization`: Used for authentication, specify it as `Token YOUR_TOKEN`
- `Content-Type`: `application/json` or `application/x-www-form-urlencoded`

#### Example request
```bash
curl -X POST \
  -H "Authorization: Token YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "to": "recipient@example.com",
    "from": "sender@example.com",
    "subject": "Test Email",
    "body": "Hello, this is a test email.",
    "contentType": "text"
}' \
  https://api.contiguity.co/send/email

```

#### Response Format

JSON response includes:

- `message` (string): Result message.
- `crumbs` (object): Additional request info.
- `email_id` (string): Email ID, used for delivery tracking and analytics.

#### Example Response

```json
{
  "message": "Successfully sent",
  "crumbs": {
    "plan": "payg",
    "quota": 12,
    "type": "email",
    "ad": false
  }
}
```

#### Error Responses

- `400 Bad Request`: Missing parameters.
- `401 Unauthorized`: Invalid or suspended token.
- `500 Internal Server Error`: Sending failed or internal errors occurred.