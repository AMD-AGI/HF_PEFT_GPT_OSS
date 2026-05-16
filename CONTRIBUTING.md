# Contributing to HF_PEFT_GPT_OSS

Thanks for your interest in contributing! This repository hosts a reference
recipe for PEFT/LoRA fine-tuning of OpenAI GPT-OSS Mixture-of-Experts models on
AMD MI300/MI355 GPUs with ROCm. We welcome bug reports, fixes, performance
improvements, and documentation updates.

## Filing issues

Please use GitHub Issues. Before opening a new issue, search existing issues to
avoid duplicates. A good bug report includes:

- Hardware (e.g. MI300X / MI355X), ROCm version, container image tag.
- Exact command(s) you ran (e.g. `bash run_peft_lora_openai.sh`).
- Full error message / traceback.
- Minimum config (`configs/`) needed to reproduce.
- What you expected vs. what happened.

For feature requests, describe the use case and, if possible, a sketch of the
proposed change.

## Pull request workflow

1. Fork the repo (external contributors) or create a feature branch in this
   repo (internal AMD-AGI contributors). Branch naming: `<type>/<short-desc>`,
   e.g. `fix/lora-grad-accum`, `perf/mi355-attn-mask`, `docs/readme-clarify`.
2. Make focused, minimal changes. Keep unrelated refactors out of the PR.
3. Run any local checks (see "Code style" and "Testing" below).
4. Open a PR against `main`. Fill in the PR template if present. Link related
   issues with `Fixes #123` / `Refs #123`.
5. Every PR requires:
   - At least **one approval from a non-author** reviewer.
   - **CODEOWNERS** review for any owned paths (see `.github/CODEOWNERS`).
   - All required status checks green.
6. Squash-merge is preferred to keep `main` history readable.

## Code style

- Python: follow PEP 8. We recommend formatting with `black` and linting with
  `ruff` before pushing:
  ```bash
  pip install black ruff
  black .
  ruff check .
  ```
- Keep imports sorted (`ruff check --select I --fix .` or `isort .`).
- Prefer clear, surgical changes over clever one-liners.
- Shell scripts: keep them POSIX-friendly where possible, document any
  hardware-specific assumptions in comments.

## Testing

This repo does not yet ship an automated test suite. At minimum, when changing
training/utility code, please verify:

- `bash requirements_MI300.sh` (or `requirements_MI355.sh`, as applicable)
  still completes inside the documented container.
- A short `bash run_peft_lora_openai.sh` smoke run starts training and
  produces at least one loss step without error.

If you add tests, prefer `pytest` and place them under `tests/`.

## Developer Certificate of Origin (DCO)

By contributing, you certify that you wrote (or have the right to submit) the
contribution under the project's MIT license. Sign off every commit:

```bash
git commit -s -m "your message"
```

This adds a `Signed-off-by: Your Name <you@example.com>` trailer.

## Security

Please **do not** open public GitHub issues for security vulnerabilities. See
[SECURITY.md](SECURITY.md) for the private disclosure process.

## License

By contributing, you agree that your contributions will be licensed under the
MIT License (see [LICENSE](LICENSE)).
