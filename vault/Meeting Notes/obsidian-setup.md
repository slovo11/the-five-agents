# Obsidian Setup

## Overview

הפרויקט פועל גם כ-Obsidian vault — הגדרות Obsidian נמצאות ב-`.obsidian/`, וה-vault עצמו ב-`vault/`. בנוסף הותקנו שלושה סקילים ייעודיים לניהול vault: `obsidian-vault-workflow` (הפרוטוקול המחייב), `obsidian-markdown` (תחביר Obsidian), ו-`obsidian-bases` (תצוגות בסיסי נתונים). הסקיל `obsidian-vault-workflow` מחייב קריאה ועדכון של קובצי vault לפני ואחרי כל משימה.

## Open Questions

- האם נגדיר plugins נוספים ב-Obsidian (Dataview, Tasks, Kanban)?
- האם ה-vault ישותף ב-iCloud / OneDrive מעבר ל-git?

## Session Log

### 2026-05-06 — הגדרת Obsidian vault ויצירת תיעוד ראשוני [shipped]

- **What was done:** יצירת מבנה `vault/` עם 4 תיקיות (Meeting Notes, Content Briefs, Brand Guidelines, Publishing Log) + `_index.md` לכל אחת. יצירת 4 קבצי תיעוד ל-3 קבוצות קבצי פרויקט (project-scaffold, claude-directory, superpowers-plugin, obsidian-setup).
- **Decisions:** שימוש ב-obsidian-vault-workflow כפרוטוקול מחייב — יש לקרוא topic file לפני כל משימה ולעדכן אחריה.
- **Notes / Caveats:** `.obsidian/app.json` ריק (`{}`) — הגדרות Obsidian ברירת מחדל.
- **Related:** [[claude-directory]], [[project-scaffold]], [[superpowers-plugin]]

---

## פירוט קבצים

### `.obsidian/` (תיקייה)
**מה זה:** קובצי הגדרות של אפליקציית Obsidian — נוצרים אוטומטית ע"י Obsidian Desktop.
**משויך ל:** Obsidian (לא סוכן)

#### `.obsidian/app.json`
הגדרות כלליות של האפליקציה. כרגע ריק (`{}`).

#### `.obsidian/appearance.json`
הגדרות מראה — theme, גופן, צבעים.

#### `.obsidian/core-plugins.json`
אילו core plugins של Obsidian מופעלים (קובץ, חיפוש, תגיות, גרף וכו').

#### `.obsidian/graph.json`
הגדרות תצוגת Graph View — צבעים, פילטרים, עוצמת חיבורים.

#### `.obsidian/workspace.json`
מצב ה-workspace האחרון — אילו קבצים פתוחים, מיקום חלונות.

**קבצים קשורים:** [[obsidian-setup#obsidian-markdown]]

---

### `vault/` (תיקייה)
**מה זה:** זיכרון ארוך-טווח של הפרויקט בפורמט Obsidian. מאורגן לפי נושא (topic per file).
**משויך ל:** כל הסוכנים (קריאה), Claude Code (כתיבה)

#### `vault/Meeting Notes/`
תיעוד החלטות ארכיטקטורה וסשני עבודה. קובץ אחד לנושא.

#### `vault/Content Briefs/`
תקצירי תוכן ומשימות עריכה.

#### `vault/Brand Guidelines/`
זהות מותג, טון, ויזואליות.

#### `vault/Publishing Log/`
תיעוד ריצות פרסום ותוצאות.

**קבצים קשורים:** [[obsidian-setup#obsidian-vault-workflow]]

---

### סקיל: `obsidian-vault-workflow` {#obsidian-vault-workflow}
**מה הוא עושה:** הפרוטוקול המחייב לעבודה עם ה-vault — Phase 1 (קריאה לפני משימה) ו-Phase 2 (כתיבת Session Log אחרי משימה). **חובה להפעיל בכל תחילת סשן ולאחר כל פקודה.**
**קובץ:** `.claude/skills/obsidian-vault-workflow/SKILL.md`
**משויך ל:** כל הסוכנים (תשתית זיכרון)
**קבצים קשורים:** [[obsidian-setup#obsidian-markdown]], [[obsidian-setup#obsidian-bases]]

---

### סקיל: `obsidian-markdown` {#obsidian-markdown}
**מה הוא עושה:** תחביר Obsidian Flavored Markdown — wikilinks, embeds, callouts, properties, tags. כולל references לדוקומנטציה מלאה.
**קובץ:** `.claude/skills/obsidian-markdown/SKILL.md`
**משויך ל:** כל מי שכותב לvault
**קבצים קשורים:** [[obsidian-setup#obsidian-vault-workflow]], [[obsidian-setup#obsidian-bases]]

---

### סקיל: `obsidian-bases` {#obsidian-bases}
**מה הוא עושה:** יצירת ועריכת קבצי `.base` — תצוגות database של notes עם פילטרים, formulas, וסיכומים. מאפשר יצירת dashboards על גבי ה-vault.
**קובץ:** `.claude/skills/obsidian-bases/SKILL.md`
**משויך ל:** מנכ"ל (דאשבורד ניהולי)
**קבצים קשורים:** [[obsidian-setup#obsidian-markdown]]
