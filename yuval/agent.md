# יובל — Creative Agent (Human Reference)

> This is a human-readable pointer doc. The canonical agent definition that Claude Code reads
> is at `.claude/agents/yuval.md`.

## What יובל Does

יובל is the project's image generation agent. Given a content request, he:

1. Scans `yuval/reference/` for inspiration images to extract a consistent visual style
2. Writes a detailed image generation prompt that combines the request with the extracted style
3. Calls the `gpt-image-gen` skill to generate the image via OpenAI gpt-image-2
4. Saves the result to `yuval/outputs/` with a dated filename
5. Saves a sibling `.txt` file logging the exact prompt used (for iteration)
6. Reports back with path, prompt, and references applied

## Adding Reference Images

Drop any `.png`, `.jpg`, or `.webp` image into `yuval/reference/`. יובל will pick them up
automatically on the next generation request. The more reference images you add, the more
precise his style extraction becomes.

There is no limit on the number of references, but 3–10 cohesive images work best.

## Output Location

All generated images are saved to `yuval/outputs/` with the naming convention:

```
yuval/outputs/<YYYY-MM-DD>-<short-slug>.png
yuval/outputs/<YYYY-MM-DD>-<short-slug>.txt   ← prompt log
```

## Canonical Agent Definition

`.claude/agents/yuval.md` — this is the file Claude Code reads to instantiate יובל as a sub-agent.
