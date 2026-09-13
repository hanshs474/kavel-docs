# .NET

```bash
dotnet add package Kavel
```

```csharp
using Kavel;

var kavel = new KavelClient();
var img = await kavel.GenerateAsync("a cozy reading nook with a green armchair, warm lamp light", aspectRatio: "4:3");
Console.WriteLine(img.Url);
```

Targets `net8.0` and `netstandard2.0`. Branch on `KavelException.Kind`. Pass `apiKey:` (or set
`KAVEL_API_KEY`) to run on your account — see [Using an API key](../api-key.md).

Source: [github.com/hanshs474/kavel-dotnet](https://github.com/hanshs474/kavel-dotnet) · [nuget.org/packages/Kavel](https://www.nuget.org/packages/Kavel)
