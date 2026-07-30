# Security Standards

## Why this exists now, not later

This isn't hypothetical. Across the sessions that built BVOS, Career Ops, and Colburn Auctions, real credentials have already moved through AI chat sessions multiple times: a GitHub personal access token, Supabase project keys, admin login credentials for a client site. That's the actual current pattern of how this work gets done — so the standard needs to match reality, not aspiration.

## Secrets handling

1. **Never commit secrets to any repository.** No API keys, tokens, or passwords in code, config files, or commit history — use environment variables (`.env`, excluded via `.gitignore`) or the hosting platform's own secret storage (Vercel Environment Variables, Supabase project settings).
2. **Prefer scoped tokens over broad ones.** A token scoped to one repo with only the permissions a task needs is safer than a full-account token reused across unrelated projects. Full-`repo`-scope personal access tokens have been used out of convenience in past sessions — acceptable for now given the single-operator reality, but fine-grained tokens are the better default going forward.
3. **Rotate tokens after single-use tasks are done**, especially any token that was shared in a chat conversation. A credential that's been typed into an AI chat session should be treated as more exposed than one that's only ever lived in a password manager.
4. **Strip tokens from git remote URLs immediately after use.** When a token is used inline in a git remote (`https://x-access-token:TOKEN@github.com/...`) for a push, reset the remote to the token-free URL right after — don't leave it sitting in local git config.

## Access model across AI platforms

See `01_GOVERNANCE.md` for the full write-access discussion. Short version: every platform currently authenticates as the Founder, so there's no way to scope "what Claude can touch" separately from "what ChatGPT can touch" today. Treat any credential shared with one platform as effectively shared with all of them until separate machine identities exist.

## What's explicitly out of scope for now

Formal security review processes, dependency scanning, and infrastructure hardening beyond the above — not warranted yet at current scale (personal projects + one live client). Revisit once the Agency has multiple concurrent clients or the products handle more sensitive data than an auction catalog.
