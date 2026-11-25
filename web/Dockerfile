FROM nginx:alpine # טוען אימג' קל של שרת Nginx מבוסס Alpine Linux
COPY index.html /usr/share/nginx/html/index.html # מעתיק את index.html לתיקיית הקבצים של Nginx
COPY nginx.conf /etc/nginx/conf.d/default.conf # מעתיק את קובץ ההגדרות nginx.conf במקום ברירת המחדל
EXPOSE 80 # מצהיר שהקונטיינר משתמש בפורט 80 מבפנים
CMD ["nginx", "-g", "daemon off;"] # מפעיל את Nginx במצב חזית כך שהקונטיינר יישאר פעיל
