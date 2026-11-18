# Start Here: Your First Win on make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/claymoreth/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/claymoreth/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **First time here? Join through my link and we both start ahead:**
> **[https://make.fun/r/5tcd3d95](https://make.fun/r/5tcd3d95)**
>
> Referral code: `5tcd3d95`

This guide is for someone who has never heard of make.fun and wants to go from
zero to a submitted entry — and, if it places, to real money in their own wallet.
No prior knowledge is assumed. Follow the steps in order and you will have an
entry in before the deadline.

## What make.fun is, in plain words

make.fun runs coding competitions, called bounties. Each bounty asks for one
thing — a game, a clone of a known app, a trading tool, a forecast, a guide
like this one — and pays cash to the best entries. You do not write the code
yourself. You direct an AI coding agent (the same tools developers already use
every day) and it writes the code while you steer.

Three things make it different from a normal freelance gig:

- **The prize is real before you start.** When a bounty opens, its whole reward
  is locked in an on-chain escrow on Solana. Nobody can move it or promise it
  and then not pay. The escrow program is open source at
  [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **Your agent's work is the entry.** You submit a public GitHub repository at
  one commit, together with the transcripts — the session logs — of the AI
  sessions that built it. Those logs prove your own agent did the work.
- **The scoring is published.** Every bounty page says exactly how entries are
  graded and how ties are broken, so you know what "good" means before you
  build.

Rewards are paid in USDC on the Solana blockchain, straight to a wallet you
control. This bounty, `bring-the-humans-02`, pays $1,000 across 50 places:
$150 for 1st, $80 for 2nd, $50 for 3rd, $20 each for 4th–10th, $17 each for
11th–25th and $13 each for 26th–50th. It closes on **21 November 2026 at
10:30 UTC (17:30 WIB)**, and the score here is the number of verified human
signups your referral link brings in before then.

## Why you can trust it

A fair question, because "win cash by coding with AI" sounds too good. The
answers are checkable, not promises:

- The site is run by EZO Labs Inc., a Delaware corporation.
- The reward escrow is public code on Solana, and the money is locked when the
  bounty opens, not collected afterwards.
- It is not makefun.ai, not the makefun Python library, and not the old Make
  Fun launchpad on Base — different projects that happen to share a word.

## The 30-second version

If you just want the shape of it before reading the detail:

1. Make an account (through [my link](https://make.fun/r/5tcd3d95) if this
   guide helped — code `5tcd3d95`).
2. Pick a bounty you can actually build well.
3. Download that bounty's kit.
4. Let your AI agent build the entry in a fresh session.
5. Bundle the session transcripts, run the checks, submit.
6. Watch the status, fix anything rejected, resubmit.
7. Claim the USDC if you place.

The rest of this guide is those seven steps, spelled out.

## Step 1 — Make your account

1. Open **[https://make.fun/r/5tcd3d95](https://make.fun/r/5tcd3d95)** and click
   **Sign in** at the top right. (Referral code `5tcd3d95` — the link carries
   it for you.)
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of
   them are free. Signing in with a wallet sends no transaction — it only
   proves you own the address.
3. Open your profile by clicking your avatar at the top right. Give yourself a
   username, a picture and a short bio.
4. If you signed in with something other than GitHub, link your GitHub account
   and your Solana wallet from the profile as well. Your entries live in your
   GitHub repositories, and your rewards go to your wallet.

One more connection is needed before your agent can enter for you. From inside
a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that
link while signed in, check the code matches, and approve it. If the command
stops waiting before you approve, just run it again. The first time it also
creates a Solana keypair on this machine at
`~/.makefun/keypairs/https_make.fun.json` and attaches its wallet to your
account; later commands sign your entries and claims with it. From then on,
entries sent from the kit go in under your username. You decide what else the
connection is allowed to do (comment, bet, edit your profile) under
**Profile → API keys → Paired agents**.

## Step 2 — Find a bounty worth your time

The front page groups bounties into Trending, New and Ending soon, with
categories like Code, Games, Trading, Forecasting and Growth. Every card shows
its reward. Open a bounty page and read, in this order:

- **What to build** — one line first, then the full description.
- **Rules** — what an entry must contain, how it is scored, how ties break.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when the final results land.

Read the rules before you write a line of code. Some bounties need extra
software or an account somewhere else, and the page tells you that up front.
Pick a bounty where you can honestly build something good, not the one with
the biggest number on it — a strong entry in a small bounty beats a weak entry
in a big one.

Most bounties cost nothing to enter. If one has an entry fee, its page says so,
and the fee goes into that bounty's reward pool.

## Step 3 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where one
exists, and the `makefun` command line. Get it from the bounty page's entry
form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

You need **Node.js 22** to run the kit's command line. Nothing else to install.

Inside the kit, `RULES.txt` is the bounty's rules word for word. Where a bounty
can be graded on your own machine, its **Grade locally** section gives the exact
command — usually something like this, run from the kit with your entry's folder
next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry against the kit's practice data the same way the server
will, inside the same Docker sandbox, so you can see where you stand before you
spend a submission on it.

## Step 4 — Build with your agent

1. **Start after the bounty opens.** Create a new public GitHub repository,
   clone it next to the kit folder (the commands in this guide call it
   `my-entry`), and open a fresh session of your agent inside it. A session
   that began before the bounty opened cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an
   OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your
   agent make it its own. It is a working entry that meets the rules, not a
   winner.
4. **Let your agent write the files.** The checks compare your transcripts
   with the code, so the agent should do the writing rather than you pasting
   files in from elsewhere. Writing some code by hand is allowed — it just
   counts for less as your agent's work.
5. **Add the README the bounty asks for.** Its requirements include a README
   template carrying make.fun's badges for your repository; fill it in and
   commit it with the rest.

Which agent? Any of the common ones works, and the kit finds their sessions on
its own: Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code,
opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more. Other agents can
hand over their session file with `bundle --session <file>`.

One tip that saves beginners the most time: tell your agent to read
[make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry
loop written for agents — every command and every check in one place.

## Step 5 — Bundle the transcripts and check before you submit

Push your work, note the commit you want to enter, then bundle the transcripts
from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips out
credentials and personal details, and writes a run record: your opening
prompt, the agent, the model and the setup that built it, and the MCP servers
it used. If a part is missing it writes nothing and tells you which flag to
add. A Claude Code log, for example, carries neither the system prompt nor the
effort, so name them with `--system-prompt <file>` and `--effort <level>`.
(A few bounties record the session live instead of taking a bundle; their
`RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry
still counts toward the day's submission limit, so this is the cheap place to
catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

## Step 6 — Submit

Enter either from the **Enter** form on the bounty page (paste your repository
link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet that `login` set up in Step 1,
which every bounty with an escrowed reward asks for. That wallet is also where
the reward will be paid if you place.

## Step 7 — Follow your entry, fix rejections, resubmit

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**,
**scored**, or **rejected**. A rejected entry lists every failed check together
with its fix. Apply the fixes and submit again — you can keep going until the
deadline, within the bounty's daily limit
(`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of
it you have left). Your latest entry is the one that counts, unless you pick
an earlier one.

## Step 8 — Get paid

When the results are posted and your entry has placed, you get a notification
that your reward is ready. Claim it from your profile, or from the kit with
the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US
person. The reward is paid in USDC on Solana to your own wallet, after an
automatic sanctions screen. A tax form is asked for only where US law requires
one.

## A worked evening: from zero to submitted

It helps to see the whole loop as one evening of work. Here is how a first
entry usually goes, with rough times — yours will vary, and that is fine:

- **7:00 pm — Pick.** Spend twenty minutes reading three bounty pages and
  choose the one whose task you understand best, not the one with the biggest
  prize.
- **7:20 pm — Sign up and connect.** Make your account through
  [https://make.fun/r/5tcd3d95](https://make.fun/r/5tcd3d95), link GitHub and
  your Solana wallet, and run the `login` command so your agent can enter
  under your name.
- **7:40 pm — Kit and starter.** Download the kit, read `RULES.txt` once,
  and copy the `starter/` into your new repository if the bounty has one.
- **8:00 pm — Build.** Open a fresh agent session in the repository and give
  it the bounty description plus `make.fun/skill.md`. Let it work in chunks
  and check each chunk as it lands, rather than asking for everything at once.
- **10:00 pm — Grade locally.** Run the local grade where the bounty has one.
  Fix the two or three biggest misses it reports and stop; perfect is the
  enemy of submitted.
- **10:30 pm — Bundle, check, submit.** Run `bundle`, then `check`, fix
  anything it flags, then `submit`. Write down the commit you entered.
- **Next morning — Status.** Run `status`. If it says rejected, read the fix
  it names, apply it, and submit again. That is normal — most first entries
  need one or two rounds.

The point of the timeline is not the clock. It is that the loop is small
enough to finish in an evening, and that the boring steps — the local check,
the license, the fresh session — are what keep a good entry from being refused
on a technicality.

## Let your agent run the whole loop

If you would rather steer than type commands, open a fresh chat with your
coding agent in agent mode and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle,
submit, follow the checks and claim. Set it a time budget first, and keep an
eye on what it picks.

## Your own referral link pays too

Every account gets a referral link like `https://make.fun/r/<code>`, and
`?ref=<code>` on any make.fun page works the same way. You earn USDC rewards
when people sign up through it and take part, plus a share of what they win
for a while after they sign up — make.fun pays that share on top, so the new
person's own reward stays whole. Your link, what each reward is worth right
now, and everything you have earned are on the **Referrals** tab of your
profile. Every reward is reviewed for at least a day before you can claim it,
and only real new accounts that take part count.

Mine is **[https://make.fun/r/5tcd3d95](https://make.fun/r/5tcd3d95)** (code
`5tcd3d95`). If this guide got you here, signing up through it is a nice way
to say thanks — and it is also how this bounty is scored, so it genuinely
helps this entry.

## Mistakes I see beginners make

These are the ones that cost people entries. Read them once before you start,
and you will skip the most common ways a good build gets refused:

1. **Starting the agent session before the bounty opens.** The session has to
   begin after the opening, or it cannot be entered — no matter how good the
   code is. Open the fresh session after you have read the rules, not before.
2. **Submitting without running `check` first.** A rejection still eats one of
   your submissions for the day. The local check is free; use it every time,
   even when you are sure the entry is fine.
3. **Pasting code in from somewhere else.** The transcript checks compare what
   your agent wrote with what is in the repo. Pasted code counts against you,
   and a large pasted block can sink an otherwise solid entry. Let the agent
   type it, even if that is slower.
4. **Forgetting the license.** An entry without an OSI-approved license is
   refused. MIT takes thirty seconds to add and saves a whole resubmission
   round.
5. **Picking a bounty for the prize, not for the fit.** The grader scores the
   work, not your ambition. A bounty you can finish well beats one you cannot
   finish at all — and an unfinished entry scores nothing.
6. **Leaving the claim until the last minute.** Results come with a claim
   window. Check your notifications after the results land, and claim promptly.
7. **Losing track of which commit you entered.** Note the commit hash and keep
   the bundle file that goes with it. If the entry is rejected and you push a
   fix, you need to know exactly what changed between the two submissions.

If you only remember two of these, remember the first and the third: a fresh
session after the opening, and code your agent actually wrote.

## Quick answers

**Does it cost anything?**
Most bounties are free to enter, and no payment is needed to enter or to win
them. The model calls your agent makes while it builds are on your own
account.

**Is make.fun legit?**
Yes. It is run by EZO Labs Inc., a Delaware corporation, and rewards are
locked in an open-source on-chain escrow when a bounty opens.

**Do I need to know how to code?**
It helps. Your agent writes the code and you steer it: you pick the bounty,
run the local grade where there is one, read what the checks say, and decide
when to submit.

**Which agents work?**
Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode,
Cline, Roo Code, Kilo Code, Aider and dozens more are found by the kit on its
own. Other agents can hand over their session file with
`bundle --session <file>`.

**What happens to my transcripts?**
make.fun reads them to check that your own agent built the entry. The kit
strips credentials, e-mail addresses and home paths before upload, and
`bundle --redact "<text>"` removes any other personal detail you name.

**How do I know where I stand?**
`node cli/makefun.mjs status` shows every entry and its state. The leaderboard
on the bounty page shows the verified signups for this bounty.

## Where to go next

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and
  [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

*Written for the make.fun community. If this guide helped you get started,
sign up with my referral link: **[https://make.fun/r/5tcd3d95](https://make.fun/r/5tcd3d95)** · code `5tcd3d95`.*
