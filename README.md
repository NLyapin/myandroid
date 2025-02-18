# Приложение Android для передачи данных о местоположении

### Описание 
Это Android-приложение, которое получает данные о местоположении и сети пользователя (оператор сети) и выводит их на экран. Приложение также записывает эти данные в файл `data.json` каждые 60 секунд в фоновом режиме, используя Android Service.
### Функциональность 

- Получение текущего местоположения устройства (широта и долгота).

- Получение информации об операторе сотовой сети.

- Отображение местоположения и информации о сети на экране.
 
- Запись данных в файл `data.json` каждые 60 секунд.

- Фоновый сервис для постоянной записи данных.

### Требования 

- Android 6.0 (API Level 23) или выше.
 
- Необходимы следующие разрешения: 
  - Доступ к местоположению (`ACCESS_FINE_LOCATION`).
 
  - Чтение информации о сети (`READ_PHONE_STATE`).
 
  - Запуск фонового сервиса (`FOREGROUND_SERVICE`).

### Зависимости 
Для сериализации данных в JSON используется библиотека [Gson](https://github.com/google/gson) .Добавьте её в `build.gradle`:

```groovy
dependencies {
    implementation 'com.google.code.gson:gson:2.8.8'
}
```

### Установка и запуск 
 
1. Клонируйте репозиторий:


```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```
 
2. Откройте проект в Android Studio.
 
3. Убедитесь, что у вас установлены необходимые разрешения в манифесте (`AndroidManifest.xml`):

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
```
 
4. Запустите приложение на устройстве или эмуляторе.

### Как работает приложение 
 
1. **MainActivity** : При запуске приложение запрашивает разрешения на доступ к местоположению и информации о сети. После получения разрешений, оно отображает на экране:
  - Широту и долготу текущего местоположения.

  - Оператора сотовой сети.
 
2. **Фоновый сервис** : Сервис `MyBackgroundService` работает в фоновом режиме и записывает данные о местоположении и сети в файл `data.json` каждые 60 секунд.
 
3. **Файл `data.json`** : Находится во внутреннем хранилище приложения и содержит JSON с полями:

```json
{
    "networkOperator": "Название оператора сети",
    "latitude": 55.7558,
    "longitude": 37.6173
}
```
Пример данных в файле `data.json`

```json
{
    "networkOperator": "MyNetworkOperator",
    "latitude": 55.7558,
    "longitude": 37.6173
}
```

### Разрешения 

Для работы приложения требуются следующие разрешения:
 
- **Доступ к местоположению** : Приложение запрашивает разрешение на доступ к точному местоположению пользователя.
 
- **Доступ к информации о сети** : Для получения оператора сотовой сети необходимо разрешение `READ_PHONE_STATE`.

### Запуск сервиса 

Фоновый сервис запускается автоматически при запуске приложения и продолжает записывать данные даже после закрытия приложения.

### Тестирование 

- Приложение можно протестировать на реальном устройстве или эмуляторе, предоставив необходимые разрешения.

- Убедитесь, что у приложения есть разрешения для доступа к местоположению и информации о телефоне.