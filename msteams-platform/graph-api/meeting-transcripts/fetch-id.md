---
title: Получение идентификатора собрания и идентификатора организатора для извлечения расшифровки собрания
description: Описывает процесс получения идентификатора собрания и идентификатора организатора для извлечения расшифровки собрания
ms.localizationpriority: high
ms.topic: concept
ms.openlocfilehash: 8be611f72a1ddac84bbe596a1bfc00621cb7c038
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027314"
---
# <a name="obtain-meeting-id-and-organizer-id"></a>Получение идентификатора собрания и идентификатора организатора

Ваше приложение может получать расшифровки собрания, используя идентификатор собрания и пользовательский идентификатор организатора собрания, также известный как идентификатор организатора. REST API Graph извлекает расшифровки на основе идентификатора собрания и идентификатора организатора, которые передаются в качестве параметров в API.

> [!NOTE]
> Срок действия неиспользованного идентификатора для запланированных собраний может истечь через несколько дней. Его можно реактивировать путем использования URL-адреса собрания для присоединения к собранию. Дополнительные сведения об истечении срока действия различных типов собраний см. в разделе [Срок действия собрания](/microsoftteams/limits-specifications-teams#meeting-expiration).

Чтобы получить идентификатор собрания и идентификатор организатора для извлечения расшифровки, выберите один из двух способов:

- [Подписка на уведомления об изменениях](#subscribe-to-change-notifications)
- [Использование Bot Framework](#use-bot-framework-to-get-meeting-id-and-organizer-id)

### <a name="subscribe-to-change-notifications"></a>Подписка на уведомления об изменениях

Вы можете оформить подписку для приложения, чтобы получать уведомления об изменениях для запланированных собраний. Когда ваше приложение получает уведомление о событиях собраний, на которые оно подписано, оно может извлечь расшифровки, авторизовавшись с помощью необходимых разрешений Azure AD.

Ваше приложение получает уведомление о типе собраний, на которые оно подписано:

- [Уведомление на уровне пользователя](#obtain-meeting-details-using-user-level-notification)
- [Уведомление на уровне клиента](#obtain-meeting-details-using-tenant-level-notification)

Когда приложение получает уведомление о событиях собраний, на которые оно подписано, оно может извлечь идентификатор собрания и идентификатор организатора из сообщения уведомления. Используя полученные сведения о собрании ваше приложение может извлечь расшифровки собраний после завершения собрания.

#### <a name="obtain-meeting-details-using-user-level-notification"></a>Получение сведений о собрании с помощью уведомления на уровне пользователя

Выберите подписку приложения на уведомления на уровне пользователя для получения расшифровок собрания конкретного пользователя. Когда для этого пользователя будет запланировано собрание, ваше приложение получит уведомление. Ваше приложение также может получать уведомления о собраниях с помощью событий календаря.

Сведения о подписке приложения на события календаря см. в разделе [Уведомления об изменениях для ресурсов Outlook в Microsoft Graph](/graph/outlook-change-notifications-overview).

Используйте следующий пример для подписки на уведомления на уровне пользователя:

```http
    
POST https://graph.microsoft.com/v1.0/subscriptions/
{
    "changeType": "created,updated,deleted",
    "notificationUrl": "https://webhook.azurewebsites.net/api/send/myNotifyClient",
    "resource": "users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events",
    "expirationDateTime": "2022-05-05T14:58:56.7951795+00:00",
    "clientState": "ClientSecret",
    "includeResourceData": false
}
```

Когда приложение получает уведомление о событии собраний, на которые оно подписано, оно ищет идентификатор события календаря в уведомлении. Используйте идентификатор события для получения `JoinWebUrl`, чтобы извлечь идентификатор определенного чата и подписаться на его сообщения. После подписки приложения на сообщения чата выполните действия, указанные для [уведомлений на уровне клиента](#obtain-meeting-details-using-tenant-level-notification), чтобы получить идентификатор собрания и идентификатор организатора.

Чтобы получить идентификатор собрания и идентификатор организатора из уведомления на уровне пользователя:

1. **Получите идентификатор события**: ваше приложение получает свойство `eventId` из полезных данных уведомления.

    <details>
    <summary><b>Пример</b>: полезные данные уведомления</summary>

    ```json
    {
        "subscriptionId": "ef30cdc6-b5ae-4702-b924-f458fd9e5fc3",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "clientState": "ClientSecret",
        "subscriptionExpirationDateTime": "2022-05-05T07:54:53.1886542-07:00",
        "resource": "Users/1273a016-201d-4f95-8083-1b7f99b3edeb/Events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",
        "resourceData": {}
    }
    ```

    В этом примере `eventID` из `resource` является *AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=*.
    </details>

2. **Получите URL-адрес собрания**: используйте идентификатор события для получения `joinUrl`, содержащего URL-адрес собрания.

    Дополнительные сведения см. в разделе [Получение события](/graph/api/event-get).

    Чтобы запросить URL-адрес собрания, используйте следующий пример:

    ```http
    GET https://graph.microsoft.com/v1.0/users/1273a016-201d-4f95-8083-1b7f99b3edeb/events/AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=
    ```

    Полезные данные ответа содержат `joinURL`.

    <details>
    <summary><b>Пример</b>. Полезные данные ответа для получения URL-адреса собрания</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('1273a016-201d-4f95-8083-1b7f99b3edeb')/events/$entity",
        "@odata.etag": "W/\"xRVh47aDEU6na1ckNYfMiwABb2Twsg==\"",
        "id": "AAMkADY0NjM1MjRhLTNiNjAtNDBiOC1hYTQxLThkMjAxN2QzMjZhYQBGAAAAAAC03Gz8aL_JQp2Kxvw5a29SBwDFFWHjtoMRTqdrVyQ1h8yLAAAAAAENAADFFWHjtoMRTqdrVyQ1h8yLAAFwC7nAAAA=",    
        "start": {
            "dateTime": "2022-05-06T15:00:00.0000000",
            "timeZone": "UTC"
        },
        "end": {
            "dateTime": "2022-05-06T15:30:00.0000000",
            "timeZone": "UTC"
        },
            
        "onlineMeeting": {
            "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MjExYzJiMTItZDY1MS00ZGZkLWE5YzQtZTBmNWI1MDg2M2Uw%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%221273a016-201d-4f95-8083-1b7f99b3edeb%22%7d",
            "conferenceId": "438824583",
            "tollNumber": "+1 213-279-1007"
        }    
    }
    ```

    </details>

    URL-адрес собрания содержится в `joinUrl`.

3. **Получите идентификатор потока чата**. Используйте URL-адрес собрания, полученный в `joinUrl`, для извлечения идентификатора потока чата. Укажите этот URL-адрес собрания в качестве значения параметра `joinWebUrl` при получении соответствующего собрания.

    Используйте следующий пример для запроса идентификатора потока:

    ``` http
    GET https://graph.microsoft.com/v1.0/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    Полезные данные ответа содержат элемент `threadID` в свойстве `chatInfo`.
    <br>
    <details>
    <summary><b>Пример</b>. Полезные данные ответа с идентификатором потока</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

    Идентификатор чата содержится в `threadId`.

4. **Подписка на сообщения чата**. Используйте идентификатор чата, чтобы подписать ваше приложение на получение сообщений чата для конкретного собрания. Дополнительные сведения см. в разделе [Подписка на сообщения в чате](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-in-a-chat).

    Если вы хотите, чтобы ваше приложение подписалось на сообщения с определенным текстом, см. раздел [Подписка на сообщения в чате с определенным текстом](/graph/teams-changenotifications-chatmessage#example-2-subscribe-to-messages-in-a-chat-that-contain-certain-text).

5. Выполните действия для [уведомлений на уровне клиента](#obtain-meeting-details-using-tenant-level-notification), чтобы получить идентификатор собрания и идентификатор организатора.

#### <a name="obtain-meeting-details-using-tenant-level-notification"></a>Получение сведений о собрании с помощью уведомления на уровне клиента

Уведомления на уровне клиента полезны, если приложение имеет право на доступ ко всем расшифровкам собраний в клиенте. Подпишите ваше приложение на получение уведомлений о событиях при запуске транскрибирования или завершении звонка для запланированных онлайн-собраний Teams. После завершения собрания ваше приложение получит доступ к расшифровке собрания и сможет извлечь ее.

Сведения о подписке приложения на уведомления на уровне клиента см. в разделе [Получение уведомлений об изменениях](/graph/teams-changenotifications-chatmessage#subscribe-to-messages-across-all-chats).

Когда ваше приложение получает уведомление о событиях собраний, на которые оно подписано, оно выполняет поиск по уведомлениям о начале транскрибирования и событиях завершения собрания. Эти события содержат идентификатор чата, который используется для получения сущности чата и, в конечном итоге, идентификатора собрания и идентификатора организатора.

Чтобы получить идентификатор собрания и идентификатор организатора из уведомления на уровне клиента:

1. **Получение идентификатора чата**: ваше приложение получает свойство `chatId` из уведомления для последующих вызовов. Ваше приложение может получить идентификатор чата из следующих полезных данных:

    - Событие начала транскрибирования: `callTranscriptEventMessageDetail` тип события

        <details>
        <summary><b>Пример</b>. Полезные данные для события начала транскрибирования</summary>

        ```json
        {
        "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
        "changeType": "created",
        "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
        "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787549174')",
        "contentDecryptedBySimulator": {
            "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
            "messageType": "systemEventMessage",
            "createdDateTime": "2022-04-12T18:19:09.174Z",
            "lastModifiedDateTime": "2022-04-12T18:19:09.174Z",
            "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
            "body": {
                "contentType": "html",
                "content": "<systemEventMessage/>"
            },
            "channelIdentity": null,
            "eventDetail": {
                "@odata.type": "#Microsoft.Teams.GraphSvc.callTranscriptEventMessageDetail",
                "callId": "16481de8-3262-419b-abc7-0139e6239515",
                "callTranscriptICalUid": "",
                "meetingOrganizer": {
                    "application": null,
                    "device": null,
                    "user": {
                    "userIdentityType": "aadUser",
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null
                        }
                    }
                }
            },
            "encryptedContent": {}
        }
        ```

        </details>

    - Событие завершения вызова:  `callEndedEventMessageDetail` тип события

        <details>
        <summary><b>Пример</b>. Полезные данные для события завершения вызова</summary>

        ```json
        {
            "subscriptionId": "1217470f-564c-4fe3-b51f-ebd962cb8797",
            "changeType": "created",
            "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
            "resource": "chats('19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2')/messages('1649787585457')",
            "resourceData": {},
            "contentDecryptedBySimulator": {
                "@odata.context": "https://graph.microsoft.com/$metadata#chats('19%3Ameeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk%40thread.v2')/messages/$entity",
                "createdDateTime": "2022-04-12T18:19:45.457Z",
                "lastModifiedDateTime": "2022-04-12T18:19:45.457Z",     
                "chatId": "19:meeting_ZjVkMjc0ZWYtNThkMy00ZGI1LWFiYjAtYjg3ZGU0ZWI3MzZk@thread.v2",
                "eventDetail": {
                    "@odata.type": "#Microsoft.Teams.GraphSvc.callEndedEventMessageDetail",
                    "callId": null,
                    "callDuration": "PT1M44S",
                    "callEventType": "meeting",
                    "callParticipants": [
                    ],
                    "initiator": {
        
                    }
                }
            },
            "encryptedContent": {
                    
            }
        }
        ```

        </details>

2. **Получение сущности чата**: ваше приложение может извлечь сущность чата, используя идентификатор чата, полученный на шаге 1. Используйте сущность чата, чтобы получить URL-адрес для присоединения к вызову. Элемент `joinWebUrl` свойства `onlineMeetingInfo` содержит этот URL-адрес и, в конечном итоге, используется для получения идентификатора собрания. Идентификатор организатора также является частью полезных данных ответа.

    Дополнительные сведения о сущности чата см. в разделе [Получение чата](/graph/api/chat-get).

    Используйте следующий пример для запроса сущности чата на основе идентификатора чата:

    ``` http
    GET https://graph.microsoft.com/v1.0/chats/19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2
    ```

    Полезные данные ответа содержат следующие элементы:

    - **Идентификатор организатора**: он содержится в элементе`id` свойства `organizer` в полезных данных ответа.
    - **URL-адрес для собрания**: этот URL-адрес используется для получения идентификатора собрания и доступен в полезных данных ответа в одном из двух сценариев:
        - Если собрание является онлайн-собранием Teams, элемент`joinWebUrl` свойства `onlineMeetingInfo` содержит этот URL-адрес.
        - Если собрание не было создано как онлайн-собрание из клиента Teams или Outlook, оно содержит элемент `calendarEventId` в свойстве `onlineMeetingInfo`. Приложение может использовать `calendarEventId` для получения`joinUrl`, что аналогично `joinWebUrl`.

      Дополнительные сведения о событиях см. в разделе [Получение события](/graph/api/event-get?view=graph-rest-1.0&tabs=http&preserve-view=true).

      Примеры сценариев полезных данных ответа в зависимости от типа URL-адреса для присоединения к собранию:

        - Онлайн-собрание Teams, где доступен `joinWebUrl`

            <details>
            <summary><b>Пример</b>. Полезные данные ответа для онлайн-собрания</b></summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2@thread.v2",
                "topic": "Test Meet Create Online Meeting",
                "createdDateTime": "2022-04-14T11:30:45.903Z",
                "lastUpdatedDateTime": "2022-04-26T06:27:45.265Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                "calendarEventId": null,
                    "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NmU0NTkxYzMtM2Y2My00NzRlLWFmN2YtNTFiMGM5OWM3ZjY2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

        - Собрание, запланированное через клиент Teams или Outlook, не помеченное как онлайн-собрание, где доступен `calendarEventId`

            <details>
            <summary><b>Пример</b>. Полезные данные ответа для собрания, не помеченного как онлайн-собрание</summary>

            ```json
            {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#chats/$entity",
                "id": "19:meeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm@thread.v2",
                "topic": "Non Online Meeting Teams Client",
                "createdDateTime": "2022-04-26T09:43:23.711Z",
                "lastUpdatedDateTime": "2022-04-26T09:43:46.157Z",
                "chatType": "meeting",
                "webUrl": "https://teams.microsoft.com/l/chat/19%3Ameeting_YzM1NGFiZWYtOGFiOS00NjM5LTg4OTktYmU0MjI4NTQyNGZm%40thread.v2/0?tenantId=2432b57b-0abd-43db-aa7b-16eadd115d34",
                "tenantId": "2432b57b-0abd-43db-aa7b-16eadd115d34",
                "viewpoint": null,
                "onlineMeetingInfo": {
                    "calendarEventId": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYeAAA=",
                    "joinWebUrl": null,
                    "organizer": {
                        "id": "14b779ae-cb64-47e7-a512-52fd50a4154d",
                        "displayName": null,
                        "userIdentityType": "aadUser"
                    }
                }
            }
            ```

            </details>

            - Используйте следующий пример, чтобы получить `joinWebUrl` из `calendarEventId`:

              ``` http
                GET https://graph.microsoft.com/beta/users/14b779ae-cb64-47e7-a512-52fd50a4154d/events/AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=
              ```

              В этом примере:

                - Идентификатор организатора — *14b779ae-cb64-47e7-a512-52fd50a4154d*.

              Полезные данные ответа этого запроса содержат `joinUrl` в свойстве `onlineMeeting`.

                > [!NOTE]
                > Элемент `joinUrl` аналогичен `joinWebUrl`.

              <br>
              <details>
              <summary><b>Пример</b>. Полезные данные ответа, которые содержат URL-адрес для присоединения к собранию</summary>

              ```json
              {
                "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/events/$entity",
                "@odata.etag": "W/\"bMMOQZSMbU+4hcmFq11dwAAAkc3Tmw==\"",
                "id": "AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQBGAAAAAAD3AG5jNnlgQJvdCL_KgXJIBwBsww5BlIxtT7iFyYWrXV3AAAAAAAENAABsww5BlIxtT7iFyYWrXV3AAACSDwYdAAA=",    
                "start": {
                    "dateTime": "2022-04-26T10:30:00.0000000",
                    "timeZone": "UTC"
                },
                "end": {
                    "dateTime": "2022-04-26T11:00:00.0000000",
                    "timeZone": "UTC"
                },    
                "onlineMeeting": {
                    "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d"
                },
                "calendar@odata.associationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')/$ref",
                "calendar@odata.navigationLink": "https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/calendars('AAMkAGE3NjJhOTVhLTNkZDQtNDE2OS05ZjU0LTJmOGQ0YTY2YTdiZQAuAAAAAAD3AG5jNnlgQJvdCL_KgXJIAQBsww5BlIxtT7iFyYWrXV3AAAAAAAENAAA=')"
                }
                ```

              </details>

3. **Получение идентификатора собрания**. Теперь ваше приложение может использовать `joinWebUrl` для получения идентификатора собрания.

    Используйте следующий пример для запроса идентификатора онлайн-собрания:

    ``` http
    GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings?$filter=JoinWebUrl%20eq%20'https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d'
    ```

    Полезные данные ответа содержат идентификатор собрания в элементе `id` свойства `value`.
    <br>
    <details>
    <summary><b>Пример</b>. Полезные данные ответа с идентификатором собрания</summary>

    ```json
    {
        "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings",
        "value": [
            {
                "id": "MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19NVE01T1RZM01HVXRObVk0TWkwMFlqZzRMVGsyTURVdFkySXlaR1JsTm1VMVpqQTJAdGhyZWFkLnYy",
                "creationDateTime": "2022-04-26T07:41:17.3736455Z",
                "startDateTime": "2022-04-26T10:30:00Z",
                "endDateTime": "2022-04-26T11:00:00Z",
                "joinUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "joinWebUrl": "https://teams.microsoft.com/l/meetup-join/19%3ameeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2%40thread.v2/0?context=%7b%22Tid%22%3a%222432b57b-0abd-43db-aa7b-16eadd115d34%22%2c%22Oid%22%3a%2214b779ae-cb64-47e7-a512-52fd50a4154d%22%7d",
                "chatInfo": {
                    "threadId": "19:meeting_MTM5OTY3MGUtNmY4Mi00Yjg4LTk2MDUtY2IyZGRlNmU1ZjA2@thread.v2",
                    "messageId": "0",
                    "replyChainMessageId": null
                }
            }
        ]
    }
    ```

    </details>

4. **Получение расшифровки**: идентификатор организатора и идентификатор собрания, полученные на этапах 2 и 3, позволяют приложению извлекать расшифровки для конкретного события собрания.

    Чтобы получить расшифровку, необходимо:

    1. **Извлечь идентификатор расшифровки на основе идентификатора организатора и идентификатора собрания**:

       Используйте следующий пример для запроса идентификатора расшифровки:

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts
        ```

        В этом примере:

        - Идентификатор собрания включен в качестве значения для `onlineMeetings`: *MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bW VldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM 1pqWTJAdGhyZWFkLnYy*.
        - Идентификатор организатора — *14b779ae-cb64-47e7-a512-52fd50a4154d*.

        Полезные данные ответа содержат идентификатор расшифровки для идентификатора собрания и идентификатора организатора в элементе `id` свойства `value`.
        <br>
        <details>
        <summary><b>Пример</b>. Полезные данные ответа для получения идентификатора расшифровки</summary>

        ```json
        {
            "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts",
            "@odata.count": 1,
            "value": [
                {
                    "id": "MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh",
                    "createdDateTime": "2022-04-14T11:34:39.5662792Z"
                }
            ]
        }
        ```

        В этом примере идентификатором расшифровки является *MSMjMCMJMDEyNjjmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh*.

        </details>

    1. **Доступ к расшифровке собрания и ее извлечение на основе идентификатора расшифровки**:

        Используйте следующий пример, чтобы запросить расшифровки для конкретного собрания в формате `.vtt`:

        ```http
        GET https://graph.microsoft.com/beta/users('14b779ae-cb64-47e7-a512-52fd50a4154d')/onlineMeetings('MSoxNGI3NzlhZS1jYjY0LTQ3ZTctYTUxMi01MmZkNTBhNDE1NGQqMCoqMTk6bWVldGluZ19ObVUwTlRreFl6TXRNMlkyTXkwME56UmxMV0ZtTjJZdE5URmlNR001T1dNM1pqWTJAdGhyZWFkLnYy')/transcripts('MSMjMCMjMDEyNjJmNjgtOTc2Zi00MzIxLTlhNDQtYThmMmY4ZjQ1ZjVh')/content?$format=text/vtt
        ```

        Полезные данные ответа будут содержать расшифровки в формате `.vtt`.

### <a name="use-bot-framework-to-get-meeting-id-and-organizer-id"></a>Используйте Bot Framework для получения идентификатора собрания и идентификатора организатора

Ваше приложение может использовать Bot Framework для получения идентификатора собрания и идентификатора организатора. Бот может автоматически получать события начала или окончания собрания из всех запланированных онлайн-собраний.

Используйте следующий пример, чтобы получить идентификатор собрания и идентификатор организатора с помощью приложения-бота:

```json
GET /v1/meetings/{meetingId}
```

Полезные данные ответа содержат:

- Идентификатор собрания в элементе `msGraphResourceId` свойства `details`.
- Идентификатор организатора в элементе `id` свойства `organizer`.
<br>
<details>
<summary><b>Пример</b>. Полезные данные ответа для получения сведений о собрании</b></summary>

```json
{
  details: {
    id: "MCMxOTptZWV0aW5nX05XTTFNVEk1TnpNdE5qZ3pNeTAwWVdRNExUaG1PV1F0WlRnM01UQm1PVGczWW1VekB0aHJlYWQudjIjMA==",
    msGraphResourceId: "MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVldGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM1ltVXpAdGhyZWFkLnYy",
    scheduledStartTime: {
    },
    scheduledEndTime: {
    },
    joinUrl: "https://teams.microsoft.com/l/meetup-join/19%3ameeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz%40thread.v2/0?context=%7b%22Tid%22%3a%22b3cdf1c8-024a-49e2-a994-f67f830b02f3%22%2c%22Oid%22%3a%226702afb6-109b-4c32-a141-6e65469502b9%22%7d",
    title: "Testing meeting bot 1 - Hun",
    type: "Scheduled",
  },
  conversation: {
    id: "19:meeting_NWM1MTI5NzMtNjgzMy00YWQ4LThmOWQtZTg3MTBmOTg3YmUz@thread.v2",
    isGroup: true,
    conversationType: "groupChat",
  },
  organizer: {
    id: "29:1VZkVr77S3GW_RdAXKrfgFeytpqMegL3tkKvEbwrPqoCVvmqrlKtVrfKWUY7xIM-bZIx4Sq-p1MjdjSZnb5W20w",
    tenantId: "b3cdf1c8-024a-49e2-a994-f67f830b02f3",
    aadObjectId: "6702afb6-109b-4c32-a141-6e65469502b9",
  },
}
```

В этом примере:

- Идентификатор собрания включен в качестве значения для `msGraphResourceId`: *MSo2NzAyYWZiNi0xMDliLTRjMzItYTE0MS02ZTY1NDY5NTAyYjkqMCoqMTk6bWVl dGluZ19OV00xTVRJNU56TXROamd6TXkwMFlXUTRMVGhtT1dRdFpUZzNNVEJtT1RnM 1ltVXpAdGhyZWFkLnYy*.
- Идентификатор организатора `aadObjectId` `organizer`содержится в качестве значения для:  *6702afb6-109b-4c32-a141-6e65469502b9*.

</details>

Получив идентификатор собрания и идентификатор организатора, приложение активирует API Graph для извлечения содержимого расшифровки с помощью этих сведений о собрании.

### <a name="code-samples"></a>Примеры кода

Вы можете попробовать следующий пример кода для приложения-бота:

| **Название примера** | **Описание** | **C#** | **Node.js** |
|----------------|-----------------|--------------|--------------|--------------|
| Транскрибирование собраний | Это пример приложения, в котором показано, как получить расшифровку с помощью API Graph и отобразить ее в модуле задачи. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-transcription/nodejs) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [API Graph для получения расшифровок](/graph/api/resources/calltranscript)
