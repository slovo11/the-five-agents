# Yael Agent — Content Writer

## Overview

יעל היא הסוכן השלישי במערכת (אחרי ראובן ויובל). תפקידה: לקחת מאמרי גלם מ-`Content/`, לשכתב אותם בסגנון הפרויקט (מוגדר ב-`yael/style-guide.md` + דוגמאות ב-`yael/reference/`), ולשמור את התוצר ב-`Output/<name>.md`. יעל היא **LLM-only** — Read/Write/Edit/Glob/Grep בלבד, ללא Bash, ללא רשת, ללא API, ללא יצירת תמונות.

כשיעל מזהה צורך בתמונה היא מכניסה `{{IMAGE_NEEDED: "<prompt>"}}` placeholder בטקסט. **היא לא קוראת ליובל ישירות** — האילוץ הארכיטקטוני של Claude Code (סאב-אייג'נט לא מפעיל סאב-אייג'נט) מחייב שראובן יהיה זה שמעבד את ה-placeholders: עובר עליהם בסדר, מפעיל את יובל פר-אחד, ומחליף את ה-placeholder ב-markdown image reference. ראובן גם מבצע את `mv Content/<name>.md Content/Ready/<name>.md` בסיום, כי ליעל אין Bash.

מבנה הקבצים: הגדרה קנונית ב-`.claude/agents/yael.md` (flat, עם `tools: Read, Write, Edit, Glob, Grep`), תיקיית עבודה `yael/` בשורש (style-guide + reference + agent.md pointer doc), ותיקיות תפעוליות `Content/`, `Content/Ready/`, `Output/`.

## Open Questions

- מילוי `yael/style-guide.md` בתוכן אמיתי — קול, טון, אוצר מילים, פתיחות/סיומים.
- אילו דוגמאות התחלתיות להעלות ל-`yael/reference/` (3-5 טקסטים שמאפיינים את הסגנון).
- האם יעל צריכה לתעד כל שכתוב בלוג נפרד (למשל `yael/log.md`), או שהתיעוד ב-`ceo_memory.json` של ראובן מספיק?
- מתי כדאי להוסיף תמונה? (פתיחה בלבד / כל סקשן / רק במעברים מרכזיים) — תלוי במילוי style-guide.
- כללי ברירת מחדל לתרגום: האם יעל מתרגמת רק כשהמשתמש מבקש במפורש, או שגם זיהוי שפת היעד מ-style-guide נחשב טריגר?

## Session Log

### 2026-05-06 — הוספת יעל (כותבת תוכן LLM-only) [shipped]

- **What was done:** נוצרו: `.claude/agents/yael.md` (הגדרה קנונית עם הגבלת tools ל-Read/Write/Edit/Glob/Grep), `yael/style-guide.md` (placeholder ראשוני), `yael/reference/.gitkeep`, `yael/agent.md` (pointer doc), ותיקיות תפעוליות `Content/`, `Content/Ready/`, `Output/` (עם .gitkeep). עודכנו: `.claude/agents/reuven.md` (טבלת Sub-Agents עם yael, Routing rule for יעל, סעיף Post-יעל protocol המתאר את עיבוד ה-placeholders+הפעלת יובל+`mv` המקור, Status שעלה ל-2 active), `agent.md` (Agent Registry עם yael active), `vault/Meeting Notes/_index.md` (לינק ל-topic זה).
- **Decisions:** **יעל לא נוגעת ב-`Content/` בכלל** — לא העתקה, לא marker, לא frontmatter. ראובן הוא שמעביר את המקור ל-`Content/Ready/` עם `mv` כחלק מה-post-processing שלו, באותו צעד שבו הוא מטפל ב-placeholders. שומר על יעל LLM-only טהורה ומרכז את כל פעולות ה-FS המבניות אצל המנכ"ל. דפוס הקבצים תואם ליובל: canonical flat ב-`.claude/agents/` + תיקיית עבודה מקבילה בשורש + `agent.md` pointer.
- **Notes / Caveats:** `yael/style-guide.md` הוא placeholder — עד שייכתב תוכן אמיתי, יעל תפעל לפי best-practice generic Hebrew content writing. `yael/reference/` ריקה — אין דוגמאות סגנון להתבסס עליהן בריצה הראשונה. Smoke test מלא (Content/test.md → ראובן→יעל→placeholders→ראובן→יובל→merge→mv) עוד לא בוצע.
- **Related:** [[ceo-agent]], [[yuval-agent-image-gen]], [[claude-directory]]
