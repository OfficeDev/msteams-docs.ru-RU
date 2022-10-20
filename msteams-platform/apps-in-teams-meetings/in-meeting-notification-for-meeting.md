---
title: Уведомление о сборке собрания для собрания Teams
author: v-sdhakshina
description: Из этой статьи вы узнаете, как создать уведомление на собрании для собрания Microsoft Teams и его пример кода.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 2bdf63ab597c00627c14b909d51efa753e0cd1b0
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615452"
---
# <a name="build-in-meeting-notification-for-teams-meeting"></a>Уведомление о сборке собрания для собрания Teams

Уведомление о собрании используется для привлечения участников и сбора сведений или отзывов во время собрания. Используйте [полезные данные уведомления на собрании](meeting-apps-apis.md#send-an-in-meeting-notification), чтобы активировать уведомление на собрании. В рамках запроса полезных данных уведомления укажите URL-адрес, в котором размещается отображаемое содержимое.

Для отображения уведомления на собрании используется URL-адрес внешнего ресурса. Вы можете использовать метод `submitTask` для отправки данных в чате собрания.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="На снимке экрана показан пример использования диалогового окна в собрании.":::

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

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="На этом снимке экрана показано, как в Teams отображается изображение и карточка людей в диалоговом окне собрания." border="true":::

## <a name="code-sample"></a>Пример кода

Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Уведомление на собрании | Демонстрирует реализацию уведомлений на собрании с помощью бота. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |

## <a name="step-by-step-guides"></a>Пошаговые руководства

Следуйте [пошаговое руководство,](../sbs-meeting-content-bubble.yml) чтобы создать уведомление о собрании в собрании Teams.

## <a name="see-also"></a>См. также

* [Создание вкладок для собрания](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [Этап сборки приложений для собраний Teams](build-apps-for-teams-meeting-stage.md)
* [Создание расширяемой беседы для чата собрания](build-extensible-conversation-for-meeting-chat.md)
* [Создание приложений для анонимных пользователей](build-apps-for-anonymous-user.md)
* [API расширенных собраний](meeting-apps-apis.md)
