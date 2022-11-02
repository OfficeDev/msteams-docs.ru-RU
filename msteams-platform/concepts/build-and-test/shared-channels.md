---
title: Teams Связи общих каналов
author: Rajeshwari-v
description: Сведения о Teams Связи общих каналов для безопасной совместной работы с внутренними и внешними пользователями в общем пространстве без переключения клиентов.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: d8c6e46a67c8cfeb1e8fa9bf0196a74fb6e183c6
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/02/2022
ms.locfileid: "68819956"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Связи общих каналов

Microsoft Teams Связи общих каналов позволяют участникам канала сотрудничать с пользователями в других командах и организациях. Вы можете создать общий канал и предоставить к ним общий доступ с помощью:

* Члены другой команды в той же организации.
* Пользователи в одной организации.
* Частные лица и другие команды других организаций.

Teams Связи общих каналов обеспечивают безопасную совместную работу. Разрешить внешним пользователям за пределами организации работать с внутренними пользователями в Teams без изменения их контекста пользователей. Улучшение взаимодействия с пользователем в отличие от гостевых учетных записей, например, участники должны выйти из Teams и снова войти с помощью гостевой учетной записи. Приложения Teams расширяют возможности совместной работы.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Схема: команда B из организации A и команда C из организации B, совместная работающая в общем канале как команда A." border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>Включение приложения для общих каналов

SupportedChannelTypes — это необязательное свойство, которое позволяет приложению использовать нестандартные каналы. Если приложение поддерживает область команды и свойство определено, Teams включает приложение в каждом типе канала соответствующим образом. Сейчас поддерживаются частные и общие каналы. Дополнительные сведения см. в разделе [SupportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes).

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
> * Если приложение поддерживает область команды, оно работает в стандартных каналах, независимо от значений, определенных в этом свойстве.
> * Чтобы обеспечить правильную работу, приложению может потребоваться учет уникальных свойств каждого из этих типов каналов.

## <a name="get-context-for-shared-channels"></a>Получение контекста для общих каналов

При загрузке пользовательского интерфейса содержимого в общий канал используйте данные, полученные из `getContext` вызова, для изменения общего канала. `getContext` при вызове публикуются два новых свойства и `hostTeamGroupID` `hostTenantID`, которые используются для получения членства в канале с помощью API Microsoft Graph. `hostTeam` — это команда, создающая общий канал.

Дополнительные сведения о включении вкладки см. в разделе:

* [Получение контекста для вкладки для частных каналов](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Получение контекста в общих каналах](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

## <a name="apps-and-permissions-in-shared-channels"></a>Приложения и разрешения в общих каналах

Вы можете работать с внешними участниками за пределами организации с помощью общих каналов. Разрешения приложений в общих каналах соответствуют списку приложений команды узла и политике приложений клиента узла.

> [!NOTE]
> [API уведомлений веб-канала действий](/graph/teams-send-activityfeednotifications) не поддерживает уведомления между арендаторами для приложений в общем канале.

## <a name="get-shared-channel-membership"></a>Получение членства в общем канале

Вы можете получить прямое членство в общем канале `hostTeamGroupID` с помощью и `getContext` выполните следующие действия:

1. Получите прямых участников с помощью API [API членов канала GET](/graph/api/channel-list-members?view=graph-rest-beta&tabs=http&preserve-view=true) .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Получение каждой общей команды с помощью GET `sharedWithTeams` API.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams
    ```

3. Используйте GET членов каждой общей команды (Team X) с ПОМОЩЬЮ API GET `sharedWithTeams` .

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/sharedWithTeams/{teamX}/members
    ```

## <a name="classify-members-in-the-shared-channel-as-in-tenant-or-out-tenant"></a>Классифицируйте члены в общем канале как в клиенте или в out-tenant

Члены можно классифицировать как в клиенте или в out-tenant путем сравнения `tenantID` участника или команды следующим `hostTeamTenantID` образом:

1. Получите элемент, который вы хотите сравнить.

    ```http
    GET /teams/{host-team-group-id}/channels/{channel-id}/members
    ```

2. Используйте `getContext`, сравните `tenantID` элемент со свойством `hostTenantID` .

## <a name="azure-ad-native-identity"></a>Azure AD собственное удостоверение

Приложения должны работать между арендаторами при установке и использовании. В следующей таблице перечислены типы каналов и соответствующие им идентификаторы групп:

|Тип канала| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | Идентификатор группы Azure AD команды | Идентификатор группы Azure AD команды |
|Shared | переменная Empty | Идентификатор группы Azure AD хост-команды |

## <a name="see-also"></a>См. также

* [Создание вкладок для Teams](../../tabs/what-are-tabs.md)
* [Схема манифеста для Teams](../../resources/schema/manifest-schema.md)
* [Общие каналы в Microsoft Teams](/MicrosoftTeams/shared-channels)
* [Тип ресурса канала](/graph/api/resources/channel)
* [Политика повторного использования для расположений Teams](/microsoft-365/compliance/create-retention-policies)
