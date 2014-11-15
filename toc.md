## Authentication with OAuth 2

- Access token
	- [Request an access token](authentication/POST_oauth_password.md)
	- [Access token for the application](authentication/POST_oauth_client_credentials.md)
- Refresh token
	- [Ask for a refresh token](authentication/POST_oauth_refresh_token.md)

## Endpoints

- Comments
	- [<code>GET</code> comments/:quote_id](endpoints/comments/GET_comments_quote_id.md)
	- [<code>PUT</code> comments/:id](endpoints/comments/PUT_comments_id.md)
	- [<code>POST</code> comments/:quote_id](endpoints/comments/POST_comments_quote_id.md)
	- [<code>DELETE</code> comments/:id](endpoints/comments/DELETE_comments_id.md)
	- [<code>GET</code> comments/:id](endpoints/comments/GET_comments_id.md)
	- [<code>GET</code> comments/users/:user_id](endpoints/comments/GET_comments_users_user_id.md)

- Countries
	- [<code>GET</code> countries](endpoints/countries/GET_countries.md)
	- [<code>GET</code> countries/:id](endpoints/countries/GET_countries_id.md)

- FavoriteQuotes
	- [<code>POST</code> favorites/:id](endpoints/favorites/POST_favorites_id.md)
	- [<code>DELETE</code> favorites/:id](endpoints/favorites/DELETE_favorites_id.md)

- Password
	- [<code>POST</code> password/remind](endpoints/password/POST_password_remind.md)
	- [<code>POST</code> password/reset](endpoints/password/POST_password_reset.md)

- Quotes
	- [<code>GET</code> quotes](endpoints/quotes/GET_quotes.md)
	- [<code>POST</code> quotes](endpoints/quotes/POST_quotes.md)
	- [<code>GET</code> quotes/random](endpoints/quotes/GET_quotes_random.md)
	- [<code>GET</code> quotes/:id](endpoints/quotes/GET_quotes_id.md)
	- [<code>GET</code> quotes/favorites/:user_id](endpoints/quotes/GET_quotes_favorites_user_id.md)
	- [<code>GET</code> quotes/:approved_type/:user_id](endpoints/quotes/GET_quotes_approved_user_id.md)
	- [<code>GET</code> quotes/search/:query](endpoints/quotes/GET_quotes_search_query.md)

- Users
	- [<code>POST</code> users](endpoints/users/POST_users.md)
	- [<code>DELETE</code> users](endpoints/users/DELETE_users.md)
	- [<code>GET</code> users](endpoints/users/GET_users_id.md)
	- [<code>GET</code> users/:id](endpoints/users/GET_users_id.md)
	- [<code>PUT</code> users/password](endpoints/users/PUT_users_password.md)
	- [<code>PUT</code> users/profile](endpoints/users/PUT_users_profile.md)
	- [<code>PUT</code> users/settings](endpoints/users/PUT_users_settings.md)
	- [<code>GET</code> users/search/:query](endpoints/users/GET_users_search_query.md)

- Search
	- [<code>GET</code> search/:query](endpoints/search/GET_search_query.md)

- Stories
	- [<code>GET</code> stories](endpoints/stories/GET_stories.md)
	- [<code>POST</code> stories](endpoints/stories/POST_stories.md)
	- [<code>GET</code> stories/:id](endpoints/stories/GET_stories_id.md)