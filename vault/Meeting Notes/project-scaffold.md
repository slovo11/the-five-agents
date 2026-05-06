# Project Scaffold

## Overview

קבצי השורש של פרויקט "The Five Agents" — מערכת יצירת תוכן רב-סוכנים. קבצים אלו מגדירים את זהות הפרויקט, משתני סביבה, והנחיות ל-Claude Code. הם נוצרו בשלב ה-bootstrap הראשוני לפני כתיבת קוד כלשהו.

## Open Questions

- אילו משתני סביבה נוספים יידרשו כשהסוכנים יתחילו לעבוד (API keys לפלטפורמות תוכן)?
- האם נוסיף `AGENT_MODEL` נפרד לכל סוכן ב-`.env`?

## Session Log

### 2026-05-06 — יצירת scaffold ראשוני [shipped]

- **What was done:** נוצרו קבצי השורש של הפרויקט: `CLAUDE.md`, `.env`, `.env.example`, `.gitignore`. הועלו ל-GitHub (`slovo11/the-five-agents`, branch main).
- **Decisions:** `.env` הוחרג מ-git דרך `.gitignore` כדי למנוע חשיפת API keys. `.env.example` נשמר ב-repo כתבנית.
- **Notes / Caveats:** `ANTHROPIC_API_KEY` ריק ב-`.env` — יש למלא לפני הרצה ראשונה.
- **Related:** [[claude-directory]], [[superpowers-plugin]]

---

## פירוט קבצים

### `CLAUDE.md`
**מה הוא עושה:** קובץ הנחיות ל-Claude Code — מוטען אוטומטית בתחילת כל סשן. מכיל תיאור הפרויקט ומבנה תיקיית `.claude/`.
**משויך ל:** Claude Code (הסוכן הראשי / מנכ"ל)
**קבצים קשורים:** [[claude-directory]]

---

### `.env`
**מה הוא עושה:** משתני סביבה מקומיים — לא נכנס ל-git. מכיל `ANTHROPIC_API_KEY`, `CLAUDE_MODEL`, `PROJECT_NAME`.
**משויך ל:** כל הסוכנים (צורך ב-API key לקריאות Claude)
**קבצים קשורים:** [[project-scaffold#env-example]]

---

### `.env.example` {#env-example}
**מה הוא עושה:** תבנית ציבורית של `.env` — מראה אילו משתנים נדרשים בלי לחשוף ערכים. כל מפתח/מכונה חדשה מעתיקה ממנו.
**משויך ל:** כל הסוכנים
**קבצים קשורים:** [[project-scaffold#env]]

---

### `.gitignore`
**מה הוא עושה:** מונע מ-git לעקוב אחרי `.env` (סודות) ו-`.claude/settings.local.json` (הגדרות מכונה מקומיות).
**משויך ל:** תשתית (לא סוכן ספציפי)
**קבצים קשורים:** [[project-scaffold#env]]
