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

   ```sh
   git clone https://github.com/bombomstory/docker-laravel-8.git
   ```

2. ทำการเข้าไปในไดเร็คทอรี่ `docker-laravel-8` เพื่อสร้างไฟล์ `.env` สำหรับใช้ใน Docker_Compose โดยใช้คำสั่งดังนี้:

   ```sh
   cd docker-laravel-8
   copy .env.example .env
   ```

3. You need **Create** or **Put** your laravel project in the folder source; to create follow the next instructions [Here](source/README.md).

4. Build the project whit the next commands:

   ```sh
   docker-compose up --build
   ```

---

## Remember

The configuration of the database **must be the same on both sides** .

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

## Special Cases

To Down and remove the volumes we use the next command:

```sh
docker-compose down -v
```

Update Composer:

```sh
docker-compose run --rm composer update
```

Run compiler (Webpack.mix.js) or Show the view compiler in node:

```sh
docker-compose run --rm npm run dev
```

Run all migrations:

```sh
docker-compose run --rm artisan migrate
```
