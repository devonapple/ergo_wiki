All examples are Base58-encoded.

# Secret → PublicKey → P2PKAddress derivation

```json
{
  "sk": "HU56FxBMCpsMybo5iX8khduFQmQUptyJPqZEEvB8rzoq",
  "pk": "wJhEaUie2b5Sp3ogkD796gWE7Zycw3wHeiKeAkP1Y649",
  "p2pk": "3Wxr5EGDUig8cKof1KwySX7KDMLc6mxFmJ9toKZ7oNQV6BUzCs1H"
}
```

# Mnemonic → Seed → Root Secret derivation
```json
{
  "mnemonic": "edge talent poet tortoise trumpet dose",
  "seed": "5KgzUvF4yZjBDkoseNyZnAHsA6cuqhvwkGUNZ4y2WQXfRhLoHfbipZR4XriVZKbVFMcP6QKLRwLZhJdRt2wKx6tY",
  "root_secret": "4rEDKLd17LX4xNR8ss4ithdqFRc3iFnTiTtQbanWJbCT"
}
```

# Root Secret → Child Secret derivation
```json
[
  {
    "root_secret": "4rEDKLd17LX4xNR8ss4ithdqFRc3iFnTiTtQbanWJbCT",
    "path": "m/1",
    "derived_secret": "CLdMMHxNtiPzDnWrVuZQr22VyUx8deUG7vMqMNW7as7M"
  },
  {
    "root_secret": "4rEDKLd17LX4xNR8ss4ithdqFRc3iFnTiTtQbanWJbCT",
    "path": "m/1/2",
    "derived_secret": "9icjp3TuTpRaTn6JK6AHw2nVJQaUnwmkXVdBdQSS98xD"
  },
  {
    "root_secret": "4rEDKLd17LX4xNR8ss4ithdqFRc3iFnTiTtQbanWJbCT",
    "path": "m/1/2/2'",
    "derived_secret": "DWMp3L9JZiywxSb5gSjc5dYxPwEZ6KkmasNiHD6VRcpJ"
  }
]
```