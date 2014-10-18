# Comments Resources

    PUT comments/:comment_id

## Description
Update a comment. **Warning**: the comment must have been posted by the logged in user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl -X PUT --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/comments/42

## Parameters
All parameters are required.

- **content** - The body of the comment. Must be between 10 and 500 characters.

Example request:

    curl -X PUT --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "content=Hello world" https://api.teen-quotes.com/v1/comments/42

## Return format
A JSON object containing keys `status` and `success`.

- `status` value: `comment_updated`
- `success` value: `The comment #:comment_id was updated.`

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key has got one of the following value:`comment_not_self`, `wrong_content`.
- **404 Not Found** — When the `status` key is `comment_not_found`

### `error` messages
- If `status` is `comment_not_found`: `The comment #:comment_id was not found.`.
- If `status` is `comment_not_self`: `The comment #:comment_id was not posted by user #:user_id.`.
- If `status` is `wrong_content`: `The content must be at least 10 characters.`, `The content field is required.`, `The content may not be greater than 500 characters.`.

## Example
**Request**

    PUT https://api.teen-quotes.com/v1/comments/42

### Success
``` json
{
   "status":"comment_updated",
   "success":"The comment #42 was updated."
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