---
title: Интеграция существующих сторонних API
author: MuyangAmigo
description: Из этой статьи вы узнаете, как набор средств помогает выполнить начальную загрузку примера доступа к существующим API. Он предоставляет список различных типов проверки подлинности.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 5933227f9ba4c8b684d624a8857304c044761578
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616811"
---
# <a name="integrate-existing-third-party-apis"></a>Интеграция существующих сторонних API

Набор средств Teams помогает получить доступ к существующим API для создания приложений Teams. Эти API разрабатываются вашей организацией или сторонним разработчиком. При использовании Набора средств Teams для подключения к существующему API Набор средств Teams выполняет следующую функцию:

* Создайте пример кода в папке `./bot` `./api` или папке.
* Добавьте ссылку на пакет в `@microsoft/teamsfx` `package.json`.
* Добавьте параметры приложения для API, чтобы  `.env.teamsfx.local` настроить локальную отладку.

## <a name="steps-to-connect-to-api"></a>Действия по подключению к API

Подключение API можно добавить с помощью Visual Studio Code и CLI.

### <a name="add-api-connection-using-visual-studio-code"></a>Добавление подключения API с помощью Visual Studio Code

Следующие шаги помогают добавить подключение API с помощью Visual Studio Code.

1. Откройте Microsoft Visual Studio Code.
2. Выберите значок :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API"::: Teams Toolkit на Visual Studio Code панели инструментов.
3. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="API add features":::

    * Вы также можете открыть палитру команд и ввести **Teams: Добавить облачные ресурсы**.

4. Во всплывающем окне выберите **подключение API** , которое вы хотите добавить в проект приложения Teams:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="Функции выбора API":::

5. Нажмите **OK**.

6. Введите конечную точку для API. Он добавляется в параметры локального приложения проекта и является базовым URL-адресом для запросов API.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="Конечная точка API":::

     > [!NOTE]
     > Убедитесь, что конечная точка является допустимым URL-адресом HTTP.S.

7. Выберите компонент, который имеет доступ к API.

8. Нажмите **OK**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="вызов API":::

9. Введите псевдоним для API. Псевдоним создает имя параметра приложения для API, добавляемого в параметр локального приложения проекта.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="Псевдоним API":::

10. Выберите необходимую проверку подлинности для запроса API из типа **проверки подлинности API**. Он создает соответствующий пример кода и добавляет соответствующие параметры локального приложения в зависимости от выбранного фрагмента.

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="аутентификация API":::

     В зависимости от выбранного типа проверки подлинности для завершения дополнительной настройки необходимо выполнить следующие действия.

# <a name="basic"></a>[Базовый](#tab/basic)

* Введите имя пользователя для обычной проверки подлинности.

  Теперь создан пример кода для вызова API по адресу bot\myAPI.js.

# <a name="certification"></a>[Сертификации](#tab/certification)

   Теперь создан пример кода для вызова API по адресу bot\myAPI.js.

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  Теперь создан пример кода для вызова API по адресу bot\myAPI.js.

# <a name="api-key"></a>[Ключ API](#tab/apikey)

* Выберите требуемую позицию ключа API в запросе.

* Введите имя ключа API.

  Теперь создан пример кода для вызова API по адресу bot\myAPI.js.

# <a name="custom-auth-implementation"></a>[Реализация пользовательской проверки подлинности](#tab/CustomAuthImplementation)

  Теперь создан пример кода для вызова API по адресу bot\myAPI.js.

---

## <a name="add-api-connection-using-cli"></a>Добавление подключения API с помощью интерфейса командной строки

Базовая команда этой функции — `teamsfx add api-connection [authentication type]`. В следующей таблице приведен список различных типов проверки подлинности и соответствующие им примеры команд:

 > [!TIP]
 > Вы можете использовать для `teamsfx add api-connection [authentication type] -h` получения справочной документации.

   |**Тип проверки подлинности**.|**Пример команды**|
   |-----------------------|------------------|
   |Базовый|teamsfx add api-connection basic--endpoint <https://example.com> --component bot--alias example--user-name exampleuser--interactive false|
   |Ключ API|teamsfx add api-connection apikey--endpoint <https://example.com> --component bot--alias example--key-location header--key-name example-key-name--interactive false|
   |Azure AD|teamsfx add api-connection aad--endpoint <https://example.com> --component bot--alias example--app-type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |Сертификат|teamsfx add api-connection cert--endpoint <https://example.com> --component bot--alias example--interactive false|
   |Пользовательские|teamsfx add api-connection custom--endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>Обновления структуры каталогов в проекте

 Набор средств Teams изменяет или `bot` папку `api` в зависимости от выбранных параметров:

1. Создание `{your_api_alias}.js/ts` файла. Файл инициализирует клиент API для API и экспортирует клиент API.

2. Добавление `@microsoft/teamsfx` пакета в `package.json`. Пакет обеспечивает поддержку распространенных методов проверки подлинности API.

3. Добавьте переменные среды в `.env.teamsfx.local`. Это конфигурации для выбранного типа проверки подлинности. Созданный код считывает значения из переменных среды.

## <a name="advantages"></a>Преимущества

Набор средств Teams помогает вам выполнить начальную загрузку примера кода для доступа к API, если у вас нет соответствующих языковых пакетов SDK для доступа к этим API.

## <a name="see-also"></a>См. также

* [Публикация приложений Teams с помощью набора средств Teams](publish.md)
