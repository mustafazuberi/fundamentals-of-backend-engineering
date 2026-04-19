# Long polling demo

Goal: a tiny runnable project that demonstrates long polling with:
- an in-memory event queue
- a `cursor` (last seen event id)
- a server timeout (e.g. 25–30s)

Planned endpoints:
- `POST /publish` — add an event
- `GET /events?since=<id>` — long poll for next events

Implementation will live under:
- `projects/long-polling/server/`
- `projects/long-polling/client/`

Tell me your course language/framework (Node/Express, Python/FastAPI, Go, Java/Spring), and I’ll scaffold the runnable demo accordingly.

