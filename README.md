# Clonar el repositorio y entrar a la carpeta
git clone https://github.com/Karlos3C/laravel-docker.git && cd laravel-docker

# Instalar dependencias de Laravel dentro de un contenedor Docker
docker run --rm -u "$(id -u):$(id -g)" -v $(pwd):/var/www/html -w /var/www/html laravelsail/php85-composer:latest composer install --ignore-platform-reqs

# Crear el archivo de configuración .env
cp .env.example .env

# Variables de entorno importantes
echo "DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=nombre_db
DB_USERNAME=sail
DB_PASSWORD=password
WWWUSER=1000
WWWGROUP=1000" > .env

# Iniciar los contenedores en segundo plano
./vendor/bin/sail up -d

# Generar la APP_KEY de Laravel
./vendor/bin/sail artisan key:generate

# Ejecutar migraciones y crear la base de datos
./vendor/bin/sail artisan migrate

# Instalar dependencias frontend
./vendor/bin/sail npm install

# Ejecutar Vite en modo desarrollo
./vendor/bin/sail npm run dev

# Acceder a MySQL dentro del contenedor
./vendor/bin/sail mysql -e "SELECT 'Host: mysql, Usuario: sail, Password: password';"

# Detener los contenedores cuando termines tu sesión de trabajo
./vendor/bin/sail down
