---
title: Добавление единого входа в приложения Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете, как добавить единый вход (SSO) в Teams Toolkit, включить поддержку единого входа и обновить приложение для использования единого входа.
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 9c221b0903d4541c4b0601e14ea347680140dfb9
ms.sourcegitcommit: 3aaccc48906fc6f6fbf79916af5664bf55537250
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68295965"
---
# <a name="add-single-sign-on-to-teams-app"></a>Добавление функциональности единого входа в приложение Teams

Microsoft Teams предоставляет функцию единого входа для приложения, чтобы получить маркер пользователя Teams, выполнившего вход, для доступа к Microsoft Graph и другим API. Набор средств Teams упрощает взаимодействие, абстрагирование некоторых Azure AD интеграции за некоторыми простыми API. Это позволяет легко добавлять функции единого входа в приложение Teams.

Для приложений, взаимодействующих с пользователем в чате, команде или канале, единый вход манифестируется как адаптивная карточка, с которой пользователь может взаимодействовать для вызова потока Azure AD согласия.

## <a name="enable-sso-support"></a>Включение поддержки единого входа

Набор средств Teams помогает добавить единый вход в следующие возможности Teams:

* Tab
* Bot
* Бот уведомлений: restify server
* Командный бот

### <a name="add-sso-using-visual-studio-code"></a>Добавление единого входа с помощью Visual Studio Code

Следующие действия помогут вам добавить единый вход с помощью Набора средств Teams в Visual Studio Code

1. Откройте **Microsoft Visual Studio Code**.
2. Выберите " :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="Добавить боковую"::: панель" на панели навигации слева.
3. Выберите **"Добавить компоненты"** в разделе **"РАЗРАБОТКА"**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-add features.png" alt-text="SSO add features":::

    * Вы также можете открыть палитру команд и выбрать **Teams: Добавить компоненты**

4. Выберите **единый вход**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/sso-select features.png" alt-text="sso select":::

### <a name="add-sso-using-teamsfx-cli"></a>Добавление единого входа с помощью CLI TeamsFx

Вы можете выполнить команду `teamsfx add sso` в **корневом каталоге проекта**

> [!Note]
> Эта функция включает единый вход для всех существующих применимых возможностей. Выполните те же действия, чтобы включить единый вход, если позже вы добавите возможность в проект.

## <a name="customize-your-project-using-teams-toolkit"></a>Настройка проекта с помощью Набора средств Teams

В следующей таблице перечислены изменения, внесенные набором средств Teams в проект:

   |**Тип**|**Файл**|**Назначение**|
   |--------|--------|-----------|
   |Create|`aad.template.json` Под `template/appPackage`|Azure AD манифест приложения представляет Azure AD приложения. `template/appPackage`помогает зарегистрировать приложение Azure AD на этапе локальной отладки или подготовки.|
   |Изменение|`manifest.template.json` Под `template/appPackage`|Объект `webApplicationInfo` добавляется в шаблон манифеста приложения Teams. Для включения единого входа в Teams требуется это поле. Это изменение вступает в силу при активации локальной отладки или подготовки.|
   |Create|`auth/tab`|Эталонный код, страницы перенаправления `README.md` проверки подлинности и файлы создаются по этому пути для проекта вкладки.|
   |Create|`auth/bot`|Эталонный код, страницы перенаправления `README.md` проверки подлинности и файлы создаются по этому пути для проекта бота.|

> [!Note]
> Добавляя единый вход, Набор средств Teams ничего не изменяет в облаке, пока вы не активируете локальную отладку. Обновите код, чтобы обеспечить работу единого входа в проекте.

## <a name="update-your-application-to-use-sso"></a>Обновление приложения для использования единого входа

Чтобы включить единый вход в приложении, выполните следующие действия.

> [!NOTE]
> Эти изменения основаны на шаблонах, которые мы создадим.

---
<br>
<br><details>
<summary><b>Проект табуляции </b></summary>

1. Скопируйте `auth-start.html` и `auth-end.htm`** в `auth/public` папку `tabs/public/`в . Teams Toolkit регистрирует эти две конечные точки в Azure AD для Azure AD перенаправления.

2. Скопируйте `sso` папку в `auth/tab` папку `tabs/src/sso/`.

    * `InitTeamsFx`: файл реализует функцию, которая инициализирует пакет SDK `GetUserProfile` TeamsFx и открывает компонент после инициализации пакета SDK.

    * `GetUserProfile`: файл реализует функцию, которая вызывает Microsoft API Graph для получения сведений о пользователе.

3. Выполните `npm install @microsoft/teamsfx-react` в .`tabs/`

4. Добавьте следующие строки для `tabs/src/components/sample/Welcome.tsx` импорта `InitTeamsFx`:

    ```Bash

    import { InitTeamsFx } from "../../sso/InitTeamsFx";

    ```

5. Замените следующую строку:

   `<AddSSO />` с `<InitTeamsFx />` заменой компонента `AddSso` компонентом `InitTeamsFx` .

</details>
<details>
<summary><b>Проект бота </b></summary>

#### <a name="set-up-the-azure-ad-redirects"></a>Настройка перенаправлений Azure AD перенаправлений

1. Переместите `auth/bot/public` папку в `bot/src`. Эта папка содержит HTML-страницы, размещаемую в приложении бота. Когда единый вход инициируется с Azure AD, он перенаправляет пользователя на HTML-страницы.
1. Измените код `bot/src/index` , чтобы добавить соответствующие `restify` маршруты на HTML-страницы.

    ```ts
    const path = require("path");

    server.get(
        "/auth-*.html",
        restify.plugins.serveStatic({
            directory: path.join(__dirname, "public"),
        })
    );
    ```

#### <a name="update-your-app"></a>Обновите приложение

Обработчик команд единого `ProfileSsoCommandHandler` входа использует Azure AD для вызова Microsoft Graph. Этот маркер получается с помощью маркера пользователя Teams, выполнив вход. Поток объединяется в диалоговом окне, в котором при необходимости отображается диалоговое окно согласия.

1. Переместите `profileSsoCommandHandler` файл в `auth/bot/sso` папку `bot/src`в . `ProfileSsoCommandHandler` Класс  — это обработчик команд единого входа для получения сведений о пользователе с помощью маркера единого входа. Следуйте этому методу и создайте собственный обработчик команд единого входа.
1. Откройте `package.json` файл и убедитесь, что версия пакета SDK teamsfx >= 1.2.0
1. Выполните команду `npm install isomorphic-fetch --save` в `bot` папке.
1. Для сценария ts выполните команду `npm install copyfiles --save-dev` в `bot` папке и замените следующие строки в `package.json`:

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src",
    ```

     с 

    ```json
    "build": "tsc --build && shx cp -r ./src/adaptiveCards ./lib/src && copyfiles src/public/*.html lib/",
    ```

    При этом копируются HTML-страницы, используемые для перенаправления проверки подлинности при создании проекта бота.

1. Чтобы поток согласия единого входа был работоем, замените следующий код в файле `bot/src/index` :

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res);
    });
    ```

     с 

    ```ts
    server.post("/api/messages", async (req, res) => {
        await commandBot.requestHandler(req, res).catch((err) => {
            // Error message including "412" means it is waiting for user's consent, which is a normal process of SSO, sholdn't throw this error.
            if (!err.message.includes("412")) {
                throw err;
            }
        });
    });
    ```

1. Замените параметры экземпляра `ConversationBot` , `bot/src/internal/initialize` чтобы добавить конфигурацию единого входа и обработчик команд единого входа:

    ```ts
    export const commandBot = new ConversationBot({
        ...
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler()],
        },
    });
    ```

     с 

    ```ts
    import { ProfileSsoCommandHandler } from "../profileSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        // To learn more about ssoConfig, please refer teamsfx sdk document: https://docs.microsoft.com/microsoftteams/platform/toolkit/teamsfx-sdk
        ssoConfig: {
            aad :{
                scopes:["User.Read"],
            },
        },
        command: {
            enabled: true,
            commands: [new HelloWorldCommandHandler() ],
            ssoCommands: [new ProfileSsoCommandHandler()],
        },
    });
    ```

1. Зарегистрируйте команду в манифесте приложения Teams. Откройте `templates/appPackage/manifest.template.json`и добавьте в бот следующие `commands` `commandLists` строки:

    ```json
    {
        "title": "profile",
        "description": "Show user profile using Single Sign On feature"
    }
    ```

#### <a name="add-a-new-sso-command-to-the-bot-optional"></a>Добавление новой команды единого входа в бот (необязательно)

После успешного добавления единого входа в проект можно добавить новую команду единого входа.

1. Создайте новый файл, например `photoSsoCommandHandler.ts` или `photoSsoCommandHandler.js` `bot/src/` добавьте собственный обработчик команд единого входа для вызова API Graph:

    ```TypeScript
    // for TypeScript:
    import { Activity, TurnContext, ActivityTypes } from "botbuilder";
    import "isomorphic-fetch";
    import {
        CommandMessage,
        TriggerPatterns,
        TeamsFx,
        createMicrosoftGraphClient,
        TeamsFxBotSsoCommandHandler,
        TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class PhotoSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
        triggerPatterns: TriggerPatterns = "photo";

        async handleCommandReceived(
            context: TurnContext,
            message: CommandMessage,
            tokenResponse: TeamsBotSsoPromptTokenResponse,
        ): Promise<string | Partial<Activity> | void> {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);

            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
                // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage: Partial<Activity> = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }
    ```

    ```javascript
    // for JavaScript:
    const { ActivityTypes } = require("botbuilder");
    require("isomorphic-fetch");
    const { createMicrosoftGraphClient, TeamsFx } = require("@microsoft/teamsfx");

    class PhotoSsoCommandHandler {
        triggerPatterns = "photo";

        async handleCommandReceived(context, message, tokenResponse) {
            await context.sendActivity("Retrieving user information from Microsoft Graph ...");

            const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

            const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
        
            let photoUrl = "";
            try {
                const photo = await graphClient.api("/me/photo/$value").get();
                const arrayBuffer = await photo.arrayBuffer();
                const buffer=Buffer.from(arrayBuffer, 'binary');
                photoUrl = "data:image/png;base64," + buffer.toString("base64");
            } catch {
            // Could not fetch photo from user's profile, return empty string as placeholder.
            }
            if (photoUrl) {
                const photoMessage = {
                    type: ActivityTypes.Message, 
                    text: 'This is your photo:', 
                    attachments: [
                        {
                            name: 'photo.png',
                            contentType: 'image/png',
                            contentUrl: photoUrl
                        }
                    ]
                };
                return photoMessage;
            } else {
                return "Could not retrieve your photo from Microsoft Graph. Please make sure you have uploaded your photo.";
            }
        }
    }

    module.exports = {
        PhotoSsoCommandHandler,
    };

    ```

1. Добавление `PhotoSsoCommandHandler` экземпляра в `ssoCommands` массив в:`bot/src/internal/initialize.ts`

    ```ts
    // for TypeScript:
    import { PhotoSsoCommandHandler } from "../photoSsoCommandHandler";

    export const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()],
        },
    });
    ```

    ```javascript
    // for JavaScript:
    ...
    const { PhotoSsoCommandHandler } = require("../photoSsoCommandHandler");

    const commandBot = new ConversationBot({
        ...
        command: {
            ...
            ssoCommands: [new ProfileSsoCommandHandler(), new PhotoSsoCommandHandler()]
        },
    });
    ...

    ```

1. Зарегистрируйте команду в манифесте приложения Teams. Откройте `templates/appPackage/manifest.template.json`и добавьте в бот следующие `commands` `commandLists` строки:

    ```JSON

    {
        "title": "photo",
        "description": "Show user photo using Single Sign On feature"
    }

    ```

</details>
<br>

## <a name="debug-your-application"></a>Отладка приложения

Нажмите клавишу F5, чтобы отладить приложение. Набор средств Teams использует Azure AD манифеста для регистрации Azure AD для единого входа. Сведения о функциях локальной отладки Набора средств Teams см. в разделе "Локальная отладка [приложения Teams"](debug-local.md).

## <a name="customize-azure-ad-application-registration"></a>Настройка регистрации Azure AD приложения

Манифест [Azure AD](/azure/active-directory/develop/reference-app-manifest) позволяет настраивать различные аспекты регистрации приложения. При необходимости манифест можно обновить. Если вам нужно включить дополнительные разрешения API для доступа к нужным API, см. сведения о разрешениях API для доступа к [нужным API](https://github.com/OfficeDev/TeamsFx/wiki/#customize-aad-manifest-template).
Чтобы просмотреть Azure AD в портал Azure, см. Azure AD [в портал Azure](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#How-to-view-the-AAD-app-on-the-Azure-portal).

## <a name="sso-authentication-concepts"></a>Основные понятия проверки подлинности единого входа

Для проверки подлинности единого входа помогают следующие понятия:

### <a name="working-of-sso-in-teams"></a>Работа единого входа в Teams

Проверка подлинности единого входа (SSO) в Microsoft Azure Active Directory (Azure AD) автоматически обновляет маркер проверки подлинности, чтобы свести к минимуму количество раз, когда пользователям необходимо вводить свои учетные данные для входа. Если пользователь соглашается использовать ваше приложение, ему не придется повторно давать согласие на другом устройстве, поскольку вход будет выполнен автоматически.

Вкладки и боты Teams имеют аналогичный поток для поддержки единого входа. Дополнительные сведения см. в следующих статьях:

1. [Проверка подлинности единого входа (SSO) на вкладке](../tabs/how-to/authentication/tab-sso-overview.md)
2. [Проверка подлинности единого входа (SSO) в Bots](../bots/how-to/authentication/auth-aad-sso-bots.md)

### <a name="simplified-sso-with-teamsfx"></a>Упрощенный единый вход с TeamsFx

TeamsFx помогает сократить количество задач разработчика, используя единый вход и доступ к облачным ресурсам до однострочного оператора с нулевой конфигурацией.

С помощью пакета SDK для TeamsFx можно написать код проверки подлинности пользователя упрощенным способом с помощью учетных данных:

1. Удостоверение пользователя в среде браузера: `TeamsUserCredential` представляет удостоверение текущего пользователя Teams.
2. Удостоверение пользователя в Node.js: `OnBehalfOfUserCredential` использует поток On-Behalf-Of и маркер единого входа.
3. Удостоверение приложения в Node.js среде: `AppCredential` представляет удостоверение приложения.

Дополнительные сведения о пакете SDK для TeamsFx см. в следующих статьях:

* [Справочник по пакету SDK](TeamsFx-SDK.md) или [API TeamsFx](/javascript/api/@microsoft/teamsfx/?view=msteams-client-js-latest&preserve-view=true)
* [Пример коллекции Microsoft Teams Framework (TeamsFx)](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2)

## <a name="see-also"></a>См. также

* [Предварительные требования для создания приложения Teams](tools-prerequisites.md)
