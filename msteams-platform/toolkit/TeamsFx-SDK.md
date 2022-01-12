---
title: Пакет SDK TeamsFx
author: MuyangAmigo
description: О teamsFx SDK
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d0ec446b51363bbbe4c3322ec1d840ad4068ff74
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768373"
---
# <a name="teamsfx-sdk-for-typescript-or-javascript"></a>TeamsFx SDK для TypeScript или JavaScript

TeamsFx стремится сократить задачи реализации удостоверений и доступа к облачным ресурсам к однострочному заявлению с нулевой конфигурацией.

Используйте библиотеку для:

- Аналогичным образом можно получить доступ к основным функциональным возможностям в клиентской и серверной среде.
- Напишите код проверки подлинности пользователей упрощенным способом.
 
## <a name="get-started"></a>Начало работы

TeamsFx SDK предварительно настроен в проекте scaffolded с помощью инструментария TeamsFx или CLI.
Дополнительные сведения см. [в Teams проекта приложения.](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md)

### <a name="prerequisites"></a>Необходимые условия

- Node.js `10.x.x` версии или более поздней версии.
- Если в проекте установлены связанные пакеты в качестве зависимостей, убедитесь, что они имеют ту же версию и `botbuilder` версия [](https://github.com/Microsoft/botbuilder-js#packages) `>= 4.9.3` . ([Проблема - все пакеты BOTBUILDER](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548)должны быть одной и той же версии )

Дополнительные сведения см. в указанных ниже статьях.
* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk) 
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) 
* [Справочная документация по API](https://aka.ms/teamsfx-sdk-help) 
* [Примеры](https://github.com/OfficeDev/TeamsFx-Samples)

### <a name="install-the-microsoftteamsfx-package"></a>Установка `@microsoft/teamsfx` пакета

Установите SDK TeamsFx для TypeScript или JavaScript с `npm` помощью:

```bash
npm install @microsoft/teamsfx
```

### <a name="create-and-authenticate-microsoftgraphclient"></a>Создание и проверка подлинности `MicrosoftGraphClient`

Чтобы создать объект клиентской диаграммы для доступа к API Graph Microsoft, необходимо проверить подлинность учетных данных. SDK предоставляет несколько классов учетных данных для выбора, отвечающих различным требованиям. Перед использованием учетных данных необходимо загрузить конфигурацию.

- В среде браузера необходимо явно передать параметры конфигурации. Проект scaffolded React предоставил переменные среды для использования.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
```

- В среде NodeJS, такой как Azure Function, можно просто `loadConfiguration` позвонить. Он будет загружаться из переменных среды по умолчанию.

```ts
loadConfiguration();
```

#### <a name="using-teams-app-user-credential"></a>Использование учетных данных Teams приложения

Используйте следующий фрагмент:

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get();
```
> [!NOTE]
> Этот класс учетных данных можно использовать в приложении браузера, например Teams Tab App.

#### <a name="using-microsoft-365-tenant-credential"></a>Использование Microsoft 365 учетных данных клиента

Microsoft 365 учетные данные клиента не требуют взаимодействия с пользователем Teams приложения. Вы можете вызвать Microsoft Graph в качестве приложения.

Используйте следующий фрагмент:

```ts
loadConfiguration();
const credential = new M365TenantCredential();
const graphClient = createMicrosoftGraphClient(credential);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get();
```

## <a name="core-concepts-and-code-structure"></a>Основные понятия и структура кода

### <a name="credentials"></a>Учетные данные

В папке учетных данных находятся 3 класса учетных данных, которые [помогут](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential) упростить проверку подлинности.

Классы учетных данных `TokenCredential` реализуют интерфейс, широко используемый в API библиотек Azure. Они предназначены для предоставления маркеров доступа для определенных областей. Следующие классы учетных данных представляют различные удостоверения в определенных сценариях:

* `TeamsUserCredential`представляют Teams текущего пользователя. С помощью этой учетной записи будет запрашиваться согласие пользователя в первый раз.
* `M365TenantCredential`представляют Microsoft 365 клиента. Он обычно используется, когда пользователь не участвует, как работа автоматизации с срабатывным временем.
* `OnBehalfOfUserCredential` используется от имени потока. Ему необходим маркер доступа, и вы можете получить новый маркер для различных областей. Он предназначен для использования в сценариях Azure Function или Bot.

### <a name="bots"></a>Боты

Классы, связанные с ботом, хранятся в [папке бота.](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot)

`TeamsBotSsoPrompt` может интегрироваться с рамками Bot. Это упрощает процесс проверки подлинности для разработки приложения-бота.

### <a name="helper-functions"></a>Функции помощника

TeamsFx SDK предоставляет дополнительные функции для облегчения конфигурации сторонних библиотек. Они находятся в основной [папке.](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core)

### <a name="error-handling"></a>Обработка ошибок

Ответ на ошибку API `ErrorWithCode` содержит код ошибки и сообщение об ошибке.

Например, чтобы отфильтровать определенную ошибку, можно использовать следующий фрагмент:

```ts
try {
  const credential = new TeamsUserCredential();
  await credential.login("User.Read");
} catch (err: unknown) {
  if (err instanceof ErrorWithCode && err.code !== ErrorCode.ConsentFailed) {
    throw err;
  } else {
    // Silently fail because user cancels the consent dialog
    return;
  }
}
```

Если экземпляр учетных данных используется в других библиотеках, таких как Microsoft Graph, возможно, ошибка будет поймана и преобразована.

```ts
try {
  const credential = new TeamsUserCredential();
  const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
  const profile = await graphClient.api("/me").get();
} catch (err: unknown) {
  // ErrorWithCode is handled by Graph client
  if (err instanceof GraphError && err.code?.includes(ErrorCode.UiRequiredError)) {
    this.setState({
      showLoginBtn: true,
    });
  }
}
```

## <a name="scenarios"></a>Сценарии

В следующем разделе содержится несколько фрагментов кода для распространенных сценариев:

### <a name="use-graph-api-in-tab-app"></a>Использование Graph API в приложении вкладки

Использование `TeamsUserCredential` и `createMicrosoftGraphClient` .

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const graphClient = createMicrosoftGraphClient(credential, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

### <a name="call-azure-function-in-tab-app"></a>Вызов функции Azure в приложении вкладки

Используйте `axios` библиотеку, чтобы сделать http-запрос в Azure Function.

```ts
loadConfiguration({
  authentication: {
    initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
    simpleAuthEndpoint: process.env.REACT_APP_TEAMSFX_ENDPOINT,
    clientId: process.env.REACT_APP_CLIENT_ID,
  },
});
const credential: any = new TeamsUserCredential();
const token = credential.getToken(""); // Get SSO token for the user
// Call API hosted in Azure Functions on behalf of user
const apiConfig = getResourceConfiguration(ResourceType.API);
const response = await axios.default.get(apiConfig.endpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

### <a name="access-sql-database-in-azure-function"></a>Доступ SQL базы данных в Azure Function

Используйте `tedious` библиотеку для доступа к SQL и `DefaultTediousConnectionConfiguration` рычагов, которые управляют проверкой подлинности.
Кроме того, вы также можете составить подключение config других SQL библиотек на основе `tedious` `sqlConnectionConfig.getConfig()` результатов .

```ts
loadConfiguration();
const sqlConnectConfig = new DefaultTediousConnectionConfiguration();
const config = await sqlConnectConfig.getConfig();
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

### <a name="use-certificate-based-authentication-in-azure-function"></a>Использование проверки подлинности на основе сертификатов в Azure Function

```ts
loadConfiguration({
  authentication: {
    clientId: process.env.M365_CLIENT_ID,
    certificateContent: "The content of a PEM-encoded public/private key certificate",
    authorityHost: process.env.M365_AUTHORITY_HOST,
    tenantId: process.env.M365_TENANT_ID,
  },
});
```

### <a name="use-graph-api-in-bot-application"></a>Использование Graph API в приложении Bot

Добавьте `TeamsBotSsoPrompt` набор диалогов.

```ts
const { ConversationState, MemoryStorage } = require("botbuilder");
const { DialogSet, WaterfallDialog } = require("botbuilder-dialogs");
const { TeamsBotSsoPrompt } = require("@microsoft/teamsfx");

const convoState = new ConversationState(new MemoryStorage());
const dialogState = convoState.createProperty("dialogState");
const dialogs = new DialogSet(dialogState);

loadConfiguration();
dialogs.add(
  new TeamsBotSsoPrompt("TeamsBotSsoPrompt", {
    scopes: ["User.Read"],
  })
);

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

## <a name="troubleshooting"></a>Устранение неполадок

### <a name="configure-log"></a>Настройка журнала

Вы можете установить уровень журнала клиента и перенаправить выходы при использовании этой библиотеки. Ведение журнала по умолчанию отключено, его можно включить, установив уровень журнала.

#### <a name="enable-log-by-setting-log-level"></a>Включить журнал, установив уровень журнала

Ведение журнала включено только при наборе уровня журнала. По умолчанию он печатает сведения журнала на консоли.

Установите уровень журнала с помощью следующего фрагмента:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Вы можете перенаправить выход журнала, установив настраиваемый регистратор или функцию журнала.

##### <a name="redirect-by-setting-custom-logger"></a>Перенаправление путем настройки настраиваемой регистратора

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

##### <a name="redirect-by-setting-custom-log-function"></a>Перенаправление путем настройки настраиваемой функции журнала

> [!NOTE]
> Функция журнала не вступает в силу, если вы установите настраиваемый регистратор.

```ts
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

## <a name="see-also"></a>См. также

[Пример коллекции Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples)