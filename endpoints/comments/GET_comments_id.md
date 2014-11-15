# Comments Resources

    GET comments/:id

## Description
Returns detailed information of a single comment.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/comments/42&quote=true


## Parameters
All parameters are optional. If you don't provide these parameters the default values will be used:

- **quote** - Adds information about the quote related to the comment for each comments if the value is `true`. Default is `false`.

## Return format
A JSON object describing the Comment object. A User object describing the author of the comment is avaible inside the `user` key in **small format**. If the parameter `quote` is specified with the value `true`, the Quote object is in **full format** in the `quote` key.

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

If the parameter `quote` is specified with the value `true`. Quote object:

- **id** - ID of the quote.
- **content** - Body of the quote
- **user_id** - ID of the author of the quote.
- **approved** - Tells the state of the quote. Since we are showing published quotes, approved will always be `1`.
- **created_at** - Date telling when the quote was submitted.
- **has_comments** - Tells if a quote has comments.
- **total_comments** - The number of comments for the quote.
- **is_favorite** - Tells if the quote is in the favorite quotes of the user.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — Comment with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/comments/1500&quote=true

### Success
**Return**
``` json
{
   "id":1500,
   "content":"Officia nihil vero quia molestias. Perspiciatis ex iusto pariatur quasi consequuntur sint assumenda. Numquam placeat est nihil qui doloremque maiores enim.",
   "quote_id":646,
   "user_id":41,
   "created_at":"2016-01-08 06:10:46",
   "user":{
      "id":41,
      "login":"odibs36",
      "profile_hidden":false,
      "url_avatar":"http:\/\/placekitten.com\/400\/400",
      "wants_notification_comment_quote":false,
      "is_admin":false
   },
   "quote":{
      "id":646,
      "content":"Ipsam et numquam sed nulla et omnis optio. Rerum sint est iure neque quisquam sit. Vero ea ratione eveniet saepe nihil sunt.",
      "user_id":24,
      "approved":1,
      "created_at":"2013-09-06 06:10:43",
      "has_comments":true,
      "total_comments":2,
      "is_favorite":false
   }
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":"comment_not_found",
   "error":"The comment #1500 was not found."
}
```