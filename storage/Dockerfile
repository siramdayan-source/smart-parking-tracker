FROM httpd:2.4-alpine # טוען אימג' רשמי של שרת Apache httpd גרסה 2.4 מבוסס Alpine
COPY ./images/ /usr/local/apache2/htdocs/images/ # מעתיק את תמונות הרכבים לתיקיית התמונות של Apache
EXPOSE 80 # מצהיר שהקונטיינר משתמש בפורט 80 מבפנים
CMD ["httpd-foreground"] # מפעיל את Apache במצב חזית כדי שהקונטיינר ימשיך לרוץ
