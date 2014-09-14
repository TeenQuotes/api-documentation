# Quotes Resources

    GET quotes/:id

## Description
Returns detailed information of a single quote.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/quotes/42

## Return format
A JSON object containing keys **user** and **comments**, where **user** is a User object in **small format** and comments is a list of **comments** associated with the quote in the following format:

- **id** — ID of the comment.
- **user_id** — The ID of the author of the comment.
- **quote_id** — Is always the ID of the quote.
- **content** — Text of the comment.
- **created_at** - Creation of the comment
- **has_comments** - Tells if the quote has at least 1 comment
- **total_comments** - The number of comments
- **is_favorite** - Tells if the quote is favorited for the current user
- **user** — Profile of the author of the comment in **short format**.

The user of a comment as got the following format:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment on one of its quotes.
- **is_admin** - True if the user is an administrator.

The author of the quote as got the following format:

- **id** - ID of the user
- **login** - username of the user
- **profile_hidden** - does the user has got a public profile or not

Information about users who favorited the quote can be found in the **favorites** key. User who favorited the quote are displayed in **small format**.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — Quote with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/quotes/200

### Success
**Return**
``` json
{
   "id":200,
   "content":"Rerum eaque autem facilis inventore ex repellendus vel voluptas. Perferendis consequatur et quis laudantium. Reprehenderit optio quia non. Saepe maiores ea eum quis.",
   "user_id":3,
   "approved":1,
   "created_at":"2012-06-17 09:45:48",
   "has_comments":true,
   "total_comments":2,
   "is_favorite":false,
   "comments":[
      {
         "id":831,
         "content":"Aliquid at numquam asperiores eaque. Asperiores molestiae impedit quisquam sit facere. Voluptas et sed et aut libero quo debitis.",
         "quote_id":200,
         "user_id":43,
         "created_at":"2014-05-25 23:34:13",
         "user":{
            "id":43,
            "login":"mouzc05",
            "profile_hidden":false,
            "url_avatar":"https:\/\/teen-quotes.com\/assets\/images\/chat.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":1392,
         "content":"Eaque exercitationem enim quia consectetur dolorem culpa. Id vero voluptatibus sunt voluptatem. Nostrum similique molestiae quo. Laboriosam quia maiores distinctio at sint recusandae qui.",
         "quote_id":200,
         "user_id":83,
         "created_at":"2012-12-30 08:02:19",
         "user":{
            "id":83,
            "login":"dfglm47",
            "profile_hidden":false,
            "url_avatar":"https:\/\/teen-quotes.com\/assets\/images\/chat.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "favorites":[
      {
         "id":1680,
         "quote_id":200,
         "user_id":76,
         "created_at":"2014-08-26 09:45:59",
         "updated_at":"2014-08-26 09:45:59",
         "user":{
            "id":76,
            "login":"xhmlo13",
            "profile_hidden":false,
            "url_avatar":"https:\/\/teen-quotes.com\/assets\/images\/chat.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":999,
         "quote_id":200,
         "user_id":78,
         "created_at":"2014-08-26 09:45:58",
         "updated_at":"2014-08-26 09:45:58",
         "user":{
            "id":78,
            "login":"cubua90",
            "profile_hidden":false,
            "url_avatar":"https:\/\/teen-quotes.com\/assets\/images\/chat.png",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "user":{
      "id":3,
      "login":"wgoir72",
      "profile_hidden":false,
      "url_avatar":"https:\/\/teen-quotes.com\/assets\/images\/chat.png",
      "wants_notification_comment_quote":false,
      "is_admin":false
   }
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":"quote_not_found",
   "error":"The quote #683 was not found"
}
```