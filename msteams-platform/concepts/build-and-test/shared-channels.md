---
title: Teams Связи общих каналов
author: Rajeshwari-v
description: Сведения о Teams Связи общих каналов для безопасной совместной работы с внутренними и внешними пользователями в общем пространстве без переключения клиентов.
ms.author: surbhigupta
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: f063be5bce83484a259e67e94f4caa73ef8afa76
ms.sourcegitcommit: bd30d33af59dd870a309ae72b4c4496c9c1f920d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/09/2022
ms.locfileid: "67635317"
---
# <a name="microsoft-teams-connect-shared-channels"></a>Microsoft Teams Связи общих каналов

Microsoft Teams Связи общие каналы позволяют участникам канала совместно работать с пользователями в других командах и организациях. Вы можете создать и поделиться общим каналом с помощью:

* Члены другой команды в той же организации.
* Частные лица в одной организации.
* Частные лица и другие команды других организаций.

Teams Связи общих каналов упрощают безопасную совместную работу. Разрешить внешним пользователям за пределами организации взаимодействовать с внутренними пользователями в Teams без изменения контекста пользователя. Улучшение взаимодействия с пользователем в отличие от использования гостевых учетных записей. Например, участники должны выйти из Teams и снова войти с помощью гостевой учетной записи. Приложения Teams расширяют мощное пространство для совместной работы.

:::image type="content" source="~/assets/images/app-fundamentals/shared-channels-teams.png" alt-text="Схема, на которой показана команда B из организации A и группа C из организации B, совместно работая в общем канале в качестве команды A." border="true" :::

## <a name="enable-your-app-for-shared-channels"></a>Включение приложения для общих каналов

SupportedChannelTypes — это необязательное свойство, которое позволяет приложению использовать нестандартные каналы. Если ваше приложение поддерживает область группы и свойство определено, Teams соответствующим образом включает ваше приложение в каждом типе канала. В настоящее время поддерживаются частные и общие каналы. Дополнительные сведения см. в [разделе supportedChannelTypes](../../resources/schema/manifest-schema.md#supportedchanneltypes).

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
> * Если приложение поддерживает область группы, оно работает в стандартных каналах независимо от того, какие значения определены в этом свойстве.
> * Для правильной работы приложения может потребоваться учет уникальных свойств каждого из этих типов каналов.

## <a name="get-context-for-shared-channels"></a>Получение контекста для общих каналов

Когда пользовательский интерфейс содержимого загружается в общий канал, используйте данные, `getContext` полученные при вызове для изменения общего канала. `getContext` Call публикует два новых свойства и `hostTeamGroupID` `hostTenantID`, которые используются для получения членства в канале с помощью API Microsoft Graph. `hostTeam` — это команда, которая создает общий канал.

Дополнительные сведения о включении вкладки см. в следующих статьях:

* [Получение контекста для вкладки для частных каналов](../../tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels)
* [Получение контекста в общих каналах](../../tabs/how-to/access-teams-context.md#get-context-in-shared-channels)

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

2. Используйте `getContext`, сравните `tenantID` элемент со свойством `hostTenantID` .

## <a name="azure-ad-native-identity"></a>Azure AD удостоверения

Приложения должны работать с несколькими клиентами при установке и использовании. В следующей таблице перечислены типы каналов и соответствующие идентификаторы групп.

|Тип канала| groupId | hostTeamGroupId |
|----------|---------|-----------------|
|Regular | Идентификатор Azure AD группы | Идентификатор Azure AD группы |
|Shared | переменная Empty | Идентификатор группы Azure AD узла |

## <a name="see-also"></a>См. также

* [Создание вкладок для Teams](../../tabs/what-are-tabs.md)
* [Схема манифеста для Teams](../../resources/schema/manifest-schema.md)
* [Общие каналы в Microsoft Teams](/MicrosoftTeams/shared-channels)
* [Политика хранения для расположений в Teams](/microsoft-365/compliance/create-retention-policies)
