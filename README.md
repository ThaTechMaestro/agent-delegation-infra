# agent-delegation-infra
Authorization and provenance infrastructure for AI agent action chains

RFC 8693 covers how tokens can be exchanged between services, including cases where one party acts on behalf of another. It describes the idea of a composite token, which is a token that holds information about both parties, but stops short of defining how to represent one unless it's a JWT. This implementation addresses that gap: a clear, format-agnostic specification for representing composite tokens, including how both parties are identified and how the delegation relationship is verified. In the context of AI agent chains, that gap matters: an agent acting on behalf of a user needs a verifiable way to carry both identities across service boundaries.

**Root Certificate**

A root cert is self-signed; the Issuer and Subject are the same entity. It is identified as a CA by the `X509v3 Basic Constraints` field: `CA: TRUE`. The `PATHLEN: 1` constraint means it can only sign one level below it, the intermediate CA. It cannot be used to sign end certificates directly. Certs are cryptographically signed identification documents; they cannot be forged without the CA's private key.

**CN (Common Name)**

The CN is the name on the identification document. In this CA it is set to `agent-delegation-infra`. When a system receives this cert, the CN tells it who issued it.

**Validity Period**

This root cert is valid for 10 years. That is too long. The longer a cert is valid, the longer an attacker has if the private key is ever compromised. For production agent infrastructure, validity periods should be short with automated rotation. Expiry is not just a timestamp; it is a hard boundary after which every cert this CA ever signed stops being trusted.
