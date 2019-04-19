# Secret → PublicKey → P2PKAddress derivation

```json
{
  "sk": "f4aa4c487af71fb8b52a3ecd0d398393c2d247d6f0a25275e5d986854b3e2db8",
  "pk": "0326df75ea615c18acc6bb4b517ac82795872f388d5d180aac90eaa84de750b942",
  "p2pk": "3Wxr5EGDUig8cKof1KwySX7KDMLc6mxFmJ9toKZ7oNQV6BUzCs1H"
}
```

# Mnemonic → Seed → Root Secret derivation
```json
{
  "mnemonic": "edge talent poet tortoise trumpet dose",
  "seed": "d82f635a69f385bb7fda33cf467def9205bf6c9d85ac35fd33fc1b943b927a427c632238f4267b521da17656642242d170d348848e9d78a8a73812ac6e9b6899",
  "root_secret": "392f75ad23278b3cd7b060d900138f20f8cba89abb259b5dcf5d9830b49d8e38"
}
```

# Root Secret → Child Secret derivation
```json
[
  {
    "root_secret": "392f75ad23278b3cd7b060d900138f20f8cba89abb259b5dcf5d9830b49d8e38",
    "path": "m/1",
    "derived_secret": "a877b1907527fc0b7595efeae85f7026c7d44815314ab9ab13a4d48d63281460"
  },
  {
    "root_secret": "392f75ad23278b3cd7b060d900138f20f8cba89abb259b5dcf5d9830b49d8e38",
    "path": "m/1/2",
    "derived_secret": "8186b7c22735c6f1f472b2578fbc3529a23d80bbe2aac71f6f7ffc83691d08ae"
  },
  {
    "root_secret": "392f75ad23278b3cd7b060d900138f20f8cba89abb259b5dcf5d9830b49d8e38",
    "path": "m/1/2/2'",
    "derived_secret": "b9d19e2139eb033523d19154bfb6ea24aaf6d257bc7b2974211f1e5642305243"
  }
]
```