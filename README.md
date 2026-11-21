<img src="assets/logo.png" width="112" height="112" alt="Cormorant logo">

# Cormorant

Separate variation in packet delivery from a constant difference between clocks. This Blyx workflow framework is part of the networking and cache control collection.

Absolute one-way delay depends on clock alignment. Changes in transit can still reveal jitter when the clock offset is stable. [IETF RFC 3550, interarrival jitter](https://www.rfc-editor.org/rfc/rfc3550.html#appendix-A.8)

## Install and run

Install [Blyx 0.2.1](https://www.blyx-lang.space/download) with a Rust toolchain and host linker for native builds.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-cormorant.git
cd blyx-cormorant
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

[Run the editable browser example](https://www.blyx-lang.space/play?example=package-cormorant) · [Package page](https://www.blyx-lang.space/packages/cormorant) · [Handbook](https://doc.blyx-lang.space/guide/cormorant)

## Import the module

Run this in the directory containing your application's entry file.

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-cormorant.git vendor/cormorant
```

```blyx
use vendor::cormorant::cormorant;

fn main() {
    let sent = [0, 16];
    let arrived = [100, 148];
    let initial = 0.0;
    let result = cormorant_trace(sent, arrived, initial);
    if len(result) == 0 { println!("invalid"); return; }
    let mut i = 0;
    while i < len(result) {
        println!(at(result, i));
        i += 1;
    }
}
```

Expected output

```text
32
2
1
```

## API

`cormorant_trace(sent, arrived, initial)`

Returns [transit range, smoothed jitter, adjacent pairs]. Input rows must be in arrival order and use unwrapped sender timestamps. Invalid arguments and nonfinite results return an empty vector. Integers carried in numeric vectors use the exact range from −(2^53−1) to 2^53−1.

| Argument | Domain |
| --- | --- |
| sent | Vector of values, each a exact signed integer |
| arrived | Vector of values, each a exact signed integer |
| initial | A nonnegative finite number |

## Run the command-line project

Run the example with your own numbers. Vector arguments accept up to 16 comma-separated entries; use `[]` for an empty vector. The imported API accepts longer vectors. Invalid arguments return a nonzero exit status.

```sh
blyxc native-run project.blyx -- "0,16" "100,148" 0
```

## Libraries

- [TransitSpan](https://github.com/Rahulchaube1/blyx-transitspan/tree/v0.1.0) — Summarize observed packet transit differences and arrival reorderings.
- [JitterMean](https://github.com/Rahulchaube1/blyx-jittermean/tree/v0.1.0) — Estimate interarrival jitter with the RFC 3550 one-sixteenth update.

This release includes identical copies of both library modules so a tagged clone can build offline.

## Verification and contributions

The regression suite in [tests.blyx](tests.blyx) checks the example, boundary cases and invalid inputs. Include a short reproducer and your compiler version in [an issue](https://github.com/Rahulchaube1/blyx-cormorant/issues). The source is dual-licensed under [MIT](LICENSE-MIT) or [Apache-2.0](LICENSE-APACHE). The package artwork uses [Lucide icons](https://lucide.dev/license); see [artwork notices](assets/NOTICE.txt).

## Connect with Rahul Chaube

[Portfolio](https://www.rahulchaube1.com/) · [GitHub](https://github.com/Rahulchaube1) · [LinkedIn](https://www.linkedin.com/in/rahulchaube1) · [Hugging Face](https://huggingface.co/oncody) · [X](https://x.com/RahulChaube_) · [EverestQ](https://www.everestqai.com/) · [Contact](https://www.rahulchaube1.com/contact)

[Blyx website](https://www.blyx-lang.space/) · [BlyxTorch](https://www.blyx-lang.space/packages/blyxtorch) · [Handbook](https://doc.blyx-lang.space/) · [Community](https://www.blyx-lang.space/community)

Support Rahul’s open-source work through [GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) or [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube).
