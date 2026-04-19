# Long polling

## What problem does it solve?
Near-real-time updates from server to client when you can’t (or don’t want to) use WebSockets/SSE.

## How it works (high level)
Client makes an HTTP request that the server **holds open** until:
- new data is available, or
- a timeout occurs (server responds with “no new data”)

Client immediately starts another request after receiving the response.

## Request/response flow (step-by-step)
1. Client sends `GET /events?since=<cursor>`
2. Server waits until it has an event newer than `cursor` (or timeout)
3. Server replies with:
   - `200` + events + new cursor, OR
   - `204` (or `200` with empty) when timed out
4. Client repeats (with updated cursor)

## Tradeoffs
- Pros: works over plain HTTP; simple infra; easy fallback.
- Cons: higher overhead than WebSockets; “thundering herd” risk; careful timeout/retry needed.

## Failure modes / gotchas
- Proxies/load balancers may kill long-held connections.
- Need server-side limits: max wait time, max concurrent polls per user.
- Retry storms: use jitter/backoff on errors.
- Correctness: cursor/last-event-id logic must be robust (avoid missing/duplicating events).

## When to use / avoid
- Use: small scale “live” updates; environments where WS/SSE aren’t viable.
- Avoid: high fanout/very chatty feeds; strict low-latency at scale (prefer WS/SSE + broker).

## Related concepts
WebSockets, Server-Sent Events (SSE), pub/sub, message brokers, idempotency, cursors.

