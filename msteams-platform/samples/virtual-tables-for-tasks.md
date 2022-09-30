---
title: Виртуальные таблицы для задач, собраний и файлов в приложении для управления совместной работой
author: surbhigupta
description: В этом модуле вы узнаете о виртуальных таблицах для задач, собраний и файлов в приложении для управления совместной работой в Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 2571787d5fba47c4ada3765dd13dd36ef1f8f63a
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243047"
---
# <a name="virtual-tables-for-tasks-meetings-files"></a>Виртуальные таблицы для задач, собраний, файлов

Новая возможность в этом выпуске — это набор виртуальных таблиц. Они позволяют разработчикам взаимодействовать с Graph с помощью API OData.

Основное решение для управления совместной работой включает набор виртуальных [таблиц, которые](/power-apps/developer/data-platform/virtual-entities/get-started-ve) можно использовать для программного доступа к данным, созданным элементами управления совместной работы.

> [!NOTE]
> В настоящее время элементы управления совместной работы доступны только в [общедоступной предварительной версии разработчика](~/resources/dev-preview/developer-preview-intro.md).

> [!TIP]
> [](/power-apps/developer/data-platform/virtual-entities/get-started-ve) Виртуальные таблицы, также называемые виртуальными сущностями, обеспечивают интеграцию данных, находящихся во внешних системах, путем простого представления этих данных в виде таблиц в Microsoft Dataverse без репликации данных и часто без пользовательского кодирования.

Внешней системой, используемой элементами управления совместной работы, является Microsoft Graph. Существуют виртуальные таблицы для групповых событий календаря, встреч резервирования, планов планировщика или задач, а также дисков, папок и файлов SharePoint.

В этой статье приведены примеры, демонстрирующие доступ к виртуальным таблицам с помощью REST API Dataverse для выполнения операций CRUD (создание, чтение, обновление и удаление).

> [!TIP]
> Дополнительные сведения об REST API Dataverse см. [в статье об использовании веб-API Microsoft Dataverse](/power-apps/developer/data-platform/webapi/overview).

* Виртуальные таблицы используют стандартный веб-API Dataverse, который упрощает заполнение данных в приложении с помощью виртуальных таблиц.
* Виртуальные таблицы реализуют сложные рабочие процессы, необходимые для поддержки элементов управления совместной работы, которые выполняются в центрах обработки данных Майкрософт для достижения оптимальной производительности.  
* Виртуальные таблицы используют стандартные возможности ведения журнала и мониторинга Dataverse.

После установки элементов управления совместной работы виртуальные таблицы можно рассматривать как другую службу для приложения, от которых можно зависеть.

:::image type="content" source="~/assets/images/collaboration-control/vt-overview.png" alt-text="Общие сведения о виртуальных таблицах":::

**Предварительные требования**

Для работы с этой статьей вам потребуется:

1. Среда Dataverse, в которой установлены элементы управления совместной работы.
1. Учетная запись пользователя в среде Dataverse, которой назначена роль пользователя **"** Совместная работа".
1. Стороннее средство, например Post man или пользовательский код C#, который позволяет выполнять проверку подлинности в экземплярах Microsoft Dataverse, а также создавать и отправлять запросы веб-API и просматривать ответы.  

> [!TIP]
> Корпорация Майкрософт предоставляет сведения о настройке среды Postman, которая подключается к экземпляру Dataverse и использует Postman для выполнения операций с веб-API. См [. раздел "Использование Postman с веб-API Microsoft Dataverse"](/power-apps/developer/data-platform/webapi/use-postman-web-api).

## <a name="virtual-tables-sample-scenario"></a>Пример сценария виртуальных таблиц

В сценарии, описанном в этом руководстве, используются виртуальные таблицы планировщика и задачи. Описанный сценарий совпадает с тем, который используется элементом управления "Совместная работа задач". С точки зрения пользователя сценарий показывает, как план планировщика и несколько задач создаются и связаны с определенной бизнес-записью. В этом сценарии показано, как получить задачи, связанные с бизнес-записью, а также как прочитать, обновить и удалить определенную задачу планировщика.

На следующей схеме последовательности объясняется взаимодействие между клиентом, которое может быть элементом управления совместной работы "Задачи", [API](/rest/api/industry/collaboration-controls/) совместной работы и виртуальными таблицами планировщика и задач.

:::image type="content" source="~/assets/images/collaboration-control/vt-sequence.png" alt-text="На рисунке показана схема последовательности для виртуальных таблиц.":::

## <a name="virtual-tables-basic-operations"></a>Основные операции виртуальных таблиц

В этом разделе описываются HTTP-запросы и ответы для каждого шага в примере сценария.

**Задача 1. Получение идентификатора группы**

Получите идентификатор группы, используемый в [параметрах для совместной работы](~/samples/app-with-collaboration-controls.md#define-settings-for-your-collaboration).

> [!NOTE]
> Пользователь, который используется для создания плана в последующих задачах, должен быть членом этой группы. В противном случае вы получите ответ "403 Запрещено".

**Задача 2. Начало сеанса совместной работы**

Сеанс совместной работы — это запись в корневой таблице совместной работы, которая позволяет связать несколько совместной работы, например задачи, события, встречи с бизнес-записью.

Сеанс совместной работы позволяет выполнять такие операции, как список событий календаря, связанных с бизнес-записью, например приложение проверки.

# <a name="request"></a>[Запрос](#tab/request)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_begincollaborationsession  
```

```json
{
    "applicationName": "{{applicationName}}", 
    "collaborationRootEntityId": "{{collaborationRootEntityId}}", 
    "collaborationRootEntityName": "{{entityName}}" 
}
```

* `applicationName`: уникальное имя приложения.
* `collaborationRootEntityName`: имя сущности бизнес-записи;  
* `collaborationRootEntityId`: первичный ключ (идентификатор) определенной бизнес-записи.

# <a name="response"></a>[Отклик](#tab/response)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.m365_begincollaborationsessionResponse", 
    "collaborationRootId": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
}
```

---

Следите за тем, `collaborationRootId` как это необходимо в последующих запросах.

**Задача 3. Создание плана планировщика**

Создайте план Планировщика и свяжите его с созданным выше сеансом совместной работы с и `Group ID` `collaborationRootId`.

# <a name="request"></a>[Запрос](#tab/request1)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannerplans  
```

```json

{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_owner": "{{groupId}}", 
    "m365_title": "{{planTitle}}" 
}

```

* `collaborationRootId`: определяет сеанс совместной работы, с которым мы хотим связать этот план, используя значение из задачи 2.

* `groupId`: определяет группу, которая владеет этим планом, используйте значение из шага 1.

* `planTitle`: название плана

# <a name="response"></a>[Отклик](#tab/response1)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https:// [Organization URI]/api/data/v9.0/$metadata#m365_graphplannerplans/$entity", 
    "@odata.etag": "W/\"JzEtUGxhbiAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:33.1833561Z", 
    "m365_owner": "03614cef-8f5b-4265-9944-080d013c55d6", 
    "m365_title": "Multi-byte plan", 
    "m365_id": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannerplanid": "5c9c3ecf-f157-0f67-dcd9-733a77ad593e", 
    "m365_details": null 
} 

```

---

Следите за тем,`m365_id` как это необходимо в последующих запросах.

**Задача 4. Создание задачи планировщика**

Создайте задачу Планировщика с и `PlanId` `collaborationRootId`. Вы можете создать несколько задач Планировщика и связать их с созданным ранее сеансом совместной работы.

# <a name="request"></a>[Запрос](#tab/request2)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json
{ 
    "m365_collaborationrootid": "{{collaborationRootId}}", 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
} 

```

* `collaborationRootId`: определяет сеанс совместной работы, с которым мы хотим связать этот план, используя значение из задачи 2.
* `planId`: определяет план, который будет назначен этой задаче. Используйте значение из предыдущего шага.
* `taskTitle`: название задачи

# <a name="response"></a>[Отклик](#tab/response2)

```http
    HTTP/1.1 201 Created 
```

```json

{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488865579062167", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-16T16:58:47.571364+00:00\",\"orderHint\":\"8585488866179218449P`\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-16T16:58:47Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_hasdescription": false, 
    "m365_orderhint": "8585488865579062167", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Team-oriented discrete time-frame", 
    "m365_id": "8WSKWaEqAU-aZV4h9VUn0GUALXbH", 
    "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f", 
    "m365_graphplannertaskid": "0a2115b9-8b03-90ee-b450-42005d906ce8", 
    "m365_completedby": null, 
    "m365_details": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
} 

```

---

Следите за тем, `m365_graphplannertaskid` как это необходимо в последующих запросах.

> [!NOTE]
> Является `m365_graphplannertaskid` первичным ключом записи в виртуальной таблице задач Планировщика. Все последующие запросы к виртуальной таблице для взаимодействия с этой записью должны использовать этот первичный ключ. Это будет называться следующими `plannerTaskId` шагами в этом документе.

Повторите этот шаг, чтобы создать несколько задач в плане.

**Задача 5. Получение связанных задач планировщика**

Получение связанных задач планировщика, связанных `collaborationRootId` с созданным ранее сеансом совместной работы.

# <a name="request"></a>[Запрос](#tab/request3)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

* `$filter`: используйте системный $filter для запроса записей, связанных с сеансом совместной работы (путем указания идентификатора корневой записи совместной работы).
* `$select`: используйте параметр $select системного запроса для запроса определенных свойств.

# <a name="response"></a>[Отклик](#tab/response3)

```http
    HTTP/1.1 200 OK 
```

```json

{ 

    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks(m365_graphplannertaskid,m365_title,m365_createddatetime)", 
    "value": [ 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "8537731e-9414-1091-8d7d-ce5b74fc2477", 
            "m365_title": "Diverse executive core", 
            "m365_createddatetime": "2022-05-16T16:58:45Z", 
            "m365_id": "N_A2qmo3j0uvZZY1yd6V_GUADDEg", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "4a89895a-050e-9165-a6e4-19c3850f22ec", 
            "m365_title": "Cloned didactic open architecture", 
            "m365_createddatetime": "2022-05-16T16:58:41Z", 
            "m365_id": "--U0zbgsO0us084C0yCyEWUALbWw", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        }, 
        { 
            "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
            "m365_graphplannertaskid": "20a08b8c-394b-b3fb-f9d1-47496df7a67b", 
            "m365_title": "Synergized zero defect interface", 
            "m365_createddatetime": "2022-05-16T16:58:43Z", 
            "m365_id": "AMn3RtbmV0m6cvkp5HKDCWUAKI0_", 
            "m365_collaborationrootid": "72fc6b52-39d5-ec11-a7b6-0022481bfe8f" 
        } 
    ] 
} 

```

---

Отслеживайте, `m365_id‘s` как идентификаторы потребуются в последующих запросах.

**Задача 6. Получение задачи планировщика**

Получение задачи Планировщика для `PlannerTaskID` выполнения операции чтения для одной из задач планировщика, созданных ранее.

# <a name="request"></a>[Запрос](#tab/request4)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})  
```

* `plannerTaskId`: первичным ключом для записи задачи планировщика является `m365_graphplannertaskid` свойство.

# <a name="response"></a>[Отклик](#tab/response4)

```http
    HTTP/1.1 200 OK 
```

```json
{ 
    "@odata.context": "https://mwtmarkwallaceunmanaged.crm10.dynamics.com/api/data/v9.0/$metadata#m365_graphplannertasks/$entity", 
    "@odata.etag": "W/\"JzEtVGFzayAgQEBAQEBAQEBAQEBAQEBARCc=\"", 
    "m365_activechecklistitemcount": 0, 
    "m365_appliedcategories": "{}", 
    "m365_assigneepriority": "8585488204334528131", 
    "m365_assignments": "{\"be330617-0e2b-48e9-8bf7-429a09c78e65\":{\"assignedBy\":{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null},\"assignedDateTime\":\"2022-05-17T11:20:52.0247676+00:00\",\"orderHint\":\"8585488204934840644P2\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}", 
    "m365_checklistitemcount": 0, 
    "m365_createdby": "{\"user\":{\"displayName\":null,\"email\":null,\"id\":\"be330617-0e2b-48e9-8bf7-429a09c78e65\"},\"group\":null}", 
    "m365_createddatetime": "2022-05-17T11:20:52Z", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_orderhint": "8585488204334528131", 
    "m365_percentcomplete": 0, 
    "m365_priority": 5, 
    "m365_planid": "8I6fu1kNS0elsbTxd67bi2UADnJu", 
    "m365_previewtype": "automatic", 
    "m365_referencecount": 0, 
    "m365_title": "Secured content-based customer loyalty", 
    "m365_id": "SXmz1hxiOk-E3MKJUyhj0mUABvix", 
    "m365_details": "{\"@odata.context\":\"https://graph.microsoft.com/beta/$metadata#planner/tasks('SXmz1hxiOk-E3MKJUyhj0mUABvix')/details/$entity\",\"@odata.etag\":\"W/\\\"JzEtVGFza0RldGFpbHMgQEBAQEBAQEBAQEBAQEBARCc=\\\"\",\"description\":null,\"previewType\":\"automatic\",\"id\":\"SXmz1hxiOk-E3MKJUyhj0mUABvix\",\"references\":{},\"checklist\":{}}", 
    "m365_graphplannertaskid": "1b326015-bb43-945c-85bc-9b2a4ed16c73", 
    "m365_completedby": null, 
    "m365_hasdescription": null, 
    "m365_collaborationrootid": null, 
    "m365_completeddatetime": null, 
    "m365_conversationthreadid": null, 
    "m365_bucketid": null, 
    "m365_startdatetime": null 
}

```

---

Отслеживайте свойство `@odata.etag` и свойство`m365_graphplannertaskid` , так как они потребуются для выполнения операций обновления или удаления.

**Задача 7. Обновление задачи планировщика**

Обновите задачу Планировщика `PlannerTask ID` , чтобы выполнить операцию обновления для одной из задач планировщика, созданных на предыдущем шаге. Чтобы обновить задачу планировщика, выполните следующий запрос:

# <a name="request"></a>[Запрос](#tab/request5)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* Заголовок: If-Match: {{@odata.etag}}

```json

{
    "m365_title": "{{$planTitle}}" 
}   

```

* `@odata.etag`: Etag для задачи, необходимо выполнить чтение, чтобы получить последнюю версию.

* `planTitle`: обновлен заголовок задачи

# <a name="response"></a>[Отклик](#tab/response5)

```http
    HTTP/1.1 204 No Content 
```

---

**Задача 8. Удаление задачи планировщика**

Удалите задачу планировщика `PlannerTask ID` , чтобы выполнить операцию удаления для одной из задач планировщика, созданных на предыдущем шаге. Чтобы удалить задачу планировщика, выполните следующий запрос:

# <a name="request"></a>[Запрос](#tab/request6)

```http
    HTTP/1.1 DELETE https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

* `@odata.etag`: Etag для задачи, необходимо выполнить чтение, чтобы получить последнюю версию.

# <a name="response"></a>[Отклик](#tab/response6)

```http
    HTTP/1.1 204 No Content
```

---

**Задача 9. Обновление сведений о задаче планировщика**

Обновите задачу Планировщика `PlannerTask ID` , чтобы выполнить операцию обновления для одной из задач планировщика, созданных на предыдущем шаге.

# <a name="request"></a>[Запрос](#tab/request7)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Заголовок: If-Match: {{@odata.etag}}

```json

{ 

    "m365_title": "{{$planTitle}}", 
    "m365_details": "{\"@odata.etag\":\"{{details.etag}}\",\"description\":\"Updated Task Description\"}" 

}   
```

* `@odata.etag`: Etag для задачи, необходимо выполнить чтение, чтобы получить последнюю версию.
* `planTitle`: обновлен заголовок задачи.
* `@details.etag`: Etag для сведений о задаче, `m365_details` необходимо выполнить чтение с помощью параметра $select запроса, чтобы включить столбец для получения самой последней версии. Это значение будет включено в столбец `m365_details` ответа. Это значение не совпадает с `@odata.etag` тем, что в серверной части Планировщика задача и ее сведения хранятся отдельно.

# <a name="response"></a>[Отклик](#tab/response7)

```http
HTTP/1.1 204 No Content 
```

---

> [!NOTE]
> Можно задать для `If-Match` заголовка значение "*", а затем не нужно будет предоставлять значения etag, но изменения всегда будут перезаписывать задачу и ее сведения.

## <a name="virtual-tables-authorization"></a>Авторизация виртуальных таблиц

Ниже приведены шаги авторизации, необходимые для выполнения HTTP-запросов с помощью виртуальных таблиц в решении для управления совместной работой.

### <a name="azure-app-registration"></a>Регистрация приложений Azure

Для получения правильного маркера носителя требуется регистрация приложения в Azure. Дополнительные сведения о регистрации приложений см. в [разделе "Регистрация приложения"](/azure/active-directory/develop/quickstart-register-app).

1. Создайте регистрацию приложения в портал Azure для проверки подлинности.
1. Перейдите **к разделу & сертификатов**.
1. Создайте новый секрет клиента.

     > [!IMPORTANT]
     > Обязательно скопируйте значение секрета и сохраните его для последующего использования. Вы не сможете снова получить к нему доступ после выхода с текущей страницы.

1. Перейдите **к разрешениям API**.
1. Добавьте **user_impersonation** делегированное разрешение от Dynamics CRM.
1. Предоставьте согласие администратора для этого разрешения.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-api-permission.png" alt-text="На снимке экрана показан пример разрешения API Power Automate.":::

1. Перейдите к **манифесту**.
1. Задайте для следующих атрибутов значение true:

   * oauth2AllowIdTokenImplicitFlow
   * oauth2AllowImplicitFlow

1. Нажмите "Сохранить".

     :::image type="content" source="../assets/images/collaboration-control/power-automate-manifest.png" alt-text="Снимок экрана: пример манифеста Power Automate":::

### <a name="powerapps-environment-permissions"></a>Разрешения среды PowerApps

После настройки регистрации приложения необходимо настроить пользователя приложения в среде PowerApps. Это позволит выполнять проверку подлинности с помощью правильных областей Dynamics, настроенных ранее.

1. Откройте Центр [Администратор Power Platform](https://admin.powerplatform.microsoft.com/).
1. Перейдите **к списку** > **Your_Environment** > **"Пользователи** > **"**.
1. Выберите **"Новый пользователь приложения** " и выберите регистрацию приложения Azure.
1. Выберите **"Изменить роли безопасности****" и** назначьте роль системного администратора пользователю приложения.

   1. Роль **системного** администратора применяется для разрешения проверки подлинности для всех пользователей с более низкой ролью безопасности. Например, **совместная работа управляет пользователем**.
   1. Это можно ограничить, применив к приложению более низкую роль. Например, службой **совместной работы управляет администратор**.

     :::image type="content" source="../assets/images/collaboration-control/power-automate-admin-center.png" alt-text="Снимок экрана: пример центра администрирования Power Automate":::

### <a name="getting-the-bearer-token"></a>Получение маркера носителя

После завершения регистрации приложения Azure и разрешений среды PowerApps отправьте следующий HTTP-запрос, чтобы получить маркер носителя.

```http
POST https://login.microsoftonline.com/<AZURE_APP_TENANT_ID>/oauth2/token
```

* **Content-Type**: application/x-www-form-urlencoded
* **client_id**: <AZURE_APP_CLIENT_ID>
* **&client_secret**: <AZURE_APP_CLIENT_ID>
* **&ресурса**: https://\<RESOURCEURL\>/
* **&имя пользователя**: \<USERNAME\>
* **&пароля**: \<PASSWORD\>
* **&grant_type**: пароль

> [!IMPORTANT]
> Обязательно включите косую черту в конце параметра ресурса. В противном случае при вызове виртуальной таблицы вы получите ошибку, связанную с областями Graph.

Из полезных данных ответа скопируйте значение свойства **access_token.** Затем этот токен носителя можно передать как часть заголовка авторизации при выполнении запросов к виртуальным таблицам.

:::image type="content" source="../assets/images/collaboration-control/power-automate-authorization.png" alt-text="На снимке экрана показан пример авторизации Power Automate":::

## <a name="virtual-tables-error-handling"></a>Обработка ошибок виртуальных таблиц

Обработка ошибок виртуальных таблиц описывает распространенные сценарии ошибок и способы реагирования виртуальных таблиц.

### <a name="attempt-to-create-a-virtual-record-without-a-collaboration-session"></a>Попытка создать виртуальную запись без сеанса совместной работы

Для каждого запроса на создание виртуальной записи требуется допустимый сеанс совместной работы.  При создании виртуальной записи виртуальная таблица создает запись карты совместной работы, которая включает первичный ключ виртуальной записи, имя сущности и внешний идентификатор, то есть идентификатор ресурса Graph. Эта схема совместной работы связана с сеансом совместной работы, и именно так элементы управления совместной работой будут отслеживать совместную работу, связанную с бизнес-записью.

# <a name="request"></a>[Запрос](#tab/request8)

```http
    HTTP/1.1 POST https://[Organization URI]/api/data/v9.0/m365_graphplannertasks  
```

```json

{ 
    "m365_planid": "{{planId}}", 
    "m365_title": "{{taskTitle}}", 
    "m365_duedatetime": "2022-05-04T08:00:00Z", 
    "m365_assignments": "{\"me\":{\"orderHint\":\" !\",\"@odata.type\":\"#microsoft.graph.plannerAssignment\"}}" 
}

```

Свойство `collaborationRootId` отсутствует в запросе.

# <a name="response"></a>[Отклик](#tab/response8)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
    "error": { 
        "code": "0x80048d0b", 
        "message": "Parameter 'm365_collaborationrootid' is null, empty, or white-space." 
    } 
} 

```

---

Чтобы устранить эту проблему, необходимо всегда предоставлять допустимое `collaborationRootId` свойство при создании виртуальной записи.

### <a name="attempt-to-read-a-virtual-record-without-a-collaboration-map"></a>Попытка чтения виртуальной записи без карты совместной работы

Виртуальные таблицы позволяют выполнять запросы, возвращаемые коллекциями виртуальных записей. Мы видели это ранее в этом документе, где запрашивали все задачи планировщика, связанные с определенным сеансом совместной работы. Вы также можете запросить все задачи планировщика, связанные с определенным планом планировщика, с помощью системного $filter следующего запроса: $filter=m365_planid eq`{{planId}}`. Одна из проблем, которые могут возникнуть при использовании такого запроса, — это то, что записи будут возвращены для задач планировщика, которые не связаны с сеансом совместной работы, то есть с задачами планировщика, созданными средствами, отличными от использования элемента управления "Совместная работа". При попытке чтения, обновления или удаления такой записи запрос завершится ошибкой, так как виртуальная таблица не может найти связанную карту совместной работы.  

# <a name="request"></a>[Запрос](#tab/request9)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Свойство `plannerTaskId` связано с задачей планировщика, которая была создана с помощью веб-интерфейса Планировщика и поэтому не имеет записи карты совместной работы.

# <a name="response"></a>[Отклик](#tab/response9)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "A record with the specified key values does not exist in m365_collaborationmap entity" 
    }
} 
```

---

Чтобы устранить эту проблему, необходимо проверить сообщение об ошибке в ответе, и если оно задано для сообщения, показанного выше, это означает, что виртуальная запись не связана. Чтобы создать связь для этой записи, необходимо вызвать [сопоставление сопоставления совместной работы — REST API](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map).

### <a name="attempt-to-read-a-virtual-record-and-the-graph-resource-has-been-deleted"></a>Попытка чтения виртуальной записи и удаление ресурса Graph

В случае предыдущей ошибки необходимо обработать случай, когда ресурс Graph был удален, но у клиента по-прежнему есть ссылка на удаленную виртуальную запись. Это может произойти, если другой пользователь удалил запись. При попытке чтения, обновления или удаления такой записи запрос завершится ошибкой, так как виртуальная таблица не может получить ресурс из Graph.

# <a name="request"></a>[Запрос](#tab/request10)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Свойство `plannerTaskId` связано с задачей планировщика, которая была удалена.

# <a name="response"></a>[Отклик](#tab/response10)

```http
    HTTP/1.1 404 Not Found 
```

```json
{ 
    "error": { 
        "code": "0x80048d02", 
        "message": "REST call failed because: Reason - NotFound, Full error - {\"error\":{\"code\":\"\",\"message\":\"The requested item is not found.\",\"innerError\":{\"date\":\"2022-05-17T16:30:51\",\"request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\",\"client-request-id\":\"b692a31a-312d-490c-8dce-d258459a0211\"}}}." 
    } 
} 
```

---

Этот случай должен обрабатываться любым клиентским кодом, который извлекает виртуальные записи, так как другой пользователь может в любое время удалить связанный ресурс Graph.

### <a name="attempt-to-update-a-virtual-record-with-an-invalid-odataetag"></a>Попытка обновить виртуальную запись с помощью недопустимого @odata.etag

Это `@odata.etag` свойство используется для параллелизма данных и предотвращения перезаписи той же записи, если она была обновлена другим пользователем. Когда запись считывает текущий тег etag, она остается действительной до тех пор, пока запись не будет изменена. Тег etag должен быть включен в любой запрос на обновление и проверяться до завершения операции. Если запись была изменена другим пользователем с момента чтения записи текущим пользователем, запрос на обновление текущих пользователей завершится ошибкой.

Если вы выполните два запроса на обновление с использованием одного @odata.etag, второй запрос завершится ошибкой:

# <a name="request"></a>[Запрос](#tab/request11)

```http
    HTTP/1.1 PATCH https://[Organization URI]/api/data/v9.0/m365_graphplannertasks({{plannerTaskId}})
```

Заголовок: If-Match: {{@odata.etag}}

```json
{
    "m365_title": "{{$planTitle}}" 
}

```

# <a name="response"></a>[Отклик](#tab/response11)

```http
    HTTP/1.1 409 Conflict 
```

```json
{ 
    "error": { 
        "code": "0x80048d08", 
        "message": "REST call failed because: Reason - Conflict, Full error - {\"error\":{\"code\":\"\",\"message\":\"The attempted changes conflicted with already accepted changes. Read the latest state and resolve differences.\",\"innerError\":{\"date\":\"2022-05-18T06:54:55\",\"request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\",\"client-request-id\":\"dc6cd2b7-1509-4e81-91ff-22cf35b86e18\"}}}." 
    }
} 
```

---

### <a name="querying-for-associated-virtual-records"></a>Запрос связанных виртуальных записей

В задаче 5 выше описано, как получить связанные задачи планировщика. Эта операция поддерживается для всех виртуальных таблиц. При выполнении этого запроса необходимо `$filter` включить запрос, который указывает корневой идентификатор службы совместной работы, как показано ниже:

# <a name="request"></a>[Запрос](#tab/request12)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphplannertasks?$filter=m365_collaborationrootid eq '{{collaborationRootId}}'&$select=m365_graphplannertaskid,m365_title,m365_createddatetime  
```

---

* Другие параметры фильтрации не могут быть объединены с этим запросом `$filter` , и если они будут игнорироваться.
* Другая фильтрация должна выполняться непосредственно в ответе запроса.

### <a name="querying-for-virtual-records-with-required-key-attributes"></a>Запрос виртуальных записей с необходимыми ключевыми атрибутами

При вызове веб-API Dataverse для получения нескольких записей из следующих виртуальных таблиц требуется обязательный ключевой атрибут. Для резервирования встреч Graph требуется, чтобы `m365_bookingbusinessid` в запрос был включен допустимый параметр. Если ключевой атрибут не указан, запрос завершится ошибкой следующим образом:

# <a name="response"></a>[Отклик](#tab/response13)

```http
    HTTP/1.1 400 Bad Request 
```

```json

{ 
  "error": { 
    "code": "0x80048d0b", 
    "message": "Key attribute is missing: 'm365_bookingbusinessid'.", 
    ….
  } 
} 

```

---

Чтобы устранить эту проблему, измените запрос на следующий формат:

# <a name="request"></a>[Запрос](#tab/request14)

```http
    HTTP/1.1 GET https://[Organization URI]/api/data/v9.0/ m365_graphbookingappointments?$filter=m365_bookingbusinessid eq '{{bookingBusinessId}}'
```

---

### <a name="creating-virtual-records-and-graph-access-control"></a>Создание виртуальных записей и управление доступом Graph

Виртуальные таблицы учитывают управление доступом, указанное для Microsoft Graph. Виртуальные таблицы не позволяют выполнять операции, которые пользователь не смог выполнить с помощью microsoft API Graph. Например, если пользователь, который используется для создания плана, является задачей 3 и не является членом используемой группы, вы получите 403 запрещенных ответа.
