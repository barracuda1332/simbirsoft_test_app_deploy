# simbirsoft_test_app_deploy

1. Тест проводился на Ubuntu Server 18.04 от пользователя root c авторизацией с помощью ключа:
    
    ssh-keygen -t rsa
    ssh-copy-id root@$host

    Обновляем систему
    
    apt upgrade
    apt update

    Устанавливаем Ansible

    apt install ansible
    
2. Сценарии запускаются командой :

    ansible-playbook git_pull.yml app_deploy.yml app_service.yml nginx_install.yml postgresql.yml

    git_pull - загружает файлы из репозитория git
    app_deploy - развертвывает среду для работы приложения
    app_service - запускает приложение как демон
    nginx_install - устанавливает и конфигурирует веб сервер
    postgres - устанавливает БД, создает пользователя и таблицу

    В каталоге templates лежат скрипты для запуска приложения как службы и конфигурация nginx, эта папка должна находиться в том же каталоге, что и сценарии
    
3. При попытке развертвывания через файл requirements, ansible выдает ошибку что не находит версию библиотеки psycopg2, я исправил на psycopg2-binary, тогда развертвывание прошло корректно.
4. Таблица в БД не создается автоматически, попробовал в скрипт ansible добавить эти поля, но все равно не смог получить данные из таблицы.
