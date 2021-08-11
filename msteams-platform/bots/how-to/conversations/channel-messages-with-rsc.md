---
title: Получение всех сообщений канала через RSC
author: surbhigupta12
description: Получение всех сообщений канала с разрешениями RSC
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 8ddbb3cd7ffa8f02caea2fb0e1e74abb9b64ffe94bb34b8a09561e744cea25b5
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705890"
---
# <a name="receive-all-channel-messages-with-rsc"></a>Получение всех сообщений канала через RSC

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../../../resources/dev-preview/developer-preview-intro.md) разработчиков.

Модель разрешений для разрешений для определенных ресурсов (RSC), изначально разработанная для Teams Graph API, теперь распространяется на сценарии ботов.

В настоящее время боты могут получать сообщения каналов пользователей только при @mentioned. Теперь с помощью RSC можно запрашивать у владельцев команд согласие на получение ботом сообщений пользователей по стандартным каналам в команде без @mentioned. Эта возможность включена, указав разрешение в манифесте включенного `ChannelMessage.Read.Group` приложения RSC Teams. После настройки владельцы команд могут предоставить согласие во время процесса установки приложения.

Дополнительные сведения о включаемом RSC для вашего [приложения](/microsoftteams/platform/graph-api/rsc/resource-specific-consent#update-your-teams-app-manifest)см. в Teams.

## <a name="enable-bots-to-receive-all-channel-messages"></a>Включить боты для получения всех сообщений канала

Разрешение `ChannelMessage.Read.Group` RSC распространяется на ботов. С согласия пользователя это разрешение позволяет приложениям графиков получать все сообщения в беседе, а боты получают все сообщения канала без @mentioned.

## <a name="update-app-manifest"></a>Манифест обновления приложения

Чтобы бот получал все сообщения канала, RSC должен быть настроен в манифесте приложения Teams с разрешения, указанного `ChannelMessage.Read.Group` в `webApplicationInfo` свойстве.

![Манифест обновления приложения](~/bots/how-to/conversations/Media/appmanifest.png)

Ниже приводится пример `webApplicationInfo` объекта:

* **id:** ID Azure Active Directory (AAD). Это может быть то же самое, что и ваш бот-ИД.
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

## <a name="sideload-in-a-team-to-test"></a>Sideload in a team to test

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

## <a name="see-also"></a>См. также

* [Беседы с ботами](/microsoftteams/platform/bots/how-to/conversations/conversation-basics)
* [Согласие для определенных ресурсов](/microsoftteams/resource-specific-consent)
* [Проверка согласия на конкретные ресурсы](/microsoftteams/platform/graph-api/rsc/test-resource-specific-consent)
* [Upload настраиваемом приложении в Teams](~/concepts/deploy-and-publish/apps-upload.md)
