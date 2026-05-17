# Deploy Evolution Horsemanship to LeftDisplay (Netlify)

## Purpose
Put the site live so Jeff can show Donna and Mike where things are at.

## Pipeline
1. **Source repo:** `https://github.com/donnywonny2025/evolutionhorsemanship.git` (main branch)
2. **Display repo:** `https://github.com/donnywonny2025/leftdisplay.git` (main branch)
3. **Local path:** `/Volumes/WORK 2TB/WORK 2026/leftdisplay/`
4. **Netlify:** Auto-deploys from leftdisplay GitHub repo on push

## Steps When Ready
1. Copy `src/` contents from evolutionhorsemanship into leftdisplay root (or a subdirectory)
2. Make sure `netlify.toml` is configured to serve from the right publish dir
3. `git add -A && git commit -m "Evolution Horsemanship preview" && git push`
4. Netlify auto-deploys → live URL ready to share

## Notes
- The coming_soon.mp4 video (945KB) needs to go up too
- HEVC codec — may need an H.264 fallback for broader browser support
- Don't overwrite anything important already in leftdisplay (check first)
- Previous content was DAAD portal (temporarily removed per git log)
