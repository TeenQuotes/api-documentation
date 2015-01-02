# Quotes Resources

    GET quotes/search/:query

## Description
Search published quotes with a query of words.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/quotes/search/lorem

## Parameters
###URL parameters

- **query** - The search query.

### Optional parameters
The following parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of quotes per page. If not specified, the default value is 10.

Example request:

    GET https://api.teen-quotes.com/v1/quotes/search/autem?page=2&pagesize=5

## Return format
A JSON object containing keys **quotes** where **quotes** is a list of Quote object in **full format** with their author in **small format**.

Quote object:

- **id** - ID of the quote.
- **content** - Body of the quote
- **user_id** - ID of the author of the quote.
- **approved** - Tells the state of the quote. Since we are showing published quotes, approved will always be `1`.
- **created_at** - Date telling when the quote was submitted.
- **rank** - Indicates the score of the quote for the search query. > 0
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

- **404 Not Found** — No quotes have been found for this query, this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/quotes/search/autem?page=1&pagesize=2

### Success
**Return**
``` json
{
   "quotes":[
      {
         "id":366,
         "content":"Autem molestias autem et facere autem. Est est voluptatem ducimus numquam quibusdam illum labore. Beatae dignissimos aut excepturi qui error. Rerum qui voluptatem sint delectus delectus tempore ex. Nesciunt sapiente eligendi dolore eaque quisquam.",
         "user_id":82,
         "approved":1,
         "created_at":"2012-11-30 17:28:54",
         "rank":1.5409713983536,
         "has_comments":true,
         "total_comments":2,
         "is_favorite":false,
         "total_favorites":10,
         "user":{
            "id":82,
            "login":"siqhp80",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":188,
         "content":"Doloribus voluptatibus laudantium fuga autem. Voluptates asperiores et est qui eveniet magnam odit corporis. Assumenda saepe nisi sit autem earum ut necessitatibus. Qui mollitia odio dolores molestiae sed fugit.",
         "user_id":37,
         "approved":1,
         "created_at":"2012-06-05 17:28:54",
         "rank":1.0273143053055,
         "has_comments":true,
         "total_comments":4,
         "is_favorite":false,
         "total_favorites":10,
         "user":{
            "id":37,
            "login":"hlfou07",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "total_quotes":113,
   "total_pages":57,
   "page":1,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/quotes\/search\/autem",
   "has_next_page":true,
   "next_page":"https:\/\/api.teen-quotes.com\/v1\/quotes\/search\/autem?page=2&pagesize=2",
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