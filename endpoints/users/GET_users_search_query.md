# Users Resources

    GET users/search/:query

## Description
Search users with a query based on their username. Returns only not hidden profiles.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/users/search/lorem

## Parameters
###URL parameters

- **query** - The search query.

### Optional parameters
The following parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of quotes per page. If not specified, the default value is 10.

Example request:

    GET https://api.teen-quotes.com/v1/users/search/antoine?page=2&pagesize=5

## Return format
A JSON object containing keys **users** and where **users** is a list of User object in **medium format**. For each users we also have a **country_object**.

**User** object:

- **id** - ID of the quote.
- **login** - Username of the user.
- **email** - Email address of the user.
- **birthdate** - The  birth date of the user. Format: YYYY-MM-DD
- **gender** - Gender of the user. Possible values: `M`,`F`
- **country** - ID of the country of the user.
- **city** - City of the user.
- **about_me** - User' self description.
- **last_visit** - Last visit time of the user. Example: 2013-12-14 17:11:53
- **created_at** - Tells when the user created its account. Example: 2013-12-14 17:11:53
- **profile_hidden** - Tells if the user has got a hidden profile or not. Boolean value.
- **url_avatar** - Full URL of the avatar of the user.
- **wants_notification_comment_quote** - Tells if the user want to receive a notification when a comment is added on one of its published quotes. Boolean value.
- **is_admin** - Tells if a user is an administrator. Boolean value.

The **country_object** has got the following format:

- **id** - ID of the country.
- **name** - English name of the country.
- **country_code** - The [ISO 3166-1 alpha-2](http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) country code.

Additional keys:

- **total_users** - The total number of published users.
- **total_pages** - The total number of pages with the given pagesize.
- **page** - The number of the current page.
- **pagesize** - The number of users to display per page.
- **url** - URL of the current page.
- **has_next_page** - True if we can hit a next page of users.
- **next_page** - Displayed if `has_next_page` is true. The URL to hit if we want the next page of users.
- **has_previous_page** - True if we can hit a previous page of users.
- **previous_page** - Displayed if `has_previous_page` is true. The URL to hit if we want the previous page of users.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — No users have been found for this query, this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/users/search/antoine?page=1&pagesize=2

### Success
**Return**
``` json
{
   "users":[
      {
         "id":42,
         "login":"antoineaugusti",
         "email":"antoine.augusti@gmail.com",
         "birthdate":"2013-11-05",
         "gender":"M",
         "country":209,
         "city":"North Verlafort",
         "about_me":"Et veritatis id dolorem ex. Ut voluptatum in quia at aspernatur est vitae. Accusamus aliquid laudantium et aliquid error debitis vitae quod.",
         "last_visit":"2014-02-21 06:18:00",
         "created_at":"2014-06-03 07:00:28",
         "profile_hidden":false,
         "url_avatar":"http:\/\/teen-quotes.com\/uploads\/avatar\/42.png",
         "wants_notification_comment_quote":true,
         "is_admin":true,
         "country_object":{
            "id":209,
            "name":"Thailand",
            "country_code": "TH"
         }
      }
   ],
   "total_users":1,
   "total_pages":1,
   "page":1,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/users\/search\/antoine",
   "has_next_page":false,
   "has_previous_page":false
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"No users have been found."
}
```