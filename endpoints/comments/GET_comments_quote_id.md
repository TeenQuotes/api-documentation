# Comments Resources

    GET comments/:quote_id

## Description
Returns information about comments posted on a quote for a given page and a given pagesize.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/comments/42

## Parameters
All parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of comments per page. If not specified, the default value is 10.
- **quote** - Adds information about the quote related to the comment for each comments if the value is `true`. Default is `false`.

Example request:

    GET https://api.teen-quotes.com/v1/comments/42?page=2&pagesize=10&quote=true

## Return format
A JSON object containing keys **comments** where **comments** is a list of Comment object in **full format** with their author in **small format**. If the parameter `quote` is specified with the value `true`, the Quote object is in **full format**.

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

- **404 Not Found** — No comments have been found for this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/comments/42?page=2&pagesize=2&quote=true

### Success
**Return**
``` json
{
   "comments":[
      {
         "id":1498,
         "content":"Ratione et numquam quaerat molestiae beatae. Ullam autem fuga aliquid est excepturi eos. Autem iure fugit consequatur. Quae esse sed saepe eligendi a est laboriosam eos. Facere ducimus ipsa aliquam totam praesentium.",
         "quote_id":747,
         "user_id":97,
         "created_at":"2016-01-06 06:10:46",
         "user":{
            "id":97,
            "login":"huhsu25",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         },
         "quote":{
            "id":747,
            "content":"Eaque repellat esse voluptas ratione. Minima quam rerum eius voluptatem quia. Doloremque eos aut quis quae. Dicta fugit odit ut fuga dolor odit dolor. Eius nam sint quo libero.",
            "user_id":58,
            "approved":1,
            "created_at":"2013-12-16 06:10:43",
            "has_comments":true,
            "total_comments":3,
            "is_favorite":false
         }
      },
      {
         "id":1497,
         "content":"Dolorem rerum sint vel dolor molestiae fugiat rerum quia. Enim reiciendis ipsa consectetur est vero. Exercitationem et aut aut voluptate temporibus ut.",
         "quote_id":448,
         "user_id":30,
         "created_at":"2016-01-05 06:10:46",
         "user":{
            "id":30,
            "login":"jqhvp55",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         },
         "quote":{
            "id":448,
            "content":"Inventore dolor vel facere id ducimus pariatur. Sed ipsum consequuntur eos voluptas nesciunt quia.",
            "user_id":71,
            "approved":1,
            "created_at":"2013-02-20 06:10:43",
            "has_comments":true,
            "total_comments":6,
            "is_favorite":false
         }
      }
   ],
   "total_comments":1500,
   "total_pages":750,
   "page":2,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/comments",
   "has_next_page":true,
   "next_page":"https:\/\/api.teen-quotes.com\/v1\/comments?page=3&pagesize=2&quote=true",
   "has_previous_page":true,
   "previous_page":"https:\/\/api.teen-quotes.com\/v1\/comments?page=1&pagesize=2&quote=true"
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