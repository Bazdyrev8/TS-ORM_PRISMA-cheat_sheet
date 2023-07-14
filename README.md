# Шпаргалка по работе с TS, ORM prisma


Создаем все необходимое, например:

    controllers/
        |-ItemsControllers.ts
    dist/
        |-controllers/
        |-views/
            |-<%EJS%>...
    prisma/
        |-schema.prisma  
    public/
        |-css/
            |-style.css
        |-img/
            |-img.jpg
    .env
    index.ts

Настраиваем TS...
    npm install -g typescript
    npm i -D typescript @types/express @types/node
    npx tsc --init
    npm install -D concurrently nodemon
    npm install //если что-то не получится

    Для компиляции TS файлов:
        tsc index.ts --outDir dist/ //вместо dist/ путь дириктории
    получится:

    controllers/
        |-ItemsControllers.ts
    dist/
        |-controllers/
            |-ItemsControllers.js
        |-index.js
    index.ts

Настраиваем ORM Prisma...

в schema.prisma

    generator client {
        provider = "prisma-client-js"
    }

    datasource db {
        provider = "mysql" //Здесь используется база данных MySQL
        url      = env("DATABASE_URL") // ссылка на файл .env
    } // настройки БД

    model items {
        id Int @id @default(autoincrement())
        title String @db.VarChar(255)
        image String @db.VarChar(255)
    } // пример таблицы БД


Установка зависимостей

    npm install

Создать файл .env в корневом каталоге и добавить конфигурацию БД

    DATABASE_URL="mysql://root:secret@localhost:3306/databaseName"

Выполнить миграцию БД из конфигурации ORM Prisma

    npx prisma migrate dev

Запуск веб-сервера

    npm run dev

# Настройка package.json

Чтобы работала команда dev нужно настроить файл package.json, в конец добавить:

    "scripts": {
        "dev": "concurrently \"npx tsc --watch\" \"nodemon -q dist/index.js\""
    }

Также можно настроить команду tsc index.ts --outDir dist/ и другие
    "scripts": {
        "dev": "concurrently \"npx tsc --watch\" \"nodemon -q dist/index.js\""
        "build": "npx tsc", //с помощью команды npm run build запустится компиляция файлов .ts
        "start": "node dist/index.js", //с помощью команды npm run start запустится файл index.js
    }
