---
title: Интеграция существующих СТОРОННИХ API
author: MuyangAmigo
description: Из этой статьи вы узнаете, как набор средств помогает выполнить начальную загрузку примера доступа к существующим API. Он предоставляет список различных типов проверки подлинности.
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 6377f7d8a38054dacca76c0f87e39e51f466d925
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833144"
---
# <a name="integrate-existing-third-party-apis"></a>Интеграция существующих СТОРОННИХ API

Набор средств Teams помогает получить доступ к существующим API для создания приложений Teams. Эти API разрабатываются вашей организацией или сторонними разработчиками. При использовании Набора средств Teams для подключения к существующему API Набор средств Teams выполняет следующую функцию:

* Создайте пример кода в `./bot` папке или `./api` .
* Добавьте ссылку на пакет в `@microsoft/teamsfx` `package.json`.
* Добавьте параметры приложения для API в  `.env.teamsfx.local` , который настраивает локальную отладку.

## <a name="steps-to-connect-to-api"></a>Действия по подключению к API

Подключение API можно добавить с помощью Visual Studio Code и команды CLI.

### <a name="add-api-connection-using-visual-studio-code"></a>Добавление подключения API с помощью Visual Studio Code

Следующие действия помогут вам добавить подключение API с помощью Visual Studio Code.

1. Откройте Microsoft Visual Studio Code.
2. Выберите :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="значок API"::: набора средств Teams на панели инструментов Visual Studio Code.
3. Выберите **Добавить компоненты** в разделе **РАЗРАБОТКА**:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="api add features":::

    * Вы также можете открыть палитру команд и ввести **Teams: добавить облачные ресурсы**.

4. Во всплывающем окне выберите **ПОДКЛЮЧЕНИЕ API** , которое вы хотите добавить в проект приложения Teams:

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="api select features":::

5. Нажмите кнопку **ОК**.

6. Введите конечную точку для API. Он добавляется в параметры локального приложения проекта и является базовым URL-адресом для запросов API.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="Конечная точка API":::

     > [!NOTE]
     > Убедитесь, что конечная точка является допустимым URL-адресом HTTP(s).

7. Выберите компонент, который обращается к API.

8. Нажмите кнопку **ОК**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="вызов api":::

9. Введите псевдоним для API. Псевдоним создает имя параметра приложения для API, добавляемого в параметр локального приложения проекта.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="псевдоним api":::

10. Выберите требуемую проверку подлинности для запроса API из **типа проверки подлинности API**. Он создает соответствующий пример кода и добавляет соответствующие параметры локального приложения в зависимости от выбранного вами.

     :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/myAPI connection.png" alt-text="api auth":::

     В зависимости от выбранного типа проверки подлинности для завершения дополнительной настройки необходимо выполнить следующие действия.

# <a name="basic"></a>[Базовый](#tab/basic)

* Введите имя пользователя для базовой проверки подлинности.

  Теперь был создан пример кода для вызова API в bot\myAPI.js.

# <a name="certification"></a>[Сертификации](#tab/certification)

   Теперь был создан пример кода для вызова API в bot\myAPI.js.

# <a name="azure-active-directory"></a>[Azure Active Directory](#tab/AAD)

  Теперь был создан пример кода для вызова API в bot\myAPI.js.

# <a name="api-key"></a>[Ключ API](#tab/apikey)

* Выберите необходимую позицию ключа API в запросе.

* Введите имя ключа API.

  Теперь был создан пример кода для вызова API в bot\myAPI.js.

# <a name="custom-auth-implementation"></a>[Реализация пользовательской проверки подлинности](#tab/CustomAuthImplementation)

  Теперь был создан пример кода для вызова API в bot\myAPI.js.

---

## <a name="add-api-connection-using-cli"></a>Добавление подключения API с помощью ИНТЕРФЕЙСА командной строки

Базовая команда этого компонента — `teamsfx add api-connection [authentication type]`. В следующей таблице приведен список различных типов проверки подлинности и соответствующие примеры команд.

 > [!TIP]
 > Вы можете использовать `teamsfx add api-connection [authentication type] -h` для получения справочного документа.

   |**Тип проверки подлинности**.|**Пример команды**|
   |-----------------------|------------------|
   |Базовый|teamsfx добавляет api-connection basic--endpoint <https://example.com> --component bot-alias example--user-name exampleuser--interactive false|
   |Ключ API|Teamsfx добавляет api-connection apikey--endpoint <https://example.com> --component bot-alias example--key-location header--key-name example-key-name-interactive false|
   |Azure AD|teamsfx добавляет api-connection aad--endpoint <https://example.com> --component bot-alias example---app-type custom--tenant-id your_tenant_id--app-id your_app_id--interactive false|
   |Сертификат|Teamsfx добавляет api-connection cert--endpoint <https://example.com> --component bot--alias example--interactive false|
   |Пользовательские|teamsfx добавляет api-connection custom--endpoint <https://example.com> --component bot--alias example--interactive false|

---

## <a name="directory-structure-updates-to-your-project"></a>Обновление структуры каталогов в проекте

 Teams Toolkit изменяет `bot` папку или `api` изменяет папку в зависимости от выбранных значений:

1. Создать `{your_api_alias}.js/ts` файл. Файл инициализирует клиент API для ВАШЕГО API и экспортирует клиент API.

2. Добавьте `@microsoft/teamsfx` пакет в `package.json`. Пакет обеспечивает поддержку распространенных методов проверки подлинности API.

3. Добавьте переменные среды в `.env.teamsfx.local`. Это конфигурации для выбранного типа проверки подлинности. Созданный код считывает значения из переменных среды.

## <a name="advantages"></a>Преимущества

Набор средств Teams помогает загрузить пример кода для доступа к API, если у вас нет пакетов SDK, соответствующих языку, для доступа к этим API.

## <a name="see-also"></a>См. также

[Публикация приложений Teams с помощью набора средств Teams](publish.md)
