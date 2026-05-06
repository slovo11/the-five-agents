# יעל — Content Writer (pointer doc)

זהו מסמך הפניה לבני אדם. ההגדרה הקנונית של הסוכן נמצאת ב-[`.claude/agents/yael.md`](../.claude/agents/yael.md).

## מה יעל עושה

יעל היא כותבת התוכן של הפרויקט. היא LLM-only — Read/Write/Edit/Glob/Grep בלבד, ללא Bash, ללא רשת, ללא API. היא לוקחת מאמרי גלם מ-`Content/`, משכתבת אותם בסגנון הפרויקט, ומסמנת צורך בתמונות דרך `{{IMAGE_NEEDED: "..."}}` placeholders.

## איפה הסגנון מוגדר

- `yael/style-guide.md` — מדריך הסגנון (קול, טון, אוצר מילים, פתיחות/סיומים).
- `yael/reference/` — דוגמאות לטקסטים בסגנון. יעל סורקת את התיקייה בתחילת כל סשן.

## Flow ברמת עין-ציפור

1. ראובן מקבל בקשת שכתוב מהמשתמש ומאציל ליעל.
2. יעל קוראת style-guide + references, שולפת קובץ מ-`Content/`, משכתבת.
3. במקום שיש צורך בתמונה — מכניסה `{{IMAGE_NEEDED: "<prompt>"}}` בטקסט.
4. שומרת ב-`Output/<name>.md` ומחזירה לראובן רשימת ה-placeholders.
5. ראובן מטפל בכל placeholder: מפעיל את יובל עם ה-prompt, מקבל path לתמונה, מחליף את ה-placeholder ב-markdown image reference, ושומר את הגרסה הסופית.
6. ראובן מעביר את המקור מ-`Content/` ל-`Content/Ready/`.

## למה יעל לא קוראת ליובל ישירות

ב-Claude Code סאב-אייג'נטים לא יכולים להפעיל סאב-אייג'נטים אחרים — רק ראובן (המנכ"ל) יכול. לכן יעל משאירה placeholders וראובן הוא שמעבד אותם.
