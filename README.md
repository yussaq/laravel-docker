## Install Laravel menggunakan Docker (PHP, Nginx, Laravel, MySql, phpMyadmin)

### Folder Structure 

- `docker` - Folder untuk file konfigurasi docker dan berbagai services
    - `nginx` - Folder untuk file konfigurasi nginx
    - `php` - Folder untuk file konfigurasi php
- `src` - Folder untuk project laravel
- `docker-compose.yml` - File konfigurasi Docker compose

### Langkah 

#### 1. Build the Project dengan Docker Compose

- Jalankan perintah
  
  ```
  docker compose build
  ```

#### 2. Install Laravel (versi 10)

-  Jalankan perintah:

  ```
  docker compose run --rm composer create-project laravel/laravel:^10 .
  ```

- Setelah dijalankan perintah tersebut, project laravel akan di intall di folder src.

- Perintah untuk Start docker containers

  ```
  docker compose up -d
  ```

- Cek laravel dengan browser:

  ```
  http://localhost
  ```

#### 3. Configure Laravel project 
 
- Configure Mysql in /src/.env . Uncomment and change:

  ```
  DB_CONNECTION=mysql       # nama koneksi
  DB_HOST=mysql             # nama mysql service pada docker-compose.yml
  DB_PORT=3306              # mysql standart port 
  DB_DATABASE=laraveldb     # nama database MYSQL_DATABASE pada docker-compose.yml
  DB_USERNAME=laravel       # username dari MYSQL_USER pada docker-compose.yml
  DB_PASSWORD=password      # user password dari MYSQL_PASSWORD pada docker-compose.yml
  ```
- Restart semua services
  
  ```
  docker compose down
  docker compose up -d
  ```

#### 4. Jalankan Migrations

  ```
  docker compose run --rm artisan migrate
  ```

#### Catatan

- Cara masuk ke php container (php adalah nama dari service dalam docker-compose.yml)

  ```
  docker compose run --rm php /bin/sh
  ```

- Jika ada masalah access Forbidden

  ```
  docker compose run --rm php /bin/sh
  chown -R laravel:laravel /var/www/html
  ```