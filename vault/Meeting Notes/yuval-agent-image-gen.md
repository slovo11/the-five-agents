# Yuval Agent & Image Generation

## Overview

יובל הוא סוכן הקריאייטיב של הפרויקט, אחראי על כל יצירת תמונות. הוא פועל עם workflow בן 7 שלבים: סריקת reference images, חילוץ סגנון ויזואלי, בניית prompt, קריאה ל-`gpt-image-gen` skill, שמירת התמונה ב-`yuval/outputs/`, כתיבת log של ה-prompt, ואימות הקובץ. הסקיל `gpt-image-gen` הוא מעטפת משותפת ל-OpenAI Images API שכל סוכן יכול להשתמש בה. יובל מוגדר ב-`.claude/agents/yuval.md`; המנכ"ל (ראובן) מאציל אליו בהתבסס על keyword routing.

## Open Questions

- מה הסגנון הויזואלי הבסיסי של הפרויקט? (יש להוסיף reference images ל-`yuval/reference/` כדי לעגן אותו)
- האם לאפשר ל-יובל להשתמש ב-`quality: high` על פי בקשה, או לנעול על `medium` תמיד?
- כיצד לנהל ארכיון outputs — האם להגדיר מדיניות ניקוי?

## Session Log

### 2026-05-06 — הוספת יובל ו-gpt-image-gen [shipped]

- **What was done:** נוצרו: `.claude/skills/gpt-image-gen/SKILL.md` (מעטפת OpenAI Images API עם curl + Python fallback), `.claude/agents/yuval.md` (הגדרת סוכן קנונית), `.claude/agents/reuven.md` (הגדרת Claude Code sub-agent למנכ"ל עם טבלת Sub-Agents), `yuval/reference/`, `yuval/outputs/`, `yuval/agent.md`, `yuval/skill.md`. עודכנו: `agent.md` (registry — agent_1 הוחלף ביובל active), `.env.example` (נוסף OPENAI_API_KEY).
- **Decisions:** `.env` כבר הכיל OPENAI_API_KEY — לא הוסף מחדש. נבחר Python fallback (לא jq) כ-primary לסביבות Windows/Git Bash. `.claude/agents/reuven.md` נוצר כ-thin Claude Code sub-agent definition שמפנה ל-`agent.md` בשורש לספציפיקציה המלאה. מבנה היברידי: קובץ flat ב-`.claude/agents/` לצד תיקיית עבודה `yuval/` בשורש.
- **Notes / Caveats:** `yuval/reference/` ריקה — יובל יפעל ללא reference style עד שיוסיפו תמונות. keyword routing מוגדר ב-`reuven.md` ובעדכון registry ב-`agent.md`.
- **Related:** [[ceo-agent]], [[claude-directory]], [[project-scaffold]]
