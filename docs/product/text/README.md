# Text
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
<!-- tabs:end -->
