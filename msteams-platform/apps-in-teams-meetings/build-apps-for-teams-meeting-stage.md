---
title: Создание приложений для этапа собрания Teams
author: v-sdhakshina
description: Узнайте, как создавать приложения для этапа собрания Teams, предоставлять общий доступ к api-интерфейсам этапа и создавать прямую ссылку для предоставления общего доступа к содержимому на этапе собраний.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 48834addceb0e7a6e4522c096cf40b117312647c
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699143"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Создание приложений для этапа собрания Teams

Совместное использование на этапе позволяет пользователям предоставлять общий доступ к приложению на этапе собрания с боковой панели собрания в текущем собрании. Этот общий доступ является интерактивным и совместным по сравнению с пассивным демонстрацией экрана.

Чтобы вызвать общий доступ к сцене, пользователи могут **щелкнуть значок Поделиться на сцену** в правом верхнем углу боковой панели собрания. Значок **"Общий доступ к сцене**" является собственным для клиента Teams, и при его выборе все приложение предоставляется на этапе собрания.

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>Параметры манифеста приложения для приложений на этапе собрания

Чтобы предоставить общий доступ к приложению этапу собрания, обновите `context` свойство в манифесте приложения следующим образом:

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>API-интерфейсы расширенного общего доступа для промежуточного использования

Существует множество сценариев, в которых общий доступ ко всему приложению на стадии собрания не так полезен, как предоставление общего доступа к определенным частям приложения:  

1. Для приложения для мозгового штурма или доски пользователю может потребоваться предоставить доступ к определенной доске на собрании, а не ко всему приложению со всеми досками.  

1. Для медицинского приложения врач может захотеть поделиться только рентгеновским лучом на экране с пациентом, а не делиться всем приложением со всеми записями пациентов или результатами и т. д.

1. Пользователю может потребоваться предоставить общий доступ к содержимому от одного поставщика содержимого (например, YouTube), а не предоставлять доступ ко всему видео-каталогу на сцене.

Чтобы помочь пользователям в таких сценариях, мы выпустили API-интерфейсы в клиентском пакете SDK Для Teams, которые позволяют программно вызывать общий доступ для этапа для определенных частей приложения с помощью кнопки на боковой панели собрания.

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="Снимок экрана: представление &quot;Общий доступ к собранию&quot;.":::

Используйте следующие API для предоставления общего доступа к определенной части приложения:

|Метод| Описание| Source|
|---|---|----|
|[**Делитесь содержимым приложения на сцене**](#share-app-content-to-stage-api)| Предоставление доступа к определенным частям приложения на стадии собрания с боковой панели собрания в собрании. | [Пакет SDK библиотеки JavaScript для Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
|[**Получить состояние обмена сцены содержимого приложения**](#get-app-content-stage-sharing-state-api)| Получить информацию о состоянии общего доступа к приложению на сцене собрания. | [Пакет SDK библиотеки JavaScript для Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**Получить возможности обмена сцены содержимого приложения**](#get-app-content-stage-sharing-capabilities-api)| Получите возможности приложения для совместного использования на сцене собрания. | [Пакет SDK библиотеки JavaScript для Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

## <a name="share-app-content-to-stage-api"></a>Поделитесь содержимым приложения на сцене API

API `shareAppContentToStage` позволяет вам делиться определенными частями вашего приложения на сцене собрания. API доступен через клиентский SDK Teams.

### <a name="prerequisite"></a>Предварительное условие

* Чтобы использовать API `shareAppContentToStage`, необходимо получить разрешения RSC. В манифесте приложения настройте свойство `authorization` и `name` и `type` в поле `resourceSpecific`. Например:

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
         "name": "MeetingStage.Write.Chat",
         "type": "Delegated"
        }
        ]
    }
    }
    ```

* `appContentUrl` должен быть разрешен массивом `validDomains` внутри manifest.json, иначе API возвращает ошибку 501.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице приведены параметры запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра, ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. *Результат* может содержать значение true, если общий ресурс успешно выполнен, или значение NULL при сбое общего ресурса. |
|**appContentURL**| String | Да | URL-адрес, который будет опубликован на сцене. |

### <a name="example"></a>Пример

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений для предоставления общего доступа к этапу.|

## <a name="get-app-content-stage-sharing-state-api"></a>Получить состояние обмена сцены содержимого приложения API

`getAppContentStageSharingState` API позволяет получать сведения о совместном использовании приложений на этапе собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра: ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, в случае ошибки, либо значение null при успешном совместном использовании.  *Результат* может содержать объект при успешном `IAppContentStageSharingState` использовании общего ресурса или значение NULL в случае ошибки.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates if app is sharing content on the meeting stage.
    }
});
```

Текст отклика JSON для `getAppContentStageSharingState` API:

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет необходимых разрешений для предоставления общего доступа к этапу.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Получить возможности обмена сцены содержимого приложения API

API `getAppContentStageSharingCapabilities` позволяет получить возможности приложения для совместного использования на сцене собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра: ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. Результат может содержать объект при успешном `IAppContentStageSharingCapabilities` использовании общего ресурса или значение NULL в случае ошибки.|

### <a name="example"></a>Пример

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

Текст отклика JSON для `getAppContentStageSharingCapabilities` API:

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>Коды ответа

В следующей таблице приведены коды ответов:

|Код ответа|Описание|
|---|---|
| **500** | Внутренняя ошибка. |
| **501** | API не поддерживается в текущем контексте.|
| **1000** | Приложение не имеет разрешений на разрешение общей папки на стадии.|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Создание глубокой ссылки для предоставления общего доступа к содержимому на этапе собраний

Вы также можете создать прямую ссылку для предоставления общего доступа к приложению, чтобы выполнить этап и начать собрание или присоединиться к нему.

> [!NOTE]
>
> * В настоящее время прямая ссылка для предоставления общего доступа к содержимому на собраниях находится в стадии улучшения пользовательского интерфейса и доступна только в [общедоступной предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).
> * Прямая ссылка для предоставления общего доступа к содержимому для этапа собрания поддерживается только в классическом клиенте Teams.

Если пользователь, являющийся частью текущего собрания, выбирает в приложении прямую ссылку, приложение передается сцене и откроется всплывающее окно разрешения. Пользователи могут предоставить участникам доступ для совместной работы с приложением.

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="На снимку экрана показан пример всплывающего окна разрешений.":::

Если пользователь не состоит в собрании, он перенаправляется в календарь Teams, где он может присоединиться к собранию или начать мгновенное собрание (Собрание сейчас).

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="На снимок экрана показан пример всплывающего окна, когда собрание отсутствует.":::

После того как пользователь инициирует мгновенное собрание (Meet now), он может добавлять участников и взаимодействовать с приложением.

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="Снимок экрана — это пример, в котором показан параметр добавления участников и способ взаимодействия с приложением.":::

Чтобы добавить прямую ссылку для предоставления общего доступа к содержимому на сцене, необходимо иметь контекст приложения. Контекст приложения позволяет клиенту Teams получить манифест приложения и проверить, возможен ли общий доступ на этапе. Ниже приведен пример контекста приложения.

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

Параметры запроса для контекста приложения:

* `appID`: это идентификатор, который можно получить из манифеста приложения.
* `appSharingUrl`: URL-адрес, к которому необходимо предоставить общий доступ на этапе, должен быть допустимым доменом, определенным в манифесте приложения. Если URL-адрес не является допустимым доменом, появится диалоговое окно с ошибкой, чтобы предоставить пользователю описание ошибки.
* `useMeetNow`: включает логический параметр, который может иметь значение true или false.
  * **True**: если `UseMeetNow` значение равно true и если текущее собрание отсутствует, будет инициировано новое собрание Meet now. При текущем собрании это значение будет игнорироваться.

  * **False**: значение по умолчанию равно false. Это означает, что при совместном использовании прямой ссылки на этап и отсутствии текущего `UseMeetNow` собрания появится всплывающее окно календаря. Однако вы можете предоставить общий доступ непосредственно во время собрания.

Убедитесь, что все параметры запроса правильно закодированы URI и контекст приложения должен быть закодирован дважды в конечном URL-адресе. См. пример.

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

Прямую ссылку можно запустить либо из Веб-сайта Teams, либо из классического клиента Teams.

* **Веб-сайт Teams**. Используйте следующий формат, чтобы запустить прямую ссылку из веб-сайта Teams для предоставления общего доступа к содержимому на сцене.

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    Пример: `https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Прямая ссылка|Формат|Пример|
    |---------|---------|---------|
    |Чтобы предоставить общий доступ к приложению и открыть календарь Teams, если параметр UseMeeetNow имеет **значение false**, по умолчанию.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Чтобы предоставить общий доступ к приложению и инициировать мгновенное собрание, если свойство UseMeeetNow имеет **значение true**.|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **Клиент team desktop**. Используйте следующий формат, чтобы запустить прямую ссылку из классического клиента Teams для предоставления общего доступа к содержимому на сцене.

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    Пример: `msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |Прямая ссылка|Формат|Пример|
    |---------|---------|---------|
    |Чтобы предоставить общий доступ к приложению и открыть календарь Teams, если параметр UseMeeetNow имеет **значение false**, по умолчанию.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |Чтобы предоставить общий доступ к приложению и инициировать мгновенное собрание, если свойство UseMeeetNow имеет **значение true**.|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

Параметры запроса:

* `deepLinkId`: любой идентификатор, используемый для корреляции телеметрии.
* `fqdn`: `fqdn` необязательный параметр, который можно использовать для переключения в соответствующую среду собрания для предоставления общего доступа к приложению на сцене. Он поддерживает сценарии, в которых определенный общий ресурс приложения происходит в определенной среде. Значение по умолчанию — корпоративный `fqdn` URL-адрес, а возможные значения — `Teams.live.com` для Teams для жизни, `teams.microsoft.com`или `teams.microsoft.us`.

Чтобы предоставить общий доступ ко всему приложению для этапа, в манифесте приложения необходимо настроить `meetingStage` и `meetingSidePanel` как контексты кадра см. в [манифесте приложения](../resources/schema/manifest-schema.md). В противном случае участники собрания могут не видеть содержимое на сцене.

> [!NOTE]
> Чтобы приложение прошло проверку, при создании глубокой ссылки с веб-сайта, веб-приложения или адаптивной карточки используйте в качестве строки или копии **общий доступ к собранию** .

## <a name="build-an-in-meeting-document-signing-app"></a>Создание приложения для подписывания документов на собрании

Вы можете создать приложение на собрании, позволяющее участникам собрания подписывать документы в режиме реального времени. Это упрощает проверку и подписывание документов в одном сеансе. Участники могут подписывать документы с помощью текущего удостоверения клиента.

Приложение для подписи на собрании можно использовать для:

- Добавление документов для проверки во время собрания
- Предоставление общего доступа к документам для проверки на главном этапе
- Подписывая документы, используя удостоверение подписывателя

Участники могут просматривать и подписывать документы, такие как соглашения о покупке и заказы на покупку.

![приложение для подписывания документов на собрании](~/assets//images/sbs-inmeeting-doc-signing/signing-clip.gif)

Во время собрания могут быть задействованы следующие роли участников:

- **Создатель документа**. Эта роль может добавлять собственные документы для проверки и подписания.
- **Подписыватель**: эта роль может подписывать проверенные документы.
- **Читатель**. Эта роль может просматривать документы, добавленные на собрание.

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|Пример сцены собрания | Пример приложения для отображения вкладки на сцене собрания для совместной работы | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Уведомление на собрании | Демонстрирует реализацию уведомлений на собрании с помощью бота. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Подписывание документов на собрании | Демонстрирует реализацию приложения Teams для подписывания документов. Включает предоставление общего доступа к определенному содержимому приложения для этапа, единого входа Teams и пользовательского представления этапа. | [Просмотр](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | Н/Д |

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте инструкциям из пошагового [руководства](../sbs-inmeeting-document-signing.yml) , чтобы создать приложение для подписывания документов на собрании.

## <a name="see-also"></a>Дополнительные ресурсы

* [Проверка подлинности Microsoft Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для собраний Teams](teams-apps-in-meetings.md)
* [Создание вкладок для собрания](build-tabs-for-meeting.md)
* [Создание расширяемой беседы для чата собрания](build-extensible-conversation-for-meeting-chat.md)
* [Создание приложений для анонимных пользователей](build-apps-for-anonymous-user.md)
* [Расширенные API собраний](meeting-apps-apis.md)
* [Настраиваемые сцены режима "Вместе"](~/apps-in-teams-meetings/teams-together-mode.md)
* [Пакет SDK Live Share](teams-live-share-overview.md)
* [Пошаговое руководство по созданию приложения для подписывания документов на собрании](../sbs-inmeeting-document-signing.yml)
