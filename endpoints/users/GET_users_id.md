# Users Resources

    GET users/:id

## Description
Returns detailed information of a user.

## Requires authentication
* A valid access token must be provided in **access_token** parameter.

The `access_token` should be sent using an HTTP header like so:

     Authorization: access_token

An example call with CURL:

     curl --header "Authorization: ZllAle9NZ11FkMyX5xm0evswWOTinrr5I26uLcGB" https://api.teen-quotes.com/v1/users/42

## Return format
A JSON object containing keys **country_object** and **newsletters**, where **country_object** is a Country object in **small format** and **newsletters** is a list of Newsletter object nested inside the User object with the following format:

- **user_id** — The ID of the user subscribed to the newsletter.
- **type** — The type of the newsletter. Possible values: daily|weekly
- **created_at** - Indicates when the object was created. Example value: 2014-05-29 07:09:49

**User** object:

- **id** - ID of the quote.
- **login** - Username of the user.
- **email** - Email address of the user.
- **birthdate** - The  birth date of the user. Format: YYYY-MM-DD
- **gender** - Gender of the user. Possible values: `M`,`F`
- **country** - ID of the country of the user.
- **city** - City of the user.
- **about_me** - User' self description.
- **last_visit** - Last visit time of the user. Example: 2013-12-14 17:11:53
- **created_at** - Tells when the user created its account. Example: 2013-12-14 17:11:53
- **profile_hidden** - Tells if the user has got a hidden profile or not. Boolean value.
- **url_avatar** - Full URL of the avatar of the user.
- **wants_notification_comment_quote** - Tells if the user want to receive a notification when a comment is added on one of its published quotes. Boolean value.
- **is_admin** - Tells if a user is an administrator. Boolean value.
- **total_comments** - Total number of comments
- **favorite_count** - Number of quotes added to the favorites of the user.
- **added_fav_count** - Number of times where published quotes of the user where added to other users favorites.
- **published_quotes_count** - Number of published quotes of the user.

The **country_object** as got the following format:

- **id** - ID of the country
- **name** - English name of the country

## Errors
All known errors cause the resource to return HTTP error code header together with a JSON array containing at least `status` and `error` keys describing the source of error.

- **404 Not Found** — User with the specified ID does not exist.

## Example
**Request**

    GET https://api.teen-quotes.com/v1/users/42

### Success
**Return**
``` json
{
   "id":"42",
   "login":"antoineaugusti",
   "email":"anonymous@gmail.com",
   "birthdate":"1980-08-01",
   "gender":"M",
   "country":"107",
   "city":"Lake Demetriusstad",
   "about_me":"Est excepturi laudantium repellendus totam recusandae sed quod. Rerum necessitatibus repellendus autem doloremque dolorum at. Est fuga adipisci mollitia fuga placeat maiores.",
   "last_visit":"2014-05-22 13:41:07",
   "created_at":"2014-05-19 12:46:56",
   "profile_hidden":true,
   "url_avatar":"http:\/\/teen-quotes.com\/uploads\/avatar\/42.jpg",
   "wants_notification_comment_quote":true,
   "is_admin":true,
   "country_object":{
      "id":"107",
      "name":"Jordan"
   },
   "newsletters":[
      {
         "user_id":"42",
         "type":"daily",
         "created_at":"2014-05-22 19:05:11"
      },
      {
         "user_id":"42",
         "type":"weekly",
         "created_at":"2014-05-22 19:05:11"
      }
   ],
   "total_comments":12,
   "favorite_count":14,
   "added_fav_count":23,
   "published_quotes_count":8
}
```

### Error
For an error with HTTP code 404:
``` json
{
   "status":404,
   "error":"User not found."
}
```