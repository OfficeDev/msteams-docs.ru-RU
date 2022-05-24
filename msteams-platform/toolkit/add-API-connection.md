---
title: Подключение к существующим API
author: MuyangAmigo
description: Описывает подключение к существующим API
ms.author: zhany
ms.localizationpriority: medium
ms.topic: Overview
ms.date: 05/20/2022
ms.openlocfilehash: 133ec7fa80950fde59529a2e1abe0415d6620171
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65655613"
---
# <a name="connect-to-existing-apis"></a>Подключение к существующим API

Teams toolkit помогает получить доступ к существующим API для создания Teams приложений. Эти API разрабатываются вашей организацией или сторонним разработчиком.

## <a name="advantage"></a>Преимущество

Teams toolkit помогает выполнить начальную загрузку примера кода для доступа к API, если у вас нет соответствующих языковых пакетов SDK для доступа к этим API.

## <a name="connect-to-the-api"></a>Подключение aPI

При использовании Teams Toolkit для подключения к существующему API Teams Toolkit выполняет следующую функцию:

* Создание примера кода в папке `./bot` или папке `./api`
* Добавление ссылки на пакет в `@microsoft/teamsfx``package.json`
* Добавление параметров приложения для API в  `.env.teamsfx.local` настройке локальной отладки

### <a name="connect-to-api-in-visual-studio-code"></a>Подключение API в Visual Studio Code

* Подключение к API можно добавить с помощью Teams Toolkit в Visual Studio Code:

    1. Откройте Microsoft Visual Studio Code.
    2. Выберите Teams :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API набора средств"::: на панели навигации слева.
    3. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**:

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-add-features.png" alt-text="API add features":::

       * Вы также можете открыть палитру команд и ввести **Teams: Добавить облачные ресурсы**.

    4. Во всплывающем окне выберите **подключение API**, которое вы хотите добавить в проект Teams приложения:

        :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-select-features.png" alt-text="Функции выбора API":::

    5. Нажмите кнопку **ОК**.

    6. Введите конечную точку для API. Он добавляется в параметры локального приложения проекта и является базовым URL-адресом для запросов API.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-endpoint.png" alt-text="Конечная точка API":::

         > [!NOTE]
         > Убедитесь, что конечная точка является допустимым URL-адресом HTTP.S.

    7. Выберите компонент, который имеет доступ к API.

    8. Нажмите кнопку **ОК**.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-invoke.png" alt-text="вызов API":::

    9. Введите псевдоним для API. Псевдоним создает имя параметра приложения для API, добавляемого в параметр локального приложения проекта.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-alias.png" alt-text="Псевдоним API":::

    10. Выберите необходимую проверку подлинности для запроса API из типа **проверки подлинности API**. Он создает соответствующий пример кода и добавляет соответствующие параметры локального приложения в зависимости от выбранного фрагмента.

         :::image type="content" source="../assets/images/teams-toolkit-v2/add-API/api-auth.png" alt-text="аутентификация API":::

         > [!NOTE]
         > В зависимости от выбранного типа проверки подлинности требуется дополнительная конфигурация.

### <a name="api-connection-in-teamsfx-cli"></a>Подключение API в CLI TeamsFx

Базовая команда этой функции — `teamsfx add api-connection [authentication type]`. В следующей таблице приведен список различных типов проверки подлинности и соответствующие им примеры команд:

 > [!Tip]
 > Вы можете использовать для `teamsfx add api-connection [authentication type] -h` получения справочной документации.

   |**Тип проверки подлинности**.|**Пример команды**|
   |-----------------------|------------------|
   |Базовый|teamsfx add api-connection basic --endpoint <https://example.com> --component bot --alias example --user-name exampleuser --interactive false|
   |Ключ API|teamsfx add api-connection apikey --endpoint <https://example.com> --component bot --alias example --key-location header --key-name example-key-name --interactive false|
   |Azure AD|teamsfx add api-connection aad --endpoint <https://example.com> --component bot --alias example --app-type custom --tenant-id your_tenant_id --app-id your_app_id --interactive false|
   |Сертификат|teamsfx add api-connection cert --endpoint <https://example.com> --component bot --alias example --interactive false|
   |Пользовательские|teamsfx add api-connection custom --endpoint <https://example.com> --component bot --alias example --interactive false|

## <a name="understand-toolkit-updates-to-your-project"></a>Общие сведения об обновлениях набора средств для проекта

 Teams toolkit изменяет или `bot` папку `api` в зависимости от выбранных параметров:

1. Создание `{your_api_alias}.js/ts` файла. Файл инициализирует клиент API для API и экспортирует клиент API.

2. Добавление `@microsoft/teamsfx` пакета в `package.json`. Пакет обеспечивает поддержку распространенных методов проверки подлинности API.

3. Добавьте переменные среды в `.env.teamsfx.local`. Это конфигурации для выбранного типа проверки подлинности. Созданный код считывает значения из переменных среды.

## <a name="test-api-connection-in-local-environment"></a>Проверка подключения API в локальной среде

Следующие шаги помогут проверить подключение API в локальной среде Teams Toolkit:

 1. **Запуск npm установки**

    Выполните `npm install` в `bot` папке `api` или в папке, чтобы установить добавленные пакеты.

 2. **Добавление учетных данных API в параметры локального приложения**

    Teams Toolkit не запрашивает учетные данные, но оставляет заполнители в файле параметров локального приложения. Замените заполнители соответствующими учетными данными для доступа к API. Файл параметров локального приложения — `.env.teamsfx.local` это файл в папке `bot` `api` или папке.

 3. **Использование клиента API для выполнения запросов API**

    Импортируйте клиент API из исходного кода, для которого требуется доступ к API:

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Создание http-запросов к целевому API (с помощью Axios)**

    Созданный клиент API является клиентом Axios API. Используйте клиент Axios для выполнения запросов к API.

     > [!Note]
     >[Axios](https://www.npmjs.com/package/axios) — это популярный пакет nodejs, который помогает с http-запросами. Дополнительные сведения о том, как выполнять http-запросы, см. в примере документации [по Axios](https://axios-http.com/docs/example) , чтобы узнать, как выполнять http-запросы.

## <a name="deploy-your-application-to-azure"></a>Развертывание приложения в Azure

Чтобы развернуть приложение в Azure, необходимо добавить проверку подлинности в параметры приложения для соответствующей среды. Например, ваш API может иметь разные учетные данные для и `dev` `prod`. В зависимости от потребностей среды настройте Teams Toolkit.

Teams Toolkit настраивает локальную среду. Пример кода начальной загрузки содержит комментарии, которые сообщают, какие параметры приложения необходимо настроить. Дополнительные сведения о параметрах приложения см. в разделе ["Добавление параметров приложения"](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="advanced-scenarios"></a>Расширенные сценарии

  В следующем разделе описаны сложные сценарии.

<br>

<details>
<summary><b>Настраиваемый поставщик проверки подлинности</b></summary>

Помимо поставщика проверки подлинности `@microsoft/teamsfx` , включенного в пакет, можно также реализовать настраиваемый поставщик проверки подлинности, `AuthProvider` реализующий интерфейс и использующий его в функции `createApiClient(..)` :

```Bash
import { AuthProvider } from '@microsoft/teamsfx'

class CustomAuthProvider implements AuthProvider {
    constructor() {
        // You can add necessary parameters for your customized logic in constructor
    }

    AddAuthenticationInfo: (config: AxiosRequestConfig) => Promise<AxiosRequestConfig> = async (
        config
    ) => {
        /*
        * The config parameter contains all the request information and can be updated to include extra authentication info.
        * Refer https://axios-http.com/docs/req_config for detailed document for the config object.
        * 
        * Add your customized logic that returns updated config
        */
    };
}
```
</details>
<details>
<summary><b>Подключение API для Azure AD разрешений</b></summary>
Azure AD выполняет проверку подлинности некоторых служб. Следующий список помогает получить доступ к этим службам для настройки разрешений API.

* [Использование контроль доступа списков управления доступом (ACL)](#access-control-lists-acls)
* [Использование Azure AD приложений](#azure-ad-application-permissions)

Получение маркера с нужными областями ресурсов для API зависит от реализации API.

Вы можете выполнить действия, чтобы получить доступ к этим API при использовании:

#### <a name="access-control-lists-acls"></a>контроль доступа списков (ACL)

   1. Запустите локальную отладку в облачной среде для проекта. Он создает Azure AD регистрации приложения Teams приложения.
  
   2. Откройте `.fx/states/state.{env}.json`и запишите значение свойства `clientId` `fx-resource-aad-app-for-teams` .

   3. Укажите идентификатор клиента поставщику API, чтобы настроить списки ACL в службе API.

#### <a name="azure-ad-application-permissions"></a>Azure AD приложения

  1. Откройте `templates/appPackage/aad.template.json` и добавьте в свойство следующее `requiredResourceAccess` содержимое:

```JSON
 {
     "resourceAppId": "The AAD App Id for the service providing the API you are connecting to",
     "resourceAccess": [
         {
             "id": "Target API's application permission Id",
             "type": "Role"
         }
     ]
 }
```

   2. Запустите локальную отладку в облачной среде для проекта. Он создает Azure AD регистрации приложения Teams приложения.

   3. Откройте `.fx/states/state.{env}.json` и запишите значение свойства `clientId` `fx-resource-aad-app-for-teams` . Это идентификатор клиента приложения.

   4. Предоставьте согласие администратора для требуемого разрешения приложения. Дополнительные сведения см. в [разделе "Предоставление согласия администратора"](/azure/active-directory/manage-apps/grant-admin-consent#grant-admin-consent-in-app-registrations).

        > [!NOTE]
        > Для разрешения приложения используйте идентификатор клиента.
</details>

## <a name="see-also"></a>См. также

* [Публикация приложений Teams с помощью набора средств Teams](publish.md)
