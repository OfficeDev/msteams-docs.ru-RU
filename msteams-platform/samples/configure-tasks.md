---
title: Настройка задач для внешних клиентов в приложении для управления совместной работой
author: surbhigupta
description: В этом модуле вы узнаете, как настроить задачи для внешних клиентов в приложении для управления совместной работой в Microsoft Teams.
ms.localizationpriority: medium
ms.author: v-npaladugu
ms.topic: conceptual
ms.openlocfilehash: bb98ab632b335717a61499600aef01e652fd0dee
ms.sourcegitcommit: 0bb822b30739e4a532a36764dad2dbf35a81ba29
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2022
ms.locfileid: "67179335"
---
# <a name="configure-tasks-for-external-clients"></a>Настройка задач для внешних клиентов

Внешние задачи, которые могут быть назначены пользователям, которые не являются частью вашей организации или не имеют доступа к приложению, например назначение задачи клиенту.

Для включения потребуется дополнительный шаг передачи XML-строки каждому экземпляру элемента управления PCF задач, подключенного к компоненту подсети в нужной форме MDA. Строка XML — это параметризованный запрос, позволяющий элементу управления извлекать необходимые данные из таблицы, содержащего сведения о клиенте.

> [!NOTE]
> В настоящее время элементы управления совместной работы доступны только в [общедоступной предварительной версии разработчика](~/resources/dev-preview/developer-preview-intro.md).

Ниже приведены шаги по созданию внешних задач.

1. Создайте новую пользовательскую сущность, например Customer, или повторно используйте существующую сущность клиента, например "Контакты".

1. Создайте новые поля, которые будут содержать следующие сведения:
    1. Имя
    1. Электронная почта
    1. Родительский элемент (подстановка в родительскую таблицу, например "Проверки")
    > [!NOTE]
    > Сущность клиента, созданная выше, будет там, где элемент управления задачами извлекет сведения о клиенте при назначении внешней задачи. Родительское поле гарантирует, что сущность клиента связана с записью проверки.

1. Создайте XML-файл Fetch, чтобы разрешить элементу управления PCF извлекать правильные сведения о клиенте.

    **Настройка схемы XML**

    Ниже приведено определение схемы для конфигурации задач Fetch XML. Любой fetch XML должен быть разработан в соответствии со следующими требованиями:

    * Результат запроса должен возвращать следующие свойства для каждого объекта пользователя:
      * ID
      * displayname
      * по электронной почте, при необходимости используйте псевдоним.
    * Запрос должен содержать параметр **@top** , позволяющий вызываемой стороне ограничить количество результатов.
    * Запрос должен иметь **@rootEntityId** для фильтрации результатов только по связанным записям, если это необходимо.
    * Запрос должен иметь **@useName** , чтобы разрешить фильтрацию результатов по имени
    * Запрос должен иметь **@useIdentifier** , чтобы разрешить выборку только выбранных пользователей.

    **XML-схема конфигурации и пример**

    Конфигурация схемы XML извлекет данные из таблицы клиента. Вы можете настроить узел `<fetch/>` , указав собственный запрос для отображения пользователей из любой другой пользовательской таблицы.

    > [!NOTE]
    > Указанные выше атрибуты и имя сущности и атрибута в XML **PublisherPrefix_TableColumn формате** .

    ```xml
    
    <custom-tasks> 
    <custom-task id="external" name="External" for="guest"> 
    <fetch top="@top"> 
    <entity name="[Name of table, e.g. Crb2891_customer]"> 
    <attribute name="[Name of ID column, e.g. Crb2891_customerid]" alias="id" /> 
    <attribute name="[Name of primary name column, e.g. Crb2891_name]" alias="displayname" /> 
    <attribute name="[Name of email column, e.g. Crb2891_email]" alias="email" /> 
    <order attribute ="[Name of primary name column, e.g. Crb2891_name]" descending="false" /> 
    <filter type="and"> 
    <condition attribute="[Name of parent lookup column, e.g. Crb2891_parent]" operator="eq" value="@rootEntityId" /> 
    <condition attribute="[Name of primary name column, e.g. Crb2891_name]" operator="like" value="@userName" /> 
    <condition attribute="[Name of email column, e.g. Crb2891_email]" operator="like" value="@userIdentifier" /> 
    </filter> 
    </link-entity> 
    </entity> 
    </fetch> 
    </custom-task> 
    </custom-tasks> 
    
    ```

1. Привяжете элементы управления Task к подсети в классическом конструкторе форм. Нажмите **кнопку "Сохранить** ", а затем **выберите "Переключиться на классическую"**.

1. Перейдите в классический конструктор форм, пока не найдете вкладку **"Задачи** ". Дважды щелкните вложенную сетку, чтобы открыть диалоговое окно его свойства.

    :::image type="content" source="~/assets/images/collaboration-control/subgrid-property.png" alt-text="Диалоговое окно свойства Tasks":::

1. В диалоговом окне свойств задайте свойства, как показано на следующем рисунке:

    :::image type="content" source="~/assets/images/collaboration-control/tasks-property.png" alt-text="Параметры свойств tasks":::

1. Перейдите на вкладку "Элементы управления" и выберите :::image type="icon" source="~/assets/images/collaboration-control/edit-icon.png" alt-text="команду &quot;Изменить задачи"::: " в свойстве "Пользовательские задачи", чтобы добавить созданный выше код Fetch XML.

1. Вставка XML-файла fetch

    :::image type="content" source="~/assets/images/collaboration-control/set-fetchproperties.png" alt-text="Выборка параметров свойств XML":::

    :::image type="content" source="~/assets/images/collaboration-control/custom-tasksproperty.png" alt-text="Выборка параметров настраиваемых свойств XML":::

1. Нажмите **кнопку "** ОК" в разделе "Настройка свойства "Настраиваемые задачи" и задайте окна свойств.

1. Сохранение и публикация.
