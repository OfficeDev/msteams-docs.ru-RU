---
title: Включение и настройка приложений для собраний Teams
author: surbhigupta
description: Узнайте, как включать и настраивать приложения для собраний Teams и различных сценариев собраний, обновлять манифест приложения, настраивать функции и многое другое.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: b551513d61e7bb9ab2b9c118f756b3ce5232dde4
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537586"
---
# <a name="enable-and-configure-apps-for-meetings"></a>Включение и настройка приложений для собраний

У каждой команды есть разные способы взаимодействия и совместной работы. Для выполнения различных задач настройте Teams с использованием приложений для собраний. Включите свои приложения для собраний Teams и настройте их доступность в области собраний в манифесте приложения.

## <a name="prerequisites"></a>Предварительные требования

С помощью приложений для собраний Teams вы можете расширить возможности своих приложений в жизненном цикле собрания. Прежде чем работать с приложениями для собраний Teams, необходимо выполнить следующие предварительные требования.

* Ознакомьтесь с разработкой приложений Teams. Дополнительные сведения о разработке приложений Teams см. в статье [Разработка приложения Teams](../overview.md).

* Используйте приложение, которое поддерживает настраиваемые вкладки в области groupchat и (или) команды. Дополнительные сведения см. [в разделах областей](../resources/schema/manifest-schema.md#configurabletabs) [и создании первого приложения табуляции](../build-your-first-app/build-channel-tab.md).

* Соблюдайте общие [руководства по разработке вкладок Teams](../tabs/design/tabs.md) для сценариев до и после собрания. Сведения о взаимодействиях во время собраний см. в [руководствах по разработке вкладок в собрании](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) и [руководствах по разработке диалоговых окон в собрании](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog).

* Чтобы ваше приложение обновлялось в режиме реального времени, оно должно обновляться на основе действий, связанных с событиями в собрании. Эти события могут быть в диалоговых окнах во время собрания и в других сценах жизненного цикла собрания. Сведения о диалоговых окнах во время собрания см. в описании параметра `completionBotId` в [полезных данных уведомления на собрании](API-references.md#send-an-in-meeting-notification).

## <a name="enable-your-app-for-teams-meetings"></a>Включение приложения для собраний Teams

Чтобы включить свое приложение для собраний Teams, обновите манифест своего приложения и используйте свойства контекста, чтобы определить, где должно отображаться приложение.

### <a name="update-your-app-manifest"></a>Обновление манифеста приложения

Возможности приложения для собраний объявляются в манифесте приложения с помощью массивов `configurableTabs`, `scopes` и `context`. Область определяет, у кого есть доступ, а контекст определяет, где доступно ваше приложение.

> [!NOTE]
>
> * Приложения на собраниях требуют или `groupchat` области `team` . Область `team` работает для вкладок в каналах или собраниях каналов.
> * Чтобы поддерживать добавление вкладок в запланированные собрания каналов, укажите область **группы** в разделе **областей** в манифесте приложения. Без **области** группы приложение не будет отображаться во всплывающем окне для собраний канала.
> * Приложения на собраниях могут использовать следующие контексты: `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` и `meetingStage`.
> * Делегированные разрешения RSC `MeetingStage.Write.Chat` `ChannelMeetingStage.Write.Group` и необходимы в манифесте для предоставления общего доступа к этапу собрания.

Следующий фрагмент кода является примером настраиваемой вкладки, используемой в приложении для собраний Teams:

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

### <a name="context-property"></a>Свойство контекста

Свойство `context` определяет, что должно отображаться, когда пользователь вызывает приложение на собрании в зависимости от того, где пользователь вызывает приложение. Свойства `context` и `scopes` вкладки позволяют определить, где должно отображаться приложение. Вкладки в области `team` или `groupchat` могут иметь несколько контекстов.

Обеспечьте поддержку области `groupchat`, чтобы включить свое приложение в чатах перед собранием и после собрания. С помощью интерфейса приложения для взаимодействия до собрания вы можете найти и добавить приложения для собраний, а также выполнить задачи перед собранием. С помощью интерфейса приложения для взаимодействия после собрания вы можете просматривать результаты собрания, например результаты опроса или оплату.

 Ниже приведены значения для свойства `context`. Вы можете использовать некоторые или все эти значения.

|Значение|Описание|
|---|---|
| **channelTab** | Вкладка в заголовке канала команды. |
| **privateChatTab** | Вкладка в заголовке группового чата между группой пользователей, а не в контексте команды или собрания. |
| **meetingChatTab** | Вкладка в заголовке группового чата между группой пользователей для запланированного собрания. Вы можете указать **meetingChatTab** или **meetingDetailsTab**, чтобы убедиться, что приложения работают на мобильных устройствах. |
| **meetingDetailsTab** | Вкладка в заголовке представления сведений о собрании календаря. Вы можете указать **meetingChatTab** или **meetingDetailsTab**, чтобы убедиться, что приложения работают на мобильных устройствах. |
| **meetingSidePanel** | Панель на собрании, открытая через единую панель (панель U-bar). |
| **meetingStage** | Приложение из `meetingSidePanel` можно продемонстрировать на сцене собрания. Это приложение нельзя использовать в клиентах на мобильных устройствах или клиентах комнат Teams. |

После включения своего приложения для собраний Teams, настройте его для взаимодействия перед собранием, во время собрания и после собрания.

## <a name="configure-your-app-for-meeting-scenarios"></a>Настройка приложения для сценариев собраний

Собрания Teams обеспечивают интерфейс взаимодействия для вашей организации. Настройте свое приложение для различных сценариев собраний и улучшите интерфейс собрания. Теперь вы можете определить, какие действия можно предпринять в следующих сценариях собраний.

* [Перед собранием](#before-a-meeting)
* [Во время собрания](#during-a-meeting)
* [После собрания](#after-a-meeting)

### <a name="before-a-meeting"></a>Перед собранием

Перед собранием пользователи могут добавлять вкладки, боты и расширения для сообщений. Пользователи с ролями организатора и докладчика могут добавлять вкладки для собрания.

Чтобы добавить вкладку для собрания:

1. В календаре выберите собрание, для которого нужно добавить вкладку.
1. Выберите вкладку **Сведения** и нажмите <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting1.png" alt="Pre-meeting experience" width="900"/>

1. В появившейся коллекции вкладок выберите приложение, которое нужно добавить, и выполните необходимые действия. Приложение устанавливается как вкладка.

Чтобы добавить расширение для сообщений в собрание:

1. Щелкните многоточие &#x25CF;&#x25CF;&#x25CF; в области создания сообщения в чате.
1. Выберите приложение, которое нужно добавить, и выполните необходимые действия. Приложение устанавливается как расширение для сообщений.

Чтобы добавить бота для собрания:

В чате собрания введите ключ **@** и выберите **Скачать ботов**.

> [!NOTE]
>
> * В диалоговом окне на собрании отображается диалог собрания и одновременно публикуется адаптивная карточка в чате собрания, к которой пользователи могут получить доступ. Адаптивная карточка в чате собрания помогает пользователям при присутствии на собрании или если приложение Teams свернуто.
> * Удостоверение пользователя должно быть подтверждено с помощью [единого входа для вкладок](../tabs/how-to/authentication/tab-sso-overview.md). После проверки подлинности приложение может получить роль пользователя с помощью API `GetParticipant`.
> * В зависимости от роли пользователя приложение может предоставлять возможности для определенной роли. Например, приложение для опросов позволяет создавать опрос только организаторам и докладчикам.
> * Назначения ролей можно изменить во время собрания. Дополнительные сведения см. в статье [Роли в собраниях Teams](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).

### <a name="during-a-meeting"></a>Во время собрания

Во время собрания вы можете использовать `meetingSidePanel` или уведомление на собрании для создания уникальных интерфейсов для своих приложений.

#### <a name="meeting-sidepanel"></a>Боковая панель собрания

`meetingSidePanel` позволяет настраивать интерфейс собрания, что дает возможность организаторам и докладчикам использовать различные наборы представлений и действий. В манифесте своего приложения добавьте `meetingSidePanel` в массив контекста. Во время собрания и во всех сценариях приложение отображается на вкладке во время собрания шириной 320 пикселей. Дополнительные сведения см. в описании [интерфейса FrameInfo](/javascript/api/@microsoft/teams-js/frameinfo) (до TeamsJS версии 2.0.0 известного как `FrameContext`).

Контекст пользователя [можно использовать для маршрутизации запросов](../tabs/how-to/access-teams-context.md#user-context). Дополнительные сведения см. в статье [Поток проверки подлинности для вкладок в Teams](../tabs/how-to/authentication/auth-flow-tab.md). Поток проверки подлинности для вкладок аналогичен потоку проверки подлинности для веб-сайтов. Вкладки могут напрямую использовать OAuth 2.0. Дополнительные сведения см. в статье [Платформа удостоверений Майкрософт и поток кода авторизации OAuth 2.0](/azure/active-directory/develop/v2-oauth2-auth-code-flow).

Расширение для сообщений работает правильно, когда пользователь находится в представлении собрания. Пользователь может публиковать карточки расширения для создания сообщения. AppName в собрании — это подсказка, которая указывает имя приложения на панели U-bar во время собрания.

> [!NOTE]
> Используйте [пакет SDK Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) версии 1.7.0 или более поздней, так как предыдущие версии не поддерживают боковую панель.

#### <a name="in-meeting-notification"></a>Уведомление на собрании

Уведомление на собрании используется для задействования участников во время собрания и сбора сведений или отзывов во время собрания. Используйте [полезные данные уведомления на собрании](API-references.md#send-an-in-meeting-notification), чтобы активировать уведомление на собрании. В составе полезных данных запроса на уведомление укажите URL-адрес, где размещается отображаемое содержимое.

Уведомление на собрании не должно использовать модуль задач. Модуль задач не вызывается в чате собрания. Для отображения уведомления на собрании используется URL-адрес внешнего ресурса. Вы можете использовать метод `submitTask` для отправки данных в чате собрания.

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text="В примере показано, как можно использовать диалоговое окно на собрании.":::

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

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="В этом примере показано, как приложение Teams отображает изображение и карточку пользователя в диалоговом окне собрания." border="true":::

#### <a name="shared-meeting-stage"></a>Общая сцена собрания

Общая сцена собрания позволяет участникам собрания взаимодействовать с содержимым приложения и совместно работать над ним в режиме реального времени. Вы можете поделиться своими приложениями на сцене собрания для совместной работы следующими способами.

* [Share entire app to stage](#share-entire-app-to-stage) using the share to stage button in the meeting side panel of Teams client or through[[deep links](#generate-a-deep-link-to-share-content-to-stage-in-meetings).
* [Демонстрация определенных частей приложения на сцене](#share-specific-parts-of-the-app-to-stage) с помощью API в клиентском пакете SDK Teams.

##### <a name="share-entire-app-to-stage"></a>Демонстрация всего приложения на сцене

Участники могут демонстрировать все приложение на сцене собрания для совместной работы, используя кнопку демонстрации на сцене на боковой панели приложения.

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

Чтобы продемонстрировать все приложение на сцене, в манифесте приложения настройте `meetingStage` и `meetingSidePanel` в качестве контекста кадров. Например:

```json
"configurableTabs": [
   {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
         "groupchat"
        ],
      "context":[
         "meetingSidePanel",
         "meetingStage"
        ]
    }
]
```

Дополнительные сведения см. в [манифесте приложения](../resources/schema/manifest-schema-dev-preview.md#configurabletabs).

##### <a name="share-specific-parts-of-the-app-to-stage"></a>Демонстрация определенных частей приложения на сцене

Участники могут демонстрировать определенные части приложения на сцене собрания для совместной работы, используя API демонстрации на сцене. API-интерфейсы доступны в клиентском пакете SDK Teams и вызываются из боковой панели приложения.

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

Чтобы продемонстрировать определенные части приложения на сцене, необходимо вызвать связанные API в библиотеке клиентского пакета SDK Teams. Дополнительные сведения см. в [справочнике по API](API-references.md).

> [!NOTE]
>
> * Чтобы продемонстрировать определенные части приложения на сцене, используйте манифест Teams версии 1.12 или более поздней.
> * Вы можете предоставлять доступ к определенным частям приложения на этапе собрания только на настольных клиентах Teams. Пользователи мобильных устройств могут совместно использовать определенные части приложения для промежуточной подготовки с помощью общей папки [для подготовки API](API-references.md#share-app-content-to-stage-api).

### <a name="after-a-meeting"></a>После собрания

Конфигурации после и [до собраний](#before-a-meeting) одинаковы.

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Создание глубокой ссылки для совместного использования содержимого на этапе собраний

Вы также можете создать прямую ссылку, чтобы поделиться приложением для [подготовки и](#share-entire-app-to-stage) запуска собрания или присоединения к собранию.

> [!NOTE]
>
> * В настоящее время прямая ссылка для совместного использования содержимого на собраниях находится в стадии улучшения пользовательского интерфейса и доступна только в общедоступной предварительной [версии разработчика](~/resources/dev-preview/developer-preview-intro.md).
> * Прямая ссылка для совместного использования содержимого на этапе собрания поддерживается только в клиенте Teams для настольных компьютеров.

Когда пользователь, который является частью текущего собрания, выбирает в приложении прямую ссылку, приложение совместно используется на этапе и появляется всплывающее окно разрешения. Пользователи могут предоставить участникам доступ для совместной работы с приложением.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="На снимке экрана показан пример всплывающего окна разрешения.":::

Если пользователь не находится на собрании, он перенаправляется в календарь Teams, где он может присоединиться к собранию или инициировать мгновенное собрание (провести собрание сейчас).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="На снимке экрана показан пример всплывающего окна при отсутствии текущего собрания.":::

Когда пользователь инициирует мгновенное собрание (провести собрание сейчас), он может добавлять участников и взаимодействовать с приложением.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="На снимке экрана показан пример, в котором показано, как добавить участников и как взаимодействовать с приложением.":::

Чтобы добавить прямую ссылку для совместного использования содержимого на этапе, необходимо иметь контекст приложения. Контекст приложения позволяет клиенту Teams получить манифест приложения и проверить, возможно ли совместное использование на этапе. Ниже приведен пример контекста приложения.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Параметры запроса для контекста приложения:

* `appID`: это идентификатор, который можно получить из манифеста приложения.
* `appSharingUrl`: URL-адрес, который должен быть общим на этапе, должен быть допустимым доменом, определенным в манифесте приложения. Если URL-адрес не является допустимым доменом, отобразит диалоговое окно ошибки с описанием ошибки.
* `useMeetNow`: включает логический параметр, который может иметь значение true или false.
  * **True**: если значение `UseMeetNow` равно true и нет текущего собрания, будет инициировано новое собрание Meet. При постоянном собрании это значение будет игнорироваться.

  * **False**: значение по `UseMeetNow` умолчанию равно false. Это означает, что при совместном использовании глубокой ссылки на этап и отсутствии текущего собрания появится всплывающее окно календаря. Однако вы можете предоставлять общий доступ непосредственно во время собрания.

Убедитесь, что все параметры запроса правильно закодированы в кодировке URI, а контекст приложения должен быть закодирован дважды в окончательном URL-адресе. См. пример.

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Прямую ссылку можно запустить с веб-сайта Teams или с настольного клиента Teams.

* **Веб-сайт Teams**: используйте следующий формат, чтобы открыть прямую ссылку из Интернета Teams, чтобы поделиться содержимым на стадии.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Пример: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Прямая ссылка|Формат|Пример|
    |---------|---------|---------|
    |Если для общего доступа к приложению и открытия календаря Teams значение UseMeeetNow **равно false**, по умолчанию.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Чтобы поделиться приложением и инициировать мгновенное собрание, если значение UseMeeetNow **истинно**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Клиент team desktop**: используйте следующий формат, чтобы открыть прямую ссылку из настольного клиента Teams, чтобы поделиться содержимым на этапе.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Пример: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Прямая ссылка|Формат|Пример|
    |---------|---------|---------|
    |Если для общего доступа к приложению и открытия календаря Teams значение UseMeeetNow **равно false**, по умолчанию.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Чтобы поделиться приложением и инициировать мгновенное собрание, если значение UseMeeetNow **истинно**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Параметры запроса:

* `deepLinkId`: любой идентификатор, используемый для корреляции телеметрии.
* `fqdn`— `fqdn` необязательный параметр, который можно использовать для перехода в соответствующую среду собрания для совместного использования приложения на этапе. Он поддерживает сценарии, в которых определенная общую папку приложения происходит в определенной среде. Значение по умолчанию — `fqdn` корпоративный URL-адрес, а возможные `Teams.live.com` значения — для Teams для жизни или `teams.microsoft.com``teams.microsoft.us`.

Чтобы поделиться всем приложением на этапе, `meetingStage` `meetingSidePanel` в манифесте приложения необходимо настроить и в качестве контекстов кадров просмотреть [манифест приложения](../resources/schema/manifest-schema.md). В противном случае участники собрания могут не видеть содержимое на стадии.

> [!NOTE]
> Чтобы приложение прошел проверку, при создании глубокой ссылки на веб-сайте, веб-приложении или адаптивной карточке  используйте общий доступ к собранию в качестве строки или копирования.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Приложение для собраний | Демонстрирует, как использовать приложение генератора маркеров собраний для запроса маркера. Маркер создается последовательно, чтобы каждый участник обладал равными возможностями участия в собрании. Маркер удобен в таких сценариях, как собрания Scrum и сеансы вопросов с ответами. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|Пример сцены собрания | Пример приложения для отображения вкладки на сцене собрания для совместной работы | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|Боковая панель собрания | Пример приложения для демонстрации добавления повестки дня на боковой панели во время собрания | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>Пошаговые руководства

* Следуйте [пошаговым инструкциям](../sbs-meeting-token-generator.yml), чтобы создать маркер собрания в своем собрании Teams.
* Следуйте [пошаговым инструкциям](../sbs-meetings-sidepanel.yml), чтобы создать боковую панель собрания в своем собрании Teams.
* Следуйте [пошаговым инструкциям](../sbs-meetings-stage-view.yml), чтобы поделиться представлением сцены собрания в своем собрании Teams.
* Следуйте [пошаговым инструкциям](../sbs-meeting-content-bubble.yml), чтобы создать пузырек содержимого собрания в своем собрании Teams.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Справочные материалы по API приложений для собраний](API-references.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Руководства по проектированию диалоговых окон на собрании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Поток проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Руководства по проектированию общего интерфейса сцены собрания](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Добавление приложений для собраний с помощью Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
