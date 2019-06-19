# Authentification

All endpoints require authentication.

This API support two approach to create an authenticated user session:

Using cookie
The easiest way is to use the Sign-In page of AskiaPortal to authenticate the user.

Using the application API key
Fill the apiKey input above with your application API key.
Use the [Session (Post)] (https://alpha.askia.com/AskiaPortal/Modules/design/swagger/ui/index#!/Session/Session_Post) endpoint to generate a session token.
The session token will expire after a certain amount of time. By default 120min.

The apiKey is a parameter in the request URL (query string) of all endpoints (<url_to_end_point>?apiKey=<your_api_key>), the askiaportal-session is an HTTP header of all endpoints (askiaportal-session=<your_session_key>)
