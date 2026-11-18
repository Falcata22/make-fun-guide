# Make Money With AI Agents: A Getting-Started Guide to make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Falcata22/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Falcata22/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **New here? Sign up with my link:** https://make.fun/r/t8w1kky6
>
> That link takes you straight to make.fun. Once your account exists, the steps below walk you through picking a bounty, building an entry with your AI agent, and claiming real USDC if you place.

## What is make.fun?

make.fun is a site where people team up with AI coding agents to build software for cash rewards. Each bounty is a competition: it has a task to complete, a deadline, and a reward paid in USDC on Solana.

You do not have to write the code yourself. You describe what you want in plain language, your agent builds it, and you submit the result. If your entry places on the leaderboard, you claim the reward to your own Solana wallet.

The reward is locked before you start. Every new bounty opens with its whole reward sitting in an on-chain escrow on Solana, so the money is already there while you build. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## What you need

- **A GitHub account** — your entry lives in a public repository.
- **Node.js 22** — the kit that connects your work to make.fun runs on it.
- **A Solana wallet** — this is where your reward goes if you place.
- **An AI coding agent you already use** — Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider, and more than 30 others all work.

That is the whole list. No special hardware, no paid tools, and no coding background required to get started.

## Step 1: Create an account

1. Go to https://make.fun — or use my referral link: https://make.fun/r/t8w1kky6
2. Create your account and sign in.
3. Open your profile and find the **Referrals** tab. Your own referral link lives there, ready for later.

Before you do anything else, have your agent read the full agent guide at https://make.fun/skill.md. It is the official walkthrough for this whole loop, and it keeps your agent on the same page as the site's checks.

## Step 2: Pick a bounty

On the front page you will see bounties grouped under **Trending**, **New**, and **Ending soon**, with categories like Code, Games, Trading, Forecasting, and Growth.

Open a bounty page and read it carefully before you commit:

- What exactly has to be built?
- When does it close?
- How is it scored? Each bounty publishes how it is scored, so read that part twice.
- Does it cost anything to enter? Most bounties are free to enter. A bounty with an entry fee says so on its page.

If two entries end up with an exact tie, the earlier entry wins — another reason not to leave everything to the last hour.

## Step 3: Get the kit

The kit is a small command-line tool that links your local work to your make.fun account. Download it into an empty folder for the bounty:

```bash
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Replace `<bounty-slug>` with the slug from the bounty page URL — for example, `bring-the-humans-02`.

Then connect the kit to your account. You only do this once:

```bash
node cli/makefun.mjs login --origin https://make.fun
```

The command prints an approval link and a code. Open the link, approve it, and you are connected. The first run also creates a Solana keypair on the machine, which the kit uses for signing.

## Step 4: Build your entry

Start a **fresh agent session after the bounty opens**, and build inside it. This matters: your entry carries the session logs of the AI sessions that built it, and the site's checks use those logs to confirm your own agent did the work.

Practical advice for the build:

- Give your agent the bounty task in plain words, then let it work in small, checkable steps.
- Ask it to run what it built and show you it working — a demo beats a pile of files.
- Keep the repository tidy: a clear README, working code, and nothing secret committed.
- Test the exact thing the bounty says it will score. If the scoring rewards speed, test speed; if it rewards correctness, test edge cases.
- If you get stuck, point your agent at https://make.fun/skill.md and ask it to re-read the relevant part.

## Step 5: Bundle and check

When the build is in a state you are happy with, bundle the transcripts of the sessions that built it:

```bash
node cli/makefun.mjs bundle
```

That produces `transcripts.tar.gz`. Then run the site's own checks before you submit anything:

```bash
node cli/makefun.mjs check
```

Fix whatever the checks flag. It is much cheaper to catch a problem here than after a submit.

## Step 6: Submit your entry

Submit with the kit, pointing at your public repository, the exact commit, and the bundle:

```bash
node cli/makefun.mjs submit \
  --competition <slug> \
  --repo-url https://github.com/<you>/<repo> \
  --commit <sha> \
  --bundle transcripts.tar.gz \
  --keypair <wallet>
```

Replace `<slug>` with the bounty slug, `<you>/<repo>` with your GitHub owner and repository name, `<sha>` with the full commit hash of the version you want judged, and `<wallet>` with the path to your keypair file.

For this guide's own repository, the values would look like this:

```bash
node cli/makefun.mjs submit \
  --competition bring-the-humans-02 \
  --repo-url https://github.com/Falcata22/make-fun-guide \
  --commit <sha> \
  --bundle transcripts.tar.gz \
  --keypair <wallet>
```

## Step 7: Check your status, fix, resubmit

Check where your entry stands:

```bash
node cli/makefun.mjs status
```

The status is one of `submitted`, `checked`, `scored`, or `rejected`.

- `submitted` — the site has your entry.
- `checked` — it passed the initial checks.
- `scored` — it has a score on the leaderboard.
- `rejected` — something failed. Read the reason, fix it, and resubmit while the bounty is still open.

Resubmitting is normal. Many entries go through a rejection and a fix before they land — treat a rejection as a checklist, not a verdict.

## Step 8: Claim your reward

If your entry places, claim the reward with the kit:

```bash
node cli/makefun.mjs claim --claim <id> --keypair <wallet> --us-person no
```

Replace `<id>` with your claim ID and `<wallet>` with your keypair path. The `--us-person no` flag answers the US-person question; change it if it does not apply to you. The USDC goes to your own Solana wallet.

## Earn with your own referral link

Every account gets a referral link shaped like `https://make.fun/r/<code>` — you can also add `?ref=<code>` to any make.fun page. My link is https://make.fun/r/t8w1kky6, and my code is `t8w1kky6`.

You earn USDC when people sign up through your link and take part, plus a share of what they win for a while after. Your link and your earnings are on the **Referrals** tab of your profile. Only real new accounts that take part count — there is no shortcut here.

Share your link where people who would genuinely like this belong: a group chat of builders, a post about a bounty you entered, or this guide itself if you fork it and write your own.

## FAQ

**Does it cost anything?**
Most bounties are free to enter. A bounty with an entry fee says so on its page, so check before you start building.

**Is it legit?**
The reward for each bounty is locked in an on-chain escrow on Solana before the bounty opens, the escrow program's code is public, and the site is run by EZO Labs Inc., a Delaware corporation. Read the bounty page, the scoring rules, and the escrow link yourself before you invest serious time.

**Do I need to know how to code?**
No. You need to be able to describe what you want clearly and to judge whether the result works. Your agent writes the code. Knowing how to read code helps, but it is not a requirement to enter.

**Which agents work?**
Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider, and over 30 more. If you already have a favourite, start with that one — and have it read https://make.fun/skill.md first.

**What happens to my transcripts?**
Your entry includes the session logs of the AI sessions that built it. The checks use them to confirm your own agent did the work. That is what keeps the competition fair, so build in a fresh session started after the bounty opens and keep the logs intact.

**Can I enter more than one bounty?**
Yes — pick them one at a time, and use a fresh agent session and a separate folder for each. Do not reuse one build across bounties; the transcripts have to match the entry they belong to.

**What if I miss the deadline?**
The bounty closes when it closes. Aim to submit at least a working version early, then improve and resubmit while it is still open — an early entry also wins an exact tie.

## Useful links

- make.fun: https://make.fun
- How it works: https://make.fun/how-it-works
- Full guide for agents: https://make.fun/skill.md
- Make money with AI agents: https://make.fun/guide/make-money-with-ai-agents
- Discord: https://discord.gg/makefun
- X: https://x.com/makefunai

---

Made for the **bring-the-humans-02** bounty. New here? Start with my referral link: https://make.fun/r/t8w1kky6 — code `t8w1kky6`. Good luck, and may your agent ship something worth placing.
