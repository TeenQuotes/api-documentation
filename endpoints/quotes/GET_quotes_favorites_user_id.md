# Quotes Resources

    GET quotes/favorites/:user_id

## Description
Returns information about favorites quotes for a given user ID.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/quotes/favorites/42

## Parameters
###URL parameters

- **user_id** - The ID of the user.

### Optional parameters
The following parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of quotes per page. If not specified, the default value is 5.

Example request:

    GET https://api.teen-quotes.com/v1/quotes/favorites/42?page=2&pagesize=5

## Return format
A JSON object containing keys **quotes** where **quotes** is a list of Quote object in **full format** with their author in **small format**.

Quote object:

- **id** - ID of the quote.
- **content** - Body of the quote
- **user_id** - ID of the author of the quote.
- **approved** - Tells the state of the quote. Since we are showing published quotes, approved will always be `1`.
- **created_at** - Date telling when the quote was submitted.
- **has_comments** - Tells if a quote has comments.
- **total_comments** - The number of comments for the quote.
- **is_favorite** - Tells if the quote is in the favorite quotes of the user.
- **total_favorites** - The number of times this quote was added to favorites.

User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment is added on one of its quotes.
- **is_admin** - True if the user is an administrator.

Additional keys:

- **total_quotes** - The total number of published quotes.
- **total_pages** - The total number of pages with the given pagesize.
- **page** - The number of the current page.
- **pagesize** - The number of quotes to display per page.
- **url** - URL of the current page.
- **has_next_page** - True if we can hit a next page of quotes.
- **next_page** - Displayed if `has_next_page` is true. The URL to hit if we want the next page of quotes.
- **has_previous_page** - True if we can hit a previous page of quotes.
- **previous_page** - Displayed if `has_previous_page` is true. The URL to hit if we want the previous page of quotes.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **400 Bad request** — When we can't find the user.
- **404 Not Found** — No quotes have been found for this page and this pagesize.

### `error` messages
- If `status` is `user_not_found`: `The user #:id was not found.`
- If `status` is `404: `No quotes have been found.`

## Example
**Request**

    GET https://api.teen-quotes.com/v1/quotes/favorites/42?page=1&pagesize=2

### Success
**Return**
``` json
{
   "quotes":[
      {
         "id":152,
         "content":"Molestiae eius aut molestiae distinctio aut aut. Nihil consequuntur omnis dolores autem adipisci vel recusandae id. Quisquam veritatis similique cum ea aut.",
         "user_id":38,
         "approved":1,
         "created_at":"2012-04-30 17:28:54",
         "has_comments":true,
         "total_comments":1,
         "is_favorite":false,
         "total_favorites":10,
         "user":{
            "id":38,
            "login":"tgdia37",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":192,
         "content":"Accusantium autem autem voluptatibus. Perferendis itaque unde aperiam et. Voluptatem debitis ea nulla vero.",
         "user_id":23,
         "approved":1,
         "created_at":"2012-06-09 17:28:54",
         "has_comments":true,
         "total_comments":3,
         "is_favorite":false,
         "total_favorites":10,
         "user":{
            "id":23,
            "login":"eyart44",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "total_quotes":21,
   "total_pages":11,
   "page":1,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/quotes\/favorites\/70",
   "has_next_page":true,
   "next_page":"https:\/\/api.teen-quotes.com\/v1\/quotes\/favorites\/70?page=2&pagesize=2",
   "has_previous_page":false
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"No quotes have been found."
}
```