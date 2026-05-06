# Claude Directory Structure

## Overview

תיקיית `.claude/` היא ה"מוח" המקומי של Claude Code לפרויקט זה. היא מכילה שלושה תתי-תיקיות: `agents/` להגדרות סוכנים מותאמים, `skills/` ליכולות שניתן לשלב בסשנים, ו-`commands/` לפקודות slash מותאמות. כל תיקייה ריקה בשלב זה (מכילה רק `.gitkeep`) ותתמלא בהמשך.

## Open Questions

- אילו סוכנים יוגדרו ב-`agents/`? (מנכ"ל + 4 סוכנים כפופים — להגדיר בשלב הבא)
- אילו פקודות slash יוגדרו ב-`commands/`?

## Session Log

### 2026-05-06 — יצירת מבנה .claude/ [shipped]

- **What was done:** נוצרו תיקיות `.claude/agents/`, `.claude/skills/`, `.claude/commands/` עם `.gitkeep` בכל אחת. הוגדר `.gitignore` שמוציא `settings.local.json`.
- **Decisions:** שימוש ב-`.gitkeep` כדי לשמור תיקיות ריקות ב-git. `settings.local.json` מוחרג כי הוא מכיל permissions מקומיים.
- **Notes / Caveats:** `settings.local.json` נוצר אוטומטית על ידי Claude Code ומכיל אישורי פקודות (Bash permissions) — הוא מכונה-ספציפי.
- **Related:** [[project-scaffold]], [[superpowers-plugin]], [[obsidian-setup]]

---

## פירוט קבצים ותיקיות

### `.claude/agents/`
**מה זה:** תיקייה לקבצי הגדרות סוכנים מותאמים לפרויקט (`.md` files עם system prompt לכל סוכן).
**משויך ל:** מנכ"ל (סוכן ראשי) + כל הסוכנים הכפופים
**סטטוס:** ריק — יתמלא בשלב בניית הסוכנים
**קבצים קשורים:** [[superpowers-plugin#dispatching-parallel-agents]]

---

### `.claude/skills/`
**מה זה:** תיקייה לסקילים — יכולות מובנות שClaude Code טוען בהתאם לקונטקסט. כל skill הוא תיקייה עם `SKILL.md`.
**משויך ל:** כל הסוכנים (שיתוף יכולות)
**סטטוס:** מכיל 17 סקילים (14 מ-Superpowers + 3 Obsidian)
**קבצים קשורים:** [[superpowers-plugin]], [[obsidian-setup]]

---

### `.claude/commands/`
**מה זה:** תיקייה לפקודות slash מותאמות לפרויקט (למשל `/publish`, `/brief`).
**משויך ל:** משתמש / מנכ"ל
**סטטוס:** ריק — יתמלא לפי הצורך
**קבצים קשורים:** [[claude-directory]]

---

### `.claude/settings.local.json`
**מה זה:** קובץ הרשאות מקומי שנוצר אוטומטית על ידי Claude Code. מגדיר אילו פקודות Bash מותרות ללא אישור ידני.
**משויך ל:** Claude Code (תשתית)
**הערה:** לא ב-git (`.gitignore`)
**קבצים קשורים:** [[project-scaffold#gitignore]]
