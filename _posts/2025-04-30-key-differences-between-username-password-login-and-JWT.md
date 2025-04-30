---
layout: post
title: What are the key differences between a Username Password Login and JWT?
---
One of the interview questions recently was about the differences between a username/password and a JWT token. Even though I answered it correctly and to the interviewer's satisfaction, I thought to research it further and give myself some more knowledge on the topic.

These are my notes for my own reference. Read some reference documentation for more accurate and up-to-date details.

### In case of Username/Password:

- Key difference is in the way the authentication and authorization is handled.
- Username/password has to be checked against a secure vault or a database entry - involves a serverside call
- Once authenticated, a session has to be created and maintained. A session means a state is maintained and passed with every call. Think of Session ID in a cookie passed in each request. 
- The user who was authenticated, has to be now Authorized (on what permissions he has to access what resources). This involves more server side calls.
- In a microservice architecture, these server calls have to be repeated for all microservices.

JWT avoids all of these issues.

### In case of JWT:

- The user provides their credentials (username and password again) to the server. The first call to the server.
- Sever checks the validity of the credentials and if valid, issues a JWT token to the user
- User stores the JWT in the code/local storage or if it is a UI, it will be stored in a cookie in the browser.
- For every subsequent requests made by the client/browser/Postman/code, an "Authorization" token has to be included which contains the JWT token as the value
- Server validates the JWT token for every request (signature and expiration) to verify the user's identity
- No session of any kind is maintained (hence session stickyness cannot be applied). Also as the token is stateless, any server can serve the request without knowing any prior context about the user.


### Advantages of JWT

- **Scalability** - No need to store cookies/session information. It will be in the JWT token
- **Stateless** - No need to maintain state information
- **Security** - JWT token can be signed with a secret key. 
- **Fine Grained Control** - For knowing what the user can access, user roles and permissions
- **Reduced Server Load** - Multiple requests are avoided which checks for authentication and authorization.


## Why use JWT if that also involves a username and password? 

This has one of the best explanations in this stack overflow post's accepted answer. Reproduced her for brevity

> 

> Suppose there are 2 servers: TRUSTED (e.g Google) and UNTRUSTED (any site that allows 'Sign in with Google').
> I don't want to send my TRUSTED username and password to UNTRUSTED. I also don't want to make a separate username and password for UNTRUSTED.
> So instead I get TRUSTED to authenticate me, and send a signed JWT containing my identity to UNTRUSTED to prove who I am. UNTRUSTED can check if the JWT is really from TRUSTED by verifying the JWT signature using TRUSTED's public key (if the signing algorithm uses public/private keys, e.g. RS256).
> JWTs can be stolen in transit, as can usernames and passwords, so this is a real risk (although, as you mentioned, JWTs will expire sooner). HTTPS will minimize the risk by encrypting data in transit.
> Another major benefit of using JWTs is that verifying a signature is often faster than checking an access token against a database.


https://security.stackexchange.com/a/191897

<br>
Followup questions include:
<br>

- How to sign a JWT token using a secret key


## References from Internet (not in any order)

- https://security.stackexchange.com/a/191897
- https://www.freecodecamp.org/news/how-to-sign-and-validate-json-web-tokens/

<br><br>
Fully written by Easo Thomas, 10% helped by AI tools. SOF link by Google search