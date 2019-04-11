# JSON Web Token
---

https://jwt.io/introduction/

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.


JSON Web Token structure

JSON Web Tokens consist of three parts separated by dots (.), which are:

- Header
- Payload
- Signature

```
xxxxx.yyyyy.zzzzz
```


Payload

The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

Registered claims: These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

Public claims: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

Private claims: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

The claims tell you, at minimum:

- Who this person is and the URI to their user resource (the sub claim)
- What this person can access with this token (the scope claim)
- When the token expires. Your API should be using this when it verifies the token.

Signature

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

## JWE, JWS, and JWT

Per the JWT Spec, “JWTs represent a set of claims as a JSON object that is encoded in a JWS and/or JWE structure.” The term “JWT” technically only describes an unsigned token; what we refer to as a JWT is most often a JWS or JWS + JWE.

**JWS — JSON Web Signature**

In the JWS scheme, the server signs the JWT and transmits it to the client with the signature. The signature provides a guarantee that the JWT claims have not been forged or tampered with. However, the JWT is not encrypted (the contents are essentially plaintext).

**JWE — JSON Web Encryption**

The JWE scheme, on the other hand, encrypts the contents without signing it. This brings confidentiality to your JWT, but not the security of signing and enclosing the JWE inside a JWS.

---

## Authentication vs. Token Authentication

The set of protocols an application uses to confirm user identity is authentication. Applications have traditionally persisted identity through session cookies. This paradigm relies on server-side storage of session IDs which forces developers to create session storage that is either unique and server-specific, or implemented as a completely separate session storage layer.

Token authentication was developed to solve problems server-side session IDs didn’t, and couldn’t. Just like traditional authentication, users present verifiable credentials, but are now issued a set of tokens instead of a session ID. The initial credentials could be the standard username/password pair, API keys, or even tokens from another service.

---

## Building of JWT token

**Building JWTs with JJWT**

the creation of the JWT is basically a three-step process:

- The definition of the internal claims of the token, like Issuer, Subject, Expiration, and ID.
- The cryptographic signing of the JWT (making it a JWS).
- The compaction of the JWT to a URL-safe string, according to the JWT Compact Serialization rules.

The final JWT will be a three-part base64-encoded string, signed with the specified signature algorithm, and using the provided key. After this point, the token is ready to be shared with the another party.

[Example with JJWT](https://stormpath.com/blog/jwt-java-create-verify)

- [Another Library Nimbus-JOSE-JWT](https://bitbucket.org/connect2id/nimbus-jose-jwt/wiki/Home)


---

# more articles

https://medium.com/vandium-software/5-easy-steps-to-understanding-json-web-tokens-jwt-1164c0adfcec

- [Logging out with JWT](https://dev.to/_arpy/how-to-log-out-when-using-jwt-4ajm)

---
































---
