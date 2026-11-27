# Signing in, credits and generation

Cutroom is free to use and works after one sign-in to andsee.

| command | what it does |
|---|---|
| `cutroom login` | prints a link and a code and opens the link; you sign in to andsee (or register) and approve this computer |
| `cutroom login --start` / `--wait` | the same in two steps, for an agent whose commands cannot wait |
| `cutroom account` | who is signed in, credits, until when this computer's licence lasts, where generation runs |
| `cutroom account use andsee` | generate with the andsee account's credits (no key to configure) |
| `cutroom account use custom` | generate with a service of your own: an OpenAI-compatible relay, a gateway, a command line or a skill |
| `cutroom account relay --name <n> --base-url <https://…>` | add a relay of your own; its key is read from `$CUTROOM_RELAY_KEY` and stays on your computer |
| `cutroom account models` | the andsee models and their price in credits |
| `cutroom account devices` | the computers signed in on the account; `--remove <id>` frees a place |
| `cutroom assets pull` | download asset packs (animated stickers …) |
| `cutroom update` | update to the newest release |
| `cutroom logout` | sign this computer out |

- The sign-in is kept in `~/.cutroom/account.json` (owner-only). The licence is renewed whenever the computer is online
  and works offline for seven days.
- Editing, captions, motion and rendering run on your computer and cost nothing. Only generating pictures, clips or
  voice costs money, and every paid step shows its price and waits for your yes.
- On a machine without a browser, set `ANDSEE_TOKEN` to a key from https://andsee.ai/cutroom.
