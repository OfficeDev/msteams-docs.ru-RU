---
title: Создание вкладок бесед
author: surbhigupta
description: Узнайте, как создавать диалоговые вкладки в Microsoft Teams, чтобы начать, продолжить, улучшить и закрыть беседу.
ms.topic: conceptual
ms.author: lomeybur
ms.localizationpriority: high
ms.openlocfilehash: fa54221a413b19704d80ec62feb1cf068e42d1a0
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820124"
---
# <a name="create-conversational-tabs"></a>Создание вкладок бесед

Подтенанты беседы позволяют пользователям проводить беседы о подотносьях на вкладке. Например, конкретная задача, пациент и возможность продажи, вместо обсуждения всей вкладки, также известной как сущность. Традиционный канал или настраиваемая вкладка позволяет пользователю беседовать о вкладке, но пользователю требуется более целенаправленная беседа. Требование к более предметной беседе может возникнуть либо при наличии слишком большого количества содержимого для централизованного обсуждения, либо из-за того, что содержимое изменилось с течением времени, что делает беседу неактуальной для отображаемого содержимого. Подотносья беседы обеспечивают гораздо более целенаправленный диалог для динамических вкладок.

Диалоговые подтенанты поддерживаются только в каналах. Их можно использовать с личной или статической вкладки для создания или продолжения бесед на вкладках, уже закрепленных в канале. Статическая вкладка полезна, если требуется предоставить пользователю одно расположение для просмотра бесед и доступа к беседам, происходящим по нескольким каналам.

## <a name="prerequisites"></a>Предварительные требования

Для поддержки диалоговых вложенных сущностей веб-приложение табуляции должно иметь возможность хранить сопоставление бесед подотделений ↔ в серверной базе данных. Предоставляется `conversationId` , но необходимо сохранить его `conversationId` и вернуть в Teams, чтобы пользователи продолжили беседу.

## <a name="start-a-new-conversation"></a>Начало новой беседы

Чтобы начать новую беседу, используйте функцию `openConversation()` . Запуск и продолжение беседы обрабатываются этим методом. Входные данные функции изменяются в зависимости от того, какое действие вы хотите выполнить, с точки зрения пользователя, откроется панель беседы справа от экрана, чтобы начать беседу или продолжить беседу.

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

**OpenConversation** принимает следующие входные данные, чтобы начать беседу в канале:

* **subEntityId**: идентификатор определенной подчиненности. Например, задача 123.
* **entityId**: идентификатор экземпляра вкладки при его создании. Идентификатор важно ссылаться на тот же экземпляр вкладки.
* **channelId**: канал, в котором находится экземпляр вкладки.
   > [!NOTE]
   > **ChannelId** является необязательным для вкладок канала. Однако рекомендуется, если вы хотите сохранить реализацию в разных каналах и на статических вкладках одинаково.
* **title**: заголовок, отображаемый пользователю на панели чата.

Большинство из этих значений также можно получить из [`app.getContext()`](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-getcontext&preserve-view=true) API (`microsoftTeams.getContext()` в TeamsJS версии 1). Дополнительные сведения см. в разделе [Интерфейс PageInfo](/javascript/api/@microsoft/teams-js/app?view=msteams-client-js-latest#@microsoft-teams-js-app-pageinfo&preserve-view=true).

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

Объект `conversationResponse` содержит сведения, связанные с начатым диалогом. Рекомендуется сохранить все свойства этого объекта ответа для последующего использования.

## <a name="continue-a-conversation"></a>Продолжение беседы

После начала беседы последующие вызовы требуют, чтобы `openConversation()` вы также предоставляли те же входные данные, что и в [начале новой беседы](#start-a-new-conversation), но также включали **conversationId**. Откроется панель беседы для пользователей с соответствующим диалогом в представлении. Пользователи могут просматривать новые или входящие сообщения в режиме реального времени.

На следующем рисунке показана панель беседы с соответствующим диалогом:

:::image type="content" source="../../assets/images/tabs/conversational-subentities/continue-conversation.png" alt-text="Продолжить беседы":::

## <a name="enhance-a-conversation"></a>Улучшение беседы

Важно, чтобы вкладка содержит [глубокие ссылки на вашу подчиненность](~/concepts/build-and-test/deep-links.md). Например, пользователь выбирает вкладку chiclet deep link из беседы канала. Ожидаемое поведение заключается в получении глубокой ссылки, открытии этой подчиненности, а затем открытии панели беседы для этой подчиненности.

Для поддержки подчиненных диалогов из личной или статической вкладки вам не нужно ничего изменять в реализации. Мы поддерживаем только начало или продолжение бесед из уже закрепленных вкладок каналов. Поддержка статических вкладок позволяет предоставить пользователям единое расположение для взаимодействия со всеми подсутями. Важно сохранить `subEntityId`, `entityId`и `channelId` при первоначальном создании вкладки в канале, чтобы иметь правильные свойства при открытии представления беседы на статической вкладке.

## <a name="close-a-conversation"></a>Закрытие беседы

Вы можете вручную закрыть представление беседы, вызвав функцию `closeConversation()` .

```javascript
microsoftTeams.conversations.closeConversation();
```

Вы также можете слушать событие, когда пользователи выбирают **Закрыть (X)** в представлении беседы.

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
|Вкладка "Создание беседы"| Пример приложения для вкладки Microsoft Teams для демонстрации вкладки создания беседы. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/csharp) |  [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-conversations/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Изменения полей вкладок](~/resources/removing-tab-margins.md)

## <a name="see-also"></a>См. также

* [Создание вкладок для Teams](../what-are-tabs.md)
* [Создание личной вкладки](create-personal-tab.md)
* [Создание вкладки канала или вкладки группы](create-channel-group-tab.md)
* [Создание вкладок с использованием адаптивных карточек](build-adaptive-card-tabs.md)
* [Вкладки на мобильных устройствах](~/tabs/design/tabs-mobile.md)
