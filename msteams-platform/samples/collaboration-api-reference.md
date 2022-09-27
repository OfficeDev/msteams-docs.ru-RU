---
title: Справочники по REST API для управления совместной работой и параметрами
author: surbhigupta
description: В этом модуле вы узнаете об управлении совместной работой и параметрах REST API для управления параметрами, запуска, сопоставления и получения действий совместной работы.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: 7a990cf23d0832e26a9d8bc6ef9dc2f34ea06a53
ms.sourcegitcommit: c1032ea4f48c4bbf5446798ff7d46d7e6e9f55d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027300"
---
# <a name="collaboration-control-and-settings-rest-api-reference"></a>Справочник по REST API управления совместной работой и параметрами

Разработчики могут использовать REST API службы совместной работы и параметров для управления параметрами, запуска, сопоставления и получения действий совместной работы с помощью собственных сущностей бизнес-модели.

> [!NOTE]
> В настоящее время элементы управления совместной работы доступны только в [общедоступной предварительной версии разработчика](~/resources/dev-preview/developer-preview-intro.md).

Эта статья содержит справочные материалы по REST API решения для управления совместной работой.

## <a name="rest-operations-collaboration---custom-api"></a>Операции REST: совместная работа — пользовательский API

|Операция|Описание|
|---------|-----------|
|[Сопоставление карты совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/associate-collaboration-map)|Связывает совместную сущность с сеансом совместной работы.|
|[Начало сеанса совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/begin-collaboration-session)|Создает запись сеанса совместной работы, связанную с бизнес-сущностью, контекстом приложения и необязательными метаданными.|
|[Отмена связи с картой совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/disassociate-collaboration-map-custom-api)|Отменяет связь сопоставленной сущности с заданным сеансом совместной работы.|
|[Получение карт совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/retrieve-collaboration-maps-custom-api)|Возвращает список карт совместной работы для сеанса определенного типа сущности.|
|[Получение сеанса совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/retrieve-collaboration-session-custom-api)|Возвращает запись сеанса совместной работы на основе предоставленных параметров.|
|[Обновление карты совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/update-collaboration-map-custom-api)|Обновления записи карты совместной работы и ее метаданных, если они указаны.|
|[Обновление сеанса совместной работы](/rest/api/industry/collaboration-controls/collaboration-custom-ap-is/update-collaboration-session)|Обновления записи сеанса совместной работы и при необходимости ее метаданных.|

## <a name="rest-operations-collaboration---standard-odata-apis"></a>Операции REST: совместная работа — стандартные API OData

|Операция|Описание|
|---------|-----------|
|[Получение карты совместной работы по идентификатору](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-map-by-id)|Возвращает сведения из записи карты совместной работы.|
|[Получение метаданных совместной работы](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-metadata)|Возвращает список записей метаданных совместной работы для данной карты совместной работы или имени корневой сущности совместной работы.|
|[Получение корневого каталога совместной работы](/rest/api/industry/collaboration-controls/collaboration-standard-o-data-ap-is/get-collaboration-root)|Список всех созданных сеансов совместной работы.|

## <a name="rest-operations-settings---custom-apis"></a>Операции REST: параметры — пользовательские API

|Операция|Описание|
|---------|-----------|
|[Создание и обновление параметров](/rest/api/industry/collaboration-controls/settings-custom-ap-is/create-update-setting-custom-api)|Создает или обновляет параметр, соответствующий пути группы и имени определения параметров.|
|[Получение параметров NULL](/rest/api/industry/collaboration-controls/settings-custom-ap-is/retrieve-null-settings-custom-api)|Возвращает список определений параметров, которые не имеют значения.|
|[Получение параметров](/rest/api/industry/collaboration-controls/settings-custom-ap-is/retrieve-settings-custom-api)|Возвращает список определенных параметров или параметров в группах.|

## <a name="rest-operations-settings---standard-odata-apis"></a>Операции REST: параметры — стандартные API OData

|Операция|Описание|
|---------|-----------|
|[Удаление определения параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-definition)|Удаляет определение параметров.|
|[Удаление группы параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-group)|Удаляет группу параметров.|
|[Тип "Удалить параметры"](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-type)|Удаление типа параметров.|
|[Удаление значения параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/delete-settings-value)|Удаляет значение параметров.|
|[Получение определений параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-definitions)|Выводит список определений параметров.|
|[Получение групп параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-groups)|Список групп параметров.|
|[Получение типов параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-types)|Перечисляет типы параметров.|
|[Получение значения параметров](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/get-settings-value)|Выводит список значений параметров.|
|[Определение параметров исправления](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-definition)|Обновления определения параметров.|
|[Группа параметров исправления](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-group)|Обновления группу параметров.|
|[Тип параметров исправления](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-type)|Обновления тип параметров.|
|[Значение параметров исправления](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/patch-settings-value)|Обновления значение параметра.|
|[Определение параметров публикации](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-definition)|Создает новое определение параметров.|
|[Группа параметров публикации](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-group)|Создает новую группу параметров.|
|[Тип параметров post](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-type)|Создает новый тип параметров.|
|[Значение параметров публикации](/rest/api/industry/collaboration-controls/settings-standard-o-data-ap-is/post-settings-value)|Создает новое значение параметра.|
