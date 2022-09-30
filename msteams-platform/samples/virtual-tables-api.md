---
title: Веб-API виртуальных таблиц
author: surbhigupta
description: В этом модуле вы узнаете о веб-API виртуальных таблиц для приложения для управления совместной работой, сортировке виртуальных таблиц и фильтрации в Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: b15c7972dfc0152d458e4ad895ed6d4f7e45cd4c
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243551"
---
# <a name="virtual-tables-web-api"></a>Веб-API виртуальных таблиц

При использовании веб-API Dataverse для получения нескольких записей из виртуальной таблицы можно включить дополнительные параметры запроса для поддержки сортировки, фильтрации и разбиения на страницы. Эти функции не поддерживаются в виртуальных таблицах элементов управления совместной работы, так как они зависят от поддержки, предоставляемой корпорацией Майкрософт API Graph. Дополнительные сведения о поддержке каждой виртуальной таблицы см. в справочнике по сущности виртуальных таблиц.

> [!NOTE]
> В настоящее время элементы управления совместной работы доступны только в [общедоступной предварительной версии разработчика](~/resources/dev-preview/developer-preview-intro.md).

## <a name="virtual-table-sorting"></a>Сортировка виртуальных таблиц

С помощью виртуальных таблиц можно использовать параметр OData $orderby запроса, чтобы задать критерии сортировки результирующего набора. Используйте суффикс asc или desc, чтобы указать порядок по возрастанию или убыванию соответственно. Значение по умолчанию — по возрастанию, если суффикс не применяется.  

**Поддерживаемые** таблицы. Каждая виртуальная таблица поддерживает те же функции сортировки, что и соответствующий ресурс Graph. Виртуальные таблицы, поддерживающие сортировку:  

* Элемент диска Graph
* Событие Graph

> [!NOTE]
> Сортировка не поддерживается для всех атрибутов соответствующих ресурсов Graph. Если пользователь пытается выполнить сортировку по виртуальной таблице с неподдерживаемым атрибутом, этот результирующий набор будет иметь порядок по умолчанию. Это то же поведение, что и веб-API Dataverse для столбцов, которые не поддерживают сортировку.

Примеры:

* GET [URI организации]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '000000000-0000-0000-0000000000000&$orderby=m365_name desc
* GET [URI организации]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '000000000-0000-0000-0000000000000$orderby=m365_subject asc

## <a name="virtual-table-filtering"></a>Фильтрация виртуальных таблиц

С помощью виртуальных таблиц можно использовать параметр OData $filter запроса, чтобы задать критерии, для которых возвращаются строки. Виртуальные таблицы запрашиваются с помощью тех же операторов OData, которые поддерживаются веб-API Dataverse.

* **Операторы сравнения**

  |Оператор|Описание|Пример|
  |----|----|----|
  |eq|Равно|$filter=m365_name eq 'Contoso'|
  |ne|Не равно|$filter=m365_name ne 'Contoso'|
  |gt|Больше|$filter=m365_price gt 50.0|
  |ge|Больше или равно|$filter=m365_price ge 50.0|
  |lt|Меньше|$filter=m365_price lt 50.0|
  |le|Меньше или равно|$filter=m365_price le 50.0|

* **Логические операторы**

  |Оператор|Описание|Пример|
  |----|----|----|
  |и|Логическое И |$filter=m365_name eq "Contoso" и m365_price eq 50.0|
  |или|Логическое ИЛИ |$filter=m365_name ne "Contoso" или m365_price eq 50.0|
  |
not|Логическое согласование |$filter=not contains(m365_name,'Contoso')|

* **Операторы группирования**

  |Оператор|Описание|Пример|
  |----|----|----|
  |( )|Группирование по приоритету |$filter=(m365_name eq 'Contoso' и m365_price eq 50.0) или contains(m365_subject,'Team Sync')|

* **Функции запросов**

  |Функция |Пример |
  |----|----|
  |contains|$filter=contains(m365_name,'Contoso')|
  |endswith|$filter=endswith(m365_name,'Contoso')|
  |startswith|$filter=startswith(m365_name,'Contoso')|

**Поддерживаемые** таблицы. Каждая виртуальная таблица поддерживает те же функции фильтрации, что и соответствующий ресурс Graph. Виртуальные таблицы, поддерживающие фильтрацию:

* Встреча с резервированием Graph
* Элемент диска Graph
* Событие Graph

> [!Note]
> Фильтрация не поддерживается для всех атрибутов соответствующих ресурсов Graph. Если пользователь пытается выполнить фильтрацию по виртуальной таблице с неподдерживаемым атрибутом, этот фильтр игнорируется. Это то же поведение, что и веб-API Dataverse для столбцов, которые не поддерживают фильтрацию.

Примеры:

* GET [URI организации]/api/data/v9.2/m365_graphbookingappointments?$filter=m365_bookingbusinessid eq "ContosoBank@Contoso.onmicrosoft.com" и m365_price eq 100.0
* GET [URI организации]/api/data/v9.2/m365_graphdriveitems?$filter=m365_collaborationrootid eq '000000000-0000-0000-00000000000000' и m365_name eq 'Meeting Notes.docx'
* GET [URI организации]/api/data/v9.2/m365_graphevents?$filter=m365_groupid eq '000000000-0000-0000-00000000000000' и m365_subject eq 'Monthly Sync'

## <a name="virtual-table-pagination"></a>Разбиение на страницы виртуальной таблицы

Разбиение на страницы — это полезный ресурс для получения большого набора записей. Разбиение на страницы виртуальной таблицы можно выполнить тремя разными способами.

Размер страницы можно указать с помощью значения `odata.maxpagesize` предпочтения в заголовке запроса. Если результирующий набор занимает несколько страниц, ответ включает свойство `@odata.nextLink` . Пример запроса и ответа:

# <a name="request"></a>[Запрос](#tab/request)

```http
  GET [Organization URI]/api/data/v9.2/m365_graphdriveitems 
  Accept: application/json 
  Prefer: odata.maxpagesize=2 
```

# <a name="response"></a>[Отклик](#tab/response)

```json
{ 

  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdriveitems", 
  "value": [ 
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      …
      },
      {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_name": "Review.doc", 
      "m365_graphdriveitemid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      … 
      } 
      ],
      "@odata.nextLink": "[Organization URI]/api/data/v9.0/m365_graphdriveitems &$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22UGFnZWQ9VFJVRSZwX1NvcnRCZWhhdmlvcj0xJnBfRmlsZUxlYWZSZWY9dGVzdCZwX0lEPTI5%22%20istracking=%22False%22%20/%3E" 
} 
```

---

В настоящее время следующие виртуальные таблицы поддерживают предпочтения `odata.maxpagesize` :

* Встреча с резервированием Graph
* Событие календаря Graph
* Графовый диск
* Элемент диска Graph

Вы можете указать количество записей, которые необходимо вернуть, передав `$top` параметр в URL-адресе. Если вам также нужно указать номер страницы, это можно сделать, передав файл cookie подкачки в виде строки в кодировке XML в качестве параметра `$skiptoken` . Чтобы получить определенный номер страницы, можно передать файл cookie подкачки в следующем формате:

  `<cookie pagenumber=3 />`

# <a name="request"></a>[Запрос](#tab/request1)

```http
     GET [Organization URL]/api/data/v9.2/m365_graphevents?$top=2&$skiptoken=<cookie pagenumber='3' /> 
```

# <a name="response"></a>[Отклик](#tab/response1)

```json

{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphevents", 
  "value": [
   { 
      "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
      "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
      "m365_subject": "Important meeting", 
      …
    }, 
    {
      "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
      "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
      "m365_subject": "Another important meeting", 
      …
    } 
  ] 
}

```

---

> [!Note]
> Ответ не будет содержать свойство `@nextLink` . Если в вашем варианте использования требуется вернуть следующую ссылку на страницу, вместо передачи параметра URI $top URI можно использовать заголовок предпочтения odata.maxpagesize, описанный в разделе 1.

В настоящее время следующие виртуальные таблицы поддерживают выборку определенной страницы:

* Встреча с резервированием Graph
* Событие календаря Graph

Вы можете передать извлечение XML в виде строки в кодировке XML. С помощью параметра fetch XML можно указать несколько параметров запроса. Параметры разбиения на страницы: страница (номер страницы) и число (размер страницы). В следующем XML-коде указывается номер и размер страницы:

  `<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="<Page Number>" count="<Page Size>"></fetch>`

# <a name="request"></a>[Запрос](#tab/request2)

```http
GET [Organization URL]/api/data/v9.2/m365_graphevents?$fetchXml=<fetch version="1.0" mapping="logical" returntotalrecordcount="true" page="3" count="2"></fetch> 

```

# <a name="response"></a>[Отклик](#tab/response2)

```json
{ 

    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#m365_graphdevents", 
    "@Microsoft.Dynamics.CRM.fetchxmlpagingcookie": "<cookie pagenumber=\"3\" pagingcookie=\"\" istracking=\"False\" />", 
    "value": [ 
        { 
            "@odata.etag": "W/\"{FA93AF7C-1F45-4714-85A5-BB95EB86E1E5}\"", 
            "m365_graphdeventid": "3d59a7e2-ec83-d0b3-270e-8ad676622027", 
            "m365_subject": "Important meeting", 
            …
        }, 
        { 
            "@odata.etag": "W/\"{3938D549-1AEF-46A5-BF3C-38472AD934C2}\"", 
            "m365_graphdeventid": "f50aae23-6644-3d35-66d7-e3c5a979dad3", 
            "m365_subject": "Another important meeting", 
            …
        } 
    ] 
} 

```

---

Следующие виртуальные таблицы поддерживают свойство count, передаваемого как часть параметра fetchXml:

* Графовый диск
* Элемент диска Graph

Следующие виртуальные таблицы поддерживают свойство страницы как часть параметра fetchXml:

* Встреча с резервированием Graph
* Событие календаря Graph
