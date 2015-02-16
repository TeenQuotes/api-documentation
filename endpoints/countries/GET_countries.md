# Countries Resources

    GET countries

## Description
Returns detailed information of a country.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/countries

## Return format
A JSON object describing a list of Country objects.

- **id** - The ID of the country.
- **name** - The English name of the country.
- **country_code** - The [ISO 3166-1 alpha-2](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/countries

### Success
**Return**
``` json
[
   {
      "id":1,
      "name":"Afghanistan",
      "country_code": "AF"
   },
   {
      "id":2,
      "name":"Albania",
      "country_code": "AL"
   },
   {
      "id":3,
      "name":"Algeria",
      "country_code": "DZ"
   }
]
```