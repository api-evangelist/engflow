---
name: Stream EngFlow build and invocation events
description: Read build/invocation events and stored invocations from an EngFlow cluster via the EventStore and ResultStore gRPC services.
api: grpc/engflow-eventstore.proto
operations: [GetBuild, GetInvocation]
---

# Stream EngFlow build and invocation events

Use the EngFlow `EventStore` (package `engflow.eventstore.v1`) and `ResultStore`
(package `engflow.resultstore.v1`) gRPC services to consume build telemetry.

## Auth
Authenticate to the cluster (see `authentication/engflow-authentication.yml`) —
mTLS, a cluster-issued JWT bearer token, or OIDC/SAML federation.

## Steps
1. **Stream a build's events** — call `EventStore.GetBuild` with the build
   identifier. The response is `stream StreamedBuildEvent`; consume the stream to
   completion.
2. **Stream a single invocation's events** — call `EventStore.GetInvocation`
   with the invocation identifier for `stream StreamedBuildEvent`.
3. **Read a stored invocation** — call `ResultStore.GetInvocation` (package
   `engflow.resultstore.v1`) for `stream StreamedInvocation` to retrieve the
   persisted result-store record (environment, results).

## Conventions
- All three operations are **server-streaming** — handle partial/streamed
  responses, not a single message.
- Errors surface as gRPC status codes; see `conventions/engflow-conventions.yml`.
