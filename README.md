# 🚰 Proyecto Laravel 12 + Vue 3 + Docker con Sail

Este proyecto está configurado con **Laravel 12**, **Vue 3**, **Vite** y **MySQL**, ejecutándose en **Docker** mediante Laravel Sail. Listo para que cualquier miembro del equipo lo ejecute en Windows, macOS o Linux sin instalar PHP, Composer ni MySQL localmente.

```bash
git clone https://github.com/Karlos3C/laravel-docker.git && cd laravel-docker
# 🧲 Clona el repositorio desde GitHub y entra en la carpeta del proyecto

docker run --rm -u "$(id -u):$(id -g)" -v $(pwd):/var/www/html -w /var/www/html laravelsail/php84-composer:latest composer install --ignore-platform-reqs
# 📦 Instala las dependencias de Laravel usando Composer dentro de un contenedor Docker

cp .env.example .env

# 🔑 Configura las variables de entorno principales para Laravel y MySQL

./vendor/bin/sail up -d
# 🐳 Inicia los contenedores en segundo plano

./vendor/bin/sail artisan key:generate
# 🔐 Genera la APP_KEY de Laravel necesaria para cifrado y seguridad

./vendor/bin/sail artisan migrate
# 🗄️ Ejecuta las migraciones y crea las tablas en la base de datos

./vendor/bin/sail npm install
# 📥 Instala las dependencias frontend necesarias para Vue y Vite

./vendor/bin/sail npm run dev
# 🚧 Levanta Vite en modo desarrollo para compilar assets y recarga en caliente

./vendor/bin/sail mysql -e "SELECT 'Host: mysql, Usuario: sail, Password: password';"
# 🐬 Verifica el acceso a MySQL desde el contenedor

./vendor/bin/sail down
# ⛔ Detiene los contenedores cuando termines tu sesión de trabajo
