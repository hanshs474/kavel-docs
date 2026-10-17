# Writing edit instructions

The edit engine keeps what it can still see and invents what it cannot. So the lever in an edit prompt
is saying **what must not change**, more than describing the change in detail.

| Weak | Strong |
|---|---|
| "make it a sunset" | "replace the sky with a warm sunset; keep the building, the window reflections and the framing unchanged" |
| "short hair" | "restyle the hair into a short textured crop; keep the same face, skin tone, expression and lighting" |
| "put it on a table" | "place the product on a pale oak table with soft window light from the left; keep the label text exactly as it is" |

Two practical rules:

- **Use a sharp source.** Detail that is blurred in the input will be re-imagined, not preserved.
- **One change per call.** Stacking three edits in one sentence makes the model trade them off.

The same engine powers the [AI hairstyle changer](https://www.kavel.ai/image/ai-hairstyle-changer?utm_source=readthedocs&utm_medium=docs),
the [AI outfit generator](https://www.kavel.ai/image/ai-outfit-generator?utm_source=readthedocs&utm_medium=docs) and the
[AI product photo editor](https://www.kavel.ai/image/ai-product-photo-editor?utm_source=readthedocs&utm_medium=docs), each preloaded with a
prompt tuned for that job — a good place to copy wording from.

## Single-edit pages to test a prompt in the browser

Before scripting an edit, it can help to see what one prompt does to one photo. Each of
these pages does exactly one change in the browser:

- [AI Smile Generator](https://ai-smile-generator-free.netlify.app/) — a natural smile on a neutral face
- [Teeth Whitening Photo Editor](https://teeth-whitening-photo-editor.onrender.com/) — whiter teeth, same smile
- [Braces Filter](https://hanshs474.github.io/braces-filter/) — see a smile with braces on
- [AI Bald Filter](https://shiny-scalp-studio.lovable.app/) — the same face with a shaved head
