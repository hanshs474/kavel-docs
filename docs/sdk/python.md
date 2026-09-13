# Python

```bash
pip install kavel
```

Standard library only, so it installs into any environment — including the restricted ones in hosted
notebooks.

```python
from kavel import generate

url = generate("a paper-cut layered mountain range at dusk, warm rim light")
```

Pass `image_url` and the prompt becomes an instruction:

```python
url = generate(
    "restyle the hair into a shoulder-length layered cut, keep the same face, skin and lighting",
    image_url="https://example.com/portrait.jpg",
)
```

`KavelError` is raised for a refused prompt, a timeout and the daily ceiling. Source and full README:
[pypi.org/project/kavel](https://pypi.org/project/kavel/).
