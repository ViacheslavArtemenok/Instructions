# Конфигурация для тестирования в проектах Laravel
![laravel_logo]

### 1. Создаем файл ``.env.testing``
### 2. В него копируем всё из ``.env``
### 3. В ``.env.testing`` меняем: 

``DB_DATABASE=project_app`` на 

``DB_DATABASE=testing``
### 4. Выполняем обновление зависимостей:
```
composer update
```
### 5. Команды:
Для тестовой б/д:
```
sail artisan migrate:fresh --env=testing
sail artisan db:seed --env=testing
```
Для основной б/д:
```
sail artisan migrate:fresh 
sail artisan db:seed 
```
### 6. Перед тестированием:
```
sail artisan config:clear
sail artisan config:cache --env=testing
```
### 7. Теперь можно выполнять команду:
```
sail artisan test 
```
### 8. Все тесты проходят проверку, чтобы обновить тестовую б/д:
```
sail artisan migrate:fresh --env=testing
sail artisan db:seed --env=testing
```
### 9. ``phpunit.xml`` и ``config/database.php`` не трогаем, оставляем по дефолту.

[laravel_logo]: img/laravel_logo.png