# NPM

← [Назад к перечню шпаргалок][back]

## Установка / обновление `npm`

    npm install npm -g
    npm install npm@latest -g

### Поиск пакетов в npm

    npm search hook.io

## Просмотр информации о пакете

    npm view hook.io

## Локальная установка пакетов

    npm install http-server

## Глобальная установка пакетов

    npm install http-server -g

## Удаление локально установленного пакета

    npm uninstall http-server

## Удаление глобально установленного пакета

    npm uninstall http-server -g

## Установка определённой версии пакета

    npm install http-server@0.3.0

## Установка модуля с Github

***Важно**. В некоторых случаях будут патчи, форки или ветви, которые вы хотите использовать, но которые еще не были
опубликованы в npm.*

    git clone git://github.com/nodeapps/http-server.git
    cd http-server/
    npm link

## Связи любых пакетов локально

*Если у вас есть отдельный каталог содержащий пакет npm, то можно создать локальную связь для него. Это удобно в
ситуациях, когда мы не хотим опубликовать наш пакет в хранилище npm.*

    cd http-server/
    npm link

## Связи локальных пакетов для нескольких приложений

    mkdir newapp/
    cd newapp/
    npm link http-server

## Отмена связи между пакетами приложения

    cd newapp/
    npm unlink http-server

## Отмена связи пакета в системе

    cd http-server/
    npm unlink

## Создание нового пакета

    mkdir mypackage/
    cd mypackage/
    npm init

## Добавление нового пользователя

    npm adduser

## Публикация пакета в репозиторий `npm`

    cd mypackage/
    npm publish

## Удаление пакета из репозитория `npm`

    npm unpublish http-server

## Remove one version

	npm unpublish [<@scope>/]<pkg>@<version>

## Remove all versions

	npm unpublish [<@scope>/]<pkg> --force

## Управление правами доступа к пакетам в репозитории `npm`

*Вы можете задать права доступа других пользователей к опубликованному пакету:*

    npm owner add marak http-server
    npm owner rm marak http-server
    npm owner ls http-server

## Чистит кэш

    npm cache rm
    npm cache clean
    npm cache clean --force

## Проверяет кэш

    npm cache verify

← [Назад к перечню шпаргалок][back]

[back]: <../.> "Назад к перечню шпаргалок"
