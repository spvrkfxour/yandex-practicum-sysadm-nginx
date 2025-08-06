# Nginx

````
sudo apt update && sudo apt upgrade
sudo apt install nginx
sudo apt install php8.3-fpm
````

### /etc/nginx/sites-available/default
````
server {
  listen 80 default_server;
  listen [::]:80 default_server;
  root /var/www/html;
  index index.html index.htm index.nginx-debian.html index.php;
  server_name _;

  location / {
    try_files $uri $uri/ =404;
  }

  location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/run/php/php8.3-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
  }
}
````

### /var/www/html/somesite/index.php
````
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Test site\</title>
</head>
<body>
<h1>Добро пожаловать на сайт!\</h1>
<p>Это главная страница.\</p>
<p>Посмотрите, что есть ещё:\</p>
<ul>
<li>\<a href="page1">Кое-что\</li>
<li>\<a href="page2">И ещё кое-что\</li>
</ul>
</body>
</html>
````

### /var/www/html/somesite/page1/index.php
````
<DOCTYPE! html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Test site page 1\</title>
</head>
<body>
<h1>Это ещё одна страница\</h1>
<p>Тут может быть кое-что ещё.\</p>
<a href="../">Назад
</body>
</html>
````

### /var/www/html/somesite/page2/index.php
````
<DOCTYPE! html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Test site page 1\</title>
</head>
<body>
<h1>Это ещё одна страница\</h1>
<p>Тут ничего не будет.\</p>
<a href="../">Назад
</body>
</html>
````

````
sudo nginx -t
sudo service php8.3-fpm restart
sudo service nginx restart 
````
