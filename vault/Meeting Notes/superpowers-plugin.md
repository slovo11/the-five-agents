# Superpowers Plugin

## Overview

14 סקילים שהותקנו ידנית מהפלאגין הפתוח [obra/superpowers](https://github.com/obra/superpowers) לתוך `.claude/skills/`. הסקילים מספקים לClaude Code יכולות מתקדמות לפיתוח רב-סוכנים, בדיקות, code review, ותכנון. כל סקיל הוא תיקייה עם `SKILL.md` (ולפעמים קבצי עזר נוספים).

## Open Questions

- none

## Session Log

### 2026-05-06 — התקנת Superpowers ידנית [shipped]

- **What was done:** clone של `obra/superpowers` ל-temp, העתקת תיקיית `skills/` ל-`.claude/skills/` ללא דריסה של קבצים קיימים. 46 קבצים, 8,475 שורות.
- **Decisions:** התקנה ידנית (לא דרך `/plugin`) כי מערכת הפלאגינים לא זמינה בסביבה זו.
- **Notes / Caveats:** ה-repo המקורי מכיל גם `commands/` ו-`agents/` — לא קיימים בגרסה הנוכחית.
- **Related:** [[claude-directory]], [[obsidian-setup]]

---

## פירוט הסקילים

### `brainstorming` {#brainstorming}
**מה הוא עושה:** סיעור מוחות עם ממשק ויזואלי — מפעיל שרת WebSocket מקומי שמציג רעיונות בדפדפן בזמן אמת.
**קבצים:** `SKILL.md`, `scripts/server.cjs`, `scripts/helper.js`, `scripts/start-server.sh`, `scripts/stop-server.sh`, `scripts/frame-template.html`, `spec-document-reviewer-prompt.md`, `visual-companion.md`
**משויך ל:** סוכן תוכן / מנכ"ל
**קבצים קשורים:** [[superpowers-plugin#subagent-driven-development]]

---

### `dispatching-parallel-agents` {#dispatching-parallel-agents}
**מה הוא עושה:** מגדיר כיצד לשגר מספר סוכני-משנה במקביל ולאסוף את תוצאותיהם.
**קבצים:** `SKILL.md`
**משויך ל:** מנכ"ל (סוכן ראשי — מתאם סוכנים)
**קבצים קשורים:** [[claude-directory#agents]], [[superpowers-plugin#subagent-driven-development]]

---

### `executing-plans` {#executing-plans}
**מה הוא עושה:** הנחיות לביצוע תכניות עבודה צעד-אחר-צעד תוך עדכון רשימת משימות.
**קבצים:** `SKILL.md`
**משויך ל:** כל הסוכנים
**קבצים קשורים:** [[superpowers-plugin#writing-plans]]

---

### `finishing-a-development-branch` {#finishing-a-development-branch}
**מה הוא עושה:** תהליך סגירת branch פיתוח — בדיקות, code review, merge, ניקיון.
**קבצים:** `SKILL.md`
**משויך ל:** סוכן פיתוח / מנכ"ל
**קבצים קשורים:** [[superpowers-plugin#requesting-code-review]], [[superpowers-plugin#using-git-worktrees]]

---

### `receiving-code-review` {#receiving-code-review}
**מה הוא עושה:** הגדרת תפקיד "מקבל ה-review" — כיצד לעבד הערות reviewer ולהשיב עליהן.
**קבצים:** `SKILL.md`
**משויך ל:** סוכן מפתח
**קבצים קשורים:** [[superpowers-plugin#requesting-code-review]]

---

### `requesting-code-review` {#requesting-code-review}
**מה הוא עושה:** הגדרת תהליך בקשת code review — שיגור reviewer כ-subagent, פורמט הדוח.
**קבצים:** `SKILL.md`, `code-reviewer.md`
**משויך ל:** מנכ"ל / סוכן מפתח
**קבצים קשורים:** [[superpowers-plugin#receiving-code-review]], [[superpowers-plugin#subagent-driven-development]]

---

### `subagent-driven-development` {#subagent-driven-development}
**מה הוא עושה:** פיתוח מונחה sub-agents — מחלק כל feature לשלבים (spec → impl → review) ומשגר סוכן נפרד לכל שלב.
**קבצים:** `SKILL.md`, `implementer-prompt.md`, `spec-reviewer-prompt.md`, `code-quality-reviewer-prompt.md`
**משויך ל:** מנכ"ל (אורקסטרציה)
**קבצים קשורים:** [[superpowers-plugin#dispatching-parallel-agents]], [[superpowers-plugin#requesting-code-review]]

---

### `systematic-debugging` {#systematic-debugging}
**מה הוא עושה:** מתודולוגיית דיבוג שיטתי — root cause tracing, condition-based waiting, defense-in-depth.
**קבצים:** `SKILL.md`, `root-cause-tracing.md`, `condition-based-waiting.md`, `condition-based-waiting-example.ts`, `defense-in-depth.md`, `find-polluter.sh`, `test-academic.md`, `test-pressure-1/2/3.md`, `CREATION-LOG.md`
**משויך ל:** סוכן פיתוח / דיבוג
**קבצים קשורים:** [[superpowers-plugin#test-driven-development]]

---

### `test-driven-development` {#test-driven-development}
**מה הוא עושה:** TDD — כתיבת בדיקות לפני קוד, אנטי-פטרנים לבדיקות שיש להימנע מהם.
**קבצים:** `SKILL.md`, `testing-anti-patterns.md`
**משויך ל:** סוכן פיתוח
**קבצים קשורים:** [[superpowers-plugin#systematic-debugging]]

---

### `using-git-worktrees` {#using-git-worktrees}
**מה הוא עושה:** עבודה עם git worktrees — הפעלת מספר branches במקביל בתיקיות נפרדות, שימושי לסוכנים מקביליים.
**קבצים:** `SKILL.md`
**משויך ל:** מנכ"ל / כל הסוכנים
**קבצים קשורים:** [[superpowers-plugin#dispatching-parallel-agents]], [[superpowers-plugin#finishing-a-development-branch]]

---

### `using-superpowers` {#using-superpowers}
**מה הוא עושה:** מדריך שימוש בפלאגין Superpowers עצמו — כיצד לזמן סקילים, references לכלי AI שונים.
**קבצים:** `SKILL.md`, `references/codex-tools.md`, `references/copilot-tools.md`, `references/gemini-tools.md`
**משויך ל:** כל הסוכנים
**קבצים קשורים:** [[superpowers-plugin]]

---

### `verification-before-completion` {#verification-before-completion}
**מה הוא עושה:** פרוטוקול אימות לפני הכרזת סיום משימה — בדיקת כל הדרישות, הרצת בדיקות, קריאה חוזרת.
**קבצים:** `SKILL.md`
**משויך ל:** כל הסוכנים
**קבצים קשורים:** [[superpowers-plugin#systematic-debugging]]

---

### `writing-plans` {#writing-plans}
**מה הוא עושה:** כתיבת תכניות עבודה מפורטות לפני ביצוע — מבנה, סעיפים, רמת פירוט.
**קבצים:** `SKILL.md`, `plan-document-reviewer-prompt.md`
**משויך ל:** מנכ"ל / כל הסוכנים
**קבצים קשורים:** [[superpowers-plugin#executing-plans]]

---

### `writing-skills` {#writing-skills}
**מה הוא עושה:** כתיבת סקילים חדשים — best practices של Anthropic, שכנוע, גרפים, בדיקת סקילים עם subagents.
**קבצים:** `SKILL.md`, `anthropic-best-practices.md`, `persuasion-principles.md`, `render-graphs.js`, `graphviz-conventions.dot`, `testing-skills-with-subagents.md`, `examples/CLAUDE_MD_TESTING.md`
**משויך ל:** מנכ"ל / developer
**קבצים קשורים:** [[superpowers-plugin#subagent-driven-development]]
