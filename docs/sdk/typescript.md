# TypeScript — Deno, Node 18+, Bun

```bash
deno add jsr:@kavel/kavel
```

Zero dependencies: `fetch` and Web Crypto.

```ts
import { generate, edit, KavelError } from "@kavel/kavel";

const controller = new AbortController();
try {
  const img = await generate("a bowl of ramen, overhead shot, steam, dark slate table", {
    aspectRatio: "4:3",
    signal: controller.signal,
  });
  console.log(img.url);
} catch (e) {
  if (e instanceof KavelError && e.kind === "quota") console.log("daily ceiling reached");
  else throw e;
}
```

`signal` lets a UI cancel a job that is still sitting in the queue. Source:
[github.com/hanshs474/kavel-ts](https://github.com/hanshs474/kavel-ts).
