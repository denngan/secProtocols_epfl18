### Possible questions

1. **What is OAuth?**  
OAuth is an authorization framework, allowing third party applications (Relying Party) to access user resources at a web server (Service Provider) without having account credentials. 
2. **What are the differences between OAuth 1.0, 1.0a, and 2.0?**  
The difference between 1.0 and 1.0a is quite small, there is only a small security improvement (adding a veryfier when redirecting back to the user). OAuth 2.0 is a reworked version. It allows two flows and is in general easier and less complex than OAuth 1.0a but a little less secure, especially the implicit flow.
3. **What are the differences between the implicit flow and the authorization flow in OAuth 2.0?**  
Both flows start similarly. A request for access is sent form the relying party via the user to the service provider. In the implicit flow the service provider answers directly with an access token, while in the authorization flow it sends an authorization code. The access token is not bound to a relying party while the authorization code is, which adds security. Also The implicit flow does not share any secrets or encryption, so no signatures can be created, which makes this flow again less secure.
4. **Define authorization and authentication.**  
*Authentication:* Verifying a party's or user's identity.  
*Authorization:* Verifying that the party or user has access rights to some protected resources.
5. **Explain the terms Relying Party, Service Provider and User in connection to OAuth.**  
*Service Provider:* A web service or application that has user data stored and allows access to it by third party applications. E.g. Facebook, Google  
*Relying Party:* Third party applications that allow the user to connect to a web service and use the data in the application.  
*User:* Persob having an account at the Service Provider, using the relying party and allowing it to use the resources from the Service Provider.  
6. **Name seven vulnerabilities of OAuth and say in which version and flow they are possible.**  
* Consumer Secret saved locally - 1.0, 1.0a
* Overwrite redirect URI - 2.0 implicit flow, 1.0a
* use for authentication - 2.0 implicit flow
* authorization code not verified - 2.0 authorization flow
* unclear consent page - any
* no state tokens - 2.0 authorization flow
* Using WebView - any
7. **Why should a Relying Party never save the secret key locally.**  
The an attacker can find the key in the code and use it to impersonate the Relying Party very easily especially in OAuth 1.0. He will also need to change the redirect URI. This will also work in 1.0a, if the redirect URI is not compared to the registered URI of the application.
8. **What was added in OAuth 1.0a and why?**  
OAuth adds a veryfier that is sent back to the Relying Party with the validated request token. The verifier makes sure that the token is sent to the same user who requested the request token, so it prevents cross site request forgery.
9. **Why should the Service Provider always verify the redirect URI?**  
If he does not OAuth 1.0a and 2.0 implicit flow pose security riscs. An attacker could overwrite the redirect URI and then access token would be sent directly to him. Especially in 2.0 implicit flow this is very dangerous as no consumer secret is needed to get the resources.In 1.0a the consumer secret must be known, too, to connect to the Service provider.
10. **What is a consent page and what information is needed?**  
A consent page appears when the user is redirected from the relying party to the service provider to authorize the access. It should inform the user of its actions and of the resources to be accessed. It should contain:
* User name / ID
* User Profile Pic
* Relying Party name
* Relying Party icon
* resources the Relying party will be authorized to access
11. **What is the danger if you use OAuth 2.0 implicit flow for authentication? Which service should be used instead?**  
If an app uses OAuth for authentication that means it allows logins via Service Providers. It asks for access authorization and then checks the users ID. If the attacker get get the access token in OAuth 2.0 implicit flow through a malicious app, he will be able to use that access token to login with the users account in Apps that authenticate the user with implicit flow, becasue there the access token is not bound to Relying Parties.
12. **What is OpenID and which problem does it solve?**  
OpenID Connect is a protocol built on OAuth that allows to authenticate users through other service providers. It achieves that by sending an ID token (JWT Json Web Token) that includes claims about the authentication event. This token is the bound to users and relying parties, making the authentication secure. Just using 2.0 implicit flow would be insecure.
13. **What should the relying party mention when registering at a Service Provider? What information does it get back?**  
When the relying party registers to the service provider it indicates what resources it would like to access on the user accounts. The service provider gives him a consumer key and a consumer secret for 1.0 or 2.0 authorization flow.
14. **How does the Service Provider know/verify the relying party's identity.**  
In 1.0 and 2.0 authorization flow the Relying party uses a consumer key and secret to connect to the Service Provider and to sign its directly sent messages. That way the Srevice provider can know and verify the identity. In 2.0 implicit flow that is not used, but the Relying party sends its application ID with the redirect URI. The app ID and the registered URI should match.
15. **Explain the use of the authorization code in the authorization flow and why it should be veruified by the Service Provider. What is the danger otherwise?**  
The authorization code is bound to a Relying Party in 2.0 authorization flow. But if it is not checked, then an attacker can make a user login in a malicious app and then replace the authorization code when logging into another application. That way the app will get the access token for another user, while the atttacker is logged in. The authorization code should also be a short living one time password.
16. **What can happen if no state tokens are used?**  
An attacker could login with his account and get the autorization code for some Relying Party. He could the plant a phishing link redirecting a user to that relying party but with the attacker's authorization code. That would make the user access the attacker's resources.
17. **Explain what state tokens are, where they should be used and why.**
A state token is sent from a relying party to the service provider in 2.0 authorization flow. The state token is bounded to a relying party user and may also include an encrypted timestamp or be short living. The service provider sends the authorization code back with the state token. That way cross site request forgery is not possible because the relying party verifies if the state token belongs to the right user.
18. **What is WebView and how secure is it?**  
WebView offers a user access to a web bundle inside a mobile application. As WebView is embedded inside the application, it lets it access its long term cookies.  That is why it should never be used to embed the OAuth login page because then the long term cookies of the login are saved and the application can later always log into the account without asking for an access token.
19. **How does a Relying Party prevent an attacker from impersonating the app in OAuth 1.0?**  
Do not save the consumer secret locally.
20. **State good practices in all OAuth versions and explain which attacks they prevent.**
* do not save the consumer secret locally - Impersonating an app prevented
* check the redirect URI, secure redirection - Overwriting redirect URI prevented
* use OpenID Connect for authentication - OAuth use for authentication, attacker login on other apps prevented
* verify authorization code with RP credentials - attacker access to another account with authorization code from malicious app prevented
* use state tokens - Phishing link to make user access attacker's resources prevented
* use informative consent page - access for unknown Relying Party prevented
* do not incorporate OAuth Login into WebView - saving longterm cookies prevented 
