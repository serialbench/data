# serialbench data

Benchmark results for Ruby serialization libraries. Pure data — no code,
no workflows. One dated directory per run attempt.

## Format

```
runs/
  2026-08-30/                              # UTC date of the run
    ubuntu-24.04-ruby-3.4.xml.yaml         # platform × ruby × format
    ubuntu-24.04-ruby-3.4.json.yaml
    macos-26-intel-ruby-4.0.xml.yaml
    ...
```

### File naming

`{platform}-ruby-{ruby-version}.{format}.yaml`

- `platform`: the GitHub Actions runner label (e.g., `ubuntu-24.04`,
  `macos-26-intel`, `windows-11-arm`)
- `ruby-version`: the Ruby version (e.g., `3.4`, `4.0`)
- `format`: `xml`, `json`, `yaml`, or `toml`

### YAML schema

Each file is the exact output of
`serialbench environment execute <env> <config> <output>`. See the
[serialbench gem](https://github.com/serialbench/serialbench) for the
schema definition.

Key sections:
- `platform`: the platform this ran on (os, arch, ruby version)
- `benchmark_result.serializers`: the libraries benchmarked and their versions
- `benchmark_result.parsing/generation/streaming`: per-serializer throughput
- `benchmark_result.memory`: per-serializer memory allocation

## Rules

- Files are **append-only**: never modified once committed
- A run with 30/46 legs deposits 30×4 files — partial data is valid
- The [site](https://github.com/serialbench/serialbench.github.io) derives
  everything (availability, versions, trends) from these files at build time
