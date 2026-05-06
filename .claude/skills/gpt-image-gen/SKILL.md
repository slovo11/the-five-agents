# Skill: gpt-image-gen

## When to Use

Invoke this skill whenever any agent needs to generate an image using OpenAI's image generation API.
Any agent that produces visual content must use this skill — do not call the API directly.

## Inputs

| Parameter | Type | Description |
|---|---|---|
| `prompt` | string | Full image generation prompt (detailed description of the desired image) |
| `output_path` | string | Destination file path for the PNG, e.g. `yuval/outputs/2026-05-06-my-image.png` |

## Steps

### 1 — Load the API key

```bash
export $(grep -v '^#' .env | xargs 2>/dev/null)
```

Verify the key is present:

```bash
if [ -z "$OPENAI_API_KEY" ]; then
  echo "ERROR: OPENAI_API_KEY is not set in .env" >&2
  exit 1
fi
```

### 2 — Call the API and save the image

**Primary path (jq available):**

```bash
curl -s -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "'"$PROMPT"'",
    "size": "1024x1024",
    "quality": "medium",
    "output_format": "png",
    "response_format": "b64_json"
  }' | jq -r '.data[0].b64_json' | base64 --decode > "$OUTPUT_PATH"
```

**Python fallback** (use when `jq` is not installed — always available on Windows/Git Bash):

```bash
curl -s -X POST "https://api.openai.com/v1/images/generations" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "gpt-image-2",
    "prompt": "'"$PROMPT"'",
    "size": "1024x1024",
    "quality": "medium",
    "output_format": "png",
    "response_format": "b64_json"
  }' | python -c "
import sys, base64, json
try:
    data = json.load(sys.stdin)
    if 'error' in data:
        print('API ERROR:', data['error']['message'], file=sys.stderr)
        sys.exit(1)
    b64 = data['data'][0]['b64_json']
    with open(sys.argv[1], 'wb') as f:
        f.write(base64.b64decode(b64))
except Exception as e:
    print('DECODE ERROR:', e, file=sys.stderr)
    sys.exit(1)
" "$OUTPUT_PATH"
```

### 3 — Verify the output

```bash
if [ -s "$OUTPUT_PATH" ]; then
  echo "Image saved: $OUTPUT_PATH"
else
  echo "ERROR: Output file is missing or empty — $OUTPUT_PATH" >&2
  exit 1
fi
```

## How to Detect Whether jq Is Available

```bash
if command -v jq &>/dev/null; then
  # use primary path
else
  # use Python fallback
fi
```

## Error Handling

- If `OPENAI_API_KEY` is empty → stop immediately, report the missing key
- If the API returns a non-200 status or an `error` field in the JSON → stop, report the error message
- If the output file is empty after decoding → stop, report failure
- **Never silently continue** past a failure — always surface the error to the calling agent

## Notes

- Model is always `gpt-image-2`; do not allow overriding the model from the prompt
- Output is always PNG at 1024×1024
- `quality: medium` is the default; `high` is available if the caller explicitly requests it
- The API key is loaded from `.env` at project root — never hardcode it
