# Kavel SDKs

Every client in this site does the same two things — **generate** an image from a prompt and **edit**
an image you already have — and none of them asks for an API key. They call the free tier of
[Kavel](https://www.kavel.ai/?utm_source=readthedocs&utm_medium=docs), which meters its allowance against a client id the SDK makes up on
the spot instead of an account you register.

That makes them useful in the places a keyed client is awkward: a CI job that renders social cards, a
prototype you want a colleague to run without sharing secrets, a teaching notebook, a cron script on a
box nobody wants to configure.

| Language | Install | Package page |
|---|---|---|
| Python | `pip install kavel` | [pypi.org/project/kavel](https://pypi.org/project/kavel/) |
| Go | `go get github.com/hanshs474/kavel-go` | [pkg.go.dev](https://pkg.go.dev/github.com/hanshs474/kavel-go) |
| Rust | `cargo add kavel` | [docs.rs/kavel](https://docs.rs/kavel) |
| TypeScript | `deno add jsr:@kavel/kavel` | [jsr.io/@kavel/kavel](https://jsr.io/@kavel/kavel) |
| PHP | `composer require hanshs474/kavel` | [packagist.org](https://packagist.org/packages/hanshs474/kavel) |
| Ruby | `gem install kavel` | [rubygems.org/gems/kavel](https://rubygems.org/gems/kavel) |
| Dart / Flutter | `dart pub add kavel` | [pub.dev/packages/kavel](https://pub.dev/packages/kavel) |
| .NET | `dotnet add package Kavel` | [nuget.org/packages/Kavel](https://www.nuget.org/packages/Kavel) |
| Anything else | two HTTP calls | [Raw HTTP](sdk/http.md) |

## What one call does

1. It mints a client id (`go-…`, `rs-…`, `ts-…`) — a fresh one per call, because the free wallet
   on an id covers three images or one edit and a reused id would stop partway through a loop.
2. It `POST`s the job and gets a task id back.
3. It polls. Free jobs wait **25–80 seconds** in a queue and are handed to the model only by the poll
   that crosses the end of that wait — polling is what starts the work, not just how you read it.
4. It returns a permanent CDN URL and whether a watermark was drawn.

## Two engines on the free shelf

- **`kavel-image-v1`** — text to image, 5 credits.
- **`nano-banana-2-lite`** — image to image, 15 credits. This is the engine behind the
  [AI hairstyle changer](https://www.kavel.ai/image/ai-hairstyle-changer?utm_source=readthedocs&utm_medium=docs) and the
  [AI outfit generator](https://www.kavel.ai/image/ai-outfit-generator?utm_source=readthedocs&utm_medium=docs) on the site, and it has its own
  [Nano Banana 2 Lite page](https://www.kavel.ai/image/nano-banana-2-lite?utm_source=readthedocs&utm_medium=docs).

Signed-in accounts get the rest of the shelf —
[Nano Banana 2](https://www.kavel.ai/image/nano-banana-2?utm_source=readthedocs&utm_medium=docs),
[GPT Image 2](https://www.kavel.ai/image/gpt-image-2?utm_source=readthedocs&utm_medium=docs),
[Qwen Image 3](https://www.kavel.ai/image/qwen-image-3?utm_source=readthedocs&utm_medium=docs) and
[Seedream 5.0 Pro](https://www.kavel.ai/image/seedream-5-pro?utm_source=readthedocs&utm_medium=docs) — plus video. See [Limits and pricing](limits.md).

When a script outgrows the free tier, the same SDKs take an API key and run on your account — see [Using an API key](api-key.md).
