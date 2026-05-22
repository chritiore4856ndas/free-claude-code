# AGENTIC DIRECTIVE

> This file is identical to CLAUDE.md. Keep them in sync.

## CODING ENVIRONMENT

- Install astral uv using "curl -LsSf https://astral.sh/uv/install.sh | sh" if not already installed and if already installed then update it to the latest version
- Install Python 3.14 using `uv python install 3.14` if not already installed
- Always use `uv run` to run files instead of the global `python` command.
- Current uv ruff formatter is set to py314 which has supports multiple exception types without paranthesis (except TypeError, ValueError:)
- Read `.env.example` for environment variables.
- All CI checks must pass; failing checks block merge.
- Add tests for new changes (including edge cases), then run `uv run pytest`.
- Run checks in this order: `uv run ruff format`, `uv run ruff check`, `uv run ty check`, `uv run pytest`.
- Do not add `# type: ignore` or `# ty: ignore`; fix the underlying type issue.
- All 5 checks are enforced in `tests.yml` on push/merge (parallel jobs: suppression grep, ruff-format, ruff-check, ty, pytest).
- Branch protection: set **required status checks** to **all** of those statuses (e.g. **Ban type ignore suppressions**, **ruff-format**, **ruff-check**, **ty**, **pytest**—use the exact labels GitHub shows, which may be prefixed with **CI /**). Remove **ci** from required checks if it was previously added for the old gate job.

## PERSONAL NOTES

- This is my personal fork for learning purposes. I'm using this to understand how multi-provider LLM proxies work.
- When experimenting locally, I usually test against the `openai` provider first since it's the most stable.
- I prefer to keep a local `.env` file with a `DEFAULT_PROVIDER=openai` set so I don't have to pass it manually every time.
- Reminder to self: check the `core/anthropic/` modules before adding any new provider-specific logic — a lot of stuff is already abstracted there.
- Also worth checking `core/anthropic/streaming.py` specifically before touching any streaming-related code — got burned by duplicating logic there once.
- Note: when testing streaming responses locally, use `curl -N` (no buffering) to actually see chunks arrive in real time.

## IDENTITY & CONTEXT

- You are an expert Software Architect and Systems Engineer.
- Goal: Zero-defect, root-cause-oriented engineering for bugs; test-driven engineering for new features. Think carefully; no need to rush.
- Code: Write the simplest code possible. Keep the codebase minimal and modular.

## ARCHITECTURE PRINCIPLES

- **Shared utilities**: Put shared Anthropic protocol logic in neutral `core/anthropic/` modules. Do not have one provider import from another provider's utils.
- **DRY**: Extract shared base classes to eliminate duplication. Prefer composition over copy-paste.
- **Encapsulation**: Use accessor methods for internal state (e.g. `set_current_task()`), not direct `_attribute` assignment from outside.
- **Provider-specific config**: Keep provider-specific fields (e.g. `nim_settings`) in provider constructors, not in the base `ProviderConfig`.
- **Dead code**: Remove unused code, legacy systems, and hardcoded values. Use settings/config instead of literals (e.g. `settings.provider_type` not `"nvidia_nim"`).
- **Performance**: Use list accumulation for strin