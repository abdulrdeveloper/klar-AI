# Contributing to Klar

Thanks for helping make Klar better. This guide explains how to set up the
project, how we work, and what a good pull request looks like.

By participating you agree to follow our [Code of Conduct](CODE_OF_CONDUCT.md).
Contributions are released under the project's [MIT License](LICENSE).

## Ways to contribute

- Report a bug or suggest a feature by opening an issue.
- Improve documentation or fix typos.
- Improve the tutor prompts or answer modes in `src/lib/chat-runtime.ts`.
- Pick up an issue labelled `good first issue` or `help wanted`.
- Review open pull requests.

For anything security related, do **not** open a public issue. See
[SECURITY.md](SECURITY.md).

## Development setup

Requirements: Node.js 20 or newer and pnpm.

```bash
git clone https://github.com/abdulrdeveloper/klar.git
cd klar
pnpm install
cp .env.local.example .env.local   # then fill in the values, see README.md
pnpm drizzle-kit migrate
pnpm dev
```

The README lists every environment variable. Never commit `.env.local`.

## Workflow

1. **Open or find an issue first** for anything bigger than a small fix, so we
   can agree on the approach before you spend time on it.
2. **Fork** the repository and create a branch from `main`. Every change goes
   through a pull request.
3. Use a descriptive branch name: `feat/short-name`, `fix/short-name`,
   `docs/short-name`, `chore/short-name`.
4. Make your change, keeping it focused. One pull request should do one thing.
5. Run the checks locally (below) and make sure they pass.
6. Open a pull request against `main` and explain what changed and why.

## Checks

```bash
pnpm lint    # eslint
pnpm build   # production build, includes the TypeScript check
```

## Database changes

If you change `src/db/schema.ts`, generate a migration and commit it with your
change:

```bash
pnpm drizzle-kit generate
```

Do not edit migrations that are already on `main`.

## Commit messages

Write short, imperative messages that explain the change, for example
`fix: keep conversation title after rename`. We use the
[Conventional Commits](https://www.conventionalcommits.org/) prefixes
(`feat:`, `fix:`, `docs:`, `chore:`, `refactor:`).

## Pull request checklist

- [ ] The change is focused and the description explains *why*.
- [ ] `pnpm lint` and `pnpm build` pass.
- [ ] Schema changes include a generated migration.
- [ ] Docs are updated if behaviour or setup changed.
- [ ] No secrets, personal data or `.env` files are included.
- [ ] UI changes include a screenshot.

## Code style

- TypeScript. Avoid `any`.
- Follow the existing structure under `src/` and the patterns already used.
- Validate input on the server with `zod` (see `src/lib/validation.ts`); never
  trust the client.
- Check the session and conversation ownership in every API route that reads
  or writes user data.
- Rate limit new endpoints that send email or call an AI provider
  (see `src/lib/rate-limit.ts`).

## Review

A maintainer will review your pull request as soon as they can. Please be
patient and responsive to feedback. Maintainers may ask for changes, or close a
PR that is out of scope; this is never personal.

## Questions

Open an issue labelled `question`.
