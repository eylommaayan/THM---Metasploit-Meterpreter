<img width="903" height="391" alt="image" src="https://github.com/user-attachments/assets/a42c1150-6eb6-4894-8be8-691f257d8470" />


משימה 1: מבוא ל-Meterpreter

Meterpreter הוא Payload (מטען תקיפה) של כלי Metasploit, שנועד לתמוך בתהליך של בדיקות חדירה (Penetration Testing) באמצעות מגוון רחב של יכולות מתקדמות.

כאשר Meterpreter מופעל:

הוא רץ על מערכת היעד

ומתפקד כ־Agent (סוכן) בתוך ארכיטקטורת
Command & Control (C2)

כלומר:

המחשב התוקף (Attack Machine) שולט מרחוק במחשב היעד דרך Meterpreter.

באמצעות Meterpreter ניתן:

ליצור אינטראקציה עם מערכת ההפעלה של היעד

לגשת ל־קבצים

להריץ פקודות ייעודיות של Meterpreter
(שאינן פקודות מערכת רגילות)

🛡️ התחמקות ממערכות אבטחה (IDS / IPS)

אחת המטרות המרכזיות של Meterpreter היא להקשות על זיהויו על־ידי מערכות אבטחה מבוססות רשת:

IDS – Intrusion Detection System

IPS – Intrusion Prevention System

Meterpreter עושה זאת באמצעות:

תקשורת מוצפנת עם השרת שעליו רץ Metasploit
(בדרך כלל – המחשב של הבודק/התוקף)

🔐 אם הארגון:

לא מפענח

ולא מבצע בדיקה עמוקה של תעבורה מוצפנת
(כמו HTTPS נכנס ויוצא מהרשת)

➡️ אז מערכות IDS/IPS לא יוכלו לזהות את הפעילות של Meterpreter.

🦠 זיהוי על־ידי אנטי־וירוס

חשוב להבין:

Meterpreter כן מזוהה על־ידי רוב תוכנות האנטי־וירוס המודרניות

אך עדיין, השימוש בהצפנה ובארכיטקטורת C2
מעניק לו רמת הסוואה מסוימת (Stealth)

📌 כלומר:
לא בלתי־נראה – אבל בהחלט קשה יותר לזיהוי ברשת.

משימה 2: סוגי Meterpreter (Meterpreter Flavors)

ל-Meterpreter קיימות גרסאות רבות, המותאמות ל:

מערכות הפעלה שונות (Windows, Linux, Android וכו’)

ארכיטקטורות שונות

סוגי Payload שונים (Staged / Inline)

כדי לקבל מושג אילו גרסאות קיימות, ניתן להשתמש בפקודה:

msfvenom --list payloads | grep meterpreter


🔍 פקודה זו:

מציגה את כל ה־Payloads הזמינים ב־Metasploit

ומסננת רק את אלו שכוללים Meterpreter

כך ניתן:

להבין אילו גרסאות זמינות
<img width="1108" height="831" alt="image" src="https://github.com/user-attachments/assets/fdd33ead-33ee-4a94-b16b-c639861d03b8" />


לבחור Meterpreter מתאים לפי מערכת היעד

<img width="1249" height="795" alt="image" src="https://github.com/user-attachments/assets/8ac00be2-9ac0-4c03-a056-e83f62265558" />:

---

## בחירת גרסת Meterpreter – על מה זה מבוסס?

ההחלטה **איזו גרסת Meterpreter לבחור** מבוססת בעיקר על **שלושה גורמים מרכזיים**:

---

### 1️⃣ מערכת ההפעלה של היעד (Target Operating System)

השלב הראשון הוא לזהות:

* האם מערכת היעד היא **Linux**?
* **Windows**?
* **macOS**?
* **Android**?
* מערכת אחרת?

📌 כל מערכת הפעלה תומכת ב־**Meterpreter שונה**, ולכן
לא ניתן להשתמש בכל Payload על כל יעד.

דוגמה:

* Windows → meterpreter/windows
* Linux → meterpreter/linux
* Android → meterpreter/android

---

### 2️⃣ רכיבים זמינים על מערכת היעד (Available Components)

כאן בודקים:

* האם **Python** מותקן?
* האם זה **שרת Web עם PHP**?
* האם יש **PowerShell**?
* האם מדובר ב־**סביבה מצומצמת** ללא כלים מתקדמים?

🧠 הסיבה:
חלק מגרסאות Meterpreter **תלויות בסביבה הקיימת** על היעד.

דוגמאות:

* אם מותקן Python → ניתן להשתמש ב־python/meterpreter
* אם מדובר באתר PHP → אפשר להשתמש ב־php/meterpreter

---

### 3️⃣ סוגי חיבורי רשת אפשריים (Network Connection Types)

זה אחד הגורמים **הכי קריטיים**:

יש לבדוק:

* האם מותר **חיבור TCP ישיר (Raw TCP)**?
* האם אפשר רק **חיבור יוצא דרך HTTPS**?
* האם **IPv6** פחות מנוטר מארכיטקטורת **IPv4**?
* האם יש **Firewall / Proxy** מגביל?

📡 בחירת ה־Payload תלויה בשאלה:

> *איזה סוג תקשורת יכול לעבור ברשת בלי להיחסם או להיחשף*

דוגמאות:

* רשת ארגונית → לרוב רק HTTPS יוצא
* חיבור Reverse HTTPS → נפוץ ו"שקט" יותר
* שימוש ב־IPv6 → לעיתים פחות מפוקח

---


