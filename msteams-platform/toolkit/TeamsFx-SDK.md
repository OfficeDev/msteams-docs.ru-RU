---
title: Пакет SDK TeamsFx
author: MuyangAmigo
description: Об SDK TeamsFx
ms.author: nintan
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d54c3d962ecc9d1fd703bd4126d71564f8358794
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111222"
---
# <a name="teamsfx-sdk"></a>Пакет SDK TeamsFx

TeamsFx помогает сократить задачи разработчика, используя единый вход Teams и доступ к облачным ресурсам в одной строке с нулевой конфигурацией. Пакет SDK TeamsFx создан для использования в среде браузера и Node.js. К распространенным сценариям относятся:

* Приложение вкладки Teams
* Функция Azure
* Бот Teams

С помощью SDK TeamsFx можно выполнить следующее.

* Получить доступ к основным функциям в клиентской и серверной среде 
* Написать код проверки подлинности пользователя упрощенным способом

## <a name="prerequisites"></a>Предварительные условия

Установите следующие средства и настройте среду разработки.

* Node.js последней версии
* Если в проекте [пакеты](https://github.com/Microsoft/botbuilder-js#packages), связанные с `botbuilder` как зависимости, убедитесь, что они имеют ту же версию. В настоящее время требуется версия 4.15.0 или более поздняя. Дополнительные сведения см. в статье [Пакеты построителя ботов должны иметь ту же версию](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548).

У вас должны быть достаточные для работы знания о следующем.

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

### <a name="create-microsoftgraphclient-service"></a>Создание службы `MicrosoftGraphClient`

Для создания клиентского объекта Graph и доступа к API Microsoft Graph требуются учетные данные для проверки подлинности. Пакет SDK предоставляет API для настройки для разработчиков.

<br>

<details>
<summary><b>Вызовите Graph API от имени пользователя Teams (личность пользователя)</b></summary>

Используйте следующий фрагмент кода:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.User, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// }
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
const profile = await graphClient.api("/me").get(); // Get the profile of current user
```

</details>

<br>

<details>
<summary><b>Вызовите Graph API без пользователя (идентификатор приложения)</b></summary>

Для этого не требуется взаимодействие с пользователем Teams. Microsoft Graph можно вызвать как удостоверение приложения.

Используйте следующий фрагмент кода:

```ts
// Equivalent to:
// const teamsfx = new TeamsFx(IdentityType.App, {
//   initiateLoginEndpoint: process.env.REACT_APP_START_LOGIN_PAGE_URL,
//   clientId: process.env.REACT_APP_CLIENT_ID,
// });
const teamsfx = new TeamsFx(IdentityType.App);
const graphClient = createMicrosoftGraphClient(teamsfx);
const profile = await graphClient.api("/users/{object_id_of_another_people}").get(); // Get the profile of certain user
```

</details>

<br>

## <a name="core-concepts-and-code-structure"></a>Основные понятия и структура кода

### <a name="teamsfx-class"></a>Класс TeamsFx

Экземпляр класса TeamsFx по умолчанию имеет доступ ко всем параметрам TeamsFx из переменных среды. Можно также настроить настраиваемые значения конфигурации для переопределения значений по умолчанию. Дополнительные сведения см. в разделе [конфигурации переопределения](#override-configuration). При создании экземпляра TeamsFx также необходимо указать тип удостоверения. Существует два типа удостоверений:

* Удостоверение пользователя
* Удостоверение приложения

#### <a name="user-identity"></a>Удостоверение пользователя

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| Подлинность приложения определяется в качестве текущего пользователя Teams. |
| `TeamsFx:setSsoToken()`| Удостоверение пользователя в среде Node.js (без браузера). |
| `TeamsFx:getUserInfo()` | Для получения базовых сведений о пользователе. |
| `TeamsFx:login()` | Он используется, чтобы позволить пользователю выполнять процесс согласия, если вы хотите использовать SSO для получения маркера доступа для определенных областей OAuth. |

> [!NOTE]
> Доступ к ресурсам можно получить от имени текущего пользователя Teams.

#### <a name="application-identity"></a>Удостоверение приложения

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Подлинность приложения проверяется как приложение. Разрешение обычно требует утверждения администратором.|
| `TeamsFx:getCredential()`| Она предоставляет экземпляры учетных данных, автоматически соответствующие типу удостоверения. |

> [!NOTE]
> Для ресурсов требуется согласие администратора.

### <a name="credential"></a>Credential

При инициализации TeamsFx необходимо выбрать тип удостоверения. После того как вы указали тип удостоверения при инициализации TeamsFx, пакет SDK использует различные типы класса учетных данных для представления удостоверения и получения маркера доступа с помощью соответствующего потока auth.

Есть три класса учетных данных для упрощения проверки подлинности. [папка с учетными данными](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential). Классы учетных данных реализуют интерфейс `TokenCredential`, который широко используется в API библиотеки Azure, предназначенных для предоставления маркеров доступа определенным областям. Другие API использует вызов учетных данных `TeamsFx:getCredential()` для получения экземпляра `TokenCredential`.

Приведем соответствующие сценарии для каждой цели класса учетных данных.

#### <a name="user-identity-in-browser-environment"></a>Удостоверение пользователя в среде браузера
`TeamsUserCredential` представляет удостоверение текущего пользователя Teams. При первом использовании этих учетных данных запрашивается согласие пользователя. Использует SSO Teams и поток "от имени" для обмена маркерами. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение пользователя в среде браузера.

Требуемая конфигурация: `initiateLoginEndpoint`, `clientId`.

#### <a name="user-identity-in-nodejs-environment"></a>Удостоверение пользователя в среде Node.js
`OnBehalfOfUserCredential` использует поток "от имени" и требует маркер SSO Teams. Он предназначен для использования в сценариях использования функций или ботов Azure. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение пользователя в среде Node.

Требуемая конфигурация: `authorityHost`, `tenantId`, `clientId`, `clientSecret` или `certificateContent`.

#### <a name="application-identity-in-nodejs-environment"></a>Удостоверение приложения в среде Node.js
`AppCredential` представляет удостоверение приложения. Обычно используется, когда пользователь не участвует, как и в задании автоматизации, инициированном по времени. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение приложения в среде Node.

Требуемая конфигурация: `tenantId`, `clientId`, `clientSecret` или `certificateContent`.

### <a name="bot-sso"></a>SSO бота

Классы, связанные с ботом, хранятся в папке [bot folder](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` имеет хорошую интеграцию с инфраструктурой ботов. Это упрощает процесс проверки подлинности при разработке приложения-бота и когда вы хотите использовать SSO бота.

Требуемая конфигурация: `initiateLoginEndpoint`, `tenantId`, `clientId` и `applicationIdUri`.

### <a name="supported-functions"></a>Поддерживаемые функции

Пакет SDK TeamsFx предоставляет несколько функций для упрощения настройки сторонних библиотек. Они находятся в [основной папке](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

*  Служба Microsoft Graph:`createMicrosoftGraphClient` и `MsGraphAuthProvider` помогают создать экземпляр Graph с проверкой подлинности.
*  SQL:`getTediousConnectionConfig` возвращает утомительную конфигурацию подключения.

Требуемая конфигурация
* `sqlServerEndpoint`, `sqlUsername`, `sqlPassword`, если вы хотите использовать удостоверение пользователя
* `sqlServerEndpoint`, `sqlIdentityId`, если вы хотите использовать удостоверение MSI

### <a name="error-handling"></a>Обработка ошибок

Отклик об ошибке API, `ErrorWithCode`, содержит код ошибки и сообщение об ошибке. Например, чтобы отфильтровать определенную ошибку, можно использовать следующий фрагмент кода:

```ts
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

```ts
try {
  const teamsfx = new TeamsFx();
  const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]); // Initializes MS Graph SDK using our MsGraphAuthProvider
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

В следующем разделе содержится несколько фрагментов кода для распространенных сценариев.

<br>

<details>
<summary><b>Использование API Graph во приложении на вкладке</b></summary>
 
Используйте `TeamsFx` и `createMicrosoftGraphClient`.

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>Вызовите Функцию Azure в приложении на вкладке</b></summary>

Используйте библиотеку `axios`, чтобы сделать HTTP-запрос функции Azure.

```ts
const teamsfx = new TeamsFx();
const token = teamsfx.getCredential().getToken(""); // Get SSO token for the use
// Call API hosted in Azure Functions on behalf of user
const apiEndpoint = teamsfx.getConfig("apiEndpoint");
const response = await axios.default.get(apiEndpoint + "api/httptrigger1", {
  headers: {
    authorization: "Bearer " + token,
  },
});
```

</details>

<br>

<details>
<summary><b>Доступ к базе данных SQL в Функции Azure</b></summary>


Используйте библиотеку `tedious` для доступа к SQL и использования `DefaultTediousConnectionConfiguration`, который управляет проверкой подлинности.
Помимо `tedious` можно также составить подключение других библиотек SQL на основе результата `sqlConnectionConfig.getConfig()`.

```ts
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
const config2 = await getTediousConnectionConfig(teamsfx "your database name");
const connection = new Connection(config);
connection.on("connect", (error) => {
  if (error) {
    console.log(error);
  }
});
```

</details>

<br>

<details>
<summary><b>Используйте проверку подлинности с применением сертификатов в Функции Azure</b></summary>

```ts
const authConfig = {
  clientId: process.env.M365_CLIENT_ID,
  certificateContent: "The content of a PEM-encoded public/private key certificate",
  authorityHost: process.env.M365_AUTHORITY_HOST,
  tenantId: process.env.M365_TENANT_ID,
};
const teamsfx = new TeamsFx(IdentityType.App);
teamsfx.setCustomeConfig({
  certificateContent: "The content of a PEM-encoded public/private key certificate"
});
const token = teamsfx.getCredential().getToken();
```

</details>

<br>

<details>
<summary><b>Использование API Graph в приложении-боте</b></summary>

Добавьте `TeamsBotSsoPrompt` в набор диалогов.

```ts
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

</details>

<br>

## <a name="advanced-customization"></a>Дополнительная настройка

### <a name="configure-log"></a>Настройка журнала

При использовании этой библиотеки можно настроить уровень журнала клиента и перенаправить выходные данные. По умолчанию ведение журнала отключено. Вы можете включить его, настроив уровень ведения журнала.

#### <a name="enable-log-by-setting-log-level"></a>Включите журнал, установив уровень ведения журнала

Ведение журнала включено, только если установлен уровень ведения журнала. По умолчанию данные журнала печатаются на консоли.

Установите уровень журнала, используя следующий фрагмент кода:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Вы можете перенаправить выходные данные журнала, настроив пользовательский регистратор или функцию журнала.

#### <a name="redirect-by-setting-custom-logger"></a>Перенаправление путем настройки пользовательской записи журнала

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Перенаправление путем настройки пользовательской функции журнала

> [!NOTE]
> Функция журнала не будет действовать, если вы настроили пользовательский регистратор.

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

## <a name="override-configuration"></a>Переопределение конфигурации
Вы можете передать настраиваемую конфигурацию при создании экземпляра TeamsFx, чтобы переопределить конфигурацию по умолчанию или настроить необходимые поля, если отсутствуют переменные среды.

- Если вы создали проект вкладки с помощью VS Code Toolkit, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- Если вы создали проект функции или бота Azure с помощью VS Code Toolkit, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:
  * initiateLoginEndpoint (INITIATE_LOGIN_ENDPOINT)
  * authorityHost (M365_AUTHORITY_HOST)
  * tenantId (M365_TENANT_ID)
  * clientId (M365_CLIENT_ID)
  * clientSecret (M365_CLIENT_SECRET)
  * applicationIdUri (M365_APPLICATION_ID_URI)
  * apiEndpoint (API_ENDPOINT)
  * sqlServerEndpoint (SQL_ENDPOINT)
  * sqlUsername (SQL_USER_NAME)
  * sqlPassword (SQL_PASSWORD)
  * sqlDatabaseName (SQL_DATABASE_NAME)
  * sqlIdentityId (IDENTITY_ID)

## <a name="upgrade-latest-sdk-version"></a>Обновление последней версии SDK

Если вы используете версию пакета SDK с `loadConfiguration()`, вы можете обновить его до последней версии.
1. Удалите `loadConfiguration()` и передайте настроенные параметры с помощью `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Заменить `new TeamsUserCredential()` на `new TeamsFx()`
3. Заменить `new M365TenantCredential()` на `new TeamsFx(IdentityType.App)`
4. Заменить `new OnBehalfOfUserCredential(ssoToken)` на `new TeamsFx().setSsoToken(ssoToken)`
5. Передайте экземпляр `TeamsFx` вспомогательным функциям помощи для замены экземпляра учетных данных

Дополнительные сведения см. в статье [класс TeamsFx](#teamsfx-class).

## <a name="next-step"></a>Следующий этап

Проект [образцов](https://github.com/OfficeDev/TeamsFx-Samples) для подробных образцов того, как следует использовать TeamsFx SDK.

## <a name="see-also"></a>Дополнительные ресурсы

[Образец галереи Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
