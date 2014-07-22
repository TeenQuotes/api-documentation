# Search Resources

    GET search/:query

## Description
Search published quotes and users with a query of words. Users are displayed only if their profile is not hidden.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/search/lorem

## Parameters
### URL parameters

- **query** - The search query.

### Optional parameters
The following parameters are optional. If you don't provide these parameters the default values will be used:

- **pagesize** - The number of results per page. If not specified, the default value is 10.

Example request:

    GET https://api.teen-quotes.com/v1/search/autem?pagesize=5

## Return format
A JSON object containing keys **quotes** and **users**. **quotes** is a list of Quote object in **full format** with their author in **small format**. **users** is a list of User object in **medium format**. For each users we also have a **country_object**.

To get info about the User objects: [go here](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/users/GET_users_search_query.md#return-format).

To get info about the Quote objects: [go here](https://github.com/TeenQuotes/api-documentation/blob/master/endpoints/quotes/GET_quotes_search_query.md#return-format).

Additional keys:

- **total_quotes** - The total number of published quotes for this query.
- **total_users** - The total number of users for this query.
- **pagesize** - The number of objects to display.
- **url** - URL of the current page.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — No results have been found for this query, this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/search/sed?pagesize=2

### Success
**Return**
``` json
{
   "quotes":[
      {
         "id":653,
         "content":"Consequatur autem odit sed eius nostrum. Ut voluptatem sed voluptatum quisquam laborum nesciunt. Modi cumque neque sed id ea architecto. Quis dolor impedit autem doloribus. Maiores sed voluptatem dolorem voluptatem sunt sit.",
         "user_id":26,
         "approved":1,
         "created_at":"2013-09-13 07:00:38",
         "rank":1.4223313331604,
         "has_comments":true,
         "total_comments":3,
         "is_favorite":false,
         "user":{
            "id":26,
            "login":"evskw67",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":237,
         "content":"Officiis ducimus sed et ut reiciendis quidem. Voluptatibus sed labore vitae voluptatem ipsa. Aut delectus adipisci doloribus dolores suscipit est blanditiis. Sed veritatis impedit suscipit aspernatur eius. Velit praesentium deleniti expedita ex velit qui nam.",
         "user_id":58,
         "approved":1,
         "created_at":"2012-07-24 07:00:38",
         "rank":1.0667484998703,
         "has_comments":true,
         "total_comments":3,
         "is_favorite":false,
         "user":{
            "id":58,
            "login":"csgbm76",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "users":[
      {
         "id":42,
         "login":"sedami",
         "email":"sedami@gmail.com",
         "birthdate":"1983-02-15",
         "gender":"M",
         "country":"232",
         "city":"North Brian",
         "about_me":"Cupiditate facilis quod excepturi deleniti molestias natus voluptas. Nesciunt voluptas molestiae molestias aperiam placeat et. Ipsa dolores dolore fugiat sequi molestiae suscipit atque.",
         "last_visit":"2014-05-29 07:55:40",
         "created_at":"2014-05-29 07:09:34",
         "profile_hidden":false,
         "url_avatar":"http:\/\/teen-quotes.com\/uploads\/avatar\/42.jpg",
         "wants_notification_comment_quote":true,
         "is_admin":true,
         "country_object":{
            "id":232,
            "name":"Virgin Islands, U.S. Virgin Islands"
         }
      }
   ],
   "total_quotes":154,
   "total_users":1,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/search\/sed"
}
```