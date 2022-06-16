---
title: Поддержка единого входа для ботов
description: В статье объясняется, как получить маркер пользователя. В настоящее время разработчик бота может использовать карточку входа или службу бота Azure с поддержкой OAuth.
keywords: токен, маркер пользователя, поддержка единого входа для ботов, разрешение, Microsoft Graph, Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: c10fe639417ad71814b060ba70e6a33c4ae4038f
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123470"
---
# <a name="single-sign-on-sso-support-for-bots"></a>Поддержка единого входа для ботов

Проверка подлинности единого входа в Microsoft Azure Active Directory (Azure AD) автоматически обновляет маркер проверки подлинности, чтобы свести к минимуму количество раз, когда пользователям необходимо вводить учетные данные для входа. Если пользователь соглашается использовать ваше приложение, ему не придется повторно давать согласие на другом устройстве, поскольку вход будет выполнен автоматически. Вкладки и боты имеют аналогичный поток для поддержки единого входа. Но бот [запрашивает маркеры](#request-a-bot-token) [и получает ответы](#receive-the-bot-token) по другому протоколу.

>[!NOTE]
> OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Для работы с проверкой подлинности в Microsoft Teams. необходимо базовое понимание механизма OAuth 2.0.

## <a name="bot-sso-at-runtime"></a>Единый вход для ботов во время выполнения

На следующем рисунке показан поток единого входа для ботов.

![Схема единого входа для ботов во время выполнения](../../../assets/images/bots/bots-sso-diagram.png)

Перечисленные ниже шаги помогут вам выполнить аутентификацию и работать с маркерами приложений бота.

1. Бот отправляет сообщение в Teams с OAuthCard, которая содержит `tokenExchangeResource` для получения маркера проверки подлинности для приложения бота. Пользователь получает сообщения во всех активных конечных точках пользователя.

   > [!NOTE]
   >
   > * Пользователь может иметь несколько активных конечных точек одновременно.
   > * Маркер бота получается от каждой активной конечной точки пользователя.
   > * Приложение должно быть установлено в личной области для поддержки единого входа.

1. Если данный пользователь впервые использует ваше приложение бота, система выведет запрос, предлагающий пользователю выполнить одно из следующих действий:
    * При необходимости предоставить согласие.
    * Обработать пошаговую проверки подлинности, например двухфакторную проверку подлинности.

1. Microsoft Teams запрашивает маркер приложения бота из конечной точки Azure AD для данного пользователя.

1. Azure AD отправляет маркер приложения бота в приложение Microsoft Teams.

1. Microsoft Teams отправляет маркер боту как часть объекта значения, возвращаемого вызовом с помощью **sign in/tokenExchange**.
  
1. Анализируемый токен в приложении бота предоставляет необходимые сведения, например адрес электронной почты пользователя.
  
## <a name="develop-an-sso-teams-bot"></a>Разработка бота Microsoft Teams с единым входом
  
Далее перечислены шаги для разработки бота Microsoft Teams с единым входом.

1. [Зарегистрируйте приложение через портал Azure AD](#register-your-app-through-the-azure-ad-portal)
1. [Обновите манифест приложения Teams для бота](#update-your-teams-application-manifest-for-your-bot).
1. [Добавьте программный код для запроса и получения маркера бота](#add-the-code-to-request-and-receive-a-bot-token).

### <a name="register-your-app-through-the-azure-ad-portal"></a>Зарегистрируйте приложение через портал Azure AD

Действия по регистрации приложения на портале Azure AD аналогичны [потоку единого входа для вкладки](../../../tabs/how-to/authentication/tab-sso-overview.md). Ниже приведены инструкции по регистрации приложения.

1. Зарегистрируйте новое приложение на [портале регистрации Microsoft Azure Active Directory (Azure AD)](https://go.microsoft.com/fwlink/?linkid=2083908).

1. Выберите **Новая регистрация**. Появится страница **Регистрация приложения**.

    ![Новая регистрация](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. На странице **Регистрация приложения** выполните следующие действия.

   > [!NOTE]
   >
   > У пользователей не запрашивают согласие, а сразу же предоставляют маркеры доступа, если приложение Azure AD зарегистрировано в том же клиенте, где был отправлен запрос на проверку подлинности в Teams. Однако если Azure AD зарегистрировано в другом клиенте, пользователи должны предоставить согласие на разрешения.

    * Введите **Название** приложения.
    * Выберите **поддерживаемые типы учетных записей**, например один клиент или многоклиентность.
    * Нажмите **Зарегистрировать**.

    ![Регистрация приложения](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. Перейдите на страницу обзора.
1. Скопируйте значение **идентификатора приложения (клиента)**.
1. В разделе **Управление** выберите **Предоставление API**.

   > [!TIP]
   > Чтобы позже изменить манифест приложения, сохраните значение **идентификатора приложения (клиента)**.

   > [!IMPORTANT]
   >
   > * Если вы создаете автономный бот, введите URI идентификатора приложения в качестве `api://botid-{YourBotId}`. Здесь *YourBotId* — это ИД приложения Azure AD.
   > * Если вы создаете приложение с ботом и вкладкой, введите URI идентификатора приложения в качестве `api://fully-qualified-domain-name.com/botid-{YourBotId}`.

1. Нажмите **Добавить область**.
1. В открывшейся панели введите `access_as_user` в качестве параметра **Имя области**.

   >[!NOTE]
   > Область "access_as_user", используемая для добавления клиентского приложения, предназначена для группы пользователей "Администраторы и пользователи".
   >
   > Необходимо учитывать следующие важные ограничения:
   >
   > * Поддерживаются только разрешения Microsoft API Graph уровня пользователя, такие как электронная почта, профиль, offline_access и OpenId. Если вам нужен доступ к другим областям microsoft Graph, `User.Read` `Mail.Read`таким как или, см. раздел "Расширение приложения табуляции с помощью [microsoft Graph и области.](../../../tabs/how-to/authentication/tab-sso-graph-api.md)
   > * Важно, чтобы доменное имя приложения совпадало с доменным именем, зарегистрированным вами для приложения Azure AD.
   > * В настоящее время множественность доменов для приложения не поддерживается.
   > * Приложения, использующие домен `azurewebsites.net`, не поддерживаются, так как они являются общими и могут быть угрозой безопасности.

1. В поле **Кто может давать согласие?** укажите **Администраторы и пользователи**.
1. Введите следующие данные для настройки запроса согласия у администраторов и пользователей со значениями, подходящими для области `access_as_user`.
    * **Отображаемое имя согласия администратора:** Teams может получить доступ к профилю пользователя.
    * **Описание согласия администратора**: Teams может вызывать веб-API приложения в качестве текущего пользователя.
    * **Название согласия пользователя**: Teams может получать доступ к вашему профилю и делать запросы от вашего имени.
    * **Описание согласия пользователя:** Teams может вызывать API этого приложения с вашими правами.

    ![администратор и пользователи](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. Убедитесь, что параметру состояния присвоено значение **Включено**.

    ![Состояние](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. Выберите **Добавить область**, чтобы сохранить сведения. Видимая пользователю доменная часть параметра **Имя области** должна автоматически соответствовать URI **идентификатора приложения**, заданному на предыдущем шаге, с добавлением `/access_as_user` в конце`api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.

1. В разделе **Авторизованные клиентские приложения** укажите приложения, которые необходимо авторизовать для веб-приложения вашего приложения.
1. Выберите **Добавить клиентское приложение**.

    ![Клиентское приложение](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. Введите каждый из следующих идентификаторов клиента и выберите авторизованную область, созданную на предыдущем шаге.
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` для мобильного или настольного приложения Teams.
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` для веб-приложения Teams.

    ![Идентификатор клиента](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. Перейдите к **проверке подлинности**.
1. В разделе **Конфигурации платформы** выберите **Добавить платформу**.

    ![платформа](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. Выберите платформу **Веб**.

    ![Настройка платформы](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. Введите **URI перенаправления** для приложения.

   >[!NOTE]
   > Этот URI должен быть полностью квалифицированным доменным именем. За ним также следует маршрут API, на который отправляется ответ проверки подлинности. Если вы следуете любому из примеров Teams, URI будет `https://token.botframework.com/.auth/web/redirect`. Дополнительные сведения см. в статье [Поток кода авторизации OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

    ![URI перенаправления](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. Чтобы включить неявное предоставление прав, выполните следующие действия.
    * Выберите **Приложения** на панели слева.
    * Установите флажки **Маркеры доступа** и **Маркеры идентификаторов**.

    ![Поток предоставления](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)

    * Нажмите кнопку **Сохранить**, чтобы сохранить изменения.

1. Добавьте необходимые **разрешения API**.
    * Выберите **разрешения API** на панели слева.
    * Выберите **Добавить платформу**, чтобы добавить все разрешения, необходимые приложению для подчиненных API, например User.Read.

#### <a name="update-manifest-in-microsoft-azure-portal"></a>Обновление манифеста на портале Microsoft Azure

Ниже приведены инструкции по обновлению манифеста бота на портале Azure.

1. Выберите **Манифест** на панели слева.
1. Убедитесь, что для элемента конфигурации задано значение **"accessTokenAcceptedVersion": 2**. Если задано иное значение, измените его на **2**.

    ![Изменение манифеста](~/assets/images/bots/update-manifest.png)

   >[!NOTE]
   > Если вы уже тестируете бот в Teams, вам необходимо выйти из этого приложения и из Teams. Затем войдите еще раз, чтобы увидеть это изменение.

1. Нажмите кнопку **Сохранить**.

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>Обновление портала Azure с помощью подключения OAuth.

Ниже приведены инструкции по обновлению портала Azure с подключением OAuth.

1. На портале Azure перейдите в раздел [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. Перейдите в раздел **Конфигурация** на панели слева.
1. Нажмите кнопку **Добавить параметры подключения OAuth** на экране Конфигурация.

    ![Параметр конфигурации](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. Ниже приведены инструкции по заполнению формы **Новый параметр подключения**:

   >[!NOTE]
   > В приложении Azure AD может потребоваться **неявное предоставление**.

    * Введите **Имя** на странице **Новый параметр подключения**.

    >[!NOTE]
    > **Имя** относится к параметрам кода службы бота на *шаге 5* [Единый вход для ботов во время выполнения](#bot-sso-at-runtime).

    * В раскрывающемся списке **Поставщик услуг** выберите **Azure Active Directory версии 2**.
    * Введите учетные данные клиента, такие как **идентификатор клиента** и **секрет клиента** для приложения Azure AD.
    * Для **URL-адреса обмена маркерами** используйте значение области, определенное на шаге [Изменение манифеста приложения Teams для бота](#update-your-teams-application-manifest-for-your-bot), например `api://botid-<your-app-id>/`. URL-адрес обмена маркерами указывает пакету SDK, что приложение Azure AD настроено для единого входа.
    * В поле **идентификатор клиента** укажите *общий*.
    * Добавьте все **области**, настроенные при указании разрешений для подчиненных API для приложения Azure AD. При указании идентификатора клиента и секрета клиента хранилище маркеров обменивает маркер на маркер графа с определенными разрешениями.
    * Нажмите кнопку **Сохранить**.
    * Нажмите **Применить**.

    ![Параметр подключения](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>Изменение манифеста приложения Teams для бота

Если приложение содержит автономный бот, используйте следующий фрагмент кода, чтобы добавить новые свойства в манифест приложения Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```

Если приложение содержит бот и вкладку, используйте следующий фрагмент кода, чтобы добавить новые свойства в манифест приложения Teams:

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**WebApplicationInfo** — родительский элемент для указанных ниже элементов.

* **id** — это идентификатор клиента приложения. Это идентификатор приложения, полученный при регистрации приложения в Azure AD. Не делитесь этим идентификатором приложения с несколькими приложениями Teams. Создайте новое приложение Azure AD для каждого манифеста приложения, использующего `webApplicationInfo`.
* **resource** — домен и поддомен вашего приложения. Это тот же универсальный код ресурса (URI), включающего протокол `api://`, зарегистрированный при создании `scope` на шаге [Регистрация на портале Azure AD](#register-your-app-through-the-azure-ad-portal). Не следует включать в ресурс путь к `access_as_user`. Доменная часть этого URI должна соответствовать домену и поддоменам, использованным в URL-адресах манифеста приложения Teams.

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>Добавление кода для запроса и получения маркера бота

#### <a name="request-a-bot-token"></a>Запрос маркера бота

Запрос на получение маркера доступа - это обычный запрос сообщения HTTP POST с использованием существующей схемы сообщений. Она включена во вложения OAuthCard. Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и аналогична карточке входа. Microsoft Teams обрабатывает запрос как автоматическое получение маркера, если свойство `TokenExchangeResource` на карточке заполнено. Для каналов Microsoft Teams учитывается только свойство `Id`, однозначно определяющее запрос маркера.

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` или `MultiProviderAuthDialog` поддерживает проверку подлинности для единого входа.

Если пользователь использует приложение в первый раз и требуется его согласие, будет выведено следующее диалоговое окно для получения согласия на продолжение работы:

![Диалоговое окно "Согласие"](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

Когда пользователь выбирает **Продолжить**, происходят следующие события:

* Если бот определяет кнопку входа, поток входа для ботов запускается аналогично потоку входа с помощью кнопки карточки OAuth в потоке сообщений. Разработчик должен решить, какие разрешения требуют согласия пользователя. Этот подход рекомендуется, если требуется маркер с разрешениями выше `openId`. Например, если требуется обменять маркер на ресурсы Microsoft Graph.

* Если бот не предоставляет кнопку входа на карточке OAuth, для получения минимального набора разрешений требуется согласие пользователя. Этот маркер полезен для обычной проверки подлинности и получения адреса электронной почты пользователя.

##### <a name="c-token-request-without-a-sign-in-button"></a>Запрос маркера C# без кнопки входа

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a>Получение маркера бота

Ответ с маркером отправляется с помощью действия вызова по той же схеме, что и другие действия вызова, получаемые ботами сегодня. Единственным отличием является имя вызова, **sign in/tokenExchange** и поле **значение**. Поле **значение** содержит **идентификатор,** строку исходного запроса на получение маркера и поле **маркер**, строковое значение, содержащее маркер.

>[!NOTE]
> Вы можете получить несколько ответов на заданный запрос, если у пользователя есть несколько активных конечных точек. Необходимо выполнить дедупликацию ответов с помощью маркера.

##### <a name="c-code-to-handle-the-invoke-activity"></a>Код C# для обработки действия вызова

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

`turnContext.activity.value` имеет тип [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который может дополнительно использоваться ботом. Маркеры необходимо хранить для оптимизации производительности и обновлять.

### <a name="token-exchange-failure"></a>Сбой обмена маркерами

Если при обмене маркерами возникла ошибка, используйте следующий код:

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

Чтобы понять, что делает бот, если при обмене маркерами не удается активировать запрос согласия, выполните следующие действия.

>[!NOTE]
> Действия пользователя не требуются, так как бот выполняет нужные действия при сбое обмена маркерами.

1. Клиент начинает беседу с ботом, запуская сценарий OAuth.
2. Бот в ответ отправляет клиенту карточку OAuth.
3. Клиент перехватывает карточку OAuth до ее показа пользователю и проверяет, содержит ли она свойство `TokenExchangeResource`.
4. Если свойство существует, клиент отправляет боту `TokenExchangeInvokeRequest`. На клиенте должен быть подлежащий обмену токен для пользователя, который должен быть маркером Azure AD версии 2 и аудитория которого должна совпадать со свойством `TokenExchangeResource.Uri`. Клиент отправляет боту действие вызова со следующим кодом:

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. Бот обрабатывает `TokenExchangeInvokeRequest` и возвращает `TokenExchangeInvokeResponse` клиенту. Клиент должен подождать, пока не получит `TokenExchangeInvokeResponse`.

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. Если у `TokenExchangeInvokeResponse` есть `status` со значением `200`, то клиент не показывает карточку OAuth. См. [схему нормального потока](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Для любого другого `status` или если объект `TokenExchangeInvokeResponse` не получен, клиент показывает пользователю карточку OAuth. См [схему потока при отработке сбоя](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true). Если возникли ошибки или какие-либо зависимости, такие как согласие пользователя, отсутствуют, это действие гарантирует, что поток единого входа переключится на обычный поток OAuthCard.

### <a name="update-the-auth-sample"></a>Изменение примера проверки подлинности

Откройте [пример проверки подлинности Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) и измените его описанным далее образом.

1. Измените TeamsBot так, чтобы он проводил дедупликацию входящего запроса, для чего вставьте следующий код:

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. Измените `appsettings.json`, чтобы включить `botId`, пароль и имя подключения, определенные на шаге [Обновление портала Azure с подключением OAuth](#update-the-azure-portal-with-the-oauth-connection).
3. Обновите манифест и убедитесь, что `token.botframework.com` находится в списке допустимых доменов. Дополнительные сведения см. в [ примере проверки подлинности в Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).
4. Запакуйте манифест с помощью образов профилей и установите его в Teams.

## <a name="code-sample"></a>Пример кода

|**Название примера** | **Описание** |**.NET** |**C#** |**Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
|Bot Framework SDK | В этом примере кода показано, как приступить к проверке подлинности в боте для Microsoft Teams. |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|[Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/csharp_dotnetcore/BotConversationSsoQuickstart)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-conversation-sso-quickstart/js)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Выполните [пошаговое руководство](../../../sbs-bots-with-sso.yml), чтобы создать бот с проверкой подлинности единого входа.
