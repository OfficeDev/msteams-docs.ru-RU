---
title: Пакет SDK TeamsFx
author: MuyangAmigo
description: О пакете SDK для TeamsFx
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ade31e39d48b92cca4309b16762dc95afccf1925
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073099"
---
# <a name="teamsfx-sdk"></a>Пакет SDK TeamsFx

TeamsFx помогает сократить задачи разработчика, используя единый вход Teams и доступ к облачным ресурсам до однострочного оператора с нулевой конфигурацией. Пакет SDK для TeamsFx предназначен для использования в браузере и Node.js среде, к распространенным сценариям относятся:

* Teams табуляции
* Функция Azure
* Teams бота

Пакет SDK TeamsFx можно использовать для выполнения следующих функций:

* Доступ к основным функциям в клиентской и серверной среде 
* Написание кода проверки подлинности пользователя упрощенным способом

## <a name="prerequisites"></a>Предварительные требования

Установите следующие средства и настроите среду разработки:

* Последняя версия Node.js
* Если в проекте установлены связанные `botbuilder` [пакеты в](https://github.com/Microsoft/botbuilder-js#packages) качестве зависимостей, убедитесь, что они имеют ту же версию. В настоящее время требуется версия 4.15.0 или более поздняя. Дополнительные сведения см. в статье о пакетах построителя ботов, которые должны иметь ту [же версию](https://github.com/BotBuilderCommunity/botbuilder-community-js/issues/57#issuecomment-508538548).

Вам необходимо иметь опыт работы со следующими сведениями:

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx)
* [Справочная документация по API](https://aka.ms/teamsfx-sdk-help)
* [Примеры](https://github.com/OfficeDev/TeamsFx-Samples)

## <a name="get-started"></a>Начало работы

Пакет SDK Для TeamsFx предварительно настроен в сформированном проекте с помощью TeamsFx набор средств или CLI.
Дополнительные сведения см[. в Teams проекта приложения](https://github.com/OfficeDev/TeamsFx/blob/main/packages/vscode-extension/README.md).

### <a name="install-the-microsoftteamsfx-package"></a>Установка пакета `@microsoft/teamsfx`

Установите пакет SDK TeamsFx для TypeScript или JavaScript с помощью:`npm`

```bash
npm install @microsoft/teamsfx
```

### <a name="create-microsoftgraphclient-service"></a>Создание службы `MicrosoftGraphClient`

Чтобы создать клиентский объект графа и получить доступ к microsoft API Graph, вам потребуются учетные данные для проверки подлинности. Пакет SDK предоставляет интерфейсы API для настройки для разработчиков.

<br>

<details>
<summary><b>Вызов API Graph от имени Teams пользователя (удостоверение пользователя)</b></summary>

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
<summary><b>Вызов API Graph без пользователя (удостоверение приложения)</b></summary>

Для этого не требуется взаимодействие с Teams пользователем. Вы можете вызвать Microsoft Graph как удостоверение приложения.

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

Экземпляр класса TeamsFx по умолчанию имеет доступ ко всем параметрам TeamsFx из переменных среды. Можно также задать настраиваемые значения конфигурации, чтобы переопределить значения по умолчанию. Дополнительные [сведения см. в описании конфигурации](#override-configuration) переопределения. При создании экземпляра TeamsFx необходимо также указать тип удостоверения. Существует два типа удостоверений:

* Удостоверение пользователя
* Удостоверение приложения

#### <a name="user-identity"></a>Удостоверение пользователя

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.User)`| Проверка подлинности приложения выполняется Teams пользователя. |
| `TeamsFx:setSsoToken()`| Удостоверение пользователя в Node.js среде (без браузера). |
| `TeamsFx:getUserInfo()` | Получение сведений об основах пользователя. |
| `TeamsFx:login()` | Он позволяет пользователю выполнять процесс предоставления согласия, если вы хотите использовать единый вход для получения маркера доступа для определенных областей OAuth. |

> [!NOTE]
> Доступ к ресурсам можно получить от имени текущего Teams пользователя.

#### <a name="application-identity"></a>Удостоверение приложения

| Команда | Описание |
|----------------|-------------|
| `new TeamsFx(IdentityType.App)`| Проверка подлинности приложения выполняется как приложение. Разрешение обычно требует утверждения администратора.|
| `TeamsFx:getCredential()`| Он предоставляет экземпляры учетных данных, автоматически соответствующие типу удостоверения. |

> [!NOTE]
> Для ресурсов требуется согласие администратора.

### <a name="credential"></a>Credential

При инициализации TeamsFx необходимо выбрать тип удостоверения. После того как вы указали тип удостоверения при инициализации TeamsFx, пакет SDK использует различные типы класса учетных данных для представления удостоверения и получения маркера доступа с помощью соответствующего потока проверки подлинности.

Существует три класса учетных данных для упрощения проверки подлинности. [папка учетных данных](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/credential). Классы учетных данных реализуют `TokenCredential` интерфейс, который широко используется в API библиотек Azure, предназначенный для предоставления маркеров доступа для определенных областей. Другие API-интерфейсы использует вызов учетных данных `TeamsFx:getCredential()` для получения экземпляра `TokenCredential`.

Ниже приведены соответствующие сценарии для каждого целевого класса учетных данных.

#### <a name="user-identity-in-browser-environment"></a>Удостоверение пользователя в среде браузера
`TeamsUserCredential`представляет Teams удостоверения текущего пользователя. При использовании этого учетного данных пользователь будет запрашивать согласие в первый раз. Он использует Teams единый вход и поток On-Behalf-Of для обмена маркерами. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение пользователя в среде браузера.

Требуемая конфигурация: `initiateLoginEndpoint`, `clientId`.

#### <a name="user-identity-in-nodejs-environment"></a>Удостоверение пользователя в Node.js среде
`OnBehalfOfUserCredential`использует поток On-Behalf-Of и требуется Teams единого входа. Он предназначен для использования в сценариях функции Или бота Azure. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение пользователя в Node.js среде.

Требуемая конфигурация: `authorityHost`, `tenantId`, или `clientId``clientSecret` `certificateContent`.

#### <a name="application-identity-in-nodejs-environment"></a>Удостоверение приложения в Node.js среде
`AppCredential` представляет удостоверение приложения. Обычно он используется, когда пользователь не участвует, как задание автоматизации, активируемого по времени. Пакет SDK использует эти учетные данные, когда разработчик выбирает удостоверение приложения в Node.js среде.

Требуемая конфигурация: `tenantId`или `certificateContent``clientId``clientSecret` .

### <a name="bot-sso"></a>Единый вход в Bot

Классы, связанные с ботом, хранятся в [папке бота](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/bot).

`TeamsBotSsoPrompt` имеет хорошую интеграцию с bot framework. Он упрощает процесс проверки подлинности при разработке приложения бота и хочет использовать единый вход бота.

Требуемая конфигурация: `initiateLoginEndpoint`, `tenantId`, и `clientId``applicationIdUri`.

### <a name="supported-functions"></a>Поддерживаемые функции

Пакет SDK для TeamsFx предоставляет несколько функций для упрощения настройки сторонних библиотек. Они находятся в основной [папке](https://github.com/OfficeDev/TeamsFx/tree/main/packages/sdk/src/core).

*  Microsoft Graph Service:`createMicrosoftGraphClient` и `MsGraphAuthProvider` помощь в создании аутентифицированного Graph экземпляра.
*  SQL:`getTediousConnectionConfig` возвращает утомительную конфигурацию подключения.

Требуемая конфигурация:
* `sqlServerEndpoint`, `sqlUsername`если `sqlPassword` вы хотите использовать удостоверение пользователя
* `sqlServerEndpoint`, `sqlIdentityId` если вы хотите использовать удостоверение MSI

### <a name="error-handling"></a>Обработка ошибок

Ответ об ошибке API— `ErrorWithCode`содержит код ошибки и сообщение об ошибке. Например, чтобы отфильтровать конкретную ошибку, можно использовать следующий фрагмент кода:

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

Если экземпляр учетных данных используется в других библиотеках, таких как Microsoft Graph, возможно, ошибка перехватывается и преобразуется.

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

В следующем разделе приведено несколько фрагментов кода для распространенных сценариев.

<br>

<details>
<summary><b>Использование API Graph в приложении табуляции</b></summary>
 
Использование `TeamsFx` и `createMicrosoftGraphClient`.

```ts
const teamsfx = new TeamsFx();
const graphClient = createMicrosoftGraphClient(teamsfx, ["User.Read"]);
const profile = await graphClient.api("/me").get();
```

</details>

<br>

<details>
<summary><b>Вызов функции Azure в приложении табуляции</b></summary>

Используйте `axios` библиотеку для выполнения HTTP-запроса к функции Azure.

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
<summary><b>Доступ SQL базы данных в Функции Azure</b></summary>


Используйте `tedious` библиотеку для доступа к SQL и использования`DefaultTediousConnectionConfiguration`, который управляет проверкой подлинности.
Кроме того`tedious`, можно создать конфигурацию подключения других библиотек SQL на основе результатов`sqlConnectionConfig.getConfig()`.

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
<summary><b>Использование проверки подлинности на основе сертификатов в функции Azure</b></summary>

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
<summary><b>Использование API Graph в приложении бота</b></summary>

Добавить `TeamsBotSsoPrompt` в набор диалогов.

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

## <a name="advanced-customization"></a>Расширенная настройка

### <a name="configure-log"></a>Настройка журнала

Вы можете задать уровень журнала клиента и перенаправить выходные данные при использовании этой библиотеки. Ведение журнала по умолчанию отключено. Его можно включить, заданный уровень журнала.

#### <a name="enable-log-by-setting-log-level"></a>Включение журнала путем настройки уровня журнала

Ведение журнала включено только при установке уровня журнала. По умолчанию он выводит сведения журнала в консоль.

Задайте уровень журнала, используя следующий фрагмент кода:

```ts
// Only need the warning and error messages.
setLogLevel(LogLevel.Warn);
```

Вы можете перенаправить выходные данные журнала, направив настраиваемое средство ведения журнала или функцию журнала.

#### <a name="redirect-by-setting-custom-logger"></a>Перенаправление путем настройки пользовательского средства ведения журнала

```ts
setLogLevel(LogLevel.Info);
// Set another logger if you want to redirect to Application Insights in Azure Function
setLogger(context.log);
```

#### <a name="redirect-by-setting-custom-log-function"></a>Перенаправление путем настройки пользовательской функции журнала

> [!NOTE]
> Функция log не будет действовать, если вы настроите пользовательское средство ведения журнала.

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
Пользовательскую конфигурацию можно передать при создании экземпляра TeamsFx, чтобы переопределить конфигурацию по умолчанию или задать обязательные поля при отсутствии переменных среды.

- Если вы создали проект вкладки с VS Code набор средств, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:
  * authorityHost (REACT_APP_AUTHORITY_HOST)
  * tenantId (REACT_APP_TENANT_ID)
  * clientId (REACT_APP_CLIENT_ID)
  * initiateLoginEndpoint (REACT_APP_START_LOGIN_PAGE_URL)
  * applicationIdUri (REACT_APP_START_LOGIN_PAGE_URL)
  * apiEndpoint (REACT_APP_FUNC_ENDPOINT)
  * apiName (REACT_APP_FUNC_NAME)

- Если вы создали проект функции Или бота Azure с помощью VS Code набор средств, из предварительно настроенных переменных среды будут использоваться следующие значения конфигурации:
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

## <a name="upgrade-latest-sdk-version"></a>Обновление последней версии пакета SDK

Если вы используете версию пакета SDK `loadConfiguration()`, выполните следующие действия, чтобы обновить пакет SDK до последней версии.
1. Удаление `loadConfiguration()` и передача настроенных параметров с помощью `new TeamsFx(IdentityType.User, { ...customConfig })`
2. Заменить на `new TeamsUserCredential()``new TeamsFx()`
3. Заменить на `new M365TenantCredential()``new TeamsFx(IdentityType.App)`
4. Заменить на `new OnBehalfOfUserCredential(ssoToken)``new TeamsFx().setSsoToken(ssoToken)`
5. Передача экземпляра вспомогательных `TeamsFx` функций для замены экземпляра учетных данных

Дополнительные сведения см. в [описании класса TeamsFx](#teamsfx-class).

## <a name="next-step"></a>Следующий этап

[Примеры проекта](https://github.com/OfficeDev/TeamsFx-Samples) для подробных примеров использования пакета SDK для TeamsFx.

## <a name="see-also"></a>См. также

[Пример коллекции Microsoft TeamsFx](https://github.com/OfficeDev/TeamsFx-Samples).
