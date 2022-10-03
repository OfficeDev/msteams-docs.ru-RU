---
title: Пакет SDK TeamsFx
author: surbhigupta
description: В этом модуле вы узнаете о пакете SDK для TeamsFx, основных понятиях и структуре кода, расширенной настройке и сценариях.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9d870680e146564bb23db0193d2e2b116a249009
ms.sourcegitcommit: 16898eebeddc1bc1ac0d9862b4627c3bb501c109
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/03/2022
ms.locfileid: "68327589"
---
# <a name="teamsfx-sdk"></a>Пакет SDK TeamsFx

TeamsFx помогает сократить количество задач, используя единый вход Microsoft Teams (Teams SSO) и доступ к облачным ресурсам до однострочного оператора с нулевой конфигурацией. Пакет SDK TeamsFx можно использовать в браузере и Node.js среде. Доступ к основным функциональным возможностям TeamsFx можно получить в клиентской и серверной среде. Код проверки подлинности пользователя можно написать упрощенным способом:

* Вкладка Teams
* Бот Teams
* Функция Azure

## <a name="prerequisites"></a>Предварительные требования

Необходимо установить следующие средства и настроить среду разработки:

| &nbsp; | Установка | Для использования... |
   | --- | --- | --- |
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download); | Сред сборки JavaScript, TypeScript или SharePoint Framework (SPFx). Используйте версию 1.55 или более позднюю. |
   | &nbsp; | [Набор средств Teams](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Расширение Microsoft Visual Studio Code, которое создает шаблон проекта для вашего приложения. Используйте версию 4.0.0. |
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Серверной среды выполнения JavaScript. Используйте последнюю версию версии 16 LTS.|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Microsoft Teams для взаимодействия в одном месте со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний и звонков.|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/) | Браузера со средствами разработчика. |

> [!NOTE]
> Если в проекте [пакеты](https://github.com/Microsoft/botbuilder-js#packages), связанные с `botbuilder` как зависимости, убедитесь, что они имеют ту же версию.

У вас должны быть знания о следующих элементах:

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Справочная документация по API](https://aka.ms/teamsfx-sdk-help)
* [Примеры](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Начало работы

Пакет SDK TeamsFx предварительно настроен в проекте со сформированными шаблонами с помощью набора средств TeamsFx или CLI.
Дополнительные сведения см. в [проекте приложения Teams](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Установка пакета `@microsoft/teamsfx`

Установите пакет SDK TeamsFx для TypeScript или JavaScript с помощью `npm`.

```bash
npm install @microsoft/teamsfx
```

## <a name="teamsfx-core-functionalities"></a>Основные функции TeamsFx

### <a name="teamsfx-class"></a>Класс TeamsFx

Экземпляр класса TeamsFx по умолчанию имеет доступ ко всем параметрам TeamsFx из переменных среды. Можно также настроить настраиваемые значения конфигурации для переопределения значений по умолчанию. Подробности см. в [конфигурации переопределения](#override-configuration).
При создании экземпляра TeamsFx также необходимо указать тип удостоверения.
Существует два типа удостоверений:

* **Удостоверение** пользователя: представляет текущего пользователя Teams.
* **Удостоверение приложения**: представляет само приложение.

    > [!NOTE]
    > Для этих двух типов удостоверений конструкторы и методы TeamsFx не совпадают.

Дополнительные сведения об удостоверении пользователя и удостоверении приложения см. в следующем разделе:

<details>
<summary><b> Удостоверение пользователя </b></summary>

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| Подлинность приложения определяется в качестве текущего пользователя Teams. |
| `TeamsFx:setSsoToken()`| Удостоверение пользователя в среде Node.js (без браузера). |
| `TeamsFx:getUserInfo()` | Для получения базовых сведений о пользователе. |
| `TeamsFx:login()` | Оно используется, чтобы позволить пользователю завершить процесс получения согласия, если вы хотите использовать единый вход для получения токена доступа для определенных областей действия OAuth. |

> [!NOTE]
> Доступ к ресурсам можно получить от имени текущего пользователя Teams.
</details>

<details>
<summary><b> Удостоверение приложения </b></summary>

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Application  is authenticated as an application. The permission usually needs administrator's approval.|
| `TeamsFx:getCredential()`| Она предоставляет экземпляры учетных данных, автоматически соответствующие типу удостоверения. |

> [!NOTE]
> Для ресурсов требуется согласие администратора.
</details>

### <a name="credential"></a>Credential

Чтобы инициализировать TeamsFx, необходимо выбрать требуемый тип удостоверения. После указания типа удостоверения пакет SDK использует другой тип класса учетных данных. Они представляют удостоверение и получают маркер доступа с помощью соответствующего потока проверки подлинности. Классы учетных данных реализуют `TokenCredential` интерфейс, широко используемый в API библиотеки Azure, предназначенный для предоставления маркеров доступа для определенных областей. Другие API полагаются на вызов учетных данных `TeamsFx:getCredential()`для получения экземпляра `TokenCredential`. Дополнительные сведения о классах, связанных с потоком проверки подлинности и учетными данными, см. в [папке учетных данных](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential).

Есть три класса учетных данных для упрощения проверки подлинности. Вот соответствующие сценарии для каждого целевого класса учетных данных.

<details>
<summary><b> Удостоверение пользователя в среде браузера </b></summary>

`TeamsUserCredential` представляет удостоверение текущего пользователя Teams. При первой проверке подлинности учетных данных пользователя единый вход Teams выполняет поток On-Behalf-Of для обмена маркерами. Пакет SDK использует эти учетные данные при выборе удостоверения пользователя в среде браузера.

Необходимые конфигурации: `initiateLoginEndpoint` и `clientId`.
</details>

<details>
<summary><b> Удостоверение пользователя в Node.js среде </b></summary>

`OnBehalfOfUserCredential` использует поток On-Behalf-Of и требует маркер единого входа Teams в сценариях функции Или бота Azure. Пакет SDK для TeamsFx использует следующие учетные данные при выборе удостоверения пользователя в Node.js среде.

Требуемая конфигурация: `authorityHost`, `tenantId`, `clientId`, `clientSecret` или `certificateContent`.
</details>

<details>
<summary><b> Удостоверение приложения в Node.js среде </b></summary>

`AppCredential` представляет удостоверение приложения. Удостоверение приложения можно использовать, если пользователь не участвует, например в задании автоматизации, активируемом по времени. Пакет SDK teamsFx использует следующие учетные данные при выборе удостоверения приложения в Node.js среде.

Требуемая конфигурация: `tenantId`, `clientId`, `clientSecret` или `certificateContent`.
</details>

### <a name="bot-sso"></a>SSO бота

Классы, связанные с ботом, хранятся в папке [bot folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` интегрируется с bot framework. Он упрощает процесс проверки подлинности при разработке приложения бота и хочет использовать единый вход бота.

Требуемая конфигурация: `initiateLoginEndpoint`, `tenantId`, `clientId` и `applicationIdUri`.

### <a name="supported-functions"></a>Поддерживаемые функции

TeamsFx SDK provides several functions to ease the configuration for third-party libraries. They're located under [core folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

* Служба Microsoft Graph:`createMicrosoftGraphClient` и `MsGraphAuthProvider` помогают создать экземпляр Graph с проверкой подлинности.
* SQL:`getTediousConnectionConfig` возвращает утомительную конфигурацию подключения.

    Требуемая конфигурация

  * Если вы хотите использовать удостоверение пользователя, то `sqlServerEndpoint`и `sqlUsername` `sqlPassword` являются обязательными.
  * Если вы хотите использовать удостоверение MSI, то `sqlServerEndpoint`и `sqlIdentityId` они являются обязательными.

### <a name="override-configuration"></a>Переопределение конфигурации

Пользовательскую конфигурацию можно передать при создании `TeamsFx` нового экземпляра, чтобы переопределить конфигурацию по умолчанию или задать обязательные поля, если `environment variables` они отсутствуют.

<details>
<summary><b> Для проекта табуляции </b> </summary>

Если вы создали проект вкладки с помощью Microsoft Visual Studio Code Toolkit, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:

* authorityHost (REACT_APP_AUTHORITY_HOST)
* tenantId (REACT_APP_TENANT_ID)
* clientId (REACT_APP_CLIENT_ID)
* initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
* applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
* apiEndpoint (REACT_APP_FUNC_ENDPOINT) // используется только при наличии серверной функции
* apiName (REACT_APP_FUNC_NAME) // используется только при наличии серверной функции

</details>

<details>
<summary><b> Для проекта функции или бота Azure </b></summary>

Если вы создали проект функции или бота Azure с помощью Visual Studio Code Toolkit, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:

* initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
* authorityHost (M365_AUTHORITY_HOST)
* tenantId (M365_TENANT_ID)
* clientId (M365_CLIENT_ID)
* clientSecret (M365_CLIENT_SECRET)
* applicationIdUri (M365_APPLICATION_ID_URI)
* apiEndpoint (API_ENDPOINT)
* sqlServerEndpoint (SQL_ENDPOINT) // используется только при наличии экземпляра SQL
* sqlUsername (SQL_USER_NAME) // используется только при наличии экземпляра sql
* sqlPassword (SQL_PASSWORD) // используется только при наличии экземпляра sql
* sqlDatabaseName (SQL_DATABASE_NAME) // используется только при наличии экземпляра SQL
* sqlIdentityId (IDENTITY_ID) // используется только при наличии экземпляра sql

</details>

### <a name="error-handling"></a>Обработка ошибок

Базовый тип ответа на ошибку API `ErrorWithCode`— содержит код ошибки и сообщение об ошибке. Например, чтобы отфильтровать определенную ошибку, можно использовать следующий фрагмент кода:

```typescript
try {
  const teamsfx = new TeamsFx();
  await teamsfx.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

Если экземпляр учетных данных используется в другой библиотеке, например Microsoft Graph, возможно, эта ошибка перехвачена и преобразована.

## <a name="microsoft-graph-scenarios"></a>Сценарии Microsoft Graph

В этом разделе содержится несколько фрагментов кода для распространенных сценариев, связанных с Microsoft Graph. В таких сценариях пользователь может вызывать API, используя разные разрешения в разных концах (интерфейсе или серверной части).

* Разрешение делегата пользователя во внешнем интерфейсе (использование TeamsUserCredential) <details>
    <summary><b>Использование API graph в приложении табуляции</b></summary>

    В этом фрагменте кода показано, как использовать `TeamsFx` `createMicrosoftGraphClient` и получать профили пользователей из Microsoft Graph. Здесь также показано, как перехватывать и разрешать объект `GraphError`.

    1. Импортируйте необходимые классы.

    ```typescript
    import {
      createMicrosoftGraphClient,
      TeamsFx,
    } from "@microsoft/teamsfx";
    ```

    2. Используется `TeamsFx.login()` для получения согласия пользователя.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups.
    await teamsfx.login(["User.Read"]); // Login with scope
    ```

    3. Вы можете инициализировать экземпляр TeamsFx и клиент graph и получить информацию из MS Graph этим клиентом.

    ```typescript
    try {
      const teamsfx = new TeamsFx();
      const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
      const profile = await graphClient.api("/me").get();
    } catch (err: unknown) {
      // ErrorWithCode is handled by Graph client
      if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
        // Need to show login button to ask for user consent.
      }
    }
    ```

    Дополнительные сведения о примере использования API Graph в приложении tab см. в примере [вкладки hello-world](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab).

    </details>

    <details>
    <summary><b>Интеграция с Microsoft Graph Toolkit</b></summary>

    Библиотека [Microsoft Graph Toolkit (mgt)](https://aka.ms/mgt) — это коллекция различных поставщиков проверки подлинности и компонентов пользовательского интерфейса на базе Microsoft Graph.

    Пакет `@microsoft/mgt-teamsfx-provider` предоставляет класс, `TeamsFxProvider` использующий `TeamsFx` класс для входа пользователей и получения маркеров для использования с Graph.

    1. Вы можете установить следующие необходимые пакеты:

    ```bash
    npm install @microsoft/mgt-element @microsoft/mgt-teamsfx-provider @microsoft/teamsfx
    ```

    2. Инициализировать поставщик внутри компонента.

    ```typescript
     // Import the providers and credential at the top of the page
    import {Providers} from '@microsoft/mgt-element';
    import {TeamsFxProvider} from '@microsoft/mgt-teamsfx-provider';
    import {TeamsUserCredential} from "@microsoft/teamsfx";

    const scope = ["User.Read"];
    const teamsfx = new TeamsFx();
    const provider = new TeamsFxProvider(teamsfx, scope);
    Providers.globalProvider = provider;   
    ```

    3. Этот метод можно использовать `teamsfx.login(scopes)` для получения необходимого маркера доступа.

    ```typescript
    // Put these code in a call-to-action callback function to avoid browser blocking automatically showing up pop-ups. 
    await teamsfx.login(this.scope);
    Providers.globalProvider.setState(ProviderState.SignedIn);
    ```

    4. Теперь вы можете добавить любой компонент на HTML-странице `render()` или в методе, React `TeamsFx` использовать контекст для доступа к Microsoft Graph.

    ```html
    <mgt-person query="me" view="threeLines"></mgt-person>
    ```

    ```typescript
    public render(): void {
    return (
        <div>
            <Person personQuery="me" view={PersonViewType.threelines}></Person>
        </div>
    );
    }    
    ```

    Дополнительные сведения о примере для инициализации поставщика TeamsFx см. в примере [экспорта контактов](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/graph-toolkit-contact-exporter).

    </details>

* Разрешение делегата пользователя в серверной части (use OnBehalfOfUserCredential) <details>
    <summary><b>Использование API Graph в приложении бота</b></summary>

    В этом фрагменте кода показано `TeamsBotSsoPrompt` , как задать диалоговое окно, а затем выполнить вход для получения маркера доступа.

    1. Инициализация и добавление `TeamsBotSsoPrompt` в набор диалогов.

    ```typescript
    const { ConversationState, MemoryStorage } = require("botbuilder");
    const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
    const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

    const convoState = new ConversationState(new MemoryStorage());
    const dialogState = convoState.createProperty("dialogState");
    const dialogs = new DialogSet(dialogState);

    const teamsfx = new TeamsFx();
    dialogs.add(
      new TeamsBotSsoPrompt(teamsfx, "TeamsBotSsoPrompt", {
        scopes: ["User.Read"],
      })
    );    
    ```

    2. Начните диалоговое окно и войдите в систему.

    ```typescript
    dialogs.add(
      new WaterfallDialog("taskNeedingLogin", [
        async (step) => {
          return await step.beginDialog("TeamsBotSsoPrompt");
        },
        async (step) => {
          const token = step.result;
          if (token) {
            // ... continue with task needing access token ...
          } else {
            await step.context.sendActivity(`Sorry... We couldn't log you in. Try again later.`);
            return await step.endDialog();
          }
        },
      ])
    );    
    ```

    Дополнительные сведения о примере использования API Graph в приложении бота см. в примере [bot-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/bot-sso).

    </details>

    <details>
    <summary><b>Использование API Graph в расширении сообщений</b></summary>

    В этом фрагменте `handleTeamsMessagingExtensionQuery` `TeamsActivityHandler`кода показано, `handleMessageExtensionQueryWithToken` как переопределить расширения и использовать пакет SDK TeamsFx для входа в систему для получения маркера доступа:

    ```typescript
    public async handleTeamsMessagingExtensionQuery(context: TurnContext, query: any): Promise<any> {
      return await handleMessageExtensionQueryWithToken(context, null, 'User.Read', 
        async (token: MessageExtensionTokenResponse) => {
          // ... continue to query with access token ...
        });
    }    
    ```

    Дополнительные сведения об использовании API graph в расширении сообщений см. в разделе [message-extension-sso-sample](https://aka.ms/teamsfx-me-sso-sample).
    </details>

    <details>
    <summary><b>Использование API Graph в command Bot</b></summary>

    В этом фрагменте кода показано, `TeamsFxBotSsoCommandHandler` как реализовать командный бот для вызова Microsoft API.

    ```typescript
    import { Activity, TurnContext } from "botbuilder";
    import {
      CommandMessage,
      TriggerPatterns,
      TeamsFx,
      createMicrosoftGraphClient,
      TeamsFxBotSsoCommandHandler,
      TeamsBotSsoPromptTokenResponse,
    } from "@microsoft/teamsfx";

    export class ProfileSsoCommandHandler implements TeamsFxBotSsoCommandHandler {
      triggerPatterns: TriggerPatterns = "profile";

      async handleCommandReceived(
        context: TurnContext,
        message: CommandMessage,
        tokenResponse: TeamsBotSsoPromptTokenResponse,
      ): Promise<string | Partial<Activity> | void> {
        // Init TeamsFx instance with SSO token
        const teamsfx = new TeamsFx().setSsoToken(tokenResponse.ssoToken);

        // Add scope for your Azure AD app. For example: Mail.Read, etc.
        const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
      
        // Call graph api use `graph` instance to get user profile information
        const me = await graphClient.api("/me").get();

        if (me) {
          // Bot will send the user profile info to user
          return `Your command is '${message.text}' and you're logged in as ${me.displayName}`;
        } else {
          return "Could not retrieve profile information from Microsoft Graph.";
        }
      }
    }    
    ```

    Дополнительные сведения об использовании этого класса в командном боте см. в разделе "Добавление единого входа [в приложение Teams"](add-single-sign-on.md). Кроме того, есть пример проекта [command-bot-with-sso](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/command-bot-with-sso) , в котором можно попробовать единый командный бот.

    </details>

    <details>
    <summary><b>Вызов функции Azure в приложении табуляции: поток On-Behalf-Of</b></summary>

    В этом фрагменте `CreateApiClient` `axios` кода показано, как использовать или библиотеку для вызова функции Azure, а также как вызывать API Graph в функции Azure для получения профилей пользователей.

    1. Пакет SDK `CreateApiClient` TeamsFx можно использовать для вызова функции Azure:

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const teamsfx = new TeamsFx();

      // Get the credential.
      const credential = teamsfx.getCredential(); 
      // Create an API client by providing the token and endpoint.
      const apiClient = CreateApiClient(
        teamsfx.getConfig("YOUR_API_ENDPOINT"), // Create an API Client that uses SSO token to authenticate requests
        new BearerTokenAuthProvider(async () =>  (await credential.getToken(""))!.token) // Call API hosted in Azure Functions on behalf of user to inject token to request header
      );

      // Send a GET request to "RELATIVE_API_PATH", "/api/functionName" for example.
      const response = await apiClient.get("RELATIVE_API_PATH");
      return response.data;
    }    
    ```

    Вы также можете использовать библиотеку `axios` для вызова функции Azure.

    ```typescript
    async function callFunction(teamsfx?: TeamsFx) {
      const accessToken = await teamsfx.getCredential().getToken(""); // Get SSO token 
      // teamsfx.getConfig("apiEndpoint") will read REACT_APP_FUNC_ENDPOINT environment variable 
      const endpoint = teamsfx.getConfig("apiEndpoint");
      const response = await axios.default.get(endpoint + "/api/" + functionName, {
        headers: {
          authorization: "Bearer " + accessToken.token,
        },
      });
      return response.data;
    }    
    ```

    2. Вызов API Graph в функции Azure от имени пользователя в ответ.

    ```typescript
    export default async function run(
      context: Context,
      req: HttpRequest,
      teamsfxContext: TeamsfxContext
    ): Promise<Response> {
      const res: Response = { status: 200, body: {},};
      // ...
      teamsfx = new TeamsFx().setSsoToken(accessToken);
      // Query user's information from the access token.
      try {
        const currentUser: UserInfo = await teamsfx.getUserInfo();
        if (currentUser && currentUser.displayName) {
          res.body.userInfoMessage = `User display name is ${currentUser.displayName}.`;
        } else {
          res.body.userInfoMessage = "No user information was found in access token.";
        }
      } catch (e) {
      }
      // Create a graph client to access user's Microsoft 365 data after user has consented.
      try {
        const graphClient: Client = createMicrosoftGraphClient(teamsfx, [".default"]);
        const profile: any = await graphClient.api("/me").get();
        res.body.graphClientMessage = profile;
      } catch (e) {
      }
      return res;
    }    
    ```

    Дополнительные сведения об использовании API Graph в приложении бота см. в примере  [hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

* Разрешение приложения в серверной части <details>
    <summary><b>Используйте проверку подлинности с применением сертификатов в Функции Azure</b></summary>

    В этом фрагменте кода показано, как использовать разрешение приложения на основе сертификатов для получения маркера, который можно использовать для вызова API Graph.

    1. Вы можете инициализировать `authConfig` объект, указав .`PEM-encoded key certificate`

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      certificateContent: "The content of a PEM-encoded public/private key certificate",
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Этот маркер можно использовать `authConfig` для получения маркера.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    </details>

    <details>
    <summary><b>Использование проверки подлинности секрета клиента в функции Azure</b></summary>

    В этом фрагменте кода показано, как использовать разрешение приложения секрета клиента для получения маркера, который можно использовать для вызова API Graph.

    1. Вы можете инициализировать `authConfig` объект, указав .`client secret`

    ```typescript
    const authConfig = {
      clientId: process.env.M365_CLIENT_ID,
      clientSecret: process.env.M365_CLIENT_SECRET,
      authorityHost: process.env.M365_AUTHORITY_HOST,
      tenantId: process.env.M365_TENANT_ID,
    };    
    ```

    2. Этот маркер можно использовать `authConfig` для получения маркера.

    ```typescript
    const teamsfx = new TeamsFx(IdentityType.App);
    teamsfx.setCustomeConfig(authConfig);
    const token = teamsfx.getCredential().getToken();    
    ```

    Дополнительные сведения об использовании API Graph в приложении бота см. в примере [hello-world-tab-with-backend](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/hello-world-tab-with-backend).

    </details>

## <a name="other-scenarios"></a>Прочие сценарии

В этом разделе содержится несколько фрагментов кода для других сценариев, связанных с Microsoft Graph. Вы можете создать клиент API в Bot или Функции Azure и получить доступ к базе данных SQL в Функции Azure.

  <details>
  <summary><b>Создание клиента API для вызова существующего API в Bot или Функции Azure</b></summary>

  В этом фрагменте кода показано, как вызвать существующий API в Bot с помощью `ApiKeyProvider`.

  ```typescript
  const teamsfx = new TeamsFx();

  // Create an API Key auth provider. In addition to APiKeyProvider, following auth providers are also available:
  // BearerTokenAuthProvider, BasicAuthProvider, CertificateAuthProvider.
  const authProvider = new ApiKeyProvider("YOUR_API_KEY_NAME",
    teamsfx.getConfig("YOUR_API_KEY_VALUE"), // This reads the value of YOUR_API_KEY_VALUE environment variable.
    ApiKeyLocation.Header
  );

  // Create an API client using above auth provider.
  // You can also implement AuthProvider interface and use it here.
  const apiClient = createApiClient(
    teamsfx.getConfig("YOUR_API_ENDPOINT"), // This reads YOUR_API_ENDPOINT environment variable.
    authProvider
  );

  // Send a GET request to "RELATIVE_API_PATH", "/api/apiname" for example.
  const response = await apiClient.get("RELATIVE_API_PATH");  
  ```

  </details>

  <details>
  <summary><b>Доступ к базе данных SQL в Функции Azure</b></summary>

  Используйте `tedious` библиотеку для доступа к SQL и использования, `DefaultTediousConnectionConfiguration` который управляет проверкой подлинности. Вы также можете создать конфигурацию подключения других библиотек SQL на основе результата `sqlConnectionConfig.getConfig()`.

  1. Задайте конфигурацию подключения.

  ```typescript
  // Equivalent to:
  // const sqlConnectConfig = new DefaultTediousConnectionConfiguration({
  //    sqlServerEndpoint: process.env.SQL_ENDPOINT,
  //    sqlUsername: process.env.SQL_USER_NAME,
  //    sqlPassword: process.env.SQL_PASSWORD,
  // });
  const teamsfx = new TeamsFx();
  // If there's only one SQL database
  const config = await getTediousConnectionConfig(teamsfx);
  // If there are multiple SQL databases
  const config2 = await getTediousConnectionConfig(teamsfx, "your database name");  
  ```

  2. Подключитесь к базе данных.

  ```typescript
  const connection = new Connection(config);
  connection.on("connect", (error) => {
    if (error) {
      console.log(error);
    }
  });  
  ```

  > [!NOTE]
  > Дополнительные сведения о примере доступа к базе данных SQL в функции Azure см. в [примере share-now](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/share-now).

</details>

## <a name="advanced-customization"></a>Дополнительная настройка

### <a name="configure-log"></a>Настройка журнала

При использовании этой библиотеки можно настроить уровень журнала клиента и перенаправить выходные данные.

> [!NOTE]
> По умолчанию ведение журнала отключено. Вы можете включить его, настроив уровень ведения журнала.

#### <a name="enable-log-by-setting-log-level"></a>Включите журнал, установив уровень ведения журнала

При установке уровня журнала ведение журнала будет включено. По умолчанию он выводит сведения журнала в консоль.

Установите уровень журнала, используя следующий фрагмент кода:

```typescript
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

> [!NOTE]
> Вы можете перенаправить выходные данные журнала, настроив пользовательский регистратор или функцию журнала.

#### <a name="redirect-by-setting-custom-logger"></a>Перенаправление путем настройки пользовательской записи журнала

```typescript
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Перенаправление путем настройки пользовательской функции журнала

```typescript
setLogLevel(LogLevel.Info);
// Only log error message to Application Insights in bot application.
setLogFunction((level: LogLevel, message: string) => {
  if (level === LogLevel.Error) {
    this.telemetryClient.trackTrace({
      message: message,
      severityLevel: Severity.Error,
    });
  }
});
```

> [!NOTE]
> Функции журнала не вступает в силу при настройке пользовательского средства ведения журнала.

## <a name="upgrade-latest-sdk-version"></a>Обновление последней версии SDK

Если вы используете версию пакета SDK `loadConfiguration()`, выполните следующие действия, чтобы обновить пакет SDK до последней версии:

1. Удалите `loadConfiguration()` и передайте настроенные параметры с помощью `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Замените `new TeamsUserCredential()` на `new TeamsFx()`.
3. Замените `new M365TenantCredential()` на `new TeamsFx(IdentityType.App)`.
4. Замените `new OnBehalfOfUserCredential(ssoToken)` на `new TeamsFx().setSsoToken(ssoToken)`.
5. Передайте экземпляр вспомогательных `TeamsFx` функций для замены экземпляра учетных данных.

## <a name="next-step"></a>Следующий этап

Подробные примеры использования проекта примеров пакета [SDK для](https://github.com/OfficeDev/TeamsFx-Samples) TeamsFx.

## <a name="see-also"></a>Дополнительные ресурсы

[Образец галереи Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
