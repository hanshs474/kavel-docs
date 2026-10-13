# LangChain

`langchain-kavel` gives a LangChain agent one tool, `KavelImageGenerator`, that turns a prompt into an
image URL. It runs on the free tier of [Kavel](https://www.kavel.ai/?utm_source=readthedocs&utm_medium=langchain)
with no API key, so the first call works on a machine with nothing configured.

## Install

```bash
pip install langchain-kavel
```

## Use it directly

```python
from langchain_kavel import KavelImageGenerator

tool = KavelImageGenerator()
url = tool.invoke({
    "prompt": "matte black ceramic mug on pale oak, soft window light",
    "aspect_ratio": "16:9",
})
print(url)  # https://cdn.kavel.ai/uploads/kie/image/....webp
```

## Give it to an agent

```python
from langchain.agents import create_agent
from langchain_kavel import KavelImageGenerator

agent = create_agent("openai:gpt-5-mini", tools=[KavelImageGenerator()])
agent.invoke({"messages": [{"role": "user", "content": "Make a cover image for a post about sourdough"}]})
```

The tool is named `kavel_image_generator`. Its arguments:

| Argument | Type | Notes |
|---|---|---|
| `prompt` | string | What the picture shows. |
| `aspect_ratio` | `1:1` · `16:9` · `9:16` · `4:3` · `3:4` | Default `1:1`. Ignored for edits. |
| `image_url` | string, optional | A public photo to edit. Editing needs an API key. |

## Free tier, then your account

Without a key the tool uses Kavel's anonymous tier: a fresh client id gets 5 credits, one
text-to-image run spends them, and free output is 1K and watermarked (see [limits](../limits.md)).
When the allowance runs out the tool returns a short message the agent can act on, instead of raising.

To run on your own account, pass `KavelImageGenerator(api_key=...)` or set `KAVEL_API_KEY`
(keys: [kavel.ai/settings/apikeys](https://www.kavel.ai/settings/apikeys?utm_source=readthedocs&utm_medium=langchain)).
A key also enables photo edits through `image_url` and `model=` for any image model on your plan.

Want a ready-made effect rather than a prompt? The [Kavel image studio](https://www.kavel.ai/image?utm_source=readthedocs&utm_medium=langchain)
has tuned tools such as the [full body AI generator](https://www.kavel.ai/image/ai-full-body-generator?utm_source=readthedocs&utm_medium=langchain).

Source: [github.com/hanshs474/langchain-kavel](https://github.com/hanshs474/langchain-kavel) ·
Package: [pypi.org/project/langchain-kavel](https://pypi.org/project/langchain-kavel/)
