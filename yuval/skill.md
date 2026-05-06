# gpt-image-gen Skill (Human Reference)

> This is a human-readable pointer doc. The canonical skill definition is at
> `.claude/skills/gpt-image-gen/SKILL.md`.

## What It Does

Wraps the OpenAI Images API (`POST /v1/images/generations`) — takes a prompt and output path,
returns a saved PNG file.

## Setup

Add your OpenAI API key to `.env` at the project root:

```
OPENAI_API_KEY=sk-...
```

The skill loads it automatically via `export $(grep -v '^#' .env | xargs)`.

## The Curl Call

```bash
curl -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "<the prompt>",
    "size": "1024x1024",
    "quality": "medium",
    "output_format": "png",
    "response_format": "b64_json"
  }'
```

## Python Fallback (when jq is not installed)

```python
python -c "
import sys, base64, json
data = json.load(sys.stdin)
open(sys.argv[1], 'wb').write(base64.b64decode(data['data'][0]['b64_json']))
" output.png
```

## Full Skill Definition

`.claude/skills/gpt-image-gen/SKILL.md`
