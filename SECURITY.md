# Security Policy

## Supported versions

This repository tracks active development on the `main` branch. Security fixes
are applied to `main` only; there are no maintained release branches at this
time.

| Version | Supported          |
| ------- | ------------------ |
| `main`  | :white_check_mark: |
| Older commits / forks | :x: |

## Reporting a vulnerability

**Please do not file a public GitHub issue for security problems.**

Preferred channel — GitHub Private Vulnerability Reporting:

- https://github.com/AMD-AGI/HF_PEFT_GPT_OSS/security/advisories/new

Fallback — AMD Product Security Incident Response Team (PSIRT):

- Email: **psirt@amd.com**
- Reference: https://www.amd.com/en/resources/product-security.html

When reporting, please include:

- A description of the issue and its potential impact.
- Steps to reproduce (commands, config, hardware/container if relevant).
- Affected commit SHA or branch.
- Any proof-of-concept, logs, or sample inputs.
- Your name / handle for credit (optional).

## Response expectations

- **Acknowledgement:** within **5 business days** of receipt.
- **Triage & status update:** within **15 business days**.
- **Fix or documented mitigation:** target within **90 days**, depending on
  severity and complexity.
- We follow **coordinated disclosure**: please give us a reasonable window to
  investigate and ship a fix before public disclosure. We are happy to credit
  reporters in the resulting advisory.

## Scope

This repository contains training/fine-tuning code, configs, and shell helper
scripts. Vulnerability classes we are particularly interested in:

- **Code execution / injection** in `train.py`, `utils.py`, or shell scripts
  (e.g. unsafe handling of user-controlled config values, paths, or shell
  arguments).
- **Supply-chain risks** in `requirements_MI300.sh` / `requirements_MI355.sh`
  (typosquatted, malicious, or compromised dependencies).
- **Secret / credential leakage** (e.g. accidentally committed Hugging Face
  tokens, SSH keys, cloud credentials) — please report privately so we can
  rotate before public disclosure.
- **AI/ML-specific issues**:
  - Training-data poisoning vectors introduced by the dataset loading path.
  - Model-weight tampering or unsafe deserialization (`torch.load` of
    untrusted checkpoints).
  - Unsafe defaults that would cause a downstream user to leak prompts, data,
    or fine-tuned weights.

Out of scope:

- Vulnerabilities in upstream dependencies (PyTorch, Transformers, PEFT,
  Accelerate, ROCm, Docker images) — please report those to the respective
  upstream projects. We will, however, update pins/instructions if a known
  upstream CVE affects users of this repo.
- Issues that require the attacker to already have root or container-host
  access.
- Rate-limiting / DoS of the training script itself.

## Handling secrets

Never commit credentials (Hugging Face tokens, cloud keys, etc.) to this
repository. The `.gitignore` excludes `.env` / `.env.*` files. If you discover
a secret in the git history, please report it privately via the channels above
so we can rotate and purge.
