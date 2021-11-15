---
title: Получение всех сообщений канала через RSC
author: surbhigupta12
description: Получение всех сообщений канала с разрешениями RSC
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 6c509475a94d7f161dd6fb26c46ecb669c4059a1
ms.sourcegitcommit: f77750f2e60f63d1e2f66a96c169119683c66950
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/15/2021
ms.locfileid: "60960231"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Получение всех сообщений канала через RSC

Модель разрешений для разрешений для конкретного ресурса (RSC), изначально разработанная для Teams Graph API, распространяется на сценарии ботов.

Теперь с помощью RSC можно запрашивать у владельцев команд согласие на получение ботом сообщений пользователей по стандартным каналам в команде без @mentioned. Эта возможность включена, указав разрешение в манифесте включенного `ChannelMessage.Read.Group` приложения RSC Teams. После настройки владельцы команд могут предоставить согласие во время процесса установки приложения.

Дополнительные сведения о включаемом RSC для вашего [приложения](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)см. в Teams.

## <a name="enable-bots-to-receive-all-channel-messages"></a>Включить боты для получения всех сообщений канала

Разрешение `ChannelMessage.Read.Group` RSC распространяется на ботов. С согласия пользователя это разрешение позволяет приложениям графиков получать все сообщения в беседе, а боты получают все сообщения канала без @mentioned.

> [!NOTE]
> * Службы, которые нуждаются в доступе ко всем Teams данным сообщений, должны использовать API Graph, которые также предоставляют доступ к архивным данным в каналах и чатах.
> * Боты должны использовать разрешение RSC надлежащим образом для создания и улучшения взаимодействия пользователей в команде, иначе они не будут `ChannelMessage.Read.Group` проходить утверждение магазина. Описание приложения должно включать использование ботом считыванных данных.
> * Разрешение RSC не может использоваться ботами для извлечения больших `ChannelMessage.Read.Group` объемов данных клиентов. 

## <a name="update-app-manifest"></a>Манифест обновления приложения

Чтобы бот получал все сообщения канала, RSC должен быть настроен в манифесте приложения Teams с разрешения, указанного `ChannelMessage.Read.Group` в `webApplicationInfo` свойстве.
![Манифест обновления приложения](~/bots/how-to/conversations/Media/appmanifest.png)

Ниже приводится пример `webApplicationInfo` объекта:

* **id:** ID Azure Active Directory (AAD) приложения. Это может быть то же самое, что и ваш бот-ИД.
* **ресурс.** Любая строка. Это поле не имеет операции в RSC, но должно быть добавлено и иметь значение, чтобы избежать ответа на ошибки.
* **applicationPermissions:** разрешения RSC для вашего приложения с `ChannelMessage.Read.Group` должны быть указаны. Дополнительные сведения см. [в ресурсных разрешениях.](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#resource-specific-permissions)

В следующем коде приводится пример манифеста приложения:

```json
"webApplicationInfo": {
"id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
"resource": "https://AnyString",
"applicationPermissions": [
"ChannelMessage.Read.Group"
    ]
  }
```

## <a name="sideload-in-a-team"></a>Боковая нагрузка в команде

Чтобы проверить, получаются ли все сообщения канала в команде с RSC без @mentioned:

1. Выберите или создайте команду.
1. Выберите эллипсы &#x25CF;&#x25CF;&#x25CF; левой области. Отображается выпадаемое меню.
1. Выберите **команду Manage** из выпадаемого меню. Сведения отображаются.

   ![Управление приложениями в команде](~/bots/how-to/conversations/Media/managingteam.png)

1. Выберите **Приложения**. Отображаются несколько приложений.
1. Выберите **Upload настраиваемого приложения из** нижнего правого угла.

    ![Загрузка настраиваемой приложения](~/bots/how-to/conversations/Media/uploadingcustomapp.png)

1. Выберите пакет приложения из **открытого** диалоговое окно.
1. Выберите **Открыть**.

    ![Выбор пакета приложений](~/bots/how-to/conversations/Media/selectapppackage.png)

1. Выберите **Добавить** из всплывающее всплывающее приложение сведений о приложении, чтобы добавить бот в выбранную команду.

    ![Добавление бота](~/bots/how-to/conversations/Media/addingbot.png)

1. Выберите канал и введите сообщение в канале для бота.

    Бот получает сообщение, не будучи @mentioned.

    ![Бот получает сообщение](~/bots/how-to/conversations/Media/botreceivingmessage.png)

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C # |Node.js|
|-------------|-------------|------|----|
|Сообщения канала с разрешениями RSC| Microsoft Teams пример приложения, демонстрирующее, как бот может получать все сообщения канала с RSC без @mentioned.|  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/csharp) |    [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-receive-channel-messages-withRSC/nodejs) |

## <a name="see-also"></a>Дополнительные ресурсы

* [Беседы с ботами](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Согласие для определенных ресурсов](/microsoftteams/resource-specific-consent)
* [Проверка согласия на конкретные ресурсы](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload настраиваемом приложении в Teams](~/concepts/deploy-and-publish/apps-upload.md)
