# Users Resources

    PUT users/settings

## Description
Update the settings of the user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users/settings

## Parameters
All parameters are required.

- **notification_comment_quote** - Boolean value. `true` is the user wants to receive a notification when a comment is posted on one of its quotes. `false` otherwise.
- **hide_profile** - Boolean value. `true` if the user wants to have a private profile. Only him will be able to see it. `false` otherwise.
- **weekly_newsletter** - Boolean value. `true` if the user wants to receive the weekly newsletter. `false` otherwise.
- **daily_newsletter** - Boolean value. `true` if the user wants to receive the daily newsletter. `false` otherwise.
- **colors** - The colors that will be used to display the quotes published by the user. Current possible values: `red`, `blue`, `purple`, `orange`, `green`. The default value is `blue`.

Example request:

    curl -X PUT --data "notification_comment_quote=true&hide_profile=true&weekly_newsletter=false&daily_newsletter=false&colors=blue" --header "Authorization: Bearer Skyr72P77dw0s2T0eulz7VgDmfntgLWkx7cN13DH" https://api.teen-quotes.com/v1/users/settings

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `profile_updated`
- `success` value: `The profile has been updated.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `wrong_color`.

### `error` messages
- If `status` is `wrong_color`: `This color is not allowed.`.

## Example
**Request**

    PUT https://api.teen-quotes.com/v1/users/settings

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
   "status":"wrong_color",
   "error":"This color is not allowed."
}
```