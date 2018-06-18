### Possible questions

1. **What is OAuth?**  
authorization framework, allowing third party applications (Relying Party) to access user resources at a web server (Service Provider) without having account credentials. 
2. **What are the differences between OAuth 1.0, 1.0a, and 2.0?**  
The difference between 1.0 and 1.0 is quite small, there is only a small security improvement (adding a veryfier when redirecting back to the user). OAuth 2.0 is a reworked version. It allows two flows and is in general easier and less complex than OAuth 1.0a but a little less secure, especially the implicit flow.
3. **What are the differences between the implicit flow and the authorization flow in OAuth 2.0?**  
Both flows start similarly. A request for access is sent form the relying party via the user to the service provider. In the implicit flow the service provider answers directly with an access token, while in the authorization flow it sends an authorization code. The access token is not bound to a relying party while the authorization code is, which adds security. Also The implicit flow does not share any secrets or encryption, so no signatures can be created, which makes this flow again less secure.
4. **Define authorization and authentication.**  
*Authentication:* Verifying a party's or user's identity.  
*Authorization:* Verifying that the party or user has access rights to some protected resources.
5. **Explain the terms Relying Party, Service Provider and User in connection to OAuth.**  
*Service Provider:* A web service or application that has user data stored and allows access to it by third party applications. E.g. Facebook, Google  
*Relying Party:* Third party applications that allow the user to connect to a web service and use the data in the application.  
*User:* Persob having an account at the Service Provider, using the relying party and allowing it to use the resources from the Service Provider.  
6. **Name six vulnerabilities of OAuth and say in which version and flow they are possible.**  

7. Why should a Relying Party never save the secret key locally.
8. What was added in OAuth 1.0a and why?
9. Why should the Service Provider always verify the redirect URI?
10. What is a consent page and what information is needed?
11. What is the danger if you use OAuth 2.0 implicit flow for authentication? Which service should be used instead?
12. What is OpenID and which problem does it solve?
13. What should the relying party mention when registering at a Service Provider? What information does it get back?
14. How does the Service Provider know/verify the relying party's identity.
15. Explain the use of the authentication code in the authorization flow and why it should be veruified by the Service Provider. What is the danger otherwise?
16. What can happen if no state tokens are used?
17. Explain what state tokens are, where they should be used and why.
18. What is WebView and how secure is it?
19. How does a Relying Party prevent an attacker from impersonating the app in OAuth 1.0?
20. State good practices in all OAuth versions and explain which attacks they prevent.
