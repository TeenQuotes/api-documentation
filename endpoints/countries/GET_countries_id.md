# Countries Resources

    GET countries/:id

## Description
Returns detailed information of a country.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/countries/42

## Return format
A JSON object describing a Country object.

- **id** - The ID of the country.
- **name** - The English name of the country.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — Country with the specified ID does not exist when the `status` key is `country_not_found`.

### `error` messages
- When `status` is `country_not_found`: `The country #:id was not found.`

## Example
**Request**

    GET https://api.teen-quotes.com/v1/countries/42

### Success
**Return**
``` json
{
   "id":42,
   "name":"Chad"
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":"country_not_found",
   "error":"The country #42 was not found."
}
```