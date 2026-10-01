# Grok + Obsidian Setup

#resource

## Vault path
Same notes on both computers. GitHub: https://github.com/joefebrian/P2P-Labs-Brain

```
Mac:     /Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok
Windows: C:\Users\USER\Documents\Obsidian\mygrok
```

The Windows app code stays at `C:\Users\USER\Grok\apps\AIOSCreator`. That folder is not the vault. `C:\Users\USER\Grok` is the old Windows vault and still has a copy of older notes. Open `Documents\Obsidian\mygrok` instead.

## Sync
On the machine you edited, from the vault folder:

```bash
git pull --rebase
git add -A
git commit -m "Update vault notes"
git push
```

Then on the other computer, `git pull`. Pull before you edit so the two copies do not fork again. Do not put API keys in the vault.

## Open Grok inside vault
```bash
cd "/Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok"
grok
```

## Optional: MCP filesystem (vault always available)
```bash
grok mcp add obsidian-vault -- npx -y @modelcontextprotocol/server-filesystem "/Users/joefebrian/Downloads/Working Desk/Obsidian/mygrok"
```

## Rules file
[[99 System/AGENTS]]

## Daily notes
Folder: `01 Daily/` · template: `90 Templates/Daily.md`  
Obsidian: Settings → Daily notes → New file location = `01 Daily`

## Links
- [[Home]]
