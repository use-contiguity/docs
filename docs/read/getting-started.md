# Quick Start 🏃

We know you want to integrate a communications solution quickly into your hamster-sitting app or other billion dollar idea. These quick start guides quickly explain how to add Contiguity into your app, whether you're using JavaScript, Python, or just the API.

> Don't want to mess around with registration / installation? Use **[Contiguity Playground](https://playground.contiguity.co)** and learn how to use Contiguity from the comfort of your own browser.


## Prerequisites 📚

- a Contiguity account
- an internet connection

?> Don't have a Contiguity account? Sign up **[here](https://contiguity.co/onboard)**

## Installing an SDK 🏗
Contiguity is working on adding several SDKs over the coming months, including ones for Swift, Java, Dart, and more.

<!-- tabs:start -->
#### **JavaScript**
Use `npm` to install `@contiguity/javascript`

```
$ npm i @contiguity/javascript
```

#### **Python**
Use `pip` to install `contiguity`
```
$ pip install contiguity
```
<!-- tabs:end -->

## Setup 🛠

After installation, import Contiguity into your project and give it your token.
<!-- tabs:start -->
#### **JavaScript**
```js
const contiguity = require('@contiguity/javascript')
const client = contiguity.login("your token here")
```

You can also initialize it with the optional 'debug' flag:

```js
const client = contiguity.login("your token here", true)
```

#### **Python**
```python
import contiguity
client = contiguity.login("your_token_here")
```

You can also initialize it with the optional 'debug' flag:

```python
client = contiguity.login("your_token_here", True)
```

#### **HTTP API**
When using the API, attach an `X-API-KEY` header that's equal to `Token YOUR_TOKEN_HERE` in each request. 

!> Authentication is required for most endpoints Contiguity provides.
<!-- tabs:end -->

## Sending an email 📨
As long as you provided Contiguity a valid token, and provide valid inputs, sending emails will be a breeze. Various email parameters can be configured in the [Dashboard](https://contiguity.co/dashboard/emails) such as tracking, where emails come from, and more.

<!-- tabs:start -->

#### **JavaScript**
```js
// HTML email
const object = {
    to: "example@example.com",
    from: "Contiguity",
    subject: "My first email!",
    html: "<b>I sent an email using Contiguity</b>"
}

await client.send.email(object)
```

or, to send a plain text email... 
```js
// Plain text email
const object = {
    to: "example@example.com",
    from: "Contiguity",
    subject: "My first email!",
    text: "I sent an email using Contiguity"
}

await client.send.email(object)
```

Optionally, use `replyTo` and `cc`.

#### **Python**
```python
# HTML email
email_object = {
    "to": "example@example.com",
    "from": "Contiguity",
    "subject": "My first email!",
    "html": "<b>I sent an email using Contiguity</b>"
}

client.send.email(email_object)
```

or, to send a plain text email... 

```py
# Plain text email
email_object = {
    "to": "example@example.com",
    "from": "Contiguity",
    "subject": "My first email!",
    "text": "I sent an email using Contiguity"
}

client.send.email(email_object)
```

#### **HTTP API**
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
<!-- tabs:end -->

## Sending a text 💬

As long as you provided Contiguity a valid token, and provide valid inputs, sending texts will be a breeze. Various text parameters can be configured in the [Dashboard](https://contiguity.co/dashboard/texts) such as selecting what number a message comes from, if Contiguity sends messages from the nearest area code, and more.

?> Note: Contiguity expects the recipient phone number to be formatted in E.164. You can attempt to pass numbers in formats like NANP, and the SDKs will try their best to convert it. The API will also attempt to do so. If conversion fails, it will throw an error!

<!-- tabs:start -->
#### **JavaScript**
```js
const object = {
    to: "+15555555555",
    message: "My first text using Contiguity"
}

await client.send.text(object)
```

#### **Python**
```python
text_object = {
    "to": "+15555555555",
    "message": "My first text using Contiguity"
}

client.send.text(text_object)
```

#### **HTTP API**
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
<!-- tabs:end -->

## Sending an OTP 🔑
Contiguity aims to make communications extremely simple and elegant. In doing so, we're providing an OTP API to send one time codes - for free (no additional charge, the text message is still billed / added to quota)

?> Contiguity supports 33 languages for OTPs, including `English (en)`, `Afrikaans (af)`, `Arabic (ar)`, `Catalan (ca)`, `Chinese / Mandarin (zh)`, `Cantonese (zh-hk)`, `Croatian (hr)`, `Czech (cs)`, `Danish (da)`, `Dutch (nl)`, `Finnish (fi)`, `French (fr)`, `German (de)`, `Greek (el)`, `Hebrew (he)`, `Hindi (hi)`, `Hungarian (hu)`, `Indonesian (id)`, `Italian (it)`, `Japanese (ja)`, `Korean (ko)`, `Malay (ms)`, `Norwegian (nb)`, `Polish (pl)`, `Portuguese - Brazil (pt-br)`, `Portuguese (pt)`, `Romanian (ro)`, `Russian (ru)`, `Spanish (es)`, `Swedish (sv)`, `Tagalog (tl)`, `Thai (th)`, `Turkish (tr)`, and `Vietnamese (vi)`

!> OTPs expire after 15 minutes. Upon successful OTP verification, the otp_id is invalidated
<!-- tabs:start -->

#### **JavaScript**
```js
const otp_id = await client.otp.send({ 
    to: "+15555555555", 
    language: "en", 
    name: "Contiguity" 
})
```

?> _The `name` parameter is optional, it customizes the message to say "Your \[name] code is ..."_

#### **Python**
```python
otp_id = client.otp.send({ 
    'to': "+15555555555", 
    'language': "en", 
    'name': "Contiguity" 
})
```

?> _The `name` parameter is optional, it customizes the message to say "Your \[name] code is ..."_

#### **HTTP API**
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

?> _The `name` parameter is optional, it customizes the message to say "Your \[name] code is ..."_
<!-- tabs:end -->

## Verifying an OTP 🔎
<!-- tabs:start --> 

#### **JavaScript**
```js
const verify = await client.otp.verify({
    otp_id: otp_id // you received this when you called client.otp.send(),
    otp: input // the 6 digits your user inputted.
})
```

#### **Python**
```python
verify = client.otp.verify({
    'otp_id': otp_id # you received this when you called client.otp.send(),
    'otp': input # the 6 digits your user inputted.
})
```

#### **HTTP API**
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
<!-- tabs:end -->


## Resending an OTP ↪️
<!-- tabs:start -->

#### **JavaScript**
```js
const resend = await client.otp.resend({
    otp_id: otp_id // you received this when you called client.otp.send(),
})
```

#### **Python**
```python
resend = client.otp.resend({
    'otp_id': otp_id # you received this when you called client.otp.send(),
})
```

#### **HTTP API**
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
<!-- tabs:end -->