# MEOW for Sandflow

A [Sandflow](https://github.com/kafuexe/sandflow) pack that integrates [MEOW](https://github.com/maya8237/MEOW) — the
harness that takes a feature request to a finished MR (plan → implement → test → review → MR, with custom workflows).

Each MEOW command is a block you can drop into any flow. MEOW runs **on your machine** with your own Claude Code
login, in its own worktree of `REPO_PATH`.

| Block | Runs | Exits |
|---|---|---|
| MEOW: feature → MR | `meow run "<input>"` | `delivered` · `mr-not-opened` · `failed` |
| MEOW: plan | `meow plan "<input>"` | `done` · `failed` |
| MEOW: review | `meow review "<input>"` (optionally `--fix`) | `pass` · `fail` |
| MEOW: multi-task sprint → MR | `meow run --orchestrate "<input>"` | `delivered` · `mr-not-opened` · `failed` |
| MEOW: Jira issue → MR | `meow run --jira [KEY]` | `delivered` · `mr-not-opened` · `failed` |
| MEOW: run status | `meow status --verbose` | `found` · `none` |

`<input>` is the block's incoming artifact, or the starting prompt when there is none (or it comes straight from
*Manual start*). Options on the node's Block tab become MEOW flags: workflow (your custom MEOW workflows are listed
when you press reload next to it), feature name, MR target, start branch, in-place delivery, tester, plan file and
workflow inputs.

Flows: **MEOW: feature → MR** (press Run) and **MEOW: GitHub issue → MR** (a new issue → MEOW → comment back).

## Setup

1. Install MEOW (Python 3.12+ and Claude Code signed in):
   - Windows: `irm https://raw.githubusercontent.com/maya8237/MEOW/main/scripts/install.ps1 | iex`
   - macOS / Linux: `curl -fsSL https://raw.githubusercontent.com/maya8237/MEOW/main/scripts/install.sh | sh`
2. In Sandflow: **Packs → Add pack** with this repo's link (or folder), and allow it to run on this machine.
3. Set `REPO_PATH` in the Inputs tab. **Integrations** shows whether `meow` was found and its version.

MEOW installed somewhere off `PATH`? Set `SANDFLOW_MEOW_PATH` to the executable before starting Sandflow.
