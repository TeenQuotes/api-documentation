# FavoriteQuotes Resources

    POST favorites/:id

## Description
Add a quote in the user's favorites.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" --data "" https://api.teen-quotes.com/v1/favorites/42

## Return format
A JSON object containing keys of the new FavoriteQuote object in the following format:

- **id** - The ID of the new FavoriteQuote
- **quote_id** - The ID of the Quote added to the user's favorites
- **user_id** - The ID of the user currently adding the quote
- **created_at** - Describes the date when the resource was created
- **updated_at** - Describes the date when the resource was created

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad request** — When the **status** key has got one of the following values: `quote_not_found`, `quote_already_favorited`.

### `error` messages
The `error` messages are the following:

- If `status` is `quote_not_found`: The quote #:id was not found
- If `status` is `quote_already_favorited`: The quote #:id was already favorited

## Example
**Request**

    POST https://api.teen-quotes.com/v1/favorites/750

### Success
**Return**
``` json
{
   "user_id":42,
   "quote_id":"750",
   "updated_at":"2014-05-24 14:14:38",
   "created_at":"2014-05-24 14:14:38",
   "id":2005
}
```
### Error
For an error with HTTP code 400:
``` json
{
   "status":"quote_already_favorited",
   "error":"The quote #750 was already favorited"
}
```