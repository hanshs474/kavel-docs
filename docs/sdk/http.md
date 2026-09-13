# Raw HTTP

Two endpoints. Pick any string as the client id and send it on both.

```bash
ID="demo-$RANDOM"
curl -s https://www.kavel.ai/api/ai/generate \
  -H "content-type: application/json" -H "x-anon-id: $ID" \
  -d '{"provider":"kie","mediaType":"image","model":"kavel-image-v1","scene":"text-to-image",
       "prompt":"a lighthouse in fog, cinematic","options":{"aspect_ratio":"16:9"}}'
# {"code":0,"message":"ok","data":{"id":"<task>", ...}}

curl -s "https://www.kavel.ai/api/ai/anon-query?taskId=<task>&provider=kie&mediaType=image" -H "x-anon-id: $ID"
# repeat every ~5 s until data.images[0] appears
```

For an edit use `"model":"nano-banana-2-lite"`, `"scene":"image-to-image"` and
`"options":{"image_input":["https://…/source.jpg"]}`. The field is `image_input`, not
`image_urls`; the wrong name fails with *a reference image is required*.

Three things that look like success and are not:

1. **The quota wall is HTTP 200 with `code: 0`.** Check `data.wall`; `data.reason` is
   `anon_credits` or `anon_ip_daily`.
2. **Status is not monotonic.** A job can go `processing → pending → success`. Only `success` and
   `failed` are final.
3. **Nothing runs until you poll.** Submitting and walking away leaves the job in the queue.

The full request and response reference lives in the [Kavel API docs on GitBook](https://hanshs474.gitbook.io/kavel-api/).
