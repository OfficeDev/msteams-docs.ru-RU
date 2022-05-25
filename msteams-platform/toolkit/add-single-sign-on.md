---
title: Добавление единого входа в приложения Teams приложений
author: zyxiaoyuer
description: Описание добавления единого входа Teams Toolkit
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 73177f96172e4fd60b7225c2463efb6a057f36c4
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656847"
---
# <a name="add-single-sign-on-to-teams-app"></a>Добавление единого входа в Teams приложения

Microsoft Teams предоставляет функцию единого входа для приложения, чтобы получить маркер пользователя Teams для доступа к Microsoft Graph и другим API. Teams Toolkit упрощает взаимодействие, абстрагирование некоторых Azure AD и интеграции за некоторыми простыми API. Это позволяет легко добавлять функции единого входа в Teams приложения.

Для приложений, взаимодействующих с пользователем в чате, команде или канале, единый вход манифестируется как адаптивная карточка, с которой пользователь может взаимодействовать для вызова потока Azure AD согласия.

## <a name="enable-sso-support"></a>Включение поддержки единого входа

Teams Toolkit помогает добавить единый вход в следующие Teams возможностей:

* Tab
* Bot
* Бот уведомлений: restify server
* Командный бот

### <a name="add-sso-using-visual-studio-code"></a>Добавление единого входа с помощью Visual Studio Code

Следующие шаги помогут вам добавить единый вход с помощью Teams Toolkit в Visual Studio Code

1. Откройте **Microsoft Visual Studio Code**.
2. Выберите Teams toolkit :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="sso add sidebar"::: from left navigation bar(Добавить боковую панель).
3. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="SSO add features":::

    * Вы также можете открыть палитру команд и выбрать Teams **: Добавить компоненты**

4. Выберите **единый вход**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>Добавление единого входа с помощью CLI TeamsFx

Вы можете выполнить команду `teamsfx add sso`  в **корневом каталоге проекта**

> [!Note]
> Эта функция включает единый вход для всех существующих применимых возможностей. Выполните те же действия, чтобы включить единый вход, если позже вы добавите возможность в проект.

## <a name="customize-your-project-using-teams-toolkit"></a>Настройка проекта с помощью Teams Toolkit

В следующей таблице перечислены изменения, Teams набор средств вносит в проект:

   |**Type (Тип)**|**File**|**Назначение**|
   |--------|--------|-----------|
   |Create|`aad.template.json` Под `template/appPackage`|Azure AD манифест приложения представляет Azure AD приложения. `template/appPackage`помогает зарегистрировать приложение Azure AD на этапе локальной отладки или подготовки.|
   |Изменение|`manifest.template.json` Под `template/appPackage`|Объект `webApplicationInfo` добавляется в шаблон манифеста Teams приложения. Teams требуется это поле для включения единого входа. Это изменение вступает в силу при активации локальной отладки или подготовки.|
   |Create|`auth/tab`|Эталонный код, страницы перенаправления проверки подлинности и `README.md` файл создаются по этому пути для проекта вкладки.|
   |Create|`auth/bot`|Эталонный код, страницы перенаправления проверки подлинности и `README.md` файл создаются по этому пути для проекта бота.|

> [!Note]
> Добавив единый вход, Teams Toolkit ничего не изменит в облаке, пока вы не активируете локальную отладку. Обновите код, чтобы обеспечить работу единого входа в проекте.

## <a name="update-your-application-to-use-sso"></a>Обновление приложения для использования единого входа

Следующие действия помогут вам включить единый вход в приложение.

> [!NOTE]
> Эти изменения основаны на шаблонах, которые мы создадим.

---
<br>
<br><details>
<summary><b>Проект табуляции </b></summary>

1. Скопируйте `auth-start.html` и `auth-end.htm`** в `auth/public` папку `tabs/public/`в . Teams Toolkit регистрирует эти две конечные точки в Azure AD для Azure AD потока перенаправления.

2. Скопируйте `sso` папку в `auth/tab` папку `tabs/src/sso/`.

    * `InitTeamsFx`: файл реализует функцию, которая инициализирует пакет SDK `GetUserProfile` TeamsFx и открывает компонент после инициализации пакета SDK.

    * `GetUserProfile`: файл реализует функцию, которая вызывает Microsoft API Graph для получения сведений о пользователе.

3. Выполните `npm install @microsoft/teamsfx-react` в .`tabs/`

4. Добавьте следующие строки для `tabs/src/components/sample/Welcome.tsx` импорта `InitTeamsFx`:

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. Замените следующую строку: `<AddSSO />` заменой `<InitTeamsFx />` компонента `AddSso` компонентом `InitTeamsFx` .

</details>
<details>
<summary><b>Проект бота </b></summary>

1. Скопируйте `auth/bot/public` папку в `bot/src`. Две папки содержат HTML-страницы, используемые для перенаправления проверки подлинности. Чтобы добавить маршрутизацию на эти страницы, `bot/src/index` необходимо изменить файл.

2. Скопируйте `auth/bot/sso` папку в `bot/src`. Две папки содержат три файла в качестве ссылки для реализации единого входа:

    * `showUserInfo`: он реализует функцию для получения сведений о пользователе с помощью маркера единого входа. Следуйте этому, чтобы создать собственный метод, для которого требуется маркер единого входа.

    * `ssoDialog`: создает [componentDialog](/javascript/api/botbuilder-dialogs/componentdialog?view=botbuilder-ts-latest&preserve-view=true) , используемый для единого входа.

    * `teamsSsoBot`: он создает [TeamsActivityHandler](/javascript/api/botbuilder/teamsactivityhandler?view=botbuilder-ts-latest&preserve-view=true) `ssoDialog` `showUserInfo` с командой, которую можно активировать, и добавляет ее в качестве команды.

3. Следуйте примеру кода и зарегистрируйте собственную команду в `addCommand` этом файле (необязательно).

4. Выполните `npm install isomorphic-fetch` в .`bot/`

5. Выполните `npm install copyfiles` в файле `bot/` package.json и замените следующую строку:
  
   ```JSON

   "build": "tsc --build",

    ```

    с 

   ```JSON

   "build": "tsc --build && copyfiles public/*.html lib/",

   ```

   HTML-страницы, используемые для перенаправления проверки подлинности, копируются при создании этого проекта бота.

6. После добавления следующих файлов необходимо создать новый экземпляр `teamsSsoBot` в файле `bot/src/index` . Замените следующий код:

   ```Bash
  
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
   await commandBot.requestHandler(req, res);
   });  

   ```

    с 

   ```Bash

   const handler = new TeamsSsoBot();
   // Process Teams activity with Bot Framework.
   server.post("/api/messages", async (req, res) => {
       await commandBot.requestHandler(req, res, async (context)=> {
           await handler.run(context);
       });
   });

   ```

7. Добавьте HTML-маршруты в `bot/src/index` файл:

   ```Bash

   server.get(
       "/auth-*.html",
       restify.plugins.serveStatic({
           directory: path.join(__dirname, "public"),
       })
   );

   ```

8. Добавьте следующие строки для `bot/src/index` импорта и `teamsSsoBot` `path`:

   ```Bash

   // For ts:
   import { TeamsSsoBot } from "./sso/teamsSsoBot";
   const path = require("path");

   // For js:
   const { TeamsSsoBot } = require("./sso/teamsSsoBot");
   const path = require("path");

   ```

9. Зарегистрируйте команду в манифесте Teams приложения. Откройте `templates/appPackage/manifest.template.json`и добавьте в бот следующие `command` `commandLists` строки:

   ```JSON

   {
       "title": "show",
       "description": "Show user profile using Single Sign On feature"
   }

   ```
</details>
<details>
<summary><b>Добавление новой команды в бот </b></summary>

> [!NOTE]
> В настоящее время эти инструкции применимы к `command bot`. Если вы начинаете с примера `bot`[bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/bot-sso).

Следующие действия помогут вам добавить новую команду после добавления единого входа в проект:

1. Создайте файл (`todo.ts`или`todo.js`) в разделе `bot/src/` и добавьте собственную бизнес-логику для вызова API Graph:

# <a name="typescript"></a>[TypeScript](#tab/typescript)

   ```typescript
   // for TypeScript:
export async function showUserImage(
    context: TurnContext,
    ssoToken: string,
    param: any[]
): Promise<DialogTurnResult> {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}  
   ```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

   ```javaScript
   // for JavaScript:
export async function showUserImage(context, ssoToken, param) {
    await context.sendActivity("Retrieving user photo from Microsoft Graph ...");

    // Init TeamsFx instance with SSO token
    const teamsfx = new TeamsFx().setSsoToken(ssoToken);

    // Update scope here. For example: Mail.Read, etc.
    const graphClient = createMicrosoftGraphClient(teamsfx, param[0]);
    
    // You can add following code to get your photo:
    // let photoUrl = "";
    // try {
    //   const photo = await graphClient.api("/me/photo/$value").get();
    //   photoUrl = URL.createObjectURL(photo);
    // } catch {
    //   // Could not fetch photo from user's profile, return empty string as placeholder.
    // }
    // if (photoUrl) {
    //   await context.sendActivity(
    //     `You can find your photo here: ${photoUrl}`
    //   );
    // } else {
    //   await context.sendActivity("Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.");
    // }

    return;
}
   ```

---

2. Регистрация новой команды

   * Добавьте следующую строку для регистрации новой команды, используя:`addCommand` `teamsSsoBot`

     ```bash

     this.dialog.addCommand("ShowUserProfile", "show", showUserInfo);

     ```

   * Добавьте следующие строки после приведенной выше строки, чтобы зарегистрировать новую `photo` команду и подключиться к методу, добавленному `showUserImage` выше:

     ```bash

     // As shown here, you can add your own parameter into the `showUserImage` method
     // You can also use regular expression for the command here
     const scope = ["User.Read"];
     this.dialog.addCommand("ShowUserPhoto", new RegExp("photo\s*.*"), showUserImage, scope);

     ```

3. Зарегистрируйте команду в манифесте Teams приложения. Откройте `templates/appPackage/manifest.template.json`и добавьте в бот следующие `command` `commandLists` строки:

   ```JSON

   {
       "title": "photo",
       "description": "Show user photo using Single Sign On feature"
   }

   ```
</details>
<br>

## <a name="debug-your-application"></a>Отладка приложения

Нажмите клавишу F5, чтобы отладить приложение. Teams Toolkit использует Azure AD манифеста для регистрации приложения Azure AD для единого входа. Сведения Teams локальной отладки набора средств см. в разделе "Отладка Teams [приложения локально"](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Настройка регистрации Azure AD приложения

Манифест [Azure AD](/azure/active-directory/develop/reference-app-manifest) позволяет настраивать различные аспекты регистрации приложения. При необходимости манифест можно обновить. Если вам нужно включить дополнительные разрешения API для доступа к нужным API, ознакомьтесь с разрешениями API для доступа к нужным [API](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Чтобы просмотреть приложение Azure AD на портале Azure, см. Azure AD [в портал Azure](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal). 

## <a name="sso-authentication-concepts"></a>Основные понятия проверки подлинности единого входа

Для проверки подлинности единого входа вам помогут следующие понятия:

### <a name="working-of-sso-in-teams"></a>Работа единого входа в Teams

Проверка подлинности единого входа (SSO) в Microsoft Azure Active Directory (Azure AD) автоматически обновляет маркер проверки подлинности, чтобы свести к минимуму количество раз, когда пользователям необходимо вводить свои учетные данные для входа. Если пользователь соглашается использовать ваше приложение, ему не придется повторно давать согласие на другом устройстве, поскольку вход будет выполнен автоматически.

Teams и боты имеют аналогичный поток для поддержки единого входа. Дополнительные сведения см. в следующих статьях:

1. [Проверка подлинности единого входа (SSO) на вкладке](../tabs/how-to/authentication/auth-aad-sso.md)
2. [Проверка подлинности единого входа (SSO) в Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Упрощенный единый вход с TeamsFx

TeamsFx помогает сократить количество задач разработчика, используя единый вход и доступ к облачным ресурсам до однострочного оператора с нулевой конфигурацией.

С помощью пакета SDK для TeamsFx можно написать код проверки подлинности пользователя упрощенным способом с помощью учетных данных:

1. Удостоверение пользователя в среде браузера: `TeamsUserCredential` Teams удостоверение текущего пользователя.
2. Удостоверение пользователя в Node.js: `OnBehalfOfUserCredentail` использует поток On-Behalf-Of и маркер единого входа.
3. Удостоверение приложения в Node.js среде: `AppCredential` представляет удостоверение приложения.

Дополнительные сведения о пакете SDK для TeamsFx см. в следующих статьях:

* [Справочник по пакету SDK](TeamsFx-SDK.md) или [API TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Microsoft Teams Framework (TeamsFx) — пример коллекции](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>См. также

* [Подготовка учетных записей для создания приложений Teams](accounts.md)