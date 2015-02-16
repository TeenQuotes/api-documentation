# Stories Resources

    GET stories

## Description
Returns information about stories for a given page and a given pagesize.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: Bearer access_token

An example call with CURL:

     curl --header "Authorization: Bearer ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/stories

## Parameters
All parameters are optional. If you don't provide these parameters the default values will be used:

- **page** - The page number starting from **1** to +infinity. If not specified, the default value is 1.
- **pagesize** - The number of stories per page. If not specified, the default value is 5.

Example request:

    GET https://api.teen-quotes.com/v1/stories?page=2&pagesize=10

## Return format
A JSON object containing keys **stories** where **stories** is a list of Story object in **full format** with their author in **small format**.

Story object:

- **id** - ID of the story.
- **represent_txt** - Tells how the user uses Teen Quotes and why it is useful for him
- **frequence_txt** - Tells how often the user uses Teen Quotes and in which context
- **user_id** - ID of the author of the story.
- **created_at** - Date telling when the story was submitted.
- **updated_at** - Date telling when the story was edited.


User object:

- **id** - ID of the user.
- **login** - Login of the user.
- **profile_hidden** - Tells if the profile of the user should be hidden.
- **url_avatar** - Full URL of the user's avatar.
- **wants_notification_comment_quote** - Tells if the user wants to be notified when a comment is added on one of its quotes.
- **is_admin** - True if the user is an administrator.

Additional keys:

- **total_stories** - The total number of stories.
- **total_pages** - The total number of pages with the given pagesize.
- **page** - The number of the current page.
- **pagesize** - The number of stories to display per page.
- **url** - URL of the current page.
- **has_next_page** - True if we can hit a next page of stories.
- **next_page** - Displayed if `has_next_page` is true. The URL to hit if we want the next page of stories.
- **has_previous_page** - True if we can hit a previous page of stories.
- **previous_page** - Displayed if `has_previous_page` is true. The URL to hit if we want the previous page of stories.

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — No stories have been found for this page and this pagesize.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/stories?page=2&pagesize=2

### Success
**Return**
``` json
{
   "stories":[
      {
         "id":7,
         "represent_txt":"Explicabo et odit officiis eligendi aut. Praesentium est pariatur assumenda explicabo et ipsum sequi. Est natus veritatis numquam ab eaque doloribus. Quidem quia sit et fugit nam provident odit. Perspiciatis magnam deleniti hic neque. Perferendis dolor et molestiae. Quibusdam commodi sint mollitia.",
         "frequence_txt":"Ad ea ut culpa accusantium corporis assumenda provident. Libero officia enim eum. Impedit sit aut hic voluptates. Omnis qui quisquam consequatur at deleniti qui.",
         "user_id":12,
         "created_at":"2014-03-21 01:23:42",
         "updated_at":"2014-06-19 06:10:52",
         "user":{
            "id":12,
            "login":"kjqcp23",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      },
      {
         "id":1,
         "represent_txt":"Consectetur rerum recusandae atque aut. Dolorem esse consequatur officia. Voluptas deserunt repellat facilis exercitationem qui. Ullam eaque saepe enim rem. Numquam eos eos explicabo harum rerum. Laboriosam et et aut debitis. Dolorum mollitia et dicta velit repellat corrupti quis.",
         "frequence_txt":"Est quam omnis consequuntur earum enim. Accusamus accusantium placeat sit qui et voluptatem. Nihil ullam occaecati aut. Nemo dolores minima laudantium ex. Nam expedita quis quisquam ea fugiat eaque veritatis. Molestiae dignissimos in eos eveniet qui sed.",
         "user_id":38,
         "created_at":"2014-01-17 22:25:33",
         "updated_at":"2014-06-19 06:10:52",
         "user":{
            "id":38,
            "login":"onqil34",
            "profile_hidden":false,
            "url_avatar":"http:\/\/placekitten.com\/400\/400",
            "wants_notification_comment_quote":false,
            "is_admin":false
         }
      }
   ],
   "total_stories":10,
   "total_pages":5,
   "page":2,
   "pagesize":2,
   "url":"https:\/\/api.teen-quotes.com\/v1\/stories",
   "has_next_page":true,
   "next_page":"https:\/\/api.teen-quotes.com\/v1\/stories?page=3&pagesize=2",
   "has_previous_page":true,
   "previous_page":"https:\/\/api.teen-quotes.com\/v1\/stories?page=1&pagesize=2"
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"No stories have been found."
}
```