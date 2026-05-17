# Evolution Horsemanship

Website project for [Evolution Horsemanship](https://www.evolutionhorsemanship.com) — equine services and personal development, founded by Donna Blem in Ocala, Florida.

## Project Structure

```
├── GEMINI.md              # Agent instructions + Superpowers tool mapping
├── AGENTS.md              # Agent directives (3-layer architecture)
├── README.md              # This file
├── KNOWLEDGE_BASE/        # Client intelligence
│   └── Master_Reference.md
├── reference/             # Current site screenshots and assets
├── src/                   # Website source code
├── directives/            # Task SOPs
├── execution/             # Automation scripts
└── .tmp/                  # Intermediate files (gitignored)
```

## Tools

- **Browser-Harness** v0.1.0 — CDP browser control (`browser-harness -c "command"`)
- **Superpowers** v5.1.0 — obra/superpowers skill framework (skills at `~/.agents/skills/`)
- **Firecrawl** — MCP-based web scraping and search
