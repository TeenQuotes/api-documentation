# Comments Resources

    GET comments/users/:user_id

## Description
Returns information about comments posted by a user for a given page and pagesize.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/comments/users/42

## Parameters
All parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of comments per page. If not specified, the default value is 10.

Example request:

    GET https://api.teen-quotes.com/v1/comments/users/42?page=2&pagesize=10

## Return format
A JSON object containing keys **comments** where **comments** is a list of Comment object in **full format** with their author in **small format**. The Quote object associated with each comment is in **full format**.

Comment object:

- **id** - ID of the comment.
- **content** - The body of the comment.
- **quote_id** - ID of the quote related to the comment.
- **user_id** - ID of the author of the comment.
- **created_at** - Date telling when the comment was submitted.

User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment is added on one of its quotes.
- **is_admin** - True if the user is an administrator.

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


Additional keys:

- **total_comments** - The total number of comments.
- **total_pages** - The total number of pages with the given pagesize.
- **page** - The number of the current page.
- **pagesize** - The number of comments to display per page.
- **url** - URL of the current page.
- **has_next_page** - True if we can hit a next page of comments.
- **next_page** - Displayed if `has_next_page` is true. The URL to hit if we want the next page of comments.
- **has_previous_page** - True if we can hit a previous page of comments.
- **previous_page** - Displayed if `has_previous_page` is true. The URL to hit if we want the previous page of comments.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — When the `status` key has got one of the following values: `404`, `user_not_found`.

### `error` messages
- If `status` is `404`: `No comments have been found.`.
- If `status` is `user_not_found`: `The user #:user_id was not found.`.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/comments/users/42?page=2&pagesize=2&quote=true

### Success
**Return**
``` json
{
   "comments":[
      {
         "id":726,
         "content":"Qui praesentium facilis deserunt molestiae cum amet qui. At possimus sint culpa rerum. A blanditiis nemo beatae vel.",
         "quote_id":476,
         "user_id":42,
         "created_at":"2014-02-16 02:37:25",
         "user":{
            "id":42,
            "login":"antoineaugusti",
            "profile_hidden":false,
            "url_avatar":"https:\/\/api.teen-quotes.com\/uploads\/avatar\/42.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         },
         "quote":{
            "id":476,
            "content":"Veniam doloribus velit soluta iure nisi. Placeat adipisci voluptatem ab similique. Facere nihil reiciendis sed et sit omnis.",
            "user_id":71,
            "approved":1,
            "created_at":"2013-03-20 15:05:55",
            "has_comments":true,
            "total_comments":2,
            "is_favorite":false,
            "total_favorites":10
         }
      },
      {
         "id":1500,
         "content":"Id pariatur eum repellendus vel. Tempore aut exercitationem dolorem quia consectetur. Fugit voluptatum totam voluptatem.",
         "quote_id":165,
         "user_id":42,
         "created_at":"2013-12-26 18:28:15",
         "user":{
            "id":42,
            "login":"antoineaugusti",
            "profile_hidden":false,
            "url_avatar":"https:\/\/api.teen-quotes.com\/uploads\/avatar\/42.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         },
         "quote":{
            "id":165,
            "content":"Labore rerum sit perspiciatis et. Natus amet amet id veritatis ut qui reiciendis. Quibusdam iure corrupti ratione perspiciatis alias quaerat et.",
            "user_id":66,
            "approved":1,
            "created_at":"2012-05-13 15:05:55",
            "has_comments":true,
            "total_comments":2,
            "is_favorite":false,
            "total_favorites":10
         }
      }
   ],
   "total_comments":17,
   "total_pages":9,
   "page":2,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/comments\/users\/42",
   "has_next_page":true,
   "next_page":"https:\/\/api.teen-quotes.com\/v1\/comments\/users\/42?page=3&pagesize=2",
   "has_previous_page":true,
   "previous_page":"https:\/\/api.teen-quotes.com\/v1\/comments\/users\/42?page=1&pagesize=2"
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"No comments have been found."
}
```