# Comments Resources

    DELETE comments/:comment_id

## Description
Delete a comment. **Warning**: the comment must have been posted by the logged in user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl -X DELETE --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/comments/42

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `comment_deleted`
- `success` value: `The comment #:comment_id was deleted.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key is `comment_not_self`.
- **404 Not Found** — When the `status` key is `comment_not_found`

### `error` messages
- If `status` is `comment_not_found`: `The comment #:comment_id was not found.`.
- If `status` is `comment_not_self`: `The comment #:comment_id was not posted by user #:user_id.`.

## Example
**Request**

    DELETE https://api.teen-quotes.com/v1/comments/42

### Success
``` json
{
   "status":"comment_deleted",
   "success":"The comment #42 was deleted."
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":"comment_not_found",
   "error":"The comment #42 was not found."
}
```