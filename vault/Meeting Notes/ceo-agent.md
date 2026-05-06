# CEO Agent

## Overview

הסוכן הראשי (CEO Agent) הוא שכבת האורקסטרציה המרכזית של מערכת "The Five Agents". הוא פועל כנקודת המגע היחידה בין המשתמש לרשת הסוכנים, ואחראי על הבנת כוונת המשתמש, פירוק משימות, האצלה לסוכנים מתמחים, סינתזת תוצאות וניהול מחזור חיי המשימה המלא. הסוכן אינו מבצע לוגיקה תחומית — הוא חושב, מאציל, מפקח ומדווח. הסוכן מוגדר ב-`agent.md` ונטען בכל סשן דרך `CLAUDE.md`. זיכרון מתמיד נשמר ב-`memory/ceo_memory.json`.

## Open Questions

- מהן יכולות הסוכנים agent_1 עד agent_4? (PRD Open Item #1)
- מהי מדיניות שמירת הזיכרון — כמה סשנים לשמור? (Open Item #2)
- מהם סף ה-timeout לכל סוכן? (Open Item #3)
- כמה סוכנים מקביליים מותר להריץ בו-זמנית? (Open Item #4)
- מהי שיטת ההפעלה של סוכנים — sub-process / tool use / API? (Open Item #5)

## Session Log

### 2026-05-06 — יצירת CEO Agent ראשוני [shipped]

- **What was done:** נוצרו שלושה קבצים: `agent.md` (הוראות מלאות ב-10 סעיפים), `memory/ceo_memory.json` (מאותחל ריק), עדכון `CLAUDE.md` עם הוראה לטעון `agent.md` בכל סשן.
- **Decisions:** הגדרת sub-agents 1–4 כ-`pending` ב-Agent Registry — ייכנסו לפי PRD Open Items. נבחר לשמור את הגדרות sub-agents ב-`.claude/agents/` (Claude Code convention) ולא ב-`agents/` בשורש (כפי שמצוין בPRD §11) כי `.claude/agents/` הוא המיקום שClaude Code קורא.
- **Notes / Caveats:** כל 5 Open Items מ-PRD §13 נשארים פתוחים ומתועדים ב-Open Questions לעיל. failure message template כתובה בעברית (עם הערה לעברית לפי שפת המשתמש).
- **Related:** [[claude-directory]], [[obsidian-setup]], [[project-scaffold]]
