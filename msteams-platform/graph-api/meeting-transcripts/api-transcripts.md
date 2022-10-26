---
title: Использование API Graph для получения расшифровки
description: Описывает API для получения расшифровок совещаний.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 2142bc1346a032f27d8612f6081156d2c4927e8f
ms.sourcegitcommit: 372aade09e62ac7e5936215173a6632fbb042c9d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/26/2022
ms.locfileid: "68699180"
---
# <a name="use-graph-apis-to-fetch-transcript"></a>Использование API Graph для получения расшифровки

Используйте REST API Graph для получения расшифровки определенного собрания. Приложение получает расшифровки на основе ИД пользователя организатора собрания и ИД собрания.

Для получения расшифровок используются следующие API:

- [Список callTranscripts](#list-calltranscripts)
- [Получение callTranscript](#get-calltranscript)
- [Получение содержимого callTranscript](#get-calltranscript-content)

### <a name="list-calltranscripts"></a>Список callTranscripts

Этот API используется для получения списка всех объектов `callTranscript` на основе ИД пользователя и ИД собрания. Он возвращает метаданные расшифровки собрания, которые содержат ИД расшифровки, а также дату и время ее создания.

**HTTP-запрос**

```http
GET /me/onlineMeetings('{meetingId}')/transcripts
GET /users('{userId}')/onlineMeetings('{meetingId}')/transcripts
```

**Необязательные параметры запросов**

Этот метод поддерживает `$skipToken` и `$top` [параметры запроса OData](/graph/query-parameters) для настройки отклика.

**Поддерживаемые шаблоны запросов**

| Шаблон                | Поддерживается | Синтаксис                                 | Примечания |
| ---------------------- | ------- | -------------------------------------- | ----- |
| Разбивка на страницы на стороне сервера |     ✓     | `@odata.nextLink`                      | Получите маркер продолжения в ответе, если набор результатов охватывает несколько страниц. |
| Ограничение страницы             |     ✓     | `/transcripts?$top=20` | Получите расшифровки с размером страницы 20. Ограничение страницы по умолчанию — 10. Максимальное ограничение страницы — 100. |

**Заголовки запросов**

| Заголовок       | Значение |
|:---------------|:--------|
| Авторизация  | Bearer {token}. Required.  |

**Текст запроса**

Не указывайте текст запроса для этого метода.

**Отклик**

В случае успеха этот метод возвращает код отклика `200 OK` и коллекцию объектов `callTranscript` в теле отклика.

<br>
<details>
<summary><b>Пример: список callTranscript</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts
```

<br>
<b>Отклик</b>
<br>

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-Type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts",
    "@odata.count": 3,
    "@odata.nextLink": "https://graph.microsoft.com/beta/users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts?$skiptoken=MSMjMCMjMjAyMS0wOS0xNlQxMzo1OToyNy4xMjEwMzgzWg%3d%3d",
    "value": [
        {
            "id": "MSMjMCMjZDAwYWU3NjUtNmM2Yi00NjQxLTgwMWQtMTkzMmFmMjEzNzdh",
            "createdDateTime": "2021-09-17T06:09:24.8968037Z"
        },
        {
            "id": "MSMjMCMjMzAxNjNhYTctNWRmZi00MjM3LTg5MGQtNWJhYWZjZTZhNWYw",
            "createdDateTime": "2021-09-16T18:58:58.6760692Z"
        },
        {
            "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
            "createdDateTime": "2021-09-16T18:56:00.9038309Z"
        }        
    ]
}
```

</details>

### <a name="get-calltranscript"></a>Получение callTranscript

Приложение анализирует список ИД расшифровок, полученных в качестве ответа API `List callTranscripts`, чтобы получить необходимый ИД расшифровки. Этот API используется для получения метаданных единой расшифровки на основе ИД пользователя, ИД собрания и ИД расшифровки.

**HTTP-запрос**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')
```

**Заголовки запросов**

| Заголовок       | Значение |
|:---------------|:--------|
| Авторизация  | Bearer {token}. Required.  |

**Текст запроса**

Не указывайте текст запроса для этого метода.

**Отклик**

В случае успеха этот метод возвратит код отклика `200 OK` и объект `callTranscript` в теле отклика.

<br>
<details>
<summary><b>Пример. Получение callTranscript</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4
```

<br>
<b>Отклик</b>
<br>

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-type: application/json

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#users('ba321e0d-79ee-478d-8e28-85a19507f456')/onlineMeetings('MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ')/transcripts/$entity",
    "id": "MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4",
    "createdDateTime": "2021-09-17T06:09:24.8968037Z"
}
```

</details>

### <a name="get-calltranscript-content"></a>Получение содержимого callTranscript

Этот API используется для получения расшифровки выбранного ИД расшифровки, полученного в ответе API `Get callTranscript`. Он возвращает содержимое расшифровки.

**HTTP-запрос**

```http
GET me/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
GET users('{userId}')/onlineMeetings('{meetingId}')/transcripts('{transcriptId}')/content
```

**Необязательные параметры запросов**

Этот метод поддерживает `$format` [параметр запроса OData](/graph/query-parameters), который позволяет настраивать ответ.

Поддерживаемые типы форматов: `text/vtt` для vtt ИЛИ `application/vnd.openxmlformats-officedocument.wordprocessingml.document` для формата docx.

**Заголовки запросов**

| Заголовок       | Значение |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |
| Accept  | text/vtt ИЛИ  application/vnd.openxmlformats-officedocument.wordprocessingml.document. Необязательный параметр.  |

**Текст запроса**

Не указывайте текст запроса для этого метода.

**Отклик**

В случае успеха этот метод возвращает `200 OK` код отклика и содержит байты для объекта callTranscript в тексте отклика. Заголовок `content-type` указывает тип содержимого расшифровки.

**Примеры**
<br>
<details>
<summary><b>Пример. Получение содержимого callTranscript</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
```

<br>
<b>Отклик</b>
<br>

Отклик содержит байты для расшифровки в тексте сообщения. Заголовок `content-type` указывает тип содержимого расшифровки.

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-type: text/vtt

WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Пример. Получение содержимого callTranscript, указывающего параметр запроса $format</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
 ```

<br>
<b>Отклик</b>
<br>

Отклик содержит байты для расшифровки в тексте сообщения. Заголовок `content-type` указывает тип содержимого расшифровки.

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
    
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>
<br>
<details>
<summary><b>Пример. Получение содержимого callTranscript, указывающего заголовок Accept</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Отклик</b>
<br>

Отклик содержит байты для расшифровки в тексте сообщения. Заголовок `content-Type` указывает тип содержимого расшифровки.

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-type: application/vnd.openxmlformats-officedocument.wordprocessingml.document
    
0:0:0.0 --> 0:0:5.320
User Name
This is a transcript test.
```

</details>
<br>
<details>
<summary><b>Пример. Получение содержимого callTranscript с приоритетом $format над заголовком accept</b></summary>
<br>
<b>Запрос</b>
<br>

```http
GET https://graph.microsoft.com/beta/users/ba321e0d-79ee-478d-8e28-85a19507f456/onlineMeetings/MSo1N2Y5ZGFjYy03MWJmLTQ3NDMtYjQxMy01M2EdFGkdRWHJlQ/transcripts/MSMjMCMjNzU3ODc2ZDYtOTcwMi00MDhkLWFkNDItOTE2ZDNmZjkwZGY4/content?$format=text/vtt
Accept: application/vnd.openxmlformats-officedocument.wordprocessingml.document
```

<br>
<b>Отклик</b>
<br>

Отклик содержит байты для расшифровки в тексте сообщения. Заголовок `content-Type` указывает тип содержимого расшифровки.

> [!NOTE]
> Объект ответа, показанный здесь, может быть сокращен для удобочитаемости.

```http
HTTP/1.1 200 OK
Content-type: text/vtt
    
WEBVTT
   
0:0:0.0 --> 0:0:5.320
<v User Name>This is a transcript test.</v>
```

</details>

