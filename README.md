# Software development, automation & data processing

Focused scripts and small fixes for repetitive work: CSV cleanup, JSON conversion, file inventories, and reproducible checks.

For a project inquiry, share a redacted input sample, the expected output, approximate data size, operating system, and deadline. Scope, price, delivery time, and acceptance checks are agreed before implementation.

[Discuss a project on Contra](https://contra.com/s/l7YZeAqs-data-cleanup-and-file-processing-automation) · [Browse the source examples](https://github.com/codeofwxz/automation-portfolio-demos)

## Open-source contributions

- **Merged — [python-markdown2 #724](https://github.com/trentm/python-markdown2/pull/724):** Reduced repeated full-text scans during Markdown token expansion while preserving nested content. Added regression coverage and a reproducible benchmark.
- **Merged — [pyexcel #314](https://github.com/pyexcel/pyexcel/pull/314):** Fixed rendering of `timedelta` values in Sheet string output.
- **Awaiting upstream review — [dataclass-wizard #257](https://github.com/rnag/dataclass-wizard/pull/257):** Added focused environment-name compatibility with regression coverage for lookup precedence, aliases and prefixes. The latest test-only update adds three empty-value precedence cases; all 80 environment tests pass on Python 3.12 and 3.14. This is targeted test coverage, not a full-suite or hosted CI result.

## Three runnable examples

These are self-directed demonstrations using synthetic data, not paid client projects. Each includes source code, sample files, CLI tests, and documented limits. The linked repository retains the implementation and testing provenance.

| Example | Input → output | How to check the result |
| --- | --- | --- |
| [CSV cleanup](https://github.com/codeofwxz/automation-portfolio-demos/tree/main/csv-cleanup) | A three-column CSV → normalized rows plus a rejection report for missing or duplicate IDs. Email domains are lowercased; local-part casing is preserved. | The bundled example accepts 3 rows and rejects 2. Compare both files with the supplied expected CSVs. |
| [JSONL order export](https://github.com/codeofwxz/automation-portfolio-demos/tree/main/json-export) | Nested orders → one CSV row per item, with validated quantities and exact decimal line totals. | The bundled example produces 3 item rows matching `expected.csv`. Invalid input reports its physical line. |
| [File inventory](https://github.com/codeofwxz/automation-portfolio-demos/tree/main/file-manifest) | A directory → a sorted manifest of paths, sizes, and SHA256 hashes; verification → added, missing, and changed files. | The baseline matches `samples/before`. Comparing `samples/after` reports `added.txt`, `removed.txt`, and `notes.txt` in the respective categories. |

## Run and verify

Use Python 3.10+ and Git. The examples use only Python's standard library. Clone into a new directory:

```sh
git clone https://github.com/codeofwxz/automation-portfolio-demos.git
cd automation-portfolio-demos
```

Then run each example from its own folder:

```sh
cd csv-cleanup
python cleanup.py examples/input.csv
python -B -m unittest -v
```

```sh
cd ../json-export
python export_orders.py demo.jsonl demo-output.csv
python -B -m unittest -v
```

```sh
cd ../file-manifest
python manifest.py create samples/before example-manifest.json
python manifest.py verify samples/before example-manifest.json
python manifest.py verify samples/after example-manifest.json
python -B -m unittest -v
```

The final `verify` command deliberately returns exit code **1** because the sample directory differs; matching verification returns **0**. Existing output files are refused, so choose new output filenames when repeating the examples. The JSON exporter requires a filesystem that supports hard links, such as local NTFS.

The three suites define 15 tests. On the checked Windows environment, 14 passed and the symlink-creation test was explicitly skipped because the OS did not permit it. The README in each folder explains its checks and limitations: email normalization does not verify deliverability; the exporter does not calculate tax or convert currencies; a file manifest is not a backup or an atomic snapshot.

## What a scoped delivery includes

- Source code and practical setup/usage instructions.
- Checks against agreed input/output examples, including relevant failure cases.
- A concise handover covering supported inputs, known limitations, and how to rerun verification.

Start with a small, testable task. Use synthetic or redacted samples for the initial discussion; keep credentials and private customer records out of public issues.
