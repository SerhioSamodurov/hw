# Самодуров Сергей Михайлович Zabbix Ч.1

## Задание 1

Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
   1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
   2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
   3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
   4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результатам
   1. Прикрепите в файл README.md скриншот авторизации в админке.
   2. Приложите в файл README.md текст использованных команд в GitHub.

### Решение 1

Хост под управлением ОС Debian 13.
На сайте zabbix сконфигурировал следующим образом

   ![1](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/1.png)

1.1 Установка PostgreSQL
  - sudo apt install postgresql
  - sudo systemctl status postgres

   ![2](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/2.png)

1.2 Установка репозитория
   - wget https://repo.zabbix.com/zabbix/7.0/debian/pool/main/z/zabbix-release/zabbix-release_latest_7.0+debian13_all.deb
   - sudo dpkg -i zabbix-release_latest_7.0+debian13_all.deb
   - cat /etc/apt/sources.list.d/zabbix.list
   - sudo apt update 

    ![3](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/3.png)

1.3 Установка Zabbix (без агента) 
  - sudo apt install zabbix-server-pgsql zabbix-frontend-php php8.4-pgsql zabbix-apache-conf zabbix-sql-scripts

   ![4](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/4.png)
  
  Установлен, но пока не запускался

1.4 Создание пользователя zabbix и БД
  Взял команды из конфигуратора
   - sudo -u postgres createuser --pwprompt zabbix
   - sudo -u postgres createdb -O zabbix zabbix
   - zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

    ![5](https://github.com/SerhioSamodurov/git_project_hw/blob/main/master/5.png)  

   Наша БД появилась 

1.5 Добавление пароля в конфиг
  - nano  /etc/zabbix/zabbix_server.conf 
   ![6](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/6.png)

1.6 Запуск и добавление в автозагрузку
   - sudo systemctl restart zabbix-server apache2
   - sudo systemctl enable zabbix-server apache2   
   ![7](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/7.png)
   ![8](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/8.png)

1.7 Web
 - Конфигуратор подключения к БД по IP адресу ВМ доступен
  
  ![9](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/9.png)

 - Все опции доступны

  ![10](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/10.png)

 - в процессе сменил тему
  ![11](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/11.png)

 - Окно с авторизацией появилось

  ![12](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/12.png)

 - После авторизации вижу стандартный шаблон zabbix

  ![13](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/13.png)

## Задание 2

Установите Zabbix Agent на два хоста.

Процесс выполнения
   1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
   2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
   3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
   4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
   5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результатам
   1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
   2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
   3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
   4. Приложите в файл README.md текст использованных команд в GitHub

### Решение 2

![14](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/14.png)
![15](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/15.png)
![16](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/16.png)
![17](https://github.com/SerhioSamodurov/git_project_hw/blob/master/img/17.png)

