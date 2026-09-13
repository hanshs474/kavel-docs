# Rust

```bash
cargo add kavel
```

Blocking, built on `ureq` — no async runtime pulled into your tree.

```rust
let opts = kavel::Options { aspect_ratio: "16:9".into(), ..Default::default() };
match kavel::generate("a red paper kite over a green hill, soft morning light", &opts) {
    Ok(img) => println!("{} watermarked={}", img.url, img.watermarked),
    Err(kavel::Error::Quota(why)) => eprintln!("come back tomorrow: {why}"),
    Err(kavel::Error::Rejected) => eprintln!("reword the prompt"),
    Err(e) => eprintln!("{e}"),
}
```

Inside Tokio, call it from `tokio::task::spawn_blocking` — one call holds a thread for the length of
the queue.

Reference: [docs.rs/kavel](https://docs.rs/kavel) · source [github.com/hanshs474/kavel-rs](https://github.com/hanshs474/kavel-rs).
