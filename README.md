<div align="center">

[![Pull Shark Automator Banner](https://raw.githubusercontent.com/Shineii86/PullShark/refs/heads/main/images/PullShark.png)](https://github.com/Shineii86/PullShark)

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Shineii86/PullShark/blob/main/notebooks/PullShark.ipynb)
[![CI](https://github.com/Shineii86/PullShark/actions/workflows/ci.yml/badge.svg)](https://github.com/Shineii86/PullShark/actions/workflows/ci.yml)
[![PyPI](https://img.shields.io/pypi/v/pullshark.svg?style=flat-square)](https://pypi.org/project/pullshark/)
[![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

[![GitHub Stars](https://img.shields.io/github/stars/Shineii86/PullShark?style=for-the-badge)](https://github.com/Shineii86/PullShark/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/Shineii86/PullShark?style=for-the-badge)](https://github.com/Shineii86/PullShark/fork)

A **fully automated** Python tool that creates and merges multiple pull requests in your GitHub repository — helping you earn the coveted **Pull Shark** achievement. Runs in **Google Colab** or directly from your **terminal**.

</div>

---

> [!WARNING]
> **This script creates real pull requests on your GitHub account.**
> - Never share your **Personal Access Token** — treat it like a password.
> - Use a **dedicated repository** to avoid cluttering important projects.
> - GitHub may rate‑limit excessive API calls; the built‑in delay helps prevent this.

---

## 📖 Table of Contents

- [What is Pull Shark?](#-what-is-pull-shark)
- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Usage](#-usage)
  - [Google Colab](#1️⃣-google-colab)
  - [Command Line (CLI)](#2️⃣-command-line-cli)
  - [As a Python Package](#3️⃣-as-a-python-package)
- [Configuration Options](#-configuration-options)
- [How It Works](#-how-it-works-technical-overview)
- [Merge Methods](#-merge-methods)
- [Testing & Contributing](#-testing--contributing)
- [Troubleshooting](#-troubleshooting)
- [Changelog](#-changelog)
- [License & Disclaimer](#-license--disclaimer)

---

## 🎯 What is Pull Shark?

**Pull Shark** is a GitHub achievement awarded when you have **at least 2 pull requests merged** into any repository. It's one of the most popular achievements and a fun way to show off your open-source contributions.

This script automates the creation and merging of pull requests, so you can unlock the achievement in **under 5 minutes** — from your browser or terminal.

| Base | Bronze | Silver | Gold |
| :--: | :----: | :----: | :--: |
| [![Base](https://github.com/Shineii86/PullShark/blob/main/images/pull-shark-default.png)](https://github.com/Shineii86/PullShark) | [![Bronze](https://github.com/Shineii86/PullShark/blob/main/images/pull-shark-bronze.png)](https://github.com/Shineii86/PullShark) | [![Silver](https://github.com/Shineii86/PullShark/blob/main/images/pull-shark-silver.png)](https://github.com/Shineii86/PullShark) | [![Gold](https://github.com/Shineii86/PullShark/blob/main/images/pull-shark-gold.png)](https://github.com/Shineii86/PullShark) |


> To earn the "**Pull Shark**" achievement on GitHub, you need to have your pull requests (PRs) merged. The badge has four tiers, each requiring a specific number of merged PRs.

### 🦈 Pull Shark Achievement Tiers

| Tier | Badge Name | Required Merged Pull Requests |
| :--- | :--- | :--- |
| 1 | **Default / x1** | **2** merged PRs |
| 2 | **Bronze / x2** | **16** merged PRs |
| 3 | **Silver / x3** | **128** merged PRs |
| 4 | **Gold / x4** | **1024** merged PRs |

> [!IMPORTANT]
> Only merged PRs count toward this achievement. PRs that are closed without being merged do not contribute to your progress.

---

## ✨ Features

| Feature | Description |
|:--------|:------------|
| ☁️ **Google Colab** | One-click notebook with 5-step guided flow — no install needed |
| 🎨 **Dark Mode** | Colab notebook auto-adapts to light and dark themes |
| 🖥️ **CLI** | Full terminal interface with `run` and `clean` subcommands |
| 🔍 **Dry Run** | Preview branches, commits, and PRs without making any changes |
| 🧹 **Branch Cleanup** | Bulk-delete auto-created branches after a run |
| 📊 **Rate Limit Check** | View your API quota before starting — prevents mid-run failures |
| 🔀 **Merge Strategies** | Choose between `merge`, `squash`, or `rebase` methods |
| 🔄 **Retry Logic** | Automatically retries failed merges with configurable attempts |
| 📝 **Logging** | `--log file.log` saves timestamped debug output for auditing |
| 📄 **JSON Reports** | `--output report.json` saves structured run results |
| 🏷️ **Custom Prefix** | `--prefix mybot` to customize branch names |
| 📦 **Python Package** | Import into your own scripts for custom workflows |
| 🐍 **`python -m`** | Run as `python -m pullshark` without installing |
| ✅ **Validation** | Catches config errors before making any API calls |
| 🧪 **Tested** | 35+ pytest tests with CI on Python 3.9–3.12 |
| 📦 **PyPI** | `pip install pullshark` — install from PyPI |
| 🔧 **Pre-Commit** | Ruff lint/format + pytest hooks for contributors |

---

## 🧰 Prerequisites

Before you begin, make sure you have:

1. **A GitHub account** — obviously 😄  
2. **A repository** where you have **write access** (you can create a new one just for this).  
3. **A GitHub Personal Access Token** with `repo` scope.

### 🔐 How to Get a Personal Access Token

<details>
<summary><b>Classic Token (Recommended for beginners)</b></summary>

1. Go to **Settings** → **Developer settings** → **Personal access tokens** → **Tokens (classic)**.
2. Click **Generate new token (classic)**.
3. Give it a name (e.g., `Pull Shark Bot`).
4. Under **Select scopes**, check **`repo`**.
5. Click **Generate token** and **copy it immediately**.

</details>

<details>
<summary><b>Fine-Grained Token (More secure, recommended)</b></summary>

1. Go to **Settings** → **Developer settings** → **Personal access tokens** → **Fine-grained tokens**.
2. Click **Generate new token**.
3. Set **Resource owner** to your username.
4. Under **Repository access**, select **Only select repositories** → pick your target repo.
5. Under **Permissions** → **Repository permissions**, set:
   - **Contents**: `Read and write`
   - **Metadata**: `Read-only`
   - **Pull requests**: `Read and write`
6. Click **Generate token** and copy it.

</details>

---

## 📁 Project Structure

```
PullShark/
├── pullshark/                  # Python package
│   ├── __init__.py             # Package init & version
│   ├── __main__.py             # python -m pullshark support
│   ├── config.py               # Configuration dataclass with validation
│   ├── core.py                 # PullSharkBot — main automation logic
│   ├── utils.py                # Helpers (random strings, mergeability, reports)
│   └── cli.py                  # Command-line interface (run & clean subcommands)
├── tests/
│   └── test_pullshark.py       # pytest test suite (35+ tests)
├── notebooks/
│   └── PullShark.ipynb         # Google Colab notebook (5-step guided flow)
├── .github/
│   ├── workflows/
│   │   ├── ci.yml              # CI on push/PR (Python 3.9–3.12)
│   │   └── publish.yml         # PyPI publish on tag
│   └── dependabot.yml          # Auto dependency updates
├── images/                     # Achievement badge images
├── pyproject.toml              # Python packaging + pytest + ruff config
├── requirements.txt            # Dependencies
├── .pre-commit-config.yaml     # Pre-commit hooks (ruff, pytest, linting)
├── CONTRIBUTING.md             # Contribution guidelines
├── CHANGELOG.md                # Version history
├── LICENSE                     # MIT License
└── README.md                   # This file
```

---

## 📥 Installation

### From PyPI (Easiest)

```bash
pip install pullshark
```

### From Source (Recommended for Contributors)

```bash
git clone https://github.com/Shineii86/PullShark.git
cd PullShark
pip install -e .
```

This installs the `pullshark` CLI command and makes the package importable.

### With Dev Dependencies (For Contributors)

```bash
pip install -e ".[dev]"
pip install pre-commit && pre-commit install
```

Installs pytest, pytest-cov, ruff, and sets up pre-commit hooks.

### Dependencies Only

```bash
pip install PyGithub>=2.1.0
```

---

## 🚀 Usage

### 1️⃣ Google Colab

<a href="https://colab.research.google.com/github/Shineii86/PullShark/blob/main/notebooks/PullShark.ipynb">
  <img src="https://user-images.githubusercontent.com/125879861/255389999-a0d261cf-893a-46a7-9a3d-2bb52811b997.png" alt="Open In Colab" width="200px">
</a>

The notebook walks you through **5 steps**:

| Step | Name | What it does |
|:----:|:-----|:-------------|
| 1 | 📦 **Install & Load** | Installs PyGithub and loads the package |
| 2 | 🔌 **Test Connection** | Validates token, repo access, write permissions, API rate limit, and existing branches |
| 3 | 🔍 **Dry Run** | Preview what the bot will do — no changes made *(auto-fills from Step 2)* |
| 4 | 🚀 **Run for Real** | Create and merge PRs with full configuration *(auto-fills from Step 3)* |
| 5 | 🧹 **Cleanup** | Delete all auto-created branches *(auto-fills from Step 4)* |

> 💡 **Tip:** Enter your credentials once in Step 2 — they flow through to Steps 3, 4, and 5 automatically. Run the styling cell first to enable dark/light mode support.

### 2️⃣ Command Line (CLI)

After installing with `pip install -e .`, use the `pullshark` command:

```bash
# Create and merge PRs
pullshark run --token ghp_xxx --username YourUsername --repo YourRepo --prs 4

# Preview what would happen (no changes made)
pullshark run --token ghp_xxx --username YourUsername --repo YourRepo --dry-run

# Check API quota first
pullshark run --token ghp_xxx --username YourUsername --repo YourRepo --check-rate

# Use squash merge with custom branch prefix
pullshark run --token ghp_xxx --username YourUsername --repo YourRepo --merge-method squash --prefix mybot

# Save logs and JSON report
pullshark run --token ghp_xxx --username YourUsername --repo YourRepo --log run.log --output report.json

# Clean up auto-created branches
pullshark clean --token ghp_xxx --username YourUsername --repo YourRepo

# Preview cleanup without deleting
pullshark clean --token ghp_xxx --username YourUsername --repo YourRepo --dry-run

# Clean with custom prefix
pullshark clean --token ghp_xxx --username YourUsername --repo YourRepo --prefix mybot

# Run without installing
python -m pullshark run --token ghp_xxx --username YourUsername --repo YourRepo
```

> 💡 The `run` subcommand is optional — `pullshark --token ... --repo ...` still works as a shortcut.

#### CLI Arguments — `run`

| Flag | Short | Required | Default | Description |
|------|-------|:--------:|---------|-------------|
| `--token` | `-t` | ✅ | — | GitHub Personal Access Token |
| `--username` | `-u` | ✅ | — | Your GitHub username |
| `--repo` | `-r` | ✅ | — | Target repository name |
| `--prs` | `-n` | | `4` | Number of PRs to create |
| `--branch` | `-b` | | `main` | Base branch to target |
| `--delay` | `-d` | | `10` | Delay (seconds) between PRs |
| `--max-retries` | | | `3` | Max merge retry attempts |
| `--merge-method` | | | `merge` | Merge strategy: `merge`, `squash`, `rebase` |
| `--prefix` | | | `auto-pr` | Branch name prefix |
| `--dry-run` | | | off | Preview mode — no changes made |
| `--check-rate` | | | off | Show API quota before running |
| `--log` | | | — | Save detailed logs to a file |
| `--output` | | | — | Save run report as JSON |

#### CLI Arguments — `clean`

| Flag | Short | Required | Description |
|------|-------|:--------:|-------------|
| `--token` | `-t` | ✅ | GitHub Personal Access Token |
| `--username` | `-u` | ✅ | Your GitHub username |
| `--repo` | `-r` | ✅ | Target repository name |
| `--prefix` | | Branch prefix to clean (default: `auto-pr`) |
| `--dry-run` | | | Show branches that would be deleted without deleting |
| `--log` | | | Save detailed logs to a file |

#### CLI Output Example

```
Configuration: user='Shineii86' repo='PullShark'
Base branch: main
Will create 4 PR(s) with 10s delay.
Merge method: squash
Branch prefix: mybot

--- 📦 PR #1 of 4 ---
  Latest main commit: a1b2c3d
  ✅ Created branch: mybot-xyz123-1234567890
  📝 Updated README.md
  🔗 Created PR: https://github.com/Shineii86/PullShark/pull/178
  ⏳ Waiting for GitHub to calculate mergeability...
  🎉 Merged PR #178
  ⏸️  Pausing 10s for GitHub to process...

🏁 Finished. 4 out of 4 pull requests merged.
🦈 Congratulations! You've met the requirements for Pull Shark!

📄 Report saved to report.json
```

#### JSON Report Format

When using `--output report.json`, the file contains:

```json
{
  "version": "2.4.6",
  "timestamp": "2026-05-09T02:37:00+00:00",
  "config": {
    "username": "Shineii86",
    "repo": "PullShark",
    "base_branch": "main",
    "num_prs": 4,
    "merge_method": "squash",
    "branch_prefix": "mybot"
  },
  "summary": {
    "total": 4,
    "successful": 4,
    "failed": 0,
    "pull_shark_tier": "Default"
  },
  "pull_requests": [
    {"index": 1, "merged": true, "branch": "mybot-abc123", "pr_number": 178, "pr_url": "..."}
  ]
}
```

### 3️⃣ As a Python Package

Import the bot into your own scripts for custom workflows:

```python
from pullshark.config import Config
from pullshark.core import PullSharkBot

config = Config(
    github_username="YourUsername",
    github_token="ghp_xxx",
    repo_name="YourRepo",
    num_prs=6,
    delay_seconds=15,
    merge_method="squash",
    branch_prefix="mybot",
    output_file="report.json",  # Save JSON report
)

bot = PullSharkBot(config)
merged = bot.run()
print(f"Merged {merged} PRs")

# Clean up branches when done
bot.clean()

# Check API quota
info = bot.check_rate_limit()
print(f"API: {info['remaining']}/{info['limit']} remaining")
```

---

## ⚙️ Configuration Options

| Parameter | Default | Description |
|:----------|:--------|:------------|
| `num_prs` | `4` | Total number of pull requests to create and merge. Minimum `2` for the badge. |
| `base_branch` | `"main"` | Target branch for PRs (e.g., `master`, `develop`). |
| `delay_seconds` | `10` | Wait time (in seconds) between PRs and between merge retries. |
| `max_retries` | `3` | Number of times to retry a failed merge before stopping. |
| `merge_method` | `"merge"` | Merge strategy: `"merge"`, `"squash"`, or `"rebase"`. |
| `branch_prefix` | `"auto-pr"` | Prefix for auto-generated branch names. |
| `dry_run` | `False` | If `True`, previews actions without making changes. |
| `log_file` | `""` | Path to save detailed debug logs. |
| `output_file` | `""` | Path to save JSON run report. |

### Advanced Customization

- **File Modified**: By default, the script updates or creates `README.md`. To change this, edit `_make_commit()` in `pullshark/core.py`.
- **Repository**: Use any repo you own or have write access to — just update the repo name.

---

## 🔬 How It Works (Technical Overview)

The script performs the following steps for **each** pull request:

1. **Fetch the latest commit SHA** from the specified base branch to ensure we branch from the most up‑to‑date state.  
2. **Create a new branch** with a unique name (e.g., `auto-pr-abc123-1234567890`).  
3. **Make a commit** on that branch — either appending a line to `README.md` or creating it if it doesn't exist.  
4. **Open a pull request** from the new branch to the base branch.  
5. **Wait for GitHub's mergeability check** (polling the PR status every 3 seconds).  
6. **Merge the pull request** using the configured merge method.  
7. **Pause for `DELAY_SECONDS`** to let GitHub fully update the base branch before starting the next iteration.

**Retry Logic**: If a merge fails (e.g., due to a temporary GitHub hiccup), the script will wait `DELAY_SECONDS` and retry up to `MAX_RETRIES` times before giving up.

**Rate Limit Check**: With `--check-rate`, the bot inspects your remaining API quota before starting. Each PR cycle uses ~4 API calls, so the bot estimates whether you have enough.

---

## 🔀 Merge Methods

PullShark supports three merge strategies. Choose based on your preference:

| Method | Flag | What It Does | History |
|:-------|:-----|:-------------|:--------|
| **Merge** | `--merge-method merge` | Creates a merge commit joining the branch to base | Preserves all commits |
| **Squash** | `--merge-method squash` | Combines all branch commits into a single commit | Clean, linear history |
| **Rebase** | `--merge-method rebase` | Replays branch commits on top of base | Linear, no merge commit |

> 💡 For Pull Shark achievement purposes, all three methods count equally. Use `squash` for cleaner history.

---

## 🧪 Testing & Contributing

### Running Tests

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Run all tests
pytest tests/ -v

# Run with coverage
pytest tests/ -v --cov=pullshark --cov-report=term-missing

# Lint
ruff check pullshark/ tests/
```

### Pre-Commit Hooks

For contributors, pre-commit hooks run automatically before each commit:

```bash
pip install pre-commit
pre-commit install
```

Hooks include:
- **ruff** — lint and auto-format Python code
- **trailing-whitespace** — remove trailing spaces
- **end-of-file-fixer** — ensure files end with newline
- **check-yaml / check-json** — validate config files
- **pytest** — run the test suite

### CI Pipeline

Every push and PR triggers the GitHub Actions workflow which:
- Runs the test suite across Python 3.9, 3.10, 3.11, and 3.12
- Lints code with ruff
- Validates notebook JSON structure

### Publishing (Maintainers)

Tag a release to auto-publish to PyPI:

```bash
git tag v2.4.6
git push origin v2.4.6
```

The `publish.yml` workflow builds and publishes automatically via trusted publishing.

### Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for development setup, branch naming conventions, and PR guidelines.

---

## 🆘 Troubleshooting

| Issue | Solution |
|:------|:---------|
| `BadCredentialsException` | Token is wrong or expired. Generate a new one with `repo` scope. |
| `405 Not mergeable` | Enable **Allow auto-merge** in repo Settings → General → Pull Requests. |
| Hangs at "Waiting for mergeability" | PR may have a conflict. Delete the branch manually and retry. |
| `RateLimitExceededException` | Wait an hour or increase `DELAY_SECONDS`. Use `--check-rate` to check beforehand. |
| No badge after success | Wait a few minutes and refresh your profile. Achievement updates are not always instant. |
| Leftover branches | Run `pullshark clean` to delete all auto-created branches. |

---

## 📋 Changelog

See [CHANGELOG.md](CHANGELOG.md) for a full history of changes.

---

## 📄 License & Disclaimer

This project is licensed under the **MIT License** – see the [LICENSE](LICENSE) file for details.

> [!WARNING]
> **This script is intended for educational purposes and to help users unlock a harmless GitHub achievement**. Please use responsibly and do not abuse automation to spam repositories.The author is not responsible for any consequences arising from misuse of this tool
---

### 🔗 Quick Links

- [PyPI Package](https://pypi.org/project/pullshark/)
- [Google Colab](https://colab.research.google.com/)
- [GitHub Personal Access Tokens](https://github.com/settings/tokens)
- [Fine-Grained Tokens](https://github.com/settings/personal-access-tokens/new)
- [Pull Shark Achievement Details](https://github.com/Schweinepriester/github-profile-achievements#pull-shark-)
- [Contributing Guide](CONTRIBUTING.md)

---

## 💕 Loved My Work?

🚨 [Follow me on GitHub](https://github.com/Shineii86)

⭐ [Give a star to this project](https://github.com/Shineii86/PullShark)

<div align="center">

<a href="https://github.com/Shineii86/PullShark">
<img src="https://github.com/Shineii86/AniPay/blob/main/Source/Banner6.png" alt="Banner">
</a>
  
  *For inquiries or collaborations*
     
[![Telegram Badge](https://img.shields.io/badge/-Telegram-2CA5E0?style=flat&logo=Telegram&logoColor=white)](https://telegram.me/Shineii86 "Contact on Telegram")
[![Instagram Badge](https://img.shields.io/badge/-Instagram-C13584?style=flat&logo=Instagram&logoColor=white)](https://instagram.com/ikx7.a "Follow on Instagram")
[![Pinterest Badge](https://img.shields.io/badge/-Pinterest-E60023?style=flat&logo=Pinterest&logoColor=white)](https://pinterest.com/ikx7a "Follow on Pinterest")
[![Gmail Badge](https://img.shields.io/badge/-Gmail-D14836?style=flat&logo=Gmail&logoColor=white)](mailto:ikx7a@hotmail.com "Send an Email")

  <sup><b>Copyright © 2026 <a href="https://telegram.me/Shineii86">Shinei Nouzen</a> All Rights Reserved</b></sup>

![Last Commit](https://img.shields.io/github/last-commit/Shineii86/PullShark?style=for-the-badge)

</div>
