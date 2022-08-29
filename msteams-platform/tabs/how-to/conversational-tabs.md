---
title: Создание вкладок бесед
author: surbhigupta
description: Узнайте, как создавать вкладки бесед в Microsoft Teams для начала, продолжения, улучшения и закрытия беседы.
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: high
ms.openlocfilehash: 37816fab1f8ca402e806dec3ec5cca77dd15cf95
ms.sourcegitcommit: 87bba925d005eb331d876a0b9b75154f8100e911
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/27/2022
ms.locfileid: "67450424"
---
# <a name="create-conversational-tabs"></a>Создание вкладок бесед

Подсущности беседы позволяют пользователям беседы о вложенности на вкладке. Например, конкретная задача, пациент и возможность продажи вместо обсуждения всей вкладки, также известной как сущность. Традиционный канал или настраиваемая вкладка позволяет пользователю иметь беседу о вкладке, но пользователю требуется более усортная беседа. Требование к более подробной беседе может возникнуть либо при наличии слишком содержимого для централизованного обсуждения, либо из-за изменения содержимого с течением времени, делая беседу нерелевантной к отображаемому содержимому. Вложенность бесед обеспечивает гораздо более уделяемое внимание диалогу для динамических вкладок.

Подсущности бесед поддерживаются только в каналах. Их можно использовать на личной или статической вкладке для создания или продолжения бесед на вкладке, уже закрепленной на канале. Статическая вкладка полезна, если вы хотите предоставить пользователю одно расположение для просмотра бесед, происходящих по нескольким каналам, и доступа к ним.

## <a name="prerequisites"></a>Предварительные требования

Для поддержки подсущностей бесед ↔ веб-приложение вкладки должно иметь возможность хранить сопоставление между беседами вложенных элементов в серверной базе данных. Он `conversationId` предоставляется, но его `conversationId` необходимо сохранить и вернуть в Teams, чтобы пользователи могли продолжить беседу.

## <a name="start-a-new-conversation"></a>Начать новую беседу

Чтобы начать новую беседу, используйте функцию `openConversation()` . Запуск и продолжение беседы обрабатываются этим методом. Входные данные функции изменяются в зависимости от того, какое действие вы хотите выполнить, с точки зрения пользователя, при этом открывается панель беседы справа от экрана, чтобы начать беседу или продолжить беседу.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**OpenConversation** принимает следующие входные данные для начала беседы в канале:

* **subEntityId**: идентификатор конкретной подущностей. Например, задача 123.
* **entityId**: идентификатор экземпляра вкладки при его создании. Идентификатор очень важен для ссылки на тот же экземпляр вкладки.
* **channelId**: канал, в котором находится экземпляр вкладки.
   > [!NOTE]
   > Идентификатор **channelId** является необязательным для вкладок канала. Однако рекомендуется сохранить реализацию в каналах и на статических вкладах одинаково.
* **title**: заголовок, отображаемый пользователю на панели чата.

Большинство из этих значений также можно получить из [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) API (`microsoftTeams.getContext()` в TeamsJS версии 1). Дополнительные сведения см. в [интерфейсе PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true)

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

На следующем рисунке показана панель беседы:

:::image type="content" source="../../assets/images/tabs/conversational-subentities/start-conversation.png" alt-text="начать беседы":::

Если пользователь начинает беседу, важно прослушать обратный вызов этого события, чтобы получить и сохранить **conversationId**:

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onStartConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

Объект `conversationResponse` содержит сведения, связанные с запущенным диалогом. Рекомендуется сохранить все свойства этого объекта ответа для последующего использования.

## <a name="continue-a-conversation"></a>Продолжение беседы

После начала беседы последующие `openConversation()` вызовы требуются, что вы также предоставляете те же входные данные, что и при запуске новой беседы [, но](#start-a-new-conversation) также **включаете conversationId**. Откроется панель беседы для пользователей с соответствующей беседой в представлении. Пользователи могут видеть новые или входящие сообщения в режиме реального времени.

На следующем рисунке показана панель беседы с соответствующей беседой:

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="продолжить беседы":::

## <a name="enhance-a-conversation"></a>Улучшение беседы

Важно, чтобы вкладка отображала [глубокие ссылки на вашу подсущную сущность](~/concepts/build-and-test/deep-links.md). Например, пользователь выбирает прямую ссылку на вкладку из беседы канала. Ожидаемое поведение — получить прямую ссылку, открыть эту подсущную сущность, а затем открыть панель беседы для этой подущности.

Для поддержки подсущностей беседы с личной или статической вкладки вам не нужно ничего менять в реализации. Мы поддерживаем только начало или продолжение бесед с уже закрепленных вкладок каналов. Поддержка статических вкладок позволяет предоставить пользователям единое расположение для взаимодействия со всеми подэлементами. Важно сохранить вкладку `subEntityId``entityId``channelId` и, когда вкладка изначально создана в канале, чтобы иметь правильные свойства при открытии представления беседы на статической вкладке.

## <a name="close-a-conversation"></a>Закрытие беседы

Представление беседы можно закрыть вручную, вызвав функцию `closeConversation()` .

```javascript
microsoftTeams.conversations.closeConversation();
```

Вы также можете прослушивать событие, когда пользователь нажмет кнопку **"Закрыть ( X) в** представлении беседы".

```javascript
⁠microsoftTeams.conversations.openConversation({
    ...,
    onCloseConversation: (conversationResponse) => {
        ⁠// console.log(conversationResponse)
    },
});
```

## <a name="code-sample"></a>Пример кода

| Название примера | Описание | C# |Node.js|
|-------------|-------------|------|----|
|Вкладка "Создание беседы"| Пример приложения на вкладке Microsoft Teams для демонстрации вкладки создания беседы. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Изменения полей вкладок](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Вкладки Teams](~/tabs/what-are-tabs.md)
* [Создание личной вкладки](~/tabs/how-to/create-personal-tab.md)
* [Создание вкладки канала или группы](~/tabs/how-to/create-channel-group-tab.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
* [Создание вкладок с использованием адаптивных карточек](~/tabs/how-to/build-adaptive-card-tabs.md)
