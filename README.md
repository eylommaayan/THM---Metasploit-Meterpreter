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
<img width="1248" height="832" alt="image" src="https://github.com/user-attachments/assets/1a744d73-f216-4f8f-b92e-f22167709651" />
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

## Payload ברירת מחדל במודולי Exploit

בחלק ממודולי ה־Exploit:

* מוגדר **Meterpreter ברירת מחדל**

לדוגמה:

* במודול **ms17_010_eternalblue**
  (ניצול פרצת EternalBlue ב־Windows)

📌 כאשר מריצים את המודול:

* Metasploit כבר מציע Payload מתאים
* אך **תמיד ניתן לשנות אותו ידנית**

---

## הצגת Payloads נוספים למודול מסוים

כדי לראות **אילו Payloads נוספים זמינים** עבור מודול Exploit כלשהו, ניתן להשתמש בפקודה:

```bash
show payloads
```

🔍 פקודה זו:

* מציגה רק Payloads **שמתאימים למודול הנוכחי**
* עוזרת לבחור Payload שמתאים:

  * ל־OS
  * לרשת
  * לסביבה

---



כשבוחרים Meterpreter – שואלים תמיד:

1. על איזה **מערכת הפעלה** אני תוקף?
2. איזה **כלים מותקנים** על היעד?
3. איזה **חיבור רשת** אני יכול להשיג בלי להיחסם?

---

👍


![Uploading image.png…]()





MS17-010 (EternalBlue)

Meterpreter רץ עם PID מספר 1304

🔸 בדיקת PID של Meterpreter
meterpreter > getpid
Current pid: 1304


📌 PID = Process ID
מספר ייחודי שמערכת ההפעלה נותנת לכל תהליך.

🔸 הצגת כל התהליכים במערכת
meterpreter > ps


🔍 מה רואים?

PID 1304 לא נקרא meterpreter.exe

הוא מופיע כ־spoolsv.exe

📌 spoolsv.exe הוא תהליך לגיטימי של Windows (שירות הדפסה)

➡️ Meterpreter מוזרק (Injected) לתוך תהליך קיים.

🔹 בדיקת DLLs של התהליך

גם אם נבדוק את הספריות שנטענו ע"י התהליך:

tasklist /m /fi "pid eq 1304"


🔍 התוצאה:

רשימה ארוכה של DLLs סטנדרטיים

❌ אין meterpreter.dll

❌ אין משהו שצועק "נוזקה"

📌 זו דוגמה מצוינת להסוואה ברמת מערכת ההפעלה.

📘 Meterpreter Flavors – סוגי Meterpreter

כפי שנלמד בפרקי Metasploit הקודמים,
Payloads של Metasploit מתחלקים לשתי קטגוריות עיקריות:

🔹 1. Payload Inline (Single)

נשלח ליעד בשלב אחד

פשוט יותר

גדול יותר בגודל

פחות גמיש

🔹 2. Payload Staged

נשלח ליעד בשני שלבים

Stager קטן (טעינה ראשונית)

טעינת ה-Payload המלא

יתרון: Payload ראשוני קטן → פחות חשוד

נפוץ מאוד ב-Meterpreter

📌 גם Meterpreter קיים בגרסאות:

Inline (stageless)

Staged

🔹 סוגי Meterpreter לפי מערכת יעד

Meterpreter מגיע בגרסאות רבות, בהתאם לפלטפורמה:

Android

Apple iOS

Java

Linux

macOS (OSX)

PHP

Python

Windows

🔹 איך רואים אילו Meterpreter קיימים?

באמצעות msfvenom:

msfvenom --list payloads | grep meterpreter


📌 הפקודה:

מציגה רק payloads של Meterpreter

מאפשרת להבין:

אילו מערכות נתמכות

איזה סוג חיבור (TCP / HTTP / HTTPS)

האם payload staged או stageless

🔹 איך בוחרים איזה Meterpreter להשתמש?

הבחירה תלויה ב־3 גורמים מרכזיים:

1️⃣ מערכת ההפעלה של היעד

Windows?

Linux?

Android?

macOS?

2️⃣ רכיבים זמינים ביעד

האם מותקן Python?

האם זה שרת PHP?

האם יש Java?

📌 דוגמה:

אתר PHP → payload מבוסס PHP

שרת Linux ללא GUI → payload CLI

3️⃣ סוג חיבורי הרשת האפשריים

האם TCP פתוח?

האם רק HTTPS יוצא החוצה?

האם IPv6 פחות מנוטר מ-IPv4?

📌 דוגמה:

רשת ארגונית → reverse_https נפוץ מאוד

NAT → Reverse ולא Bind

🔹 Payload ברירת מחדל של Exploit

חלק מה-Exploits:

מגיעים עם Payload ברירת מחדל

לדוגמה:

use exploit/windows/smb/ms17_010_eternalblue


פלט:

Using configured payload windows/x64/meterpreter/reverse_tcp


📌 כלומר:

Exploit כבר בחר Payload שמתאים

אבל אפשר לשנות אותו

🔹 הצגת Payloads תואמים ל-Exploit
show payloads


📌 זה קריטי:

לא כל Payload מתאים לכל Exploit

Metasploit מסנן אוטומטית Payloads לא תואמים

📘 פקודות Meterpreter – מבוא

בכל Session של Meterpreter:

meterpreter > help


📌 הפקודה תציג:

כל הפקודות הזמינות

מחולקות לפי קטגוריות

⚠️ חשוב:

לא כל פקודה תעבוד בכל מערכת
תלוי ב-OS, הרשאות, וגרסת Meterpreter

🔹 קטגוריות פקודות עיקריות

Core Commands

File System Commands

Networking Commands

System Commands

User Interface Commands

Webcam / Audio Commands

Privilege Escalation

Password & Hash Commands

📘 פקודות Core (החשובות ביותר)
פקודה	הסבר
background	מחזיר ל-msfconsole
exit	סוגר Session
guid	מזהה ייחודי ל-Session
help	תפריט עזרה
load	טעינת הרחבות
migrate	מעבר לתהליך אחר
sessions	מעבר בין Sessions
📘 פקודות מערכת (System)
פקודה	הסבר
getuid	באיזה משתמש אנחנו רצים
getpid	PID נוכחי
ps	רשימת תהליכים
kill	סיום תהליך
execute	הרצת פקודה
shell	פתיחת CMD רגיל
sysinfo	מידע על מערכת
reboot / shutdown	שליטה במערכת
🔹 בדיקת הרשאות – getuid
meterpreter > getuid


פלט:

NT AUTHORITY\SYSTEM


📌 זה אומר:

הרשאות SYSTEM

רמת שליטה מקסימלית ב-Windows

🔹 רשימת תהליכים – ps
meterpreter > ps


📌 שימושים:

לראות תהליכים פעילים

למצוא תהליך יציב ל-Migration

לזהות תהליכים של משתמשים

📘 migrate – מעבר בין תהליכים
meterpreter > migrate <PID>


📌 למה עושים migrate?

יציבות Session

גישה לפונקציות (כמו keylogger)

התחמקות מזיהוי

⚠️ אזהרה חשובה:

מעבר מתהליך SYSTEM → תהליך משתמש
עלול להוריד הרשאות ולא ניתן תמיד לשחזר

📘 hashdump – שליפת סיסמאות
meterpreter > hashdump


📌 מה זה עושה?

שולף את SAM database

מחזיר Hashes מסוג NTLM

📌 שימושים:

Pass-the-Hash

Rainbow Tables

זיהוי סיסמאות חלשות

📘 search – חיפוש קבצים
meterpreter > search -f flag2.txt


📌 שימושים:

CTF → מציאת flags

PT אמיתי → מציאת:

קבצי config

סיסמאות

מידע רגיש

📘 shell – מעבר ל-CMD רגיל
meterpreter > shell


📌 מה זה נותן?

סביבת CMD רגילה

פקודות Windows רגילות

🔁 חזרה ל-Meterpreter:

CTRL + Z

🧠 סיכום לשינון

✔ Meterpreter = Payload מתקדם
✔ מותאם לפלטפורמות שונות
✔ תומך ב-Post Exploitation
✔ כולל File, Network, System, Privilege
✔ migrate ו-hashdump הם כלים קריטיים
✔ תמיד להריץ help ולבדוק מה זמין



<img width="924" height="840" alt="image" src="https://github.com/user-attachments/assets/2730fa78-bb45-4050-8c4e-309c3fa331ef" />





