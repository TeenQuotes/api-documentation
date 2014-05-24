# FavoriteQuotes Resources

    DELETE favorites/:id

## Description
Remove a quote from the user's favorites.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl -X DELETE --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" 'https://api.teen-quotes.com/v1/favorites/750'

## Return format
A JSON object containing keys `status` and `success` with an HTTP code 200.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad request** — When the **status** is `quote_not_found`.

### `error` messages
The `error` messages are the following:

- If `status` is `quote_not_found`: The quote #:id was not found

## Example
**Request**

    DELETE https://api.teen-quotes.com/v1/favorites/750

### Success
**Return**
``` json
{
   "status":"favorite_deleted",
   "success":"The quote #750 was deleted from favorites"
}
```
### Error
For an error with HTTP code 400:
``` json
{
   "status":"quote_not_found",
   "error":"The quote #750 was not found"
}
```