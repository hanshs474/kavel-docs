# Handling the three failures

Only three things go wrong often enough to code for, and each wants a different response.

| Failure | How it shows up | What to do |
|---|---|---|
| **Quota** — the id's wallet or the machine's day is used up | HTTP 200, `data.wall: true` | Stop the batch, resume tomorrow, or sign in |
| **Rejected** — the content filter or model refused | task status `failed` | Reword. Retrying the same text fails the same way |
| **Timeout** — the queue ran past your deadline | no image before the deadline | Retry once; free queues vary from 25 to 80 s |

Every SDK exposes these as separate cases — `ErrQuota`/`ErrRejected` in Go, `Error::Quota`/
`Error::Rejected` in Rust, `KavelError.kind` in TypeScript and PHP — so the branch is a comparison,
not a string search.

A dropped connection **during polling** is not a failure. The job is still queued on the server; the
SDKs keep polling until the deadline instead of abandoning a job that is about to run.

If a prompt keeps coming back *rejected*, the [free AI image generator](https://www.kavel.ai/image?utm_source=readthedocs&utm_medium=docs) runs the same engine in a browser, which is a quicker place to iterate on wording than a script.
