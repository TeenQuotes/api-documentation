# Quotes Resources

    GET quotes

## Description
Returns information about quotes for a given page and a given pagesize.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

## Parameters
All parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of quotes per page. If not specified, the default value is 10.

Example request:

    GET https://api.teen-quotes.com/v1/quotes?page=2&pagesize=10

## Return format
A JSON object containing keys **quotes** where **quotes** is a list of Quote object in **full format** with their author is **small author**.

Quote object:

- **id** - ID of the quote.
- **content** - Body of the quote
- **user_id** - ID of the author of the quote.
- **approved** - Tells the state of the quote. Since we are showing published quotes, approved will always be `one`.
- **created_at** - Date telling when the quote was submitted.
- **has_comments** - Tells if a quote has comments.
- **total_comments** - The number of comments for the quote.
- **is_favorite** - Tells if the quote in the favorite quotes of the user.


User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment on one of its quotes.
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

- **404 Not Found** — No quotes have been found for this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/quotes?page=2&pagesize=2

**Return**
``` json
{
   "quotes":[
      {
         "id":"748",
         "content":"Eos sed voluptas facilis doloribus labore. Officiis debitis distinctio qui saepe non. Error officia adipisci facilis suscipit nisi. Aut nulla quo nesciunt consequatur sit non.",
         "user_id":"8",
         "approved":"1",
         "created_at":"2013-12-17 12:54:27",
         "has_comments":true,
         "total_comments":2,
         "is_favorite":false,
         "user":{
            "id":"8",
            "login":"xsdpd49",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":"747",
         "content":"Ut aut ut vitae sunt ea sed. Similique asperiores culpa minima perferendis.",
         "user_id":"80",
         "approved":"1",
         "created_at":"2013-12-16 12:54:27",
         "has_comments":true,
         "total_comments":2,
         "is_favorite":false,
         "user":{
            "id":"80",
            "login":"ohgsg37",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "total_quotes":601,
   "total_pages":301,
   "page":2,
   "pagesize":2,
   "url":"http:\/\/localhost:8000\/v1\/quotes",
   "has_next_page":true,
   "next_page":"http:\/\/localhost:8000\/v1\/quotes?page=3&pagesize=2",
   "has_previous_page":true,
   "previous_page":"http:\/\/localhost:8000\/v1\/quotes?page=1&pagesize=2"
}
```

For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"No quotes have been found."
}
```