---
title: Получение всех сообщений канала через RSC
author: surbhigupta12
description: Разрешите ботам получать все сообщения канала без @mentioned с помощью разрешений RSC. Чтение в разделе webApplicationInfo или авторизации в манифесте.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: bd740c999139d9b5f98c10800646501dd55e87f5
ms.sourcegitcommit: 217025a61ed9c3b76b507fe95563142abc6d0318
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/17/2022
ms.locfileid: "67363468"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Получение всех сообщений канала через RSC

Модель разрешений для конкретного ресурса (RSC), изначально разработанная для API Graph Teams, распространяется на сценарии бота.

Теперь с помощью RSC вы можете запрашивать у владельцев команд согласие на получение ботом сообщений пользователей в стандартных каналах команды без @упоминания. Эта возможность включается путем указания разрешения `ChannelMessage.Read.Group` в манифесте приложения Teams с поддержкой RSC. После настройки владельцы команд могут предоставлять согласие во время установки приложения.

Дополнительные сведения о включении RSC для вашего приложения см. в разделе [о согласии для конкретных ресурсов в Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Включение ботов для получения всех сообщений каналов

Разрешение RSC `ChannelMessage.Read.Group` распространяется на ботов. С согласия пользователя это разрешение позволяет приложениям Graph получать все сообщения в беседе, а ботам — получать все сообщения каналов без @упоминания.

> [!NOTE]
>
> * Службы, которым требуется доступ ко всем данным сообщений Teams, должны использовать API-интерфейсы Graph, также предоставляющие доступ к архивным данным в каналах и чатах.
> * Боты должны соответствующим образом использовать разрешение RSC `ChannelMessage.Read.Group` для создания и расширения взаимодействия с пользователями в команде. В противном случае они не пройдут утверждение магазина. Описание приложения должно включать способ использования ботом считываемых данных.
> * Боты могут не использовать разрешение RSC `ChannelMessage.Read.Group` для извлечения больших объемов данных клиента.

## <a name="update-app-manifest"></a>Обновление манифеста приложения

Чтобы ваш бот получал все сообщения каналов, RSC должно быть настроено в манифесте приложения Teams с разрешением `ChannelMessage.Read.Group`, указанным в свойстве `webApplicationInfo`.

:::image type="content" source="~/bots/how-to/conversations/Media/appmanifest.png" alt-text="Снимок экрана: обновление манифеста приложения.":::

Ниже приведен пример объекта `webApplicationInfo`.

* **id**: идентификатор вашего приложения Microsoft Azure Active Directory (Azure AD). Может совпадать с идентификатором вашего бота.
* **resource**: любая строка. Это поле не используется в RSC, но должно быть добавлено и иметь значение, чтобы избежать отклика с ошибкой.
* **applicationPermissions**: необходимо указать разрешения RSC для вашего приложения с `ChannelMessage.Read.Group`. Дополнительные сведения см. в разделе [Разрешения для определенных ресурсов](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

В следующем коде приведен пример манифеста приложения.

```json
"webApplicationInfo": {
  "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
  "resource": "https://AnyString",
  "applicationPermissions": [
    "ChannelMessage.Read.Group"
  ]
}
```

## <a name="sideload-in-a-team"></a>Загрузка без публикации в команде

Чтобы выполнить загрузку без публикации в команде для тестирования того, удается ли получить все сообщения каналов в команде с RSC без @упоминания:

1. Выберите или создайте команду.
1. Щелкните многоточие &#x25CF;&#x25CF;&#x25CF; в области слева. Появится раскрывающееся меню.
1. Выберите **Управление командой** в раскрывающемся меню. Отобразятся сведения.

   :::image type="content" source="Media/managingteam.png" alt-text="Снимок экрана: параметр &quot;Управление командой&quot; в приложении Teams.":::

1. Выберите **Приложения**. Появится несколько приложений.

1. Выберите **Отправить пользовательское приложение** в правом нижнем углу.

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="Снимок экрана: отправка параметра пользовательского приложения.":::
  
1. Выберите пакет приложения в диалоговом окне **Открыть**.

1. Выберите **Открыть**.

      :::image type="content" source="Media/selectapppackage.png" alt-text="Снимок экрана: открытое диалоговое окно для выбора пакета приложения." lightbox="Media/selectapppackage.png":::

1. Нажмите **Добавить** во всплывающем окне со сведениями о приложении, чтобы добавить бота в выбранную команду.

      :::image type="content" source="Media/addingbot.png" alt-text="Снимок экрана: кнопка &quot;Добавить&quot; для добавления бота в команду." lightbox="Media/addingbot.png":::

1. Выберите канал и введите сообщение в канале для своего бота.

    Бот получает сообщение без @упоминания.

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="Снимок экрана: бот, получающий сообщение в канале." lightbox="Media/botreceivingmessage.png":::

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приведен пример разрешений RSC.

# <a name="c"></a>[C#](#tab/dotnet)

```csharp

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text("Using RSC the bot can recieve messages across channels in team without being @mentioned."));
}
```

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Handle when a message is addressed to the bot. 
// When rsc is enabled the method will be called even when bot is addressed without being @mentioned
this.onMessage(async (context, next) => {
   await context.sendActivity(MessageFactory.text("Using RSC the bot can recieve messages across channles in team without being @mentioned."))
   await next();
});
```

---

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Сообщения каналов с разрешениями RSC| Пример приложения Microsoft Teams, демонстрирующий, как бот может получать все сообщения каналов с RSC без @упоминания.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Беседы с ботами](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Согласие для определенных ресурсов](/microsoftteams/resource-specific-consent)
* [Проверка согласия для конкретных ресурсов](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Отправка пользовательского приложения в Teams](~/concepts/deploy-and-publish/apps-upload.md)
* [Вывод списка ответов на сообщения в канале](/graph/api/chatmessage-list-replies?view=graph-rest-1.0&tabs=http&preserve-view=true)
