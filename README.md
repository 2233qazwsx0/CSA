# CSA — Luau Obfuscator

**Cryptographic Script Armor for Roblox/Luau developers.**

The obfuscator that draws the kill line: anything weaker than CSA, at any price, gets cut.

---

## What is CSA

CSA compiles your Luau script into a self-contained protected runtime. The original
source never appears in the output — not the strings, not the control flow, not even
the load entry points that reverse engineers normally grep for.

- **Virtualized bytecode** — your logic runs on a custom VM, not native Luau
- **Standard-grade cryptography** — real cipher encryption, not in-house XOR
- **Deep defense chain** — compression → layered decryption → integrity → runtime guard
- **Anti-dump & anti-debug** — the output fights back while running

> Every build is different. Every string has its own key. Every layer defeats a
> different attack.

---

## Install

Download the `csa` binary for your platform and put it on your PATH.

```bash
chmod +x csa
./csa --help
```

---

## Quick Start

```bash
# Obfuscate a script (max protection by default)
csa script.lua

# Specify output
csa script.lua protected.lua

# Pick a tier and seed
csa script.lua --tier standard --seed 42
```

---

## Security Tiers

| Tier | What you get | Use when |
|------|-------------|---------|
| `lite` ⚡ | AST-level obfuscation only, no VM, no encryption | Fast iteration, minimal overhead |
| `standard` 🛡 | VM + encryption + LZ77 + anti-dump | Most production scripts |
| `max` 🔥 | Everything: multi-fragment decryption, integrity, anti-debug, identity gate | High-value scripts |

---

## Options

```
-i, --input <file>      Input Luau source
-o, --output <file>     Output (default: input.obf.lua)
-s, --seed <num>        Deterministic seed
-t, --tier <level>      lite | standard | max (default: max)
-d, --dead-code <ratio> Dead-code injection 0.0-1.0
-l, --lang <lang>       UI language: en | zh (default: en)
    --no-color          Disable ANSI colors
-h, --help              Help
```

---

## Why CSA over the rest

Measured against real obfuscators on the same input, CSA is the only one that
gives you all of:

1. **Zero plaintext leakage** — `loadstring`, strings, and API names are all hidden
2. **Standard cipher, not in-house XOR** — per-string independent keys
3. **A self-contained VM** — no reliance on a hookable load step

Others leak `loadstring` in plaintext, expose their in-house XOR constants, or
ship incomplete Luau support. CSA closes those gaps.

---

## License

Proprietary. This is a closed-source release. Redistribution is not permitted.
