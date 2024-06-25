# AbyssControlCenter_v2 
Программа для управления очередью а также простой чат-бот для Twitch.tv в помощь безднаботам.

Он будет использовать Google Docs и Twitch API для:
1. Обработки команд в чате
2. Прослушивания наград канала
3. Редактирования очереди в таблице Google
4. UI для управления очередью и командами

# Как внести вклад
Просто [сделайте форк этого репозитория](https://github.com/TwilightFoxy/coffee_bot/fork)

После внесения изменений создайте pull request.

# Дальнейшие инструкции пока игнорировать

## Как подключить Google Таблицу?

Чтобы настроить учетную запись службы в Google Cloud Console, выполните следующие шаги:
![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/ec78d92e-d1bb-403f-9fc4-807beb97c204)

1. **Создание учетной записи службы:**
    - Перейдите в Google Cloud Console.
    - Введите имя учетной записи службы:
      ```text
      Service account name (Имя учетной записи службы): Введите описательное имя, например, twitch-bot-service-account.
      Service account ID (Идентификатор учетной записи службы): Он будет автоматически заполняться на основе введенного имени.
      Service account description (Описание учетной записи службы): Это поле необязательно, но вы можете добавить описание, чтобы было понятно, для чего используется эта учетная запись, например, Service account for Twitch bot accessing Google Sheets.
      ```
    - Нажмите **Create and continue** (Создать и продолжить).

2. **Предоставление доступа к проекту (опционально):**
    - На этом шаге вы можете указать роли, которые нужны вашей учетной записи службы для выполнения необходимых операций.
    - Например, выберите роль **Editor** (Редактор) или **Owner** (Владелец), чтобы обеспечить доступ к Google Sheets и другим необходимым ресурсам.
    - Нажмите **Continue** (Продолжить).

3. **Предоставление доступа пользователям (опционально):**
    - Этот шаг можно пропустить, если вам не нужно предоставлять доступ другим пользователям.
    - Нажмите **Done** (Готово).

![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/fdc36286-c440-4272-bb20-3dbc8ee2150a)

![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/d534870c-b33b-4b2c-9325-e3c8235973fc)

4. **Создание и загрузка JSON ключа:**
    - Перейдите на вкладку **Keys** (Ключи) учетной записи службы.
    - Нажмите **Add Key** (Добавить ключ) и выберите **Create New Key** (Создать новый ключ).
    - Выберите формат **JSON** и нажмите **Create** (Создать).
    - Скачанный файл переименуйте в `access.json` и сохраните в корневую директорию вашего проекта.

5. **Активация Google Sheets API:**
    - Перейдите по ссылкам: [Google Sheets API](https://console.cloud.google.com/apis/library/sheets.googleapis.com) и [Google Drive API](https://console.cloud.google.com/apis/library/drive.googleapis.com) и активируйте их.

6. **Предоставление доступа к Google Таблице:**
    - Откройте Google Таблицу и предоставьте доступ на редактирование адресу электронной почты, указанному в строке `client_email` вашего `access.json` файла.

Следуя этим шагам, вы настроите учетную запись службы для доступа к Google Таблице и сможете использовать ее в своем проекте.

## Как подключить Twitch учетную запись?
1. **Создание приложения на Twitch Developer Portal:**
    - Перейдите на [Twitch Developer Console](https://dev.twitch.tv/console/apps).
    - ![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/be86589a-8569-4282-abf0-a552016357d9)

    - Нажмите **Register Your Application** (Подать заявку).
    - Заполните форму регистрации приложения:
      ```text
      Name (Имя): Введите имя вашего приложения, например, Coffee Bot. Оно будет отображаться только в ващей Твич консоли.
      OAuth Redirect URLs (URL для перенаправления OAuth): Введите http://localhost.
      Category (Категория): Выберите категорию, Chat Bot.
      ```
    - Нажмите **Create** (Создать).

![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/3a35d67c-8436-491f-a0bc-3af006c3f136)

![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/fb2b298d-c2c1-4ae6-b686-1092e84f69c8)

2. **Получение OAuth токена:**
    - После создания приложения вы увидите `Client ID` и `Client Secret`.
    - Занесите эти значения в приложение.
    - Перейдите по ссылке "Получить ключ активации" прямо в приложении.
    - Авторизуйтесь и получите OAuth токен.

3. **Заполнение конфигурации в приложении:**
    - Откройте приложение и перейдите на вкладку **Подключить аккаунт**.
    - Заполните следующие поля:
      ```text
      TWITCH_OAUTH_TOKEN: Ваш OAuth токен.
      TWITCH_CLIENT_ID: Ваш Client ID.
      TWITCH_CLIENT_SECRET: Ваш Client Secret.
      TWITCH_CHANNEL: Ваш Twitch канал.
      Таблица: Имя вашей Google Таблицы.
      Лист: Имя листа в вашей Google Таблице.
      ```
    - Нажмите **Сохранить**.

Теперь ваш бот настроен для работы с Twitch и Google Sheets!

## Как работать с очередью?

На вкладке **Очередь** вы можете управлять очередями пользователей, используя следующие элементы управления:
![image](https://github.com/TwilightFoxy/coffee_bot/assets/62305710/07f3ca75-d8a4-48c6-b960-70832e6edec9)

1. **Добавление пользователя в очередь:**
    - Введите имя пользователя в поле **Добавить пользователя**.
    - Выберите тип очереди (Обычная или VIP) из выпадающего списка.
    - Нажмите кнопку **Добавить**, чтобы добавить пользователя в очередь.

2. **Отметка пользователя как выполненного:**
    - Введите имя пользователя в поле **Отметить пользователя**.
    - Выберите тип очереди (Обычная или VIP) из выпадающего списка.
    - Нажмите кнопку **Отметить**, чтобы отметить пользователя как выполненного.

3. **Скрытие выполненных пользователей:**
    - Установите флажок **Скрыть пройденные**, чтобы скрыть выполненных пользователей из отображаемых очередей.

4. **Автоматическое добавление пользователей за баллы:**
    - Введите команду в поле **Автоматическое добавление пользователей за баллы** и нажмите **Сохранить**.

5. **Обновление очереди:**
    - Нажмите кнопку **Обновить очереди**, чтобы обновить отображение текущих очередей из Google Таблицы.

6. **Экспорт очереди в CSV:**
    - Нажмите кнопку **Экспортировать в CSV**, чтобы экспортировать текущие очереди в файл CSV (эта функция пока находится в разработке).

7. **Удаление ячеек в Google Таблице:**
    - Если нужно удалить ячейку, сделайте это в онлайн таблице, удалив ячейку и её состояние со сдвигом вверх.

Следуя этим инструкциям, вы сможете эффективно управлять очередями пользователей через пользовательский интерфейс.

# Благодарности и помощь
Если хотите отблагодарить автора: [Донейшин алертс](https://www.donationalerts.com/r/twilightfoxy)

Если вам нужна помощь в настройке или есть предложения по новым функциям, то можете писать в [телеграмм @twilight_foxy](https://t.me/twilight_foxy)
