<p align="center">
  <img src="public/klar.png" alt="Klar" height="80" />
</p>

<h3 align="center">An AI tutor that gets straight to the point.</h3>

<p align="center">
  Klar is a free, open-source AI tutor for students. Ask a question and start
  chatting right away, or create an account to keep your conversations.
  It answers in English, Roman Urdu or Urdu script.
</p>

<p align="center">
  <a href="https://klar.abdulrdeveloper.me"><strong>klar.abdulrdeveloper.me</strong></a>
</p>

<p align="center">
  <a href="LICENSE"><img alt="License: MIT" src="https://img.shields.io/badge/license-MIT-blue.svg" /></a>
  <img alt="Next.js 16" src="https://img.shields.io/badge/Next.js-16-black.svg" />
  <img alt="React 19" src="https://img.shields.io/badge/React-19-61dafb.svg" />
  <img alt="TypeScript" src="https://img.shields.io/badge/TypeScript-5-3178c6.svg" />
  <img alt="PostgreSQL" src="https://img.shields.io/badge/PostgreSQL-Drizzle-336791.svg" />
  <a href="CONTRIBUTING.md"><img alt="PRs welcome" src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" /></a>
</p>

---

## What is Klar?

Klar is built for school prep, coding help and quick explanations. It is told
to skip filler, guide you through homework before handing over answers, and
reply in the language you write in, with technical terms kept in English.

- **Guests** can open `/chat` and start asking questions without signing up.
- **Account holders** get the full dashboard with saved, per-conversation history.

## What you can do

### Pick how Klar answers

| Mode | Best for |
| --- | --- |
| **Flash** | The fastest answer, in 1 to 3 sentences |
| **Speed** | One-line answers or raw snippets |
| **Smart** | Complex school topics, with the "why" behind the answer |
| **Thinking** | Step-by-step working for math and logic |
| **Coder** | Debugging, reviews and code fixes (Python by default) |
| **Deep** | Long, thorough answers that cover edge cases |

Each mode routes to Mistral first and falls back to Groq if the first provider
is unavailable.

### Keep your conversations
- Sign up with email and password, then verify your email to log in.
- Conversations and messages are saved in PostgreSQL.
- Forgot your password? Reset it with an emailed link.

### Safe by default
- The dashboard is protected by middleware that checks a signed JWT session cookie.
- Passwords are hashed with bcrypt.
- Upstash Redis rate limits chat, registration, login and verification or
  password-reset emails.
- Email links always point to the production URL, so request headers cannot
  redirect them.

## Run it yourself

### You need

- **Node.js 20+** and **pnpm**
- A **PostgreSQL** database (for example [Neon](https://neon.tech))
- API keys for **Groq** and **Mistral**
- A **Resend** API key for verification and reset emails
- An **Upstash Redis** database for rate limiting

### Quick start

```bash
git clone https://github.com/abdulrdeveloper/klar.git
cd klar
pnpm install
cp .env.local.example .env.local   # then fill in the values
pnpm drizzle-kit migrate           # create the database tables
pnpm dev
```

Open **http://localhost:3000**.

### Configuration

| Variable | What it is |
| --- | --- |
| `DATABASE_URL` | PostgreSQL connection string |
| `JWT_SECRET` | Long random string used to sign session cookies |
| `GROQ_API_KEY` | Groq API key (fallback provider) |
| `MISTRAL_API_KEY` | Mistral API key (primary provider) |
| `RESEND_API_KEY` | Resend API key for transactional email |
| `UPSTASH_REDIS_REST_URL` | Upstash Redis REST URL |
| `UPSTASH_REDIS_REST_TOKEN` | Upstash Redis REST token |

All variables are required. The app will not start without `JWT_SECRET` and
the Upstash variables.

The public URL used in email links is set in `src/lib/request-security.ts`.
Change it there if you host your own copy.

Never commit `.env.local`.

## Tech stack

| Area | Tools |
| --- | --- |
| Framework | Next.js 16 (App Router), React 19, TypeScript |
| UI | Tailwind CSS 4, Lucide icons, React Markdown |
| AI | Vercel AI SDK with Mistral and Groq |
| Data | PostgreSQL (Neon) with Drizzle ORM |
| Auth | JWT session cookies (`jose`), bcrypt, Zod validation |
| Email | Resend |
| Rate limiting | Upstash Redis |

## Useful commands

| Command | What it does |
| --- | --- |
| `pnpm dev` | Start the dev server |
| `pnpm build` / `pnpm start` | Production build and server |
| `pnpm lint` | ESLint |
| `pnpm drizzle-kit generate` | Create a migration after changing the schema |
| `pnpm drizzle-kit migrate` | Apply migrations to the database |

## Project layout

```text
src/app/              Pages and API routes (Next.js App Router)
src/app/chat/         Guest chat
src/app/dashboard/    Logged-in chat with saved history
src/app/auth/         Register, verify, login, forgot and reset password
src/app/api/          Auth, chat, me and conversation routes
src/app/components/   Landing page sections and the markdown renderer
src/lib/              Auth, validation, rate limiting and chat runtime
src/db/               Database connection and Drizzle schema
drizzle/              SQL migrations
public/               Logo
```

## Contributing

Contributions are welcome, from typo fixes to new features. Please read
[CONTRIBUTING.md](CONTRIBUTING.md) for setup, workflow and the pull request
checklist, and follow our [Code of Conduct](CODE_OF_CONDUCT.md).

## Security

Found a vulnerability? Please report it privately as described in
[SECURITY.md](SECURITY.md) instead of opening a public issue.

## License

Released under the [MIT License](LICENSE). Copyright (c) 2026 abdulrdeveloper.
