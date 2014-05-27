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

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — Quote with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/quotes/683

### Success
**Return**
``` json
[
   {
      "id":"683",
      "content":"Rerum vero in iusto saepe dolor sit ipsa. Eius ut sapiente quod. Aut nobis atque perferendis maiores quos odit.",
      "user_id":"17",
      "approved":"1",
      "created_at":"2013-10-13 12:54:27",
      "has_comments":true,
      "total_comments":1,
      "is_favorite":true,
      "comments":[
         {
            "id":"487",
            "content":"Architecto voluptas officiis alias dicta et. Nihil libero eveniet sint qui quia. Vitae quas dicta consequatur qui et provident et. Non ut fugiat occaecati quia. Illum tenetur consequatur eum dolorem.",
            "quote_id":"683",
            "user_id":"10",
            "created_at":"2013-03-31 17:40:07",
            "user":{
               "id":"10",
               "login":"urijh94",
               "profile_hidden":false,
               "url_avatar":"http:\/\/placekitten.com\/400\/400",
               "wants_notification_comment_quote":false,
               "is_admin":false
            }
         }
      ],
      "user":{
         "id":"17",
         "login":"qzymi52",
         "profile_hidden":false,
         "url_avatar":"http:\/\/placekitten.com\/400\/400",
         "wants_notification_comment_quote":false,
         "is_admin":false
      }
   }
]
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":"quote_not_found",
   "error":"The quote #683 was not found"
}
```