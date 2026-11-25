# Smart Parking License Plate Tracker

מערכת מיקרו-סרביסים לניהול כניסת רכבים לחניון חכם (Track 1 - Lite).

## ארכיטקטורת המערכת

- **Web Service (`nginx:alpine`)**: מנגיש את לוח הבקרה (Dashboard) לשומר בפורט `8080`, ומבצע Reverse Proxy לנתיב `/parking-images/` אל שרת האחסון הפנימי.
- **Storage Service (`httpd:2.4`)**: שרת Apache המשמש לאחסון והגשת תמונות לוחיות הרישוי בפורט `8081`.
- **Data Persistence (`parking_images_volume`)**: שימוש ב-Docker Named Volume לשמירת תמונות הרכבים גם לאחר הסרה והפעלה מחדש של הקונטיינרים.
- **CI/CD (`GitHub Actions`)**: הרצת `docker compose build` לבדיקת תקינות בכל `push`, והעלאת האימג'ים ל-GitHub Container Registry (`ghcr.io`).

## הוראות הרצה

1. שכפול הפרויקט והפעלת השירותים:

```bash
git clone https://github.com/siramdayan-source/smart-parking-tracker.git
cd smart-parking-tracker
docker compose up -d --build
```

2. כניסה ללוח הבקרה בדפדפן: http://localhost:8080

3. בדיקת Data Persistence (Volume):

הוספת תמונה לקונטיינר רץ:

```bash
docker cp storage/images/car1.jpg parking_storage:/usr/local/apache2/htdocs/images/car3.jpg
```

כיבוי והפעלה מחדש של הקונטיינרים:

```bash
docker compose down && docker compose up -d
```

התמונה `car3.jpg` נשארת זמינה בכתובת http://localhost:8081/images/car3.jpg

## צוות הפרויקט וחלוקת עבודה

- **שירם דיין**: הקמת שרת Storage (Apache), הגדרת `docker-compose.yml` וניהול Named Volume.
- **לבן אלבז**: הקמת שרת Web (Nginx + Dashboard HTML), הגדרת CI/CD ב-GitHub Actions, העלאה ל-GHCR ותיעוד.
