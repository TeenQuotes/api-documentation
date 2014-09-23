# Users Resources

    DELETE users

## Description
Delete the logged in user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users

## Parameters
None

Example request:

    curl -X DELETE --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/users

## Return format
A JSON object containing keys `status` and `success`.

## Errors
No known error.

## Example
**Request**

    DELETE https://api.teen-quotes.com/v1/users

### Success
``` json
{
  "status":"user_deleted",
  "success":"The user has been deleted."
}
```