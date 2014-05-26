# Users Resources

    PUT users/password

## Description
Update the password of the user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users/password

## Parameters
All parameters are required.

- **password** - The new password of the user. Must be at least 6 characters.
- **password_confirmation** - Must be the same as the `password` field.

Example request:

    curl -X PUT --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "password=azerty&password_confirmation=azerty" https://api.teen-quotes.com/v1/users/password

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `password_updated`
- `success` value: `The new password has been set.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `wrong_password`.

### `error` messages
- If `status` is `wrong_password`: `The password must be at least 6 characters.`, `The password confirmation does not match.`

## Example
**Request**

    PUT https://api.teen-quotes.com/v1/users/password

### Success
With HTTP code 200:
``` json
{
   "status":"password_updated",
   "success":"The new password has been set."
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_password",
   "error":"The password confirmation does not match."
}
```