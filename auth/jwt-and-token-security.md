# JWT and Token Security

[< Back](./oauth2-and-oidc.md) | [Index](./README.md) | [Next: Authorization Patterns >](./authorization-patterns.md)

---

JSON Web Tokens (JWTs) are everywhere in modern web dev. They are powerful, but incredibly easy to shoot yourself in the foot with.

## The Anatomy of a JWT

A JWT is just a Base64-encoded string divided into three parts by dots: `Header.Payload.Signature`

```mermaid
graph LR
    A[eyJhbG... (Header)] -->|Describes algorithm| B
    B[eyJzdW... (Payload)] -->|Contains user data| C
    C[SflKxw... (Signature)] -->|Ensures tamper-proofing| D
```

1. **Header:** Defines token type and signing algorithm (e.g., `{"alg": "HS256", "typ": "JWT"}`).
2. **Payload:** The actual data (claims). Remember: **this is just Base64, NOT encrypted**. Anyone can read it. Never put sensitive data here.
3. **Signature:** The hash of the header + payload + a secret key. This proves the token wasn't tampered with.

## Signing Algorithms

- **Symmetric (HS256):** Uses one shared secret to both sign and verify the token. Fast, but anyone who needs to verify the token also has the power to create fake tokens.
- **Asymmetric (RS256 / ES256):** Uses a private key to sign and a public key to verify. Services can verify the token without being able to forge one. **Always prefer asymmetric for distributed systems.**

## Registered Claims

Standard fields you should include in your payload:
- `iss` (Issuer): Who created it (e.g., auth.yourcorp.com)
- `sub` (Subject): Who it's about (User ID)
- `aud` (Audience): Who it's for (e.g., api.yourcorp.com)
- `exp` (Expiration): When it dies (Unix timestamp)
- `iat` (Issued At): When it was born

## Token Validation Checklist

When your API receives a JWT, you must verify:
1. Is the signature valid?
2. Is it expired (`exp`)?
3. Is it intended for my API (`aud`)?
4. Was it issued by the right auth server (`iss`)?

```javascript
// Node.js example using jsonwebtoken
const jwt = require('jsonwebtoken');

try {
  const decoded = jwt.verify(token, publicKey, {
    audience: 'https://api.myapp.com',
    issuer: 'https://auth.myapp.com',
    algorithms: ['RS256']
  });
  // Token is valid!
} catch(err) {
  // Signature invalid, expired, or wrong audience
}
```

## Where to Store Tokens

| Storage Location | XSS Vulnerable | CSRF Vulnerable | Verdict |
|------------------|----------------|-----------------|---------|
| Local Storage | High | Low | Bad idea. Any malicious script can steal it. |
| Memory | None | Low | Secure, but lost on refresh. |
| HttpOnly Cookie | None | High | **Recommended** (with anti-CSRF measures like `SameSite=Lax`). |

## Token Revocation

The biggest flaw of stateless JWTs is that you can't easily revoke them. If a token is valid for 24 hours, and you ban a user, they still have access for 24 hours.

**How to handle this:**
1. **Short-lived tokens + Refresh Tokens:** Make JWTs expire in 15 minutes. The client silently uses a refresh token to get a new one. To ban a user, you revoke the refresh token in your database.
2. **Blocklist:** Maintain a Redis cache of revoked token IDs (`jti` claim). You have to check this cache on every request, which partially defeats the point of being stateless.

## Common JWT Attacks

- **The "none" algorithm:** Attackers change the header to `{"alg": "none"}` and strip the signature. Always explicitly specify allowed algorithms in your verification library!
- **Key Confusion:** Tricking the server into verifying an asymmetric token using a public key as a symmetric shared secret.

## The Takeaways

- **JWTs are signed, not encrypted.** Anyone can read the payload.
- Always use **asymmetric algorithms (RS256)** for microservices.
- Always validate `exp`, `aud`, and `iss`.
- Store tokens in **HttpOnly cookies**, not Local Storage.
- Keep JWT lifetimes short and rely on refresh tokens for session management.

---

[< Back](./oauth2-and-oidc.md) | [Index](./README.md) | [Next: Authorization Patterns >](./authorization-patterns.md)
