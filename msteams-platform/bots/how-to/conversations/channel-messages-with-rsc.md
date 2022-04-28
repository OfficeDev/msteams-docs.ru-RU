---
title: Получение всех сообщений канала через RSC
author: surbhigupta12
description: Получение всех сообщений канала с разрешениями RSC
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: a78910b083943e5296f3e0d50eae00a713f194aa
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102076"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Получение всех сообщений канала через RSC

Модель разрешений для конкретного ресурса (RSC), изначально разработанная для Teams Graph API, распространяется на сценарии бота.

Теперь с помощью RSC вы можете запросить у владельцев команды согласие на получение ботом сообщений пользователей по стандартным каналам в команде без @mentioned. Эта возможность включена путем указания `ChannelMessage.Read.Group` разрешения в манифесте приложения, Teams RSC. После настройки владельцы команд могут предоставить согласие во время процесса установки приложения.

Дополнительные сведения о включении RSC для вашего приложения см. в разделе о согласии для конкретных ресурсов [в Teams](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest).

## <a name="enable-bots-to-receive-all-channel-messages"></a>Включение ботов для получения всех сообщений канала

Разрешение `ChannelMessage.Read.Group` RSC распространяется на ботов. С согласия пользователя это разрешение позволяет приложениям graph получать все сообщения в беседе и ботам получать все сообщения каналов без @mentioned.

> [!NOTE]
>
> * Службы, для которых требуется доступ ко всем Teams сообщений, должны использовать API-интерфейсы Graph, которые также предоставляют доступ к архивным данным в каналах и чатах.
> * Боты должны соответствующим `ChannelMessage.Read.Group` образом использовать разрешение RSC для создания и улучшения взаимодействия с пользователями в команде, в противном случае они не будут проходить утверждение магазина. Описание приложения должно включать использование ботом считывания данных.
> * Боты `ChannelMessage.Read.Group` могут не использовать разрешение RSC для извлечения больших объемов данных клиента.

## <a name="update-app-manifest"></a>Обновление манифеста приложения

Для получения ботом всех сообщений канала RSC `ChannelMessage.Read.Group` необходимо настроить в манифесте Teams с разрешением, указанным в свойстве`webApplicationInfo`.

![Обновление манифеста приложения](~/bots/how-to/conversations/Media/appmanifest.png)


Ниже приведен пример `webApplicationInfo` объекта:

* **id**: идентификатор Microsoft Azure Active Directory (Azure AD). Это может быть тот же идентификатор бота.
* **resource**: любая строка. Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ошибки.
* **applicationPermissions**: необходимо указать разрешения RSC `ChannelMessage.Read.Group` для вашего приложения. Дополнительные сведения см. [в разделе о разрешениях для конкретных ресурсов](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions).

В следующем коде приведен пример манифеста приложения:

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>Загрузка неопубликованных приложений в команде

Чтобы загрузить неопубликованную команду для проверки, должны ли все сообщения канала в команде с RSC получаться без @mentioned:

1. Выберите или создайте команду.
1. Щелкните многоточие &#x25CF;&#x25CF;&#x25CF; области слева. Появится раскрывающееся меню.
1. В **раскрывающемся меню выберите** команду "Управление". Отобразятся сведения.

   ![Управление приложениями в команде](~/bots/how-to/conversations/Media/managingteam.png)

      :::image type="content" source="Media/managingteam.png" alt-text="управление командой"border="true":::

1. Выберите **Приложения**. Появится несколько приложений.
1. Выберите **Upload пользовательское приложение в** правом нижнем углу.

      :::image type="content" source="Media/uploadingcustomapp.png" alt-text="отправка пользовательского приложения":::
  
1. Выберите пакет приложения в диалоговом окне **"** Открыть".
1. Выберите **Открыть**.

      :::image type="content" source="Media/selectapppackage.png" alt-text="Выбор пакета приложения"lightbox="Media/selectapppackage.png"border="true":::

1. Выберите **"** Добавить" во всплывающем окне сведений о приложении, чтобы добавить бота в выбранную команду.

      :::image type="content" source="Media/addingbot.png" alt-text="Добавление бота"lightbox="Media/addingbot.png"border="true":::

1. Выберите канал и введите сообщение в канале для бота.

    Бот получает сообщение, не @mentioned.

      :::image type="content" source="Media/botreceivingmessage.png" alt-text="Получение сообщения ботом"lightbox="Media/botreceivingmessage.png"border="true":::

## <a name="code-snippets"></a>Фрагменты кода

В следующем коде приведен пример разрешений RSC:

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
|Сообщения канала с разрешениями RSC| Microsoft Teams пример приложения, демонстрирующий, как бот может получать все сообщения канала с помощью RSC, не @mentioned.| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Беседы с ботами](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Согласие для определенных ресурсов](/microsoftteams/resource-specific-consent)
* [Проверка согласия для конкретного ресурса](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload пользовательского приложения в Teams](~/concepts/deploy-and-publish/apps-upload.md)
