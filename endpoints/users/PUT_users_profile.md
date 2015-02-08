# Users Resources

    PUT users/profile

## Description
Update the profile of the user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users/profile

## Parameters
All parameters are optional.

- **gender** - The user's gender. `M` for male, `F` for female.
- **birthdate** - The birthdate of the user. Format: Y-m-d. Example: `1975-01-25`.
- **country** - The ID of a country. See [<code>GET</code> countries](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/countries/GET_countries.md).
- **city** - The user's city.
- **about_me** - The user's description. Must not be greater than 500 characters.
- **avatar** - The user's avatar. Available extensions: (`jpeg`, `png`, `bmp`, or `gif`). Must not be greater than 500 kb.

Example request:

    curl -i -X PUT --data "gender=M&city=Paris&country=17&birthdate=1975-01-01" --header "Authorization: Bearer Skyr72P77dw0s2T0eulz7VgDmfntgLWkx7cN13DH" https://api.teen-quotes.com/v1/users/profile

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `profile_updated`
- `success` value: `The profile has been updated.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `wrong_gender`, `wrong_birthdate`, `wrong_country`, `wrong_avatar`, `wrong_about_me`.

### `error` messages
- If `status` is `wrong_gender`: `The selected gender is invalid.`.
- If `status` is `wrong_birthdate`: `The birthdate does not match the format Y-m-d.`.
- If `status` is `wrong_country`: `The selected country was not found.`.
- If `status` is `wrong_avatar`: `The avatar must be an image.`, `The avatar may not be greater than 500 kilobytes.`.
- If `status` is `wrong_about_me`: `The about me may not be greater than 500 characters.`.

## Example
**Request**

    PUT https://api.teen-quotes.com/v1/users/profile

### Success
With HTTP code 200:
``` json
{
   "status":"profile_updated",
   "success":"The profile has been updated."
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_birthdate",
   "error":"The birthdate does not match the format Y-m-d."
}
```