# andsee Cutroom — agent plugin

**See a video that works. Cut your own.** Cutroom is a video-editing engine that runs on your computer and is driven
by an agent (Claude Code, Codex, Antigravity …) or by its own browser editor. Give it a reference video and your
talking-head take: it works out how the reference is edited and lays that edit on your own material — captions,
layouts, B-roll, motion graphics, music and sound, all anchored to the words you say — then renders it and scores the
result against the reference.

[Website and account](https://studio.andsee.ai/cutroom) · [简体中文](./README.zh-CN.md) · [Signing in and generation](./docs/account.md) · [Agents](./docs/agents.md)

This repository is the open part: the starter skill agents read, and the plugin manifests. The engine is installed
separately (free, sign-in required).

## Install

Paste this into your agent:

```text
Read https://github.com/andsee-ai/cutroom-agent-plugin/blob/main/skills/cutroom-start/SKILL.md and set up Cutroom.
```

or do it yourself (macOS, Apple silicon):

```sh
curl -fsSL https://studio.andsee.ai/install/cutroom.sh | sh
cutroom login            # sign in to andsee in your browser (free) and approve this computer
cutroom env              # check the machine: FFmpeg, Chrome …
cutroom skill install    # link the skill into Claude Code / Codex / Antigravity
```

Windows and Intel Macs are being prepared.

## What you can ask for

| | |
|---|---|
| **Remake** (复刻) | "Remake this reference with my take" — the reference's structure, rhythm, layouts and packaging on your footage, compared frame by frame |
| **Smart edit** (智能剪辑) | "Edit this take into a TikTok" — segments by meaning, shots, an opening hook, B-roll and cards where the picture is flat, a score and a prescription |
| **Packaging** (包装) | word-level captions, motion units, music ducking and sound effects, all anchored to the script: rewrite a line and the timing re-flows |
| **Variants** | one edit that works, many versions of it |

Or open the editor and point at what to change: `cutroom editor`.

## What costs money

Editing, captions, motion and rendering are local and free. Generating pictures, clips or voice needs a generation
service, and you choose which:

- **andsee** — the credits of your andsee account, nothing to configure: `cutroom account use andsee`
- **your own** — an OpenAI-compatible relay, a gateway, a command line or a skill of yours; its key stays on your
  computer: `cutroom account use custom`

Every paid step shows its price and waits for your yes.

## Your footage and your rights

Your media and projects stay on your computer. Cutroom copies *how* a reference is edited onto your own material;
whether you may use a picture, a person, a song or a logo from someone else's video is yours to decide.

## Licence

The contents of this repository are licensed under [Apache-2.0](./LICENSE). The Cutroom engine is distributed as an
installer under its own [terms](https://studio.andsee.ai/install/cutroom-terms.html). Cutroom is an independent
implementation; the third-party components it includes are listed in the `THIRD-PARTY-NOTICES.md` of the installer.
