# Password Resources

    POST password/remind

## Description
Send a reset password token to the user by e-mail when its password is lost. The reset token is available during 24 hours.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

Since we can't have an **access_token** that identifies the user, the application should provide its own **access_token**. To get one, use the [<code>client_credentials</code> method](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_client_credentials.md).

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/password/remind

## Parameters
All parameters are required.

- **email** - The email address of the user. Must be a valid email address.

Example request:

    curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "email=testuser@teen-quotes.com" https://api.teen-quotes.com/v1/password/remind

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `reminder_sent`
- `success` value: `An email was sent to the user.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `wrong_user`.

### `error` messages
- If `status` is `wrong_user`: `The email address doesn't match a user.`

## Example
**Request**

    POST https://api.teen-quotes.com/v1/password/remind

### Success
``` json
{
   "status":"reminder_sent",
   "success":"An email was sent to the user."
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_user",
   "error":"The email address doesn't match a user."
}
```