# Using the API 💻

## Prerequisites
The Contiguity API accepts **both** JSON and form-encoded data. Make sure you set a 'Content-Type' header ! 

Know the endpoint meanings:
* `/user/` deals with anything user related. (e.g) verifiying your token is still active, getting your quota, etc.

* `/verify/` handles any verification requests, like verifying phone numbers and emails. Eventually, this will incorporate into Contiguity Identity Services to identify and prevent fraud.

* `/send/` is practically the point of Contiguity, where your options include `/text`, `/email`, and eventually `/call` (send an automated call to a number, speak via TTS)

* `/otp/` is where Contiguity's managed OTP solution resides. Includes `/otp/new`, `/otp/resend`, and `/otp/verify`

## Sending texts
#### Endpoint

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

## Sending emails
#### Endpoint

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

## OTPs
### Create New OTP
#### Endpoint

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

#### Notes
- OTPs expire after 15 minutes.
- Upon successful OTP verification, the otp_id is invalidated
  
---------------

### Verify OTP
#### Endpoint

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

-------------
### Resend OTP
#### Endpoint

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
