
This is based on:
https://spring.io/guides/tutorials/spring-boot-oauth2/
Also read this. https://spring.io/guides/tutorials/spring-security-and-angular-js/


For google create crdentials using webapp
and select redirect url of http://localhost:8080/login/google

https://console.developers.google.com/projectselector/apis/credentials

there is a ClientApplication to demonstrate how to use servers that use our authorization server for login.

If using a mobile app can do this.
acme:acmesecret@localhost:8080/oauth/token

Content-Type: application/x-www-form-urlencoded
acme:acmesecret are passed using basic

data posted includes
grant_type:password
username:user
password:the default password foundin log


$ curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=password -d username=user -d password=...
{"access_token":"aa49e025-c4fe-4892-86af-15af2e6b72a2",
"token_type":"bearer",
"refresh_token":"97a9f978-7aad-4af7-9329-78ff2ce9962d",
"expires_in":43199,"scope":"read write"}

see http://www.slideshare.net/briandavidcampbell/is-that-a-token-in-your-phone-in-your-pocket-or-are-you-just-glad-to-see-me-oauth-20-and-mobile-devices

How to use the token:

post.setHeader("Authorization", "Bearer "+ accessToken);

If we get 200 good.
Else can issue a refresh request

$ curl acme:acmesecret@localhost:8080/oauth/token -d grant_type=refresh_token -d refresh_token=use the refresh token
{"access_token":"370592fd-b9f8-452d-816a-4fd5c6b4b8a6","token_type":"bearer","expires_in":43199,"scope":"read write"}
