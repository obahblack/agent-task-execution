# ticket-002 — Implement the login API

## Objective
Implement the login endpoint against contract.md v1.

## Context and sources
Fictional demonstration: an existing application has approved email/password login, session conventions, a logout flow, and supported viewport definitions. These are example assumptions, not requirements for the user’s repository. A real worker must locate and cite those project artifacts before Ready.

## Scope and requirements
- R1: Accept valid email/password credentials and establish the session defined by contract v1.
- R2: Return the contracted invalid-credential response without establishing a session.

## Dependencies
ticket-001

## Exclusions
No registration, password reset, new identity provider, or deployment.
