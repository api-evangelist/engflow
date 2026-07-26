---
name: Manage EngFlow IAM roles
description: Create, read, update, list, and delete access-control roles on an EngFlow cluster via the IdentityAndAccessManagement gRPC service.
api: grpc/engflow-identity_and_access_management.proto
operations: [ListRoles, GetRole, CreateRole, UpdateRole, DeleteRole]
---

# Manage EngFlow IAM roles

Use the EngFlow `IdentityAndAccessManagement` gRPC service (package
`engflow.iam.v1`) to administer cluster access-control roles.

## Auth
Authenticate to the cluster first (see `authentication/engflow-authentication.yml`).
Typical path: run `engflow_auth login <cluster-url>` and let the Bazel/gRPC
client attach the credential, or present an mTLS client certificate. All calls
are gRPC over TLS.

## Steps
1. **List current roles** — call `ListRoles`. The response is server-streamed
   (`stream ListRolesResponse`); read the stream to completion to enumerate all
   roles.
2. **Inspect a role** — call `GetRole` with the role identifier to read its
   policy bindings before changing it.
3. **Create a role** — call `CreateRole` with the role definition and its
   policy. Capture the returned identifier.
4. **Update a role** — call `UpdateRole` to change policy bindings on an existing
   role.
5. **Delete a role** — call `DeleteRole` with the role identifier when it is no
   longer needed.

## Conventions
- Transport/error semantics: `conventions/engflow-conventions.yml` (gRPC status
  codes, not HTTP problem+json; no idempotency-key contract — retries must be
  safe on your side).
- Streaming: `ListRoles` streams; do not assume a single response message.
