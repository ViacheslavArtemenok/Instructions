# Инструкция Docker+Laravel

![docker_logo] &nbsp; ![laravel_logo]

## 1. Устанавливаем docker на рабочий стол с [официального сайта][официальный сайт] 

### Полезные видео:

[Docker Desktop - Docker failed to initialize]

[Docker Failed To Initialize | Docker Desktop Is Shutting Down]

[Подробная видео-инструкция по установке Sail]

### Полезные статьи:
[Начало работы с Laravel]

[Установка Laravel Sail]

[Форум на laracasts][laracasts]

[Статья на Хабр: Laravel Sail под Windows][Laravel Sail под Windows]


## 2. Запустить докер
* После установки и запуска от имени администратора в ``Docker`` будет открыта вкладка ``Containers``, там будет наш будущий контейнер с Laravel.

* При первом запуске может возникать ошибка, тогда:

Через диспетчер задач выключаем докер.

В папке ``C:\Users\user\AppData\Roaming\Docker`` удаляем файл settings.json, после запускаем от имени администратора.

Если не помогает, снова выключаем все сервисы Docker через диспетчер задач, удаляем папки:

``C:\Users\user\AppData\Local\Docker``

``C:\Users\user\AppData\Roaming\Docker``

``C:\Users\user\AppData\Roaming\Docker Desktop``

Запускаем Docker от имени администратора.

* Видео по этой ошибке (см. выше)

## 3. Настройка Linux for Windows
``Если у вас MacOS или Linux, пропускаем этот шаг``

* Настройка WSL 2, установка ubuntu 20.04

* Команды по установке WSL 2 выполняются в PowerShell

* Посмотреть версию windows -> комбинация WINDOWS + R -> вводим winver

* Важно!!! В конце установки Ubuntu нужно придумать логин и пароль, их запомнить, сохранить, понадобится в дальнейшем.

* Установка Ubuntu-20.04 из Microsoft Store, либо с официального сайта, ниже подробно расписан алгоритм: [Установка и настройка WSL2]

## 4. Настройка Docker
После установки WSL 2 в настройках Docker (символ &#9881;) выбрать параметры:

``General -> Use Docker Compose V2 включить``

``Resources -> WSL Integration -> Ubuntu 20.04 включить``

## 5. Работа с терминалом Linux Ubuntu 20.04
* В ``Microsoft Store -> Библиотека`` открыть ``Ubuntu 20.04``, появится терминал Ubuntu.
* Для удобства закрепить в панели задач

* В терминале Ubuntu из документации по Laravel, если у вас Windows,выполнить: 
```
 curl -s https://laravel.build/example-app | bash
```
``* Вместо 'example-app' название вашего проекта ('project-app' и т.п.)``
     
Идет установка проекта Laravel...
   
* После установки выбираем папку проекта в Ubuntu:
```
cd example-app 
```
  (или 'project-app' и т.п.)

* Далее поднимаем сервер, устанавливаем контейнер в Docker:
```
  ./vendor/bin/sail up
```

* Остановить сервер: ``CTRL+С``

## 6. Создание псевдонима alias для удобного запуска сервера

В терминале Ubuntu:

* Вводим эту команду, зададим алиас, чтобы не писать (./vendor/bin/sail):
```
  alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
```
ИЛИ

Если мы в папке проекта, выполняем:
```
cd ../
```
в корневой директории ``~$`` выполняем команду, чтобы открыть файл ``.bashrc``:
```
sudo nano .bashrc
```
В редакторе nano дописываем внизу файла
```
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
alias sart='[ -f sail ] && bash sail artisan || bash vendor/bin/sail artisan'
```
и сохраняем файл
* Теперь уже можно запускать сервер простой короткой командой:
```
  sail up
```
или в фоновом режиме, чтобы иметь доступ к консоли команд:
```
sail up -d
```
Команду sail artisan теперь можно запускать через sart:
```
sart route:list
```
  Снова запускаем сервер

* В браузере http://localhost открывает стартовую страницу Laravel, проект готов к разработке. 

## 7. Прямой доступ к дереву папок проекта в Linux Ubuntu 20.04
* Получить доступ к файлам проекта, чтобы открыть через vs code, php storm.

* Если нет папки example-app(или 'project-app' и т.д.) в C:\Users\user, то ищем в Ubuntu.

* ``Важно!!!`` Путь начинается не с диска ``С``, а с двух обратных слэшей. 

В любой папке указать путь: ``\\wsl$\Ubuntu-20.04\home``

Обязательно должен быть запущен sail up!!!

* Откроется дерево с проектом Laravel внутри директорий Linux, открыть папку с проектом с помощью vs code.

Мы готовы к разработке!!!
	

## 8. Доступ к терминалу Ubuntu из терминала VS code 
* Чтобы добавить терминал Ubuntu в терминал VS code, находим в расширениях vs code и устанавливаем расширение WSL (можно Remote - WSL)

* В консоли Ubuntu выбрать папку проекта:
```
cd example-app 
```
Останавливаем сервер: ``CTRL+С``

Вводим команду:
```
code . 
```
``* Обязательно пробел перед точкой``


* Установится терминал управления Ubuntu в VS code

* С помощью команды ``cd`` в терминале vs code уже можно передвигаться по проекту в vs code и начинать разработку.

Cоответственно в терминале VS code запускаем сервер:
```
sail up 
```  
Успехов в разработке!!!

[официальный сайт]: https://www.docker.com
[docker_logo]: img/docker_logo.png
[laravel_logo]: img/laravel_logo.png
[Docker Desktop - Docker failed to initialize]: https://www.youtube.com/watch?v=jEsVRTNLW7s&t=1s
[Docker Failed To Initialize | Docker Desktop Is Shutting Down]: https://www.youtube.com/watch?v=4jqNSXN6qbI&list=LL&index=11&t=1s
[Установка и настройка WSL2]: https://learn.microsoft.com/ru-ru/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package

[Подробная видео-инструкция по установке Sail]: https://www.youtube.com/watch?v=dYpEXzkh25k&t=62s
[Начало работы с Laravel]: https://laravel.com/docs/10.x/installation
[Установка Laravel Sail]: https://laravel.com/docs/10.x/sail
[Laravel Sail под Windows]:https://habr.com/ru/articles/658753/
[laracasts]: https://laracasts.com/discuss/channels/general-discussion/permanent-bash-alias-for-laravel-sail