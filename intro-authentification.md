# Authentification

All endpoints require authentication.

This is a work in progress. The authentification process is going to be altered soon. For now, in order to authenticate you first have to establish a session with AskiaPortal:

1. Sign into AskiaPortal on the server that you will target (e.g. https://alpha.askia.com/askiaportal/SignIn)
2. Open the developer tools provided by your browser
3. Locate the cookie created by AskiaPortal when you signed in; note that the cookie has the name `askiaportal-sessionkey`

![cookie](https://github.com/Askia/designonline-api-doc/blob/master/assets/doc-cookie.png)

4. Copy the value of this cookie
5. For all requests made to the API, include a HTTP header with the key `Cookie` and the value set to the text you copied from the cookie
