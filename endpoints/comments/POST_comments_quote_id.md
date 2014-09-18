# Comments Resources

    POST comments/:quote_id

## Description
Submit a new comment on a quote.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/comments/42

## Parameters
All parameters are required.

- **content** - The body of the comment. Must be between 10 and 500 characters.

Example request:

    curl --data "content=Hello world" --header "Authorization: uv9w4BkB1TlJOxM3OgefXYDOLRkixjiOBpCRIK1Z" https://api.teen-quotes.com/v1/comments/708

## Return format
A JSON object containing the Comment object that has just been created.

Comment object:

- **id** - ID of the comment.
- **content** - The body of the comment.
- **quote_id** - ID of the quote related to the comment.
- **user_id** - ID of the author of the comment.
- **created_at** - Date telling when the comment was submitted.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key has got one of the following values: `wrong_content`, `wrong_quote_id`.

### `error` messages
- If `status` is `wrong_content`: `The content must be at least 10 characters.`, `The content field is required.`, `The content may not be greater than 500 characters.`.
- If `status` is `wrong_quote_id`: `The quote should be published.`, `The selected quote id was not found.`.

## Example
**Request**

    POST https://api.teen-quotes.com/v1/comments/708

### Success
With an HTTP code 201.
``` json
{
   "content":"Hello world",
   "quote_id":708,
   "user_id":42,
   "created_at":"2014-06-20 09:15:36",
   "id":1501
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_quote_id",
   "error":"The quote should be published."
}
```