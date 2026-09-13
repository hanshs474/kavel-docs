# Using an API key

The free tier is for trying things. When a script needs to keep running — a batch job, a busy CI
workflow, a production feature — give it an API key and every call runs on your
[Kavel](https://www.kavel.ai/?utm_source=readthedocs&utm_medium=docs) account instead.

## Get a key

1. Sign in at [kavel.ai](https://www.kavel.ai/?utm_source=readthedocs&utm_medium=docs) (new accounts start with free credits).
2. Open [Settings → API Keys](https://www.kavel.ai/settings/apikeys?utm_source=readthedocs&utm_medium=docs) and create one.
3. Copy it straight away — only a fingerprint is stored, so the full key is shown once.

Keep keys on a server or in CI secrets. A key shipped inside a browser page or a mobile app can be
extracted, which is why the API does not answer cross-origin browser requests.

## What changes with a key

| | Free tier | With an API key |
|---|---|---|
| Pays with | a 15-credit anonymous wallet | your account's credits |
| Daily limit | 30 credits per IP | none beyond your balance |
| Models | `kavel-image-v1`, `nano-banana-2-lite` | any image model your plan includes |
| Watermark | always | none on a paid plan |
| Queue | 25–80 s | none on a paid plan |
| Concurrency | — | 1 on a free account, 3 on a paid plan |

Prices are the site's prices — a call through the API costs exactly what the same generation costs
in the browser. [Pricing](https://www.kavel.ai/pricing?utm_source=readthedocs&utm_medium=docs) lists the plans; model pages such as
[GPT Image 2](https://www.kavel.ai/image/gpt-image-2?utm_source=readthedocs&utm_medium=docs) and
[Nano Banana 2](https://www.kavel.ai/image/nano-banana-2?utm_source=readthedocs&utm_medium=docs) list what each model does.

## Raw HTTP

```bash
curl https://www.kavel.ai/api/ai/generate \
  -H "Authorization: Bearer $KAVEL_API_KEY" -H "Content-Type: application/json" \
  -d '{"provider":"kie","mediaType":"image","model":"gpt-image-2","scene":"text-to-image",
       "prompt":"a glass perfume bottle on wet black stone, studio light","options":{"aspect_ratio":"4:5"}}'
# {"code":0,"message":"ok","data":{"id":"<task>", ...}}

curl https://www.kavel.ai/api/ai/query \
  -H "Authorization: Bearer $KAVEL_API_KEY" -H "Content-Type: application/json" \
  -d '{"taskId":"<task>"}'
# repeat until data.status is "success"; data.cleanImages holds the unwatermarked file on a paid plan
```

Your balance: `POST /api/user/get-user-credits` with the same header.

## Errors

| Message | Meaning |
|---|---|
| `invalid API key` | the key is wrong or was deleted |
| `insufficient credits` | the account balance cannot cover this run |
| `This model requires a subscription` | the model is on a paid plan |
| a concurrency message | wait for a running job to finish |

## In the SDKs

Every SDK takes the key as an option and falls back to the `KAVEL_API_KEY` environment variable, so
existing code picks it up without changes: [Python](sdk/python.md) · [Go](sdk/go.md) · [Rust](sdk/rust.md) ·
[TypeScript](sdk/typescript.md) · [PHP](sdk/php.md) · [Ruby](sdk/ruby.md) · [Dart](sdk/dart.md) · [.NET](sdk/dotnet.md).
