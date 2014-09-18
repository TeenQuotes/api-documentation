# Quotes Resources

    POST quotes

## Description
Submit a new quote.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" https://api.teen-quotes.com/v1/quotes

## Parameters
All parameters are required.

- **content** - The content of the quote. The content should be between 50 and 300 characters.

Example request:

    curl --header "Authorization: jLJeOz8aEIsKtGSdXsqTDGxmtEduUGkZTVJBo3We" --data "content=Hello this is an amazing quote it should be displayed" https://api.teen-quotes.com/v1/quotes

## Return format
A JSON object containing the Quote object that has just been created.

Quote object:

- **id** - ID of the quote.
- **content** - Body of the quote
- **user_id** - ID of the author of the quote.
- **created_at** - Date telling when the quote was submitted.
- **has_comments** - Tells if a quote has comments.
- **total_comments** - The number of comments for the quote.
- **is_favorite** - Tells if the quote in the favorite quotes of the user.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad Request** — When the `status` key has got one of the following values: `too_much_submitted_quotes`, `wrong_content`.

### `error` messages
- If `status` is `too_much_submitted_quotes`: `The maximum number of quotes you can submit is 5 per day`
- If `status` is `wrong_content`: `Content of the quote should be between 50 and 300 characters`

## Example
**Request**

    POST https://api.teen-quotes.com/v1/quotes

### Success
With an HTTP code 201.
``` json
{
   "content":"Hello this is an amazing quote it should be displayed",
   "user_id":42,
   "created_at":"2014-05-23 17:29:41",
   "id":751,
   "has_comments":false,
   "total_comments":0,
   "is_favorite":false
}
```

### Error
For an error with HTTP code 400:
``` json
{
   "status":"wrong_content",
   "error":"Content of the quote should be between 50 and 300 characters"
}
```