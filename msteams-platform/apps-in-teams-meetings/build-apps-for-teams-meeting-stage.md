---
title: Этап сборки приложений для собраний Teams
author: v-sdhakshina
description: Узнайте, как создавать приложения для этапов собраний Teams, предоставлять общий доступ к API-интерфейсам и создавать прямую ссылку для совместного использования содержимого на собраниях.
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: 440e48d370d18564f5bba869d95c63bc25b11e4e
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615434"
---
# <a name="build-apps-for-teams-meeting-stage"></a>Этап сборки приложений для собраний Teams

Предоставление общего доступа к этапу позволяет пользователям делиться приложением на этапе собрания с панели на стороне собрания во время текущего собрания. Этот общий доступ является интерактивным и совместным по сравнению с пассивным демонстрацией экрана.

Чтобы вызвать общий доступ к этапу, пользователи могут  щелкнуть значок "Поделиться на стадию" в правой верхней части панели собрания. **Значок "Поделиться на** стадию" является собственным для клиента Teams, и его выбор предоставляет общий доступ ко всему приложению на этапе собрания.

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>Параметры манифеста приложения для приложений на этапе собрания

Чтобы поделиться приложением на этапе собрания, `context` обновите свойство в манифесте приложения следующим образом:

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>Расширенный общий доступ к API-интерфейсам этапа

Существует множество сценариев, в которых общий доступ ко всему приложению на этапе собрания не так полезен, как совместное использование определенных частей приложения:  

1. Для проведения мозгового штурма или доски пользователю может потребоваться поделиться определенной доской на собрании, а не всем приложением со всеми досками.  

1. Для медицинского приложения может потребоваться поделиться только снимком X-Луча на экране с пациентом, а не всем приложением со всеми записями, результатами и т. д.

1. Пользователю может потребоваться предоставить общий доступ к содержимому от одного поставщика содержимого за раз (например, YouTube) и предоставить общий доступ ко всему каталогу видео на стадии.

Чтобы помочь пользователям в таких сценариях, мы выпустили API-интерфейсы в клиентском пакете SDK Teams, которые позволяют программно вызывать общую папку для определенных частей приложения с помощью кнопки на панели на стороне собрания.

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="На снимке экрана показан общий доступ к представлению стадии собрания.":::

Используйте следующие API для совместного использования определенной части приложения:

|Метод| Описание| Source|
|---|---|----|
|[**Делитесь содержимым приложения на сцене**](#share-app-content-to-stage-api)| Предопубликуйте определенные части приложения на этапе собрания на боковой панели собрания. | [Пакет SDK библиотеки JavaScript для Microsoft Teams](/javascript/api/@microsoft/teams-js/meeting) |
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
|**callback**| String | Да | Обратный вызов содержит два параметра, ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. Результат *может* содержать значение true, если общий ресурс успешно выполнен, или значение NULL в случае сбоя общей папки. |
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
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="get-app-content-stage-sharing-state-api"></a>Получить состояние обмена сцены содержимого приложения API

API `getAppContentStageSharingState` позволяет получать сведения о совместном использовании приложений на этапе собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра: ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, в случае ошибки, либо значение null при успешном совместном использовании.  Результат *может* содержать объект `IAppContentStageSharingState` , если общий доступ выполнен успешно, или значение NULL в случае ошибки.|

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
| **1000** | Приложение не имеет необходимых разрешений, чтобы разрешить общий доступ к этапу.|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>Получить возможности обмена сцены содержимого приложения API

API `getAppContentStageSharingCapabilities` позволяет получить возможности приложения для совместного использования на сцене собрания.

### <a name="query-parameter"></a>Параметр запроса

В следующей таблице содержится параметр запроса:

|Значение|Тип|Обязательный|Описание|
|---|---|----|---|
|**callback**| String | Да | Обратный вызов содержит два параметра: ошибку и результат. *Ошибка* может содержать либо ошибку типа *SdkError*, либо значение null при успешном совместном использовании. Результат может содержать объект `IAppContentStageSharingCapabilities` , если общий доступ выполнен успешно, или значение NULL в случае ошибки.|

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
| **1000** | У приложения нет разрешений на предоставление общего доступа к этапу.|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>Создание глубокой ссылки для совместного использования содержимого на этапе собраний

Вы также можете создать прямую ссылку, чтобы поделиться приложением для подготовки и запуска собрания или присоединения к собранию.

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
|Пример сцены собрания | Пример приложения для отображения вкладки на сцене собрания для совместной работы | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Уведомление на собрании | Демонстрирует реализацию уведомлений на собрании с помощью бота. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Подписывание документа на собрании | Демонстрирует реализацию приложения Teams для подписи документов. Включает предоставление общего доступа к определенному содержимому приложения на этапе, единый вход Teams и представление стадии для конкретного пользователя. | [Просмотр](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | Недоступно |

## <a name="see-also"></a>См. также

* [Проверка подлинности Microsoft Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Приложения для собраний Teams](teams-apps-in-meetings.md)
* [Создание вкладок для собрания](build-tabs-for-meeting.md)
* [Создание расширяемой беседы для чата собрания](build-extensible-conversation-for-meeting-chat.md)
* [Создание приложений для анонимных пользователей](build-apps-for-anonymous-user.md)
* [API расширенных собраний](meeting-apps-apis.md)
* [Настраиваемые сцены режима "Вместе"](~/apps-in-teams-meetings/teams-together-mode.md)
* [Пакет SDK Live Share](teams-live-share-overview.md)
