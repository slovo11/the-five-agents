# Yuval Agent & Image Generation

## Overview

יובל הוא סוכן הקריאייטיב של הפרויקט, אחראי על כל יצירת תמונות. הוא פועל עם workflow בן 7 שלבים: סריקת reference images, חילוץ סגנון ויזואלי, בניית prompt, קריאה ל-`gpt-image-gen` skill, שמירת התמונה ב-`yuval/outputs/`, כתיבת log של ה-prompt, ואימות הקובץ. הסקיל `gpt-image-gen` הוא מעטפת משותפת ל-OpenAI Images API שכל סוכן יכול להשתמש בה. יובל מוגדר ב-`.claude/agents/yuval.md`; המנכ"ל (ראובן) מאציל אליו בהתבסס על keyword routing.

## Open Questions

- מה הסגנון הויזואלי הבסיסי של הפרויקט? (יש להוסיף reference images ל-`yuval/reference/` כדי לעגן אותו)
- האם לאפשר ל-יובל להשתמש ב-`quality: high` על פי בקשה, או לנעול על `medium` תמיד?
- כיצד לנהל ארכיון outputs — האם להגדיר מדיניות ניקוי?
- לעדכן את הסקיל: להחליף Python fallback ב-PowerShell (Python לא זמין ב-Git Bash בסביבה הנוכחית)
- לעדכן את הסקיל: להסיר `response_format` מה-payload של gpt-image-2 (פרמטר לא נתמך)

## Session Log

### 2026-05-06 — הוספת יובל ו-gpt-image-gen [shipped]

- **What was done:** נוצרו: `.claude/skills/gpt-image-gen/SKILL.md` (מעטפת OpenAI Images API עם curl + Python fallback), `.claude/agents/yuval.md` (הגדרת סוכן קנונית), `.claude/agents/reuven.md` (הגדרת Claude Code sub-agent למנכ"ל עם טבלת Sub-Agents), `yuval/reference/`, `yuval/outputs/`, `yuval/agent.md`, `yuval/skill.md`. עודכנו: `agent.md` (registry — agent_1 הוחלף ביובל active), `.env.example` (נוסף OPENAI_API_KEY).
- **Decisions:** `.env` כבר הכיל OPENAI_API_KEY — לא הוסף מחדש. נבחר Python fallback (לא jq) כ-primary לסביבות Windows/Git Bash. `.claude/agents/reuven.md` נוצר כ-thin Claude Code sub-agent definition שמפנה ל-`agent.md` בשורש לספציפיקציה המלאה. מבנה היברידי: קובץ flat ב-`.claude/agents/` לצד תיקיית עבודה `yuval/` בשורש.
- **Notes / Caveats:** `yuval/reference/` ריקה — יובל יפעל ללא reference style עד שיוסיפו תמונות. keyword routing מוגדר ב-`reuven.md` ובעדכון registry ב-`agent.md`.
- **Related:** [[ceo-agent]], [[claude-directory]], [[project-scaffold]]

### 2026-05-06 — יצירת תמונת שור ראשונה [shipped]

- **What was done:** יובל הריץ workflow מלא לבקשת "תמונה של שור". reference/ ריקה — תמונה ראשונה ללא style extraction. נוצרו `yuval/outputs/2026-05-06-bull.png` (1.3MB) ו-`2026-05-06-bull.txt` עם prompt log.
- **Decisions:** gpt-image-2 עדיין ממתין להפצת org verification (עד 15 דקות לאחר אימות) — השתמשנו ב-dall-e-3 כ-fallback. PowerShell שימש לפענוח base64 במקום Python (Python לא זמין ב-Git Bash בסביבה זו).
- **Notes / Caveats:** שני תיקונים נדרשים בסקיל: (1) החלפת Python fallback ב-PowerShell; (2) הסרת `response_format` מ-payload של gpt-image-2. פותחו כ-Open Questions לעיל.
- **Related:** [[yuval-agent-image-gen]]

### 2026-05-06 — איציק קאובוי רוכב על שור — תיאור טקסטואלי [shipped]

- **What was done:** יצירת `yuval/outputs/2026-05-06-izik-cowboy.png` (1.7MB, dall-e-3 HD) — גבר ממושקל שנות 50 עם שיער לבן-אפור, זקן מלוח-פלפל, עור כהה, רוכב על שור שחור. הסגנון עקבי עם התמונות הקודמות.
- **Decisions:** DALL-E 3 text-only — לא ניתן להשתמש בתמונת reference. תיארנו את האדם מהתמונה שהועלתה ובנינו prompt מפורט. PowerShell שימש ל-API call ו-base64 decode (Bash נכשל בגלל Unicode בנתיב).
- **Notes / Caveats:** הפנים קרובות אבל לא מדויקות — לדיוק מלא נדרש gpt-image-2 + תמונת reference. המשתמש יכול לשמור תמונה ב-`yuval/reference/` לשימוש עתידי.
- **Related:** [[yuval-agent-image-gen]]

### 2026-05-06 — קאובוי רוכב על שור [shipped]

- **What was done:** יצירת `yuval/outputs/2026-05-06-cowboy-on-bull.png` (1.8MB) — קאובוי עם כובע ולבוש מערבי רוכב על שור שחור באצטדיון רודאו, golden hour.
- **Decisions:** reference/ ריקה — ירשנו סגנון מ-bull.png הקודם (golden hour, cinematic, dark bull). המשכנו עם dall-e-3 + PowerShell decode.
- **Notes / Caveats:** סגנון עקבי עם התמונה הקודמת ללא reference images פורמליות — כשיתווספו references ל-yuval/reference/ יהיה style extraction מדויק יותר.
- **Related:** [[yuval-agent-image-gen]]
