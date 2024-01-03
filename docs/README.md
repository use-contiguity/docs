# Contiguity Documentation
Contiguity is a communications service designed from the ground up to be the best for all developers - from hobbyists to Fortune 500.

## Prerequisites
Use of Contiguity's services requires an account to be made with Contiguity.

?> Don't have a Contiguity account? Sign up **[here](https://contiguity.co/onboard)**

## Best Practices

### Avoid "spamming" the API
While Contiguity's API can scale and is meant to handle millions of requests, it still rate limits users beyond a certain amount of requests per second. Avoid, for example, running `client.otp.verify({})` with every digit your user types - instead wait for all 6 digits before requesting verification.

### Respect local laws
Contiguity was designed to not be required to follow certain 'regulations', i.e A2P 10DLC registration in the US. However, it is still up to you, the user, to follow all laws applicable to you (i.e, in the US, CAN-SPAM) - not Contiguity's.

?> Contiguity will offer Contiguity Compliance, a service meant to take the burden of managing compliance with privacy/communications laws, in late-2024.

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


<!--
## Table of Contents
Our documentation provides a variety of information regarding our SDKs, API, services, and more. 

- [Getting Started](/read/getting-started.md)
- [Contiguity CLI](/read/cli.md)
- [JavaScript SDK](/read/js.md)
- [Python SDK](/read/py.md)
- [API Reference](/read/api.md)
- [Playground](/read/playground.md)

<div class="cc-container">
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            Text
        </a>
    </div>
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            Email
        </a>
    </div>
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            Call
        </a>
    </div>
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            Identity
        </a>
    </div>
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            Enterprise Uses
        </a>
    </div>
    <div class="cc-product">
        <a class="cc-product-bar" href="https://docs.contiguity.co/#/read/getting-started">
            All documentation
        </a>
    </div>
</div>

## More about Contiguity... 
Contiguity offers core services, which are:

- SMS
- Email
- Call (coming soon)
- Identity Verification (coming soon)

and Contiguity offers extensions of those services, where you are only billed for the product you use (e.g OTPs only bill you per text)

- Text OTPs
- Email OTPs (coming soon)
- Contiguity Form (coming soon)
- Contiguity Compliance (coming soon)
- etc.

In our free tier, users get (per month):

| Text   	| Email  	| Call  	| Identity 	|
|--------	|--------	|-------	|----------	|
| 1,000 	| 5,000 	| 100 mins	| 50 verifications    	|

When paying for usage, Contiguity offers a flat-rate model for every service, which is **$0.005** per text, email, minute, verification, etc. 

Eventually, pricing will change to:

| Text   	| Email  	| Call  	| Identity 	|
|--------	|--------	|-------	|----------	|
| $0.005 	| $0.002 	| $0.01 	| $1.00    	|

As of August 2023, pricing changes are set to take effect later in November.

-->