# Authentication

All requests to Pact API must be authenticated.

## API V1

There are two options for autentication:

Pact expects for the API key to be included in all API requests to the server in a header that looks like the following:

`X-Private-Api-Token: YOUR_API_TOKEN`

or as a additional parameter in URI

`"API_ENDPOINT_HERE?private_api_token=YOUR_API_TOKEN"`

<aside class="notice">
You must replace <code>YOUR_API_TOKEN</code> with your personal API key.
</aside>

<aside class="warning">
You must use personal API key on each request to the API.
</aside>

You can get your Pact API key from [account settings page](https://app.pact.im/account).


### Examples

```shell
# Header
curl -X GET "API_ENDPOINT_HERE"
  -H "X-Private-Api-Token: YOUR_API_TOKEN"

# OR use a private_api_token parameter
curl -X GET "API_ENDPOINT_HERE?private_api_token=YOUR_API_TOKEN"
```

```php
<?php
$token = '<your super secret token>';
$pact = new \Pact\PactClient($token);
```

## API V2

Pact expects for an authentication token to be included in all API requests to the server in a header that looks like the following:

`X-Api-Token: YOUR_AUTHENTICATION_TOKEN`

Here are steps to receive your Authentication Token

1. Set `webhook_url` in your user settings at `https://msg.pact.im/account`
2. To receive security code on your `webhook_url` send request`POST https://api.pact.im/api/verification?locale=ru&source=private_api_v2&phone=YOUR_PHONE`
3. Send request `POST https://api.pact.im/api/sign_in?phone=YOUR_PHONE&code=SECURITY_CODE` to receive your pair of tokens: Authentication Token in Authentication-Token header and Refresh Token in Refresh-Token header (lifespan is 1 hour / 30 days respectivly). Refresh Token is one use only.

To receive new pair of tokens send `POST https://api.pact.im/api/refresh_token` which includes header `X-Api-Refresh-Token: Refresh Token`

### Examples

```shell
# Header
curl -X GET "API_ENDPOINT_HERE"
  -H "X-Api-Token: YOUR_AUTHENTICATION_TOKEN"
```
