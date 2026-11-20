---
name: cutroom-start
description: andsee Cutroom — turn a reference video into the user's own video on their computer (复刻 / 一比一复刻 / 智能剪辑 / 口播包装 / remake / clone this video / edit my talking-head take / add captions, B-roll, motion graphics and sound). Use this when the user asks for any of that and the full `cutroom` skill is not available yet: it installs Cutroom, signs it in to andsee and hands over to the full skill. If a skill named `cutroom` is already available, use that one instead.
---

# Cutroom — getting started

Cutroom is a local video-editing engine for agents. It measures a reference video, lays its edit on the user's own
take, compiles a word-anchored story (`slate.yaml`) into a timeline, renders an MP4 + SRT and scores the result.
All of it runs on the user's computer through the `cutroom` command line; the book that says how to edit — playbooks,
references, styles — ships with the engine and is called the `cutroom` skill.

This skill only gets you there. Do the steps in order; stop and ask where it says ask.

## 1. Is Cutroom here?

Run `cutroom --version`.

- It answers → go to step 2.
- Command not found → Cutroom is not installed. **Ask the user before installing.** Show them this command and what it
  does (downloads Cutroom from andsee into `~/.andsee/cutroom`, no sudo, checksum verified):

  ```sh
  curl -fsSL https://studio.andsee.ai/install/cutroom.sh | sh
  ```

  After a yes, run it. If `cutroom` is still not found afterwards, call it by its full path
  `~/.local/bin/cutroom` and tell the user the one line the installer printed for their PATH.
  macOS (Apple silicon) is supported today; on another system say so and point to
  https://studio.andsee.ai/cutroom instead of improvising.

## 2. Is it signed in?

Run `cutroom account --json`.

- `"signed_in": true` → go to step 3.
- Otherwise sign in. It is free, and the user does it in their browser — never ask for a password or a key in the chat:
  1. `cutroom login --start --json` returns `url` and `user_code` at once.
  2. Give the user the link and the code. They sign in to andsee there (or register — same page), check that the code
     matches and click 允许.
  3. `cutroom login --wait --timeout 120`; while it answers `pending`, wait for the user and run it again.

A command that answers `code: signed_out`, `license` or `must_update` later on is fixed the same way: `cutroom login`,
or `cutroom update` for `must_update`. Do not work around it.

## 3. Check the machine, link the full skill

1. `cutroom env` lists what the machine lacks (FFmpeg, Google Chrome, …) with the command to install each. Installing
   system tools changes the user's computer: show the commands and ask first.
2. `cutroom skill install` links the full `cutroom` skill into this agent (Claude Code, Codex, Antigravity).
3. `cutroom skill status --json` says where it is linked. **Read that `SKILL.md` now and follow it** — it picks the job
   (remake, smart edit, packaging …) and sends you to the playbook. From here on this starter skill has nothing to add.

## Rules that hold from the first command

- **Money needs a yes.** Editing, captions, motion and rendering are local and free. Generating pictures, clips or
  voice costs money: andsee credits, or whatever the user's own service charges. Cutroom shows an estimate first; run a
  paid step only after the user agreed to that estimate. `cutroom account` shows the credits and which service is the
  default; `cutroom account use andsee|custom` switches it.
- **The user's footage stays on their computer.** Only a generation the user approved uploads the reference files that
  generation needs.
- **Rights are the user's call.** Cutroom copies how a reference is edited — structure, rhythm, packaging — onto the
  user's own material. Whether a picture, a person, a song or a logo from someone else's video may be used is for the
  user to decide; when a job would reuse such material as it is, say so and ask.
- **Look before you say done.** Render the frame or the range and look at it; report the score `cutroom doctor` gives.
- Every command prints a `→ next:` line and takes `--json`; errors carry `next_action`. Follow those rather than guessing.
