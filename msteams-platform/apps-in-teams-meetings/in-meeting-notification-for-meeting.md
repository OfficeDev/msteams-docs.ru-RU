---
title: Создание уведомления о собрании для собрания Teams
author: v-sdhakshina
description: Из этой статьи вы узнаете, как создать уведомление о собрании для собрания Microsoft Teams и его пример кода.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: e62958535fa1bcbcdeb104b5fd5fdd2882250aa3
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699131"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>Создание уведомления о собрании для собрания Teams

Уведомление на собрании используется для привлечения участников и сбора информации или отзывов во время собрания. Используйте [полезные данные уведомления на собрании](meeting-apps-apis.md#send-an-in-meeting-notification), чтобы активировать уведомление на собрании. В рамках запроса полезных данных уведомления включите URL-адрес, по которому размещается отображаемое содержимое.

Для отображения уведомления на собрании используется URL-адрес внешнего ресурса. Вы можете использовать метод `submitTask` для отправки данных в чате собрания.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="На снимке экрана показан пример использования диалогового окна собрания.":::

Также можно добавить отображаемое изображение Teams и карточку пользователя в уведомление собрания на основе маркера `onBehalfOf`, при этом MRI пользователя и отображаемое имя передаются в полезных данных. Ниже приведен пример полезных данных:

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="На этом снимке экрана показано, как Teams отображает изображение и карточку людей с диалоговым окном в собрании." border="true":::

## <a name="code-sample"></a>Пример кода

Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Уведомление на собрании | Демонстрирует реализацию уведомлений на собрании с помощью бота. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте инструкциям из [пошагового руководства](../sbs-meeting-content-bubble.yml) , чтобы создать уведомление о собрании в собрании Teams.

## <a name="see-also"></a>См. также

* [Создание вкладок для собрания](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Создание приложений для этапа собрания Teams](build-apps-for-teams-meeting-stage.md)
* [Создание расширяемой беседы для чата собрания](build-extensible-conversation-for-meeting-chat.md)
* [Создание приложений для анонимных пользователей](build-apps-for-anonymous-user.md)
* [Расширенные API собраний](meeting-apps-apis.md)
