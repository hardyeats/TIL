## RS256 vs HS256

Both choices refer to what algorithm the identity provider uses to **sign** the JWT. Signing is a cryptographic operation that generates a "signature" (part of the JWT) that the recipient of the token can validate to ensure that the token has not been tampered with.

- RS256 (RSA Signature with [SHA-256](https://en.wikipedia.org/wiki/SHA-256)) is an [asymmetric algorithm](https://en.wikipedia.org/wiki/Public-key_cryptography), and it uses a public/private key pair: the identity provider has a private (secret) key used to generate the signature, and the consumer of the JWT gets a public key to validate the signature. Since the public key, as opposed to the private key, doesn't need to be kept secured, most identity providers make it easily available for consumers to obtain and use (usually through a metadata URL).
- HS256 ([HMAC](https://en.wikipedia.org/wiki/HMAC) with SHA-256), on the other hand, is a [symmetric algorithm](https://en.wikipedia.org/wiki/Symmetric-key_algorithm), with only one (secret) key that is shared between the two parties. Since the same key is used both to generate the signature and to validate it, care must be taken to ensure that the key is not compromised.

If you will be developing the application consuming the JWTs, you can safely use HS256, because you will have control on who uses the secret keys. If, on the other hand, you don't have control over the client, or you have no way of securing a secret key, RS256 will be a better fit, since the consumer only needs to know the public (shared) key.

Since the public key is usually made available from metadata endpoints, clients can be programmed to retrieve the public key automatically. If this is the case (as it is with the .Net Core libraries), you will have less work to do on configuration (the libraries will fetch the public key from the server). Symmetric keys, on the other hand, need to be exchanged out of band (ensuring a secure communication channel), and manually updated if there is a signing key rollover.

Auth0 provides metadata endpoints for the OIDC, SAML and WS-Fed protocols, where the public keys can be retrieved. You can see those endpoints under the "Advanced Settings" of a client.

The OIDC metadata endpoint, for example, takes the form of `https://{account domain}/.well-known/openid-configuration`. If you browse to that URL, you will see a JSON object with a reference to `https://{account domain}/.well-known/jwks.json`, which contains the public key (or keys) of the account.

If you look at the RS256 samples, you will see that you don't need to configure the public key anywhere: it's retrieved automatically by the framework.



## References

[RS256 vs HS256: What's the difference?](https://stackoverflow.com/questions/39239051/rs256-vs-hs256-whats-the-difference)

