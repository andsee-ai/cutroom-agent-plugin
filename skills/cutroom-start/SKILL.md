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

## 1. Is Cutroom here? (install or update)

First see which system this shell is on: macOS on Apple silicon (`uname -sm` → `Darwin arm64`), or Windows 10 / 11
on 64-bit (PowerShell or cmd; `$env:OS` / `%OS%` → `Windows_NT`). Cutroom runs on those two today. On anything else
(an Intel Mac, Linux, WSL — a Linux shell inside Windows) say so and point to https://andsee.ai/cutroom; do not
improvise an install. Inside WSL, the user can run their agent in a normal Windows PowerShell window instead.

Run `cutroom --version`.

- **It answers** → run `cutroom update`. It installs a newer release when there is one (checksum verified, the old
  version kept as a way back) or says this one is the newest. If it says this copy was not installed by the installer
  (a developer's source checkout), leave it as it is. Then go to step 2.
- **Command not found** → Cutroom is not installed. If the user's message asked you to install or set up Cutroom, that
  is the yes; otherwise ask first. Tell them in one line what the command does: downloads Cutroom from andsee into
  their home folder, checks the checksum, needs no administrator rights and touches nothing system-wide. Then run the
  command for their system.

  macOS (Terminal, zsh / bash):

  ```sh
  curl -fsSL https://andsee.ai/install/cutroom.sh | sh
  ```

  Windows (works from PowerShell and from cmd):

  ```powershell
  powershell -NoProfile -ExecutionPolicy Bypass -Command "irm https://andsee.ai/install/cutroom.ps1 | iex"
  ```

  It ends with `✓ cutroom <version> 已安装到 …`. The download is about 100 MB; give it a few minutes.

  **If it fails on the network or on writing to the home folder** (cannot resolve or reach andsee.ai or github.com, a
  timeout, "连不上", access denied under `~/.andsee` / `%USERPROFILE%\.andsee` or to the PATH): your shell is probably
  sandboxed. Run the same command again with network and write access outside the workspace — in Codex, request
  escalated permissions (outside the sandbox) for it; the user approves once. Do not download the archive some other
  way, and do not change the user's sandbox settings yourself.

  **After the install, this session may not find `cutroom` yet**: your shell started before the installer put it on
  the PATH, and every command you run inherits that old PATH. Do not ask the user to restart anything. For the rest of
  this session call Cutroom by its full path, everywhere this skill or the full `cutroom` skill says `cutroom`:

  | system | full path |
  |---|---|
  | macOS | `~/.local/bin/cutroom` |
  | Windows, PowerShell | `& "$env:USERPROFILE\.andsee\cutroom\bin\cutroom.cmd"` |
  | Windows, cmd | `"%USERPROFILE%\.andsee\cutroom\bin\cutroom.cmd"` |

  Check it with `<full path> --version`. New terminals and new agent sessions find plain `cutroom` (on macOS, if the
  installer printed a line for the PATH, give the user that line).

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

1. `cutroom env` lists what the machine lacks (FFmpeg, Google Chrome or Microsoft Edge, …) with the command to install
   each (Homebrew on macOS, winget on Windows). Installing system tools changes the user's computer: show the commands
   and ask first. On Windows, a tool winget just installed is found only by new terminals: run `cutroom env` again in a
   new shell, or tell the user to open a new agent session if it still says missing.
2. `cutroom skill install` links the full `cutroom` skill into this agent (Claude Code, Codex, Antigravity).
3. `cutroom skill status --json` says where it is linked. **Read that `SKILL.md` now and follow it** — it picks the job
   (remake, smart edit, packaging …) and sends you to the playbook. From here on this starter skill has nothing to add,
   except the full path of step 1 while this session's PATH is old.
4. Tell the user it is ready, in one or two lines: the version, that they are signed in, and that `cutroom editor`
   opens the editor (which updates Cutroom by itself while nothing runs). Then do what they asked for, if anything.

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
- **The video speaks its material's language.** On-screen text, captions, voice and the words inside generated
  pictures and clips follow the language heard in the user's take or reference (`cutroom language` shows it), not the
  language the user chats in. When nothing can be heard, ask which market the video is for, then `cutroom language <code>`.
- **Export whenever the user asks.** `cutroom render --final [--out <folder>]` — a score, an unfinished remake gate or
  missing elements never hold the file back; say what is still off and export.
- **A failed generation is explained, not retried blindly.** The error says why (refused content, no credits, a busy or
  uncertain service) and what to do; never resubmit an "uncertain" job yourself — it may already be paid.
- **Tell the user when you stop.** Before you wait for them (a question, a budget, a confirmation) and when a long job
  ends, run `cutroom notify "<what you need>"`: a system notification with a sound, for a user busy in another window.
- **Look before you say done.** Render the frame or the range and look at it; report the score `cutroom doctor` gives.
- Every command prints a `→ next:` line and takes `--json`; errors carry `next_action`. Follow those rather than guessing.
