# Using Contiguity CLI

## Overview

Contiguity CLI provides a command-line interface to interact with Contiguity's API.

## Installation

?> Using Contiguity CLI requires Node.js to be installed. 

You can install the Contiguity CLI globally using the following command:

```bash
$ npm install -g contiguity-cli
```

## Setup

Before using other commands, set your Contiguity API token using the following command:

```bash
$ contiguity set-token <your_token_here>
```

## Sending a text

To send a text message, use the following command:

```bash
$ contiguity --number "(234) 567-8910" --text "Hello, world!"
```

You can also use shorthands for the options:

```bash
$ contiguity -tn +12345678910 "Hello, world!"
```

### Options

- `-n, --number`: The phone number to send the message to.
- `-t, --text`: Send a text message.

## Sending an email

To send a basic email, use the following command:

```bash
$ contiguity --email "user@example.com" "Hello, world!"
```

### Email Options

- `-e, --email`: Send an email to this address.
- `-s, --subject`: Subject line.
- `-f, --from`: Sender of the email.
- `-H, --html`: Send email as HTML.
- `-r, --reply-to`: Reply-to address.

## OTPs

To send and verify OTPs, use the following command:

```bash
$ contiguity otp "(234) 567-8910"
```

?> Contiguity CLI will provide you with a UI to enter the OTP.

## Poll Quota

To check your account quota, use the following command:

```bash
$ contiguity quota
```

## Additional Options

- `-k, --token`: Your Contiguity token.
- `-m, --mock`: Mock all API requests, token not needed.
- `-d, --debug`: Print debug information.

## Examples

- Set token before using other commands:
  ```bash
  $ contiguity set-token <your_token_here>
  ```
- Verify phone number with OTP:
  ```bash
  $ contiguity otp "(234) 567-8910"
  ```
- Check your account quota:
  ```bash
  $ contiguity quota
  ```
- Set any option with env vars:
  ```bash
  $ CONTIGUITY_NUMBER=2345678910 CONTIGUITY_TEXT=1 contiguity "Hi"
  ```
