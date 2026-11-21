# Fluff-be-gone

An [Agent Skill](https://docs.claude.com/en/docs/claude-code/skills) that removes filler from your agent's replies (preambles, recaps, flattery, stacked hedges, empty offers) **without breaking grammar**.

Telegraphic "caveman" modes save tokens by dropping articles and writing in fragments. Fluff-be-gone takes a different route: it cuts the sentences that say nothing and keeps the ones that matter, so replies stay short **and** easy to read.

> **The one test:** if a sentence is deleted, does the reader lose a fact, a decision, a warning or a next step? No → delete it.

## Before / after

**Before (64 words)**
> Great question! I'd be happy to help you with that. So, basically, the issue you're seeing is most likely caused by the fact that your environment variable isn't being loaded. Let me explain: Node doesn't read `.env` files automatically. To fix this, you can simply install dotenv. Hope this helps, and let me know if you have any other questions!

**After, `full` level (25 words)**
> Node doesn't read `.env` automatically, so `API_KEY` is undefined. Load it at startup:
> ```js
> import 'dotenv/config';
> ```
> Or run `node --env-file=.env app.js` (Node 20.6+).

## Install

### Claude Code (plugin)

```text
/plugin marketplace add iMhdi/fluff-be-gone
/plugin install fluff-be-gone@fluff-be-gone
```

### Manual (any agent that reads `SKILL.md`)

```bash
git clone https://github.com/iMhdi/fluff-be-gone.git
cp -r fluff-be-gone/skills/fluff-be-gone ~/.claude/skills/
```

## Usage

Turn it on by saying any of these: `fluff-be-gone`, `no fluff`, `be concise`, `stop the fluff`, `sans blabla`, `droit au but`, `va à l'essentiel`.

It stays on for the whole session. To turn it off, say `fluff back`, `normal mode` or `mode normal`.

| Level | What it does |
|---|---|
| `lite` | Cuts openers, closers, flattery and empty offers. Keeps explanations. |
| `full` (default) | Cuts all filler. Puts the answer first. Keeps a one-line why. |
| `ultra` | Same as `full`, minus the why unless you ask. Prefers code, commands and tables to prose. |

Switch levels with `fluff-be-gone lite|full|ultra`.

### Never cut

Some content stays whatever the level:

- security warnings
- data-loss risks
- confirmations before irreversible actions
- code, commands, paths, error messages and versions, exactly as written
- anything that was not done or not verified
- numbered steps, kept in order
- clarifying questions
- a full explanation when you are confused or ask "why"

## Français

Fluff-be-gone supprime le remplissage des réponses de l'agent (« Bonne question ! », « N'hésitez pas si… », « En résumé… ») tout en gardant des phrases complètes. Il fonctionne en français comme en anglais et répond dans la langue de l'utilisateur.

## Credits

Inspired by [no-fluff](https://github.com/yeaight7/agent-powerups/tree/main/skills/no-fluff) from agent-powerups, which uses a telegraphic style instead.

## License

[MIT](LICENSE)
