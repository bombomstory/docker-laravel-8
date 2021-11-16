# การติดตั้ง Docker - Laravel เวอร์ชั่น 8

![Docker](https://github.com/supermavster/docker-laravel-8/workflows/Docker/badge.svg)

![Image](https://repository-images.githubusercontent.com/309769351/1c0dfc80-1def-11eb-9e5c-641da3e3c9b4)

ขั้นตอนการติดตั้ง LEMP (Linux, NGINX, MySQL, PHP) ผ่าน Docker-Composer แบบง่ายเหมาะสำหรับการพัฒนา Laravel บน localhost

## ค่า default port ที่ตั้งไว้ตามสคริป

Ports used in the project:
| Software | Port |
|-------------- | -------------- |
| **nginx** | 8080 |
| **phpmyadmin** | 8081 |
| **mysql** | 3306 |
| **php** | 9000 |
| **xdebug** | 9001 |
| **redis** | 6379 |

## ขั้นตอนการติดตั้ง

ก่อนเริ่มโปรดตรวจสอบให้แน่ใจว่าได้ทำการติดตั้ง Docker [Docker installed](https://docs.docker.com/) และ Docker_Compose [Docker Compose](https://docs.docker.com/compose/install/) ลงในเครื่องแล้ว จากนั้นทำการ clone repository ดังนี้

1. Clone โปรเจ็ค:

   เปิด Command Promt ด้วยสิทธิ์ Administrator แล้วทำการ clone git ดังนี้ (อย่าลืมติดตั้งโปรแกรม git ลงในเครื่องก่อน)
   ```sh
   git clone https://github.com/bombomstory/docker-laravel-8.git
   ```

2. ทำการเข้าไปในไดเร็คทอรี่ `docker-laravel-8` เพื่อสร้างไฟล์ `.env` สำหรับใช้ใน Docker_Compose โดยใช้คำสั่งดังนี้:

   ```sh
   cd docker-laravel-8
   copy .env.example .env
   ```

3. สร้าง Project laravel ตามนี้
   
##โหลดซอร์สโค้ด laravel มาไว้ในเครื่องก่อน ด้วยคำสั่งนี้

   ```sh
   git clone https://github.com/laravel/laravel.git
   ```   

##ย้าย ไฟล์สภาพแวดล้อม .env ไปไว้ใน laravel ด้วยคำสั่งนี้

   ```sh
   move .env laravel/
   ```   

##เปลี่ยนไดเร็คทอรี่เข้าไปทำงานใน laravel ด้วยคำสั่งนี้

   ```sh
   cd laravel
   ```   

## อย่าลืม ทำการแก้ไขกำหนดค่าชื่อฐานข้อมูล username password สำหรับจัดการฐานข้อมูลในไฟล์ .env ก่อนสั่งสรา้ง Project laravel

```dotenv
# .env
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
DB_ROOT_PASSWORD=secret
```

```dotenv
# source/.env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=db_name
DB_USERNAME=db_user
DB_PASSWORD=db_password
```

The only change is the `DB_HOST` in the `source/.env` where is called to the container of `mysql`:

```dotenv
# source/.env
DB_HOST=mysql
```

---

### สร้างโปรเจ็ค Laravel ด้วยคำสั่งด้านล่างนี้

```sh
docker-compose run --rm composer create-project laravel/laravel .
```

### Copy Environment

```sh
copy .env.example .env
```

---

### Install Libraries from Composer

```sh
docker-compose run --rm composer install
```

### ติดตั้ง Libraries จาก Node

```sh
docker-compose run --rm npm install
```

### Clear/Clean the project

```sh
docker-compose run --rm artisan clear:data
docker-compose run --rm artisan cache:clear
docker-compose run --rm artisan view:clear
docker-compose run --rm artisan route:clear
docker-compose run --rm artisan clear-compiled
docker-compose run --rm artisan config:cache
docker-compose run --rm artisan storage:link
```

### สร้าง Keys

```sh
docker-compose run --rm artisan key:generate
```

### รัน migrations

```sh
docker-compose run --rm artisan migrate --seed
```

### รัน Passport (Optional)

```sh
docker-compose run --rm artisan passport:install
```


4. สร้าง LEMP Laravel ด้วยคำสั่ง:

   ```sh
   docker-compose up --build
   ```

---


## คำสั่งอื่น ๆ

ปิดหรือลบโปรเจ็คด้วยคำสั่ง:

```sh
docker-compose down -v
```

อัพเดท Composer ด้วยคำสั่ง:

```sh
docker-compose run --rm composer update
```

รัน compiler (Webpack.mix.js) หรือแสดง view compiler ใน node:

```sh
docker-compose run --rm npm run dev
```

รัน migrations ทุกตัว:

```sh
docker-compose run --rm artisan migrate
```
