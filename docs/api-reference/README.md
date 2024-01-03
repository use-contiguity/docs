# Contiguity API

## Setup
Use of Contiguity's services requires an account to be made with Contiguity. This, apart from needing a connection to the internet, is all you need to begin using Contiguity.

?> Don't have a Contiguity account? Sign up **[here](https://contiguity.co/onboard)**

!> The Contiguity API accepts **both** JSON and form-encoded data. Make sure you set a `Content-Type` header.

## Base URLs
When sending requests, the base URL for your requests will likely be:
```
https://api.contiguity.co/
```

However, for some data or request, you may encounter base URLs such as:
```
https://orwell.contiguity.co/
```
```
https://dropoff.contiguity.co/
```
```
https://identity.usa.contiguity.co/
```

## Authentication
When using the API, attach an `X-API-KEY` header that's equal to `Token YOUR_TOKEN_HERE` in each request.

!> Authentication is required for most endpoints Contiguity provides.

## API Best Practices

### Avoid "spamming" the API
While Contiguity's API can scale and is meant to handle millions of requests, it still rate limits users beyond a certain amount of requests per second. Avoid, for example, polling `/otp/verify` with every digit your user types - instead wait for all 6 digits before requesting verification.

### Respect local laws
Contiguity was designed to not be required to follow certain 'regulations', i.e A2P 10DLC registration in the US. However, it is still up to you, the user, to follow all laws applicable to you (i.e, in the US, CAN-SPAM) - not Contiguity's.

?> Contiguity will offer Contiguity Compliance, a service meant to take the burden of managing compliance with privacy/communications laws, in late-2024/

### Secure your tokens at all times
It is advisable to never use your account token in production. You can generate throwaway tokens in the [dashboard](https://contiguity.co/dashboard/tokens), that can easily be revoked in the end of misuse by an unauthorized third party.

!> If your account token leaks, your only option to mediate the situation is emailing support@contiguity.co

## Pricing
Contiguity offers the lowest pricing in the industry for any volume of text and email, offering three tiers.

In our free tier, users get (per month):

| Text   	| Email  	| Call  	| Identity 	|
|--------	|--------	|-------	|----------	|
| 1,000 	| 5,000 	| 10 mins	| 5 requests    	|

When paying for usage, Contiguity offers simple and affordable pricing for each product:

| Text   	| Email  	| Call  	| Identity 	|
|--------	|--------	|-------	|----------	|
| $0.005 	| $0.002 	| $0.01 / min 	| $1.00*    	|

When subscribed to Unlimited, you pay a flat fee of $19.99 per month.

| Text   	| Email  	| Call  	| Identity 	|
|--------	|--------	|-------	|----------	|
| Unlimited 	| Unlimited 	| Unlimited 	| Unlimited**  	|

_*Identity has several tiers of requests, from free verifications to high-fidelity fraud detection. Average pricing is $1 per request._

_**Unlimited Identity, when launched, will likely incur an additional fee._

## API Status
Contiguity strives for 99.99% uptime. In the event Contiguity begins to return any `5xx` error, check Contiguity's [status page](https://status.contiguity.co). If an incident hasn't been marked as `Investigating`, notify Contiguity immediately via email (support@contiguity.co) or [Discord](https://discord.gg/pCuTaY84Vy)