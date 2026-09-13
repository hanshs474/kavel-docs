# Ruby

```bash
gem install kavel
```

```ruby
require "kavel"

img = Kavel.generate("a stack of three colorful macarons, studio light", aspect_ratio: "4:3")
puts img.url

edited = Kavel.edit(img.url, "put the macarons on a pale marble slab; keep the colors")
```

Rescue by intent: `Kavel::QuotaError`, `Kavel::RejectedError`, `Kavel::SignInError`, `Kavel::AuthError`.
Pass `api_key:` (or set `KAVEL_API_KEY`) to run on your account — see [Using an API key](../api-key.md).

Source: [github.com/hanshs474/kavel-rb](https://github.com/hanshs474/kavel-rb) · [rubygems.org/gems/kavel](https://rubygems.org/gems/kavel)
