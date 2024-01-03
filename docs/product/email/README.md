# Email
?> Don't want to mess around with registration / installation? Use **[Contiguity Playground](https://playground.contiguity.co)** and learn how to use Contiguity from the comfort of your own browser.

## Installing an SDK
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

## Setup

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
<!-- tabs:end -->

## Send
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

Optionally, use `replyTo` and `cc`.
<!-- tabs:end -->
