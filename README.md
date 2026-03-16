# agent-delegation-infra
Authorization and provenance infrastructure for AI agent action chains

RFC 8693 covers how tokens can be exchanged between services, including cases where one party acts on behalf of another. It describes the idea of a composite token, which is a token that holds information about both parties, but stops short of defining how to represent one unless it's a JWT. This implementation addresses that gap: a clear, format-agnostic specification for representing composite tokens, including how both parties are identified and how the delegation relationship is verified. In the context of AI agent chains, that gap matters: an agent acting on behalf of a user needs a verifiable way to carry both identities across service boundaries.
