# Batch jobs under the daily ceiling

The limit you will hit is **30 credits per IP per day**, not the per-id grant. That is six images or two
edits from one machine. A batch that ignores it fails on item seven with a quota error — indistinguishable
from a bug if you are not looking for it.

Plan the batch in credits, not items:

```python
from kavel import generate, KavelError

prompts = open("prompts.txt").read().splitlines()
budget = 30
done = []
for p in prompts:
    if budget < 5:
        break  # stop cleanly; resume tomorrow from len(done)
    try:
        done.append((p, generate(p)))
        budget -= 5
    except KavelError as e:
        if "429" in str(e) or "ceiling" in str(e).lower():
            break
        done.append((p, None))  # refused prompt: credits are spent either way
open("progress.txt", "w").write(str(len(done)))
```

Write progress after every item. A job that only saves at the end loses everything to one interruption.

For larger runs — a catalogue of product shots, a set of social cards for every post — a signed-in plan
on [kavel.ai](https://www.kavel.ai/pricing?utm_source=readthedocs&utm_medium=docs) removes the ceiling. Browse finished output in the
[showcase](https://www.kavel.ai/showcases?utm_source=readthedocs&utm_medium=docs) before deciding which model a batch should use.
