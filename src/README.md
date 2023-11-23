# Simple Docker

## Part 1. Готовый докер

+ ***Взять официальный докер образ с nginx и выкачать его при помощи docker pull***
  
  ***Сделали pull докер-образа с nginx***
  
  ![pull](images/pull.png)

+ ***Проверить наличие докер образа через docker images***
  
  ***Проверяем наличие докер образа***
  
  ![docker_images](images/docker_images.png)

+ ***Запустить докер образ через docker run -d [image_id|repository]***
  
  ***Запускаем докер командой docker run -d nginx***
  
  ![docker_first_run](images/docker_first_run.png)

+ ***Проверить, что образ запустился через docker ps***
  
  ***Проверка запуска***
  
  ![docker_first_ps](images/docker_first_ps.png)

+ ***Посмотреть информацию о контейнере через docker inspect [container_id|container_name]***
  
  ***Иформация контейнера***
  
  ![docker_inspect](images/docker_inspect.png)

+ ***По выводу команды определить и поместить в отчёт размер контейнера, список замапленных портов и ip контейнера***
  
  ***Размер контейнера***
  
  ![shmSize](images/shmSize.png)
  
  ***Список замапленных портов***
  
  ![ports](images/ports.png)
  
  ***IP контейнера***
  
  ![IPAddress](images/IPAddress.png)

+ ***Остановить докер образ через docker stop [container_id|container_name]***
  
  ***Остановка докер-образа***
  
  ![docker_first_stop](images/docker_first_stop.png)

+ ***Проверить, что образ остановился через docker ps***
  
  ***Проверка того, что образ остановился (ни один процесс не запущен)***
  
  ![docker_second_ps](images/docker_second_ps.png)

+ ***Запустить докер с портами 80 и 443 в контейнере, замапленными на такие же порты на локальной машине, через команду run***
  
  ***Тк контейнеры по-умолчанию запускаются с портом 80, то нужно изменить в его конфиге, на любой другой порт (я изменил на порт 90). После чего запускаем докер-образ.***

  ![docker_run_with_ports](images/docker_run_with_ports.png)

+ ***Проверить, что в браузере по адресу localhost:80 доступна стартовая страница nginx***
  
  ***Для начала проверим, что докер-образ запустился командой docker ps. Все ок, у нас он запущен. Далее проверим стартовую страницу nginx***

  ![check_docker_run](images/check_docker_run.png)
  
  ![check_site_after_run](images/check_site_after_run.png)

+ ***Перезапустить докер контейнер через docker restart [container_id|container_name]***
  
  ***Делаем рестарт докер-контейнера***
  
  ![docker_first_restart_cont](images/docker_restart_first_cont.png)

+ ***Проверить любым способом, что контейнер запустился***
  
  ![check_docker_after_restart](images/check_docker_after_restart.png)

## Part 2. Операции с контейнером

+ ***Прочитать конфигурационный файл nginx.conf внутри докер контейнера через команду exec***
  
  ***Читаем файл nginx.conf с помощью exec***
  
  ![cat_nginx_conf_via_exec](images/cat_nginx_conf_via_exec.png)

+ ***Создать на локальной машине файл nginx.conf***
  
  ***Создаем файл nginx.conf и прописываем в нем порт 80, также location = /status {stub_status on}; для того, чтобы появилась страница по адресу localhost/status с отображением статуса***
  
  ![create_nginx_conf](images/create_nginx_conf.png)

+ ***Скопировать созданный файл nginx.conf внутрь докер образа через команду docker cp. Перезапустить nginx внутри докер образа через команду exec***
  
  ***Скопировали nginx.conf по пути /etc/nginx/nginx.conf, после чего перезапустили докер-образ. Сигнал успешный***
  
  ![copy_and_reload_container](images/copy_and_reload_container.png)

+ ***Проверить, что по адресу localhost:80/status отдается страничка со статусом сервера nginx***
  
  ***Переходим по адресу localhost:80/status и видим, что все работает***
  
  ![check_page_with_status](images/check_page_with_status.png)

+ ***Экспортировать контейнер в файл container.tar через команду export***
  
  ***Прописываем соответственно экспорт для контейнера***
  
  ![expot_container](images/export_container.png)

+ ***Остановить контейнер. Удалить образ через docker rmi [image_id|repository], не удаляя перед этим контейнеры***
  
  ***Остановили контейнер и удалили образ***
  
  ![docker_stop_and_rmi](images/docker_stop_and_rmi.png)

+ ***Удалить остановленный контейнер***
  
  ![docker_rm](images/docker_rm.png)

+ ***Импортировать контейнер обратно через команду import. Запустить импортированный контейнер.***
  
  ***Прописываем импорт контейнера, все ок, появился его хэш код. Запускаем импортированный контейнер в интерактивном режиме (-it), после чего, внутри контейнера, запускаем его***
  
  ![docker_import_and_run](images/docker_import_and_run.png)

+ ***Проверить, что по адресу localhost:80/status отдается страничка со статусом сервера nginx***
  
  ***Переходим по адресу localhost:80/status и видим, что страничка отдается вместе со статусом***
  
  ![check_status_page](images/check_status_page.png)

## Part 4. Свой докер

+ ***Написать свой докер образ, который:***
  
  ***1) собирает исходники мини сервера на FastCgi из Части 3***
  
  ***2) запускает его на 8080 порту***
  
  ***3) копирует внутрь образа написанный ./nginx/nginx.conf***
  
  ***4) запускает nginx.***

  ![dockerfile](images/dockerfile.png)

+ ***Собрать написанный докер образ через docker build при этом указав имя и тег***
  
  ***Cборка с именем test и тегом 1***
  
  ![docker_build](images/docker_build.png)

+ ***Проверить через docker images, что все собралось корректно***
  
  ![123](images/123.png)

+ ***Запустить собранный докер образ с маппингом 81 порта на 80 на локальной машине и маппингом папки ./nginx внутрь контейнера по адресу, где лежат конфигурационные файлы nginx'а (см. Часть 2)***
  
  ![docker_80_81](images/docker_80_81.png)

+ ***Проверить, что по localhost:80 доступна страничка написанного мини сервера***
  
  ![1234](images/1234.png)

+ ***Перезапустить докер образ***
  
  ![docker_restart_7c0](images/docker_restart_7c0.png)

+ ***Проверить, что теперь по localhost:80/status отдается страничка со статусом nginx***
  
  ![docker_restart_status](images/docker_restart_status.png)

## Part 5. Dockle

+ ***Просканировать образ из предыдущего задания через dockle [image_id|repository]***
  
  ![dockle_test_1](images/dockle_test_1.png)

+ ***Исправленный докерфайл***
  
  ![dockerfile_part5](images/dockerfile_part5.png)

+ ***Исправить образ так, чтобы при проверке через dockle не было ошибок и предупреждений***
  
  ![dockle_with_keys](images/dockle_with_keys.png)

## Part 6. Базовый Docker Compose

+ ***Написать файл docker-compose.yml, с помощью которого:***
  
  ***1) Поднять докер контейнер из Части 5 (он должен работать в локальной сети, т.е. не нужно использовать инструкцию EXPOSE и мапить порты на локальную машину)***
  
  ***2) Поднять докер контейнер с nginx, который будет проксировать все запросы с 8080 порта на 81 порт первого контейнера***

  ***Написали docker-compose.yaml***

  ![docker_compose_yaml](images/docker_compose_yaml.png)

  ***Прописываем docker-compose build***

  ![docker_compose](images/docker_compose.png)

+ ***Собрать и запустить проект с помощью команд docker-compose build и docker-compose up. Проверить, что в браузере по localhost:80 отдается написанная вами страничка, как и ранее.***
  
  ![result_docker_images](images/result_docker_images.png)

  ![docker_website](images/docker_website.png)