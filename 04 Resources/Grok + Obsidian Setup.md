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
GitHub is the shared copy: https://github.com/joefebrian/P2P-Labs-Brain
The Windows PC is already logged in as `joefebrian`.

Every day at 23:30 the task `mygrok github sync` does this:

1. Commit notes changed on the Mac.
2. Commit notes changed on Windows.
3. Merge the two into `main`.
4. Push `main` to GitHub.
5. Fast-forward the Mac to that same `main`.

If the same note was edited on both computers and git cannot merge it, the task stops and does not push. The next session resolves that merge, then both computers get `main` again. Do not put API keys in the vault.

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
