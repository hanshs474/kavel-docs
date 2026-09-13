# Limits and pricing

Every number here was read back from the running service, not copied from a pricing table.

| | Value | What it means in practice |
|---|---|---|
| Free grant per client id | **15 credits** | The SDKs mint a new id per call |
| Text to image | **5 credits** | Three per id |
| Image edit | **15 credits** | One per id |
| Per-IP ceiling | **30 credits / day** | About six images, or two edits, per machine per day |
| Output | **1K, watermarked** | The response tells you whether the mark was drawn |
| Queue before the model runs | **25–80 s** | Default deadlines are six minutes |
| Video | **not available signed out** | The cheapest clip costs 40 credits, more than the grant |

The per-IP ceiling is the one you will actually meet. It comes back as a normal HTTP 200 with
`wall: true` and `reason: "anon_ip_daily"` — every SDK turns that into a *quota* error so you can tell
it apart from a refused prompt. [Batch jobs under the daily ceiling](recipes/batch.md) shows how to plan
around it.

## Past the free tier

Signing in at [kavel.ai](https://www.kavel.ai/?utm_source=readthedocs&utm_medium=docs) removes the watermark, lifts the ceiling and opens
4K output and video. The [pricing page](https://www.kavel.ai/pricing?utm_source=readthedocs&utm_medium=docs) lists each plan's credits, and
the [AI video generator](https://www.kavel.ai/video?utm_source=readthedocs&utm_medium=docs) has the video models.
