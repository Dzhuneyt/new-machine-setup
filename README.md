Install:

1. [Claude Code](https://claude.com/product/claude-code) + Bash Guard + [RTK AI](https://github.com/rtk-ai/rtk)
2. [Cursor CLI](https://cursor.com/download)
3. [Antigravity](https://antigravity.google/product/antigravity-cli)
4. [Ollama](https://ollama.com/)
5. [Homebrew](https://brew.sh/)

Authenticate to each individually.

## Post-install: disable Claude Code attribution

After installing Claude Code, disable the attribution it adds to git commits and
pull requests. Set both `attribution.commit` and `attribution.pr` to empty
strings in your user settings (`~/.claude/settings.json`). See the
[settings docs](https://code.claude.com/docs/en/settings).

Run this once per new machine:

```bash
mkdir -p ~/.claude
node -e '
  const fs = require("fs");
  const path = require("os").homedir() + "/.claude/settings.json";
  const cfg = fs.existsSync(path) ? JSON.parse(fs.readFileSync(path, "utf8")) : {};
  cfg.attribution = { ...(cfg.attribution || {}), commit: "", pr: "" };
  fs.writeFileSync(path, JSON.stringify(cfg, null, 2) + "\n");
  console.log("Attribution disabled in " + path);
'
```

Or edit `~/.claude/settings.json` manually:

```json
{
  "attribution": {
    "commit": "",
    "pr": ""
  }
}
```
