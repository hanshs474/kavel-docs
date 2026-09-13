# Go

```bash
go get github.com/hanshs474/kavel-go
```

```go
img, err := kavel.Generate(ctx, "matte black ceramic mug on pale oak, soft window light", kavel.Options{AspectRatio: "16:9"})
if errors.Is(err, kavel.ErrQuota) {
    // this machine is done for today
}
fmt.Println(img.URL, img.Watermarked)

edited, err := kavel.Edit(ctx, img.URL, "place the mug on white marble", kavel.Options{})
```

Sentinel errors: `ErrQuota` (wait or sign in), `ErrRejected` (reword), `ErrSignIn` (off the free
shelf). The context you pass bounds the whole call, including the queue.

Try it without writing a file:

```bash
go run github.com/hanshs474/kavel-go/example@latest "an isometric coffee shop, pastel palette"
```

Reference: [pkg.go.dev/github.com/hanshs474/kavel-go](https://pkg.go.dev/github.com/hanshs474/kavel-go).
