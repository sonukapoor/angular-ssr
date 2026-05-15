# angular-ssr

An [Agent Skill](https://agentskills.io) that guides AI coding assistants to correctly set up Angular SSR, diagnose NG05xx hydration errors, and apply SSR patterns in Angular v17+ applications.

Works with Claude Code, GitHub Copilot, OpenAI Codex, Cursor, Gemini CLI, and any other agent that supports the [Agent Skills](https://agentskills.io) open standard.

---

## What it does

- **Setup** — correct wiring of `provideClientHydration()`, HTTP Transfer State, incremental hydration, engine selection, and server route configuration
- **Diagnose** — structured 7-step root cause process for NG05xx hydration errors before suggesting any fix
- **Patterns** — correct vs incorrect patterns for DOM access, platform detection, browser-only APIs, and per-request server providers
- **Anti-pattern blacklist** — stops the AI from reaching for `ngSkipHydration`, `isPlatformBrowser` in templates, or `typeof window !== 'undefined'` as a first instinct

### NG05xx errors covered

| Code | Meaning |
|---|---|
| NG0500 | Missing hydration annotations |
| NG0501 | Skip hydration flag on mismatched node |
| NG0502 | No hydration info in server response |
| NG0503 | Node not found / DOM mismatch |
| NG0506 | Application unstable (stability timeout) |

---

## Installation

Clone this repo into your agent's skills directory:

### Claude Code
```bash
git clone https://github.com/sonukapoor/angular-ssr ~/.claude/skills/angular-ssr
```

### OpenAI Codex
```bash
git clone https://github.com/sonukapoor/angular-ssr ~/.codex/skills/angular-ssr
```

### Gemini CLI
```bash
git clone https://github.com/sonukapoor/angular-ssr ~/.gemini/skills/angular-ssr
```

### Other agents
See [agentskills.io/clients](https://agentskills.io/clients) for your agent's skills directory path.

---

## Requirements

- Angular v17 or later
- `@angular/ssr` (built-in SSR — not Angular Universal)

---

## Scope

Covers the modern Angular SSR stack:

- `provideClientHydration()`, `withEventReplay()`, `withIncrementalHydration()`
- `AngularNodeAppEngine`, `CommonEngine`, `AngularAppEngine`
- HTTP Transfer State with `withHttpTransferCacheOptions()`
- `afterNextRender`, `DOCUMENT` token, `REQUEST` / `RESPONSE_INIT` / `REQUEST_CONTEXT` tokens
- Server route configuration with `RenderMode`
- i18n hydration support with `withI18nSupport()`

Does **not** cover Angular Universal / v16 and earlier, noop-zone SSR, or platform-specific adapters (Netlify, Vercel edge).

---

## Contributing

Issues and PRs welcome. If you find a pattern that AI assistants consistently get wrong in Angular SSR, open an issue with a reproduction and it'll be added to the skill.
