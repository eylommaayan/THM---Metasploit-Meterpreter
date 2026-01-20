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



משימה 3: פקודות Meterpreter

כאשר אתה נמצא בתוך Session של Meterpreter
(כלומר, רואה בשורת הפקודה את הסימון):

meterpreter>


ניתן להקליד את הפקודה:

help


📌 פקודה זו תציג רשימה מלאה של כל הפקודות הזמינות ב־Meterpreter.

<img width="923" height="682" alt="image" src="https://github.com/user-attachments/assets/c9c2d619-cd66-43be-95e6-92e066b10f11" />

use exploit/windows/smb/psexec

set smbuser ballen
set smbpass Password1

set rhosts 10.65.189.26

run


משימה 4: Post-Exploitation עם Meterpreter

שלב Post-Exploitation הוא השלב שמגיע אחרי שכבר הושגה גישה למערכת היעד.
בשלב זה בודקים, חוקרים ומבינים את המערכת מבפנים.

🔹 PS – הצגת תהליכים רצים

הפקודה ps מציגה:

רשימה של כל התהליכים שרצים כרגע על מערכת היעד

לכל תהליך מוצג גם PID (Process ID) – מזהה ייחודי של התהליך

📌 למה זה חשוב?

מידע על תהליכים עוזר להבין:

אילו תוכנות פעילות

באיזה הקשר Meterpreter רץ

ה־PID משמש בהמשך לצורך Migration (מעבר תהליך)

🔹 Migrate – מעבר לתהליך אחר

Migration פירושו:

העברת ה־Meterpreter מתהליך אחד לתהליך אחר במערכת

📌 למה עושים Migration?

כדי ש־Meterpreter:

יהיה יציב יותר

יוכל לפעול בהקשר מתאים יותר

ולעיתים להיטמע טוב יותר בתוך פעילות המערכת

כדי לבצע Migration:

משתמשים בפקודת migrate

ומספקים לה את ה־PID של תהליך היעד

בדוגמה שמוצגת:

Meterpreter עובר לתהליך עם מזהה PID 716

🧠 רעיון מרכזי:

Meterpreter הוא לא “תהליך קבוע” – הוא יכול לזוז בין תהליכים בהתאם לצורך.

🔹 Search – חיפוש קבצים במערכת

הפקודה search משמשת ל:

חיפוש קבצים על מערכת היעד

איתור קבצים שעשויים להכיל מידע רגיש או מעניין

📌 דוגמאות לשימוש לימודי:

קבצי תצורה

קבצים עם שמות חשודים

מסמכים או נתונים שנשמרו מקומית

הפקודה מאפשרת:

חיפוש לפי שם

סיומת

מיקום

🔹 Shell – פתיחת שורת פקודה רגילה

הפקודה shell:

פותחת Command Line רגיל של מערכת היעד

למשל: CMD / Bash

📌 הבדל חשוב:

Meterpreter = סביבת פקודות ייעודית

Shell = שורת פקודה רגילה של מערכת ההפעלה

כדי לחזור מ־Shell ל־Meterpreter:

לוחצים CTRL + Z

🧠 סיכום לימודי קצר

ב־Post-Exploitation עם Meterpreter:

ps → מבינים מה רץ במערכת
<img width="691" height="131" alt="image" src="https://github.com/user-attachments/assets/c0bed08c-8959-4cf5-88ca-969eed66e4f6" />

migrate → עובדים מתוך תהליך מתאים

search → מאתרים מידע מעניין

shell → גישה ישירה למערכת ההפעלה

📌 זהו שלב של חקירה והבנה, לא רק “שליטה”

בשמחה 😊
להלן **ניסוח מדריך לימודי מסודר** לשלב שביצעתם – **מעבר ממודול אחד למודול אחר ב-Metasploit**.
הטקסט מתאים לקורס / אתר / README לימודי.

---

# 📘 מעבר בין מודולים ב-Metasploit (שלב לימודי)

## 🎯 מטרת השלב

בשלב זה נלמד כיצד **לעבור ממודול Exploit אחד למודול Exploit אחר** בתוך Metasploit,
ומה המשמעות של מעבר כזה ברמת סביבת העבודה.

---

## 🔍 רקע חשוב להבנה

ב-Metasploit:

* כל **Exploit** הוא **מודול עצמאי**
* אין “גרסאות” בתוך אותו מודול
* כדי לעבוד עם Exploit אחר — יש **לבחור מודול חדש**

📌 כלומר:
**לא משנים הגדרה בתוך אותו מודול, אלא מחליפים מודול עבודה**

---

## 📂 המצב ההתחלתי

בתחילת השלב היינו בתוך המודול:

```
exploit/windows/smb/ms17_010_eternalblue
```

זהו מודול שמבוסס על **ניצול חולשה (Vulnerability-based Exploit)**.

במהלך המעבדה הופיעה הפניה למודול אחר:

```
exploit/windows/smb/psexec
```

זהו מודול מסוג שונה, שמבוסס על **הרשאות (Credential-based Exploit)**.

---

## 🔄 שלב המעבר – החלפת מודול עבודה

כדי לעבור למודול החדש:

1. אין צורך “לצאת” בצורה מיוחדת מהמודול הקודם
2. פשוט בוחרים מודול חדש לפי **שם הנתיב המלא שלו**
3. הבחירה מחליפה את סביבת העבודה הנוכחית

📌 לאחר הבחירה:

* כל ההגדרות הקודמות מתאפסות
* אנחנו עובדים עכשיו עם Exploit אחר לגמרי
<img width="987" height="591" alt="image" src="https://github.com/user-attachments/assets/f13e0a24-97e8-42f7-824c-0145339f72a0" />

---

## ✅ איך יודעים שהמעבר הצליח?

הסימן לכך שהמעבר בוצע בהצלחה הוא שינוי ה-prompt.

לדוגמה:

```
msf6 exploit(windows/smb/psexec) >
```

זה מעיד שאנחנו נמצאים כעת בתוך **מודול חדש**, ולא באותו Exploit קודם.

---

#

* Metasploit בנוי ממודולים נפרדים
* כל Exploit הוא מודול עצמאי
* מעבר בין Exploits מתבצע באמצעות **בחירת מודול חדש**
* זהו מעבר של *סביבת עבודה*, לא שינוי הגדרה
* ההבנה הזו חשובה לפני שממשיכים לשלבים מתקדמים יותר


מעולה 👍
להלן **ניסוח מדריך לימודי מסודר** לשלב הסיום –
**הכניסה המוצלחת ל-Meterpreter**.
הטקסט מתאים לקורס / אתר / README, ומסביר *מה היה צריך לקרות כדי שזה יצליח*.

---

# 📘 כניסה מוצלחת ל-Meterpreter – סיכום שלב לימודי

## 🎯 מטרת השלב

בשלב זה למדנו **מהם התנאים הנדרשים** כדי שמודול PsExec יסתיים בפתיחת
**Meterpreter Session פעיל**.

המטרה אינה “הרצה”, אלא הבנה:

> למה הפעם זה עבד, ומה חייב להיות מוגדר נכון.

---

## 🔑 התנאים להצלחה בכניסה ל-Meterpreter

כדי להגיע לשורת:

```
meterpreter >
```

נדרשו **כל התנאים הבאים יחד**:

---

### 1️⃣ מודול מתאים

המודול הפעיל היה:

```
exploit/windows/smb/psexec
```

📌 זהו מודול המבוסס על:

* SMB
* הרשאות קיימות
* יצירת שירות זמני במערכת היעד

---
<img width="962" height="362" alt="image" src="https://github.com/user-attachments/assets/39815238-1ce8-4ffe-8289-eb1eccc9638c" />

### 2️⃣ Credentials תקפים

הוגדרו:

* שם משתמש תקף
* סיסמה תקפה
* משתמש עם הרשאות מתאימות (לרוב Administrator)

📌 ללא הרשאות מתאימות – PsExec לא יוכל לבצע את הפעולה.

<img width="777" height="137" alt="image" src="https://github.com/user-attachments/assets/5b754f49-3bf1-4fc8-900a-cc6f64b01eee" />


<img width="943" height="611" alt="image" src="https://github.com/user-attachments/assets/c739c94f-db1d-4c97-9e58-efd73d2c1967" />


### 3️⃣ כתובת יעד נכונה (RHOSTS)

הוגדרה כתובת מערכת היעד:

* IP נכון
* מערכת זמינה
* פורט SMB פתוח (445)

📌 זהו תנאי בסיסי לכל מודול מרוחק.

run
<img width="1003" height="372" alt="image" src="https://github.com/user-attachments/assets/a4c8c479-d888-483c-a7e2-29f3586df64a" />


### 4️⃣ Payload מסוג Meterpreter

📘 סדר פקודות – כניסה מוצלחת ל-Meterpreter (PsExec)
1️⃣ בחירת מודול העבודה
use exploit/windows/smb/psexec

2️⃣ הגדרת פרטי התחברות (Credentials)
set smbuser <USERNAME>
set smbpass <PASSWORD>


דוגמה לימודית:

set smbuser ballen
set smbpass Password1

3️⃣ הגדרת כתובת היעד
set rhosts <TARGET_IP>


דוגמה לימודית:

set rhosts 10.65.189.26

4️⃣ בדיקת הגדרות (שלב וידוא)
show options


ודא ש-:

SMBUSER ו-SMBPASS מוגדרים

RHOSTS מוגדר

ה-Payload (Meterpreter) וה-Listener מופיעים

5️⃣ הפעלה (בסביבה מורשית)
run

6️⃣ אינדיקציה להצלחה

אם כל התנאים מתקיימים, תיפתח שורת:

meterpreter >

🧠 נקודות לימוד חשובות

rhosts הוא Option, לא פקודה → תמיד עם set

PsExec מבוסס הרשאות קיימות, לא על חולשה

Meterpreter הוא תוצאה של שילוב נכון: מודול + Credentials + RHOSTS + Payload + Listener

```
meterpreter >
```

📌 זהו **סימן חד־משמעי להצלחה**.

---

## 🧠 נקודה לימודית חשובה

ההצלחה כאן אינה נובעת מ”פקודה אחת נכונה”, אלא מ־
**שרשרת של הגדרות נכונות**.

אם אחד מהבאים היה שגוי:

* IP
* Credentials
* Payload
* Listener
  ➡️ Meterpreter לא היה נפתח.

---


