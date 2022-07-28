---
title: Общие каналы
author: Rajeshwari-v
description: Совместная работа с общими каналами.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 044a5189a626acfcb26631d7d8ee843264401dfe
ms.sourcegitcommit: dd70fedbe74f13725e0cb8dd4f56ff6395a1c8bc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/28/2022
ms.locfileid: "67058298"
---
# <a name="shared-channels"></a>Общие каналы

Общие каналы в Teams позволяют участникам канала совместно работать с пользователями в других teams и организациях. Вы можете создать и поделиться общим каналом с помощью:

* Члены другой команды в той же организации.
* Частные лица в одной организации.
* Частные лица и другие команды других организаций.

Общие каналы упрощают совместную работу. Позволяет внешним пользователям за пределами организации совместно работать с внутренними пользователями в Teams без изменения контекста пользователя. Улучшает взаимодействие с пользователем в отличие от использования гостевых учетных записей. Например, участники должны выйти из Teams и снова войти с помощью гостевой учетной записи. Теперь приложения Teams могут расширять мощное пространство для совместной работы.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Изображение общего канала"border="true" :::

## <a name="manifest-update-in-shared-channels"></a>Обновление манифеста в общих каналах

Когда пользовательский интерфейс содержимого загружается в общий канал, используйте данные, `getContext` полученные при вызове для изменения общего канала. `getContext`Вызов  публикует два новых свойства и `hostTeamGroupID` `hostTenantID`, которые используются для получения членства в каналах из microsoft API Graph. `hostTeam` — это команда, создавшего общий канал.

SupportedChannelTypes — это необязательное свойство, которое позволяет приложению использовать нестандартные каналы. Если приложение поддерживает область группы и свойство определено, Teams включит ваше приложение в каждом типе канала соответствующим образом. В настоящее время поддерживаются частные и общие каналы. Дополнительные сведения см. в [разделе supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes)

```JSON
"supportedChannelTypes": {
      "type": "array",
      "description": "List of ‘non-standard’ channel types that the app supports. Note: Channels of standard type are supported by default if the app supports team scope. ",
      "maxItems": 2,
      "items": { 
        "enum": [
          "sharedChannels",
          "privateChannels"
        ]
      }
    }
```

> [!NOTE]
>
> * Если приложение поддерживает область группы, оно всегда будет работать в стандартных каналах, независимо от того, какие значения определены в этом свойстве.
> * Для правильной работы приложения может потребоваться учет уникальных свойств каждого из этих типов каналов.

Дополнительные сведения о включении вкладки см. в следующих статьях:

* [Получение контекста для вкладки для частных каналов](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Получение контекста для вкладки для общих каналов](../../tabs/how-to/access-teams-context.md#retrieve-context-in-microsoft-teams-connect-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>Приложения и разрешения в общих каналах

Вы можете совместно работать с внешними членами за пределами организации с помощью общих каналов. Разрешения приложения в общих каналах соответствуют списку приложений и политике приложения главного клиента.

> [!NOTE]
> [API уведомлений веб-канала](/graph/teams-send-activityfeednotifications) действий не поддерживает уведомления между клиентами для приложений в общем канале.

## <a name="get-shared-channel-membership"></a>Получение сведений о членстве в общем канале

Вы можете получить прямое членство в общем канале, выполнив `hostTeamGroupID` `getContext` следующие действия:

1. Получение прямых членов с помощью [API-интерфейса API членов канала GET](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Получите каждую общую команду с помощью API GET `sharedWithTeams` .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. Используйте get членов каждой общей команды (team X) с API GET `sharedWithTeams` .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>Классификация членов в общем канале как в клиенте или в клиенте

Вы можете классифицировать участников как в клиенте или вне клиента `tenantID` `hostTeamTenantID` , сравнивая участника или команду следующим образом:

1. Получите член, который вы хотите сравнить.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. При `getContext`использовании сравните `tenantID` элемент со свойством `hostTenantID` .

## <a name="azure-ad-native-identity"></a>Azure AD удостоверения

Приложения должны работать в разных клиентах при установке и использовании. В следующей таблице перечислены типы каналов и соответствующие идентификаторы групп.

|Тип канала| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | Идентификатор Azure AD группы | Идентификатор Azure AD группы |
|Shared | переменная Empty | Идентификатор группы Azure AD узла |

## <a name="see-also"></a>См. также

* [Создание вкладок для Teams](../../tabs/what-are-tabs.md)
* [Схема манифеста приложения для Teams](../../resources/schema/manifest-schema.md)
