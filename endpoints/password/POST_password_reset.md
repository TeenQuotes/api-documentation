# Password Resources

    POST password/reset

## Description
Reset a user's password with a reset password token.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

Since we can't have an **access_token** that identifies the user, the application should provide its own **access_token**. To get one, use the [<code>client_credentials</code> method](https://github.com/TeenQuotes/api-documentation/blob/master/authentication/POST_oauth_client_credentials.md).

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/password/reset

## Parameters
All parameters are required.

- **email** - The email address of the user. Must be a valid email address.
- **token** - The reset token previously obtained by [<code>POST</code> password/remind](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/password/POST_password_remind.md).
- **password** - The new password of the user. Must be at least 6 characters.

Example request:

    curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "email=testuser@teen-quotes.com&token=lt5hrb0s5pz2_qcc4wl4k3f00000gp&password=azerty" https://api.teen-quotes.com/v1/password/reset

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `password_reset`
- `success` value: `The new password has been set.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `wrong_user`, `wrong_password`, `wrong_token`.

### `error` messages
- If `status` is `wrong_user`: `The email address doesn't match a user.`
- If `status` is `wrong_token`: `The reset token is invalid.`
- If `status` is `wrong_password`: `The password is wrong.`

## Example
**Request**

    POST https://api.teen-quotes.com/v1/password/reset

### Success
``` json
{
   "status":"password_reset",
   "success":"The new password has been set."
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