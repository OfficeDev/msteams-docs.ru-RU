---
title: Выбор людей в адаптивных карточках
description: Описывает, как использовать управление выборщиком людей в адаптивных картах
localization_priority: Normal
keywords: Выбор людей адаптивных карт
ms.topic: reference
author: Rajeshwari-v
ms.author: surbhigupta
ms.openlocfilehash: b09293c26dac6721b92fcf1d574560a3da7e281a
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212477"
---
# <a name="people-picker-in-adaptive-cards"></a>Выбор людей в адаптивных карточках

>[!NOTE]
> В настоящее время выбор людей в [](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) адаптивных картах доступен в предварительном просмотре общедоступных разработчиков только для мобильных устройств и обычно доступен (GA) для настольных компьютеров.

Выбор людей помогает пользователям искать и выбирать пользователей в адаптивной карте. В адаптивную карточку, которая работает в чатах, каналах, модулях задач и вкладочных устройствах, можно добавить выборщика людей в качестве управления входными данными. Выбор людей поддерживает следующие функции:        

* Поиск одного или нескольких пользователей.
* Выбирает отдельных или нескольких пользователей. 
* Перенамеряется для одного или нескольких пользователей. 
* Prepopulates the name of selected users.

## <a name="popular-scenarios"></a>Популярные сценарии 

В следующей таблице приводится популярные сценарии для выборщика людей в адаптивных картах и соответствующие действия:

|Сценарии|Действия|
|----------|-------------------------|
|Сценарии, основанные на утверждении| Запрашивать, назначать и переназначить утверждение предназначенного пользователя в зависимости от этого требования.|
|Управление инцидентами| Отслеживание инцидентов и уведомление о незамедлительных действиях, назначение и назначение пользователю.| 
|Управление проектами| Назначение билетов или ошибок определенным пользователям.|
|Пользовательский вид| Поиск пользователей по всей организации.|

# <a name="desktop"></a>[Компьютер](#tab/desktop)

Веб-и настольный клиент поддерживают выбор людей в адаптивной карте. При поиске в Интернете, выбор людей включает в себя в текстовую линию.

### <a name="reassignment-scenario-example"></a>Пример сценария перенамерения

Пользователь A (Роберт) получает билет на задачу в канале и понимает неправильное назначение. Пользователь A перенаправит задачу, которая отправляет информацию обратно в бот. 

**Перенанаменование любой задачи**

1. Выберите **reassign,** в котором поле выбора людей предварительно заселяется именем, чтобы перенанаменовывать задачу целевому пользователю.
1. Удалите неправильное имя пользователя. 
1. Выберите предполагаемых пользователей по сценарию изображения, пользователя B (Mona) и пользователя C (Robin) для задачи. 
1. Выберите **Назначение**. После назначения информация отправляется боту. 
   Бот обновляет адаптивную карту и сообщает предполагаемым пользователям. 
 
На следующем изображении показан сценарий перенанаменования:    

![Выбор людей на рабочем столе](../../assets/images/cards/desktoppp.gif)

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

> [!NOTE]
> В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../../resources/dev-preview/developer-preview-intro.md#public-developer-preview-for-microsoft-teams) разработчиков.

Мобильные клиенты Android и iOS поддерживают выбор людей в адаптивных картах. Вы можете использовать выбор людей в мобильном телефоне для поиска и выбора пользователя для улучшения пользовательского интерфейса. Опыт поиска похож на любой другой пользовательский интерфейс выбора в мобильном телефоне.

### <a name="reassignment-scenario-example"></a>Пример сценария перенамерения

Пользователь A (Роберт) получает билет на задачу в канале и понимает неправильное назначение. Пользователь A перенаправит задачу, которая отправляет информацию обратно в бот. 

**Перенанаменование любой задачи**

1. Выберите **reassign,** в котором поле выбора людей предварительно заселяется именем, чтобы перенанаменовывать задачу целевому пользователю.
1. Удалите неправильное имя пользователя.
1. Выберите предполагаемых пользователей по сценарию изображения, пользователя B (Mona) и пользователя C (Robin) для задачи.
1. Нажмите кнопку **Готово**.
1. Выберите **Назначение**. После назначения информация отправляется боту. 
   Бот обновляет адаптивную карту и сообщает предполагаемым пользователям. 

На следующем изображении показан сценарий перенанаменования: 

![Выбор людей на мобильных устройствах](../../assets/images/cards/mobilepp.gif)

---

## <a name="implement-people-picker"></a>Реализация выборки людей

Выбор людей реализуется в качестве расширения управления [Input.ChoiceSet.](https://adaptivecards.io/explorer/Input.ChoiceSet.html) Управление входом включает следующие выборки:   

* Dropdown, например расширенный выбор.
* Кнопка "Радио", например один выбор.
* Флажки, например несколько выборов.  

> [!NOTE]
> Управление `Input.ChoiceSet` основано на `style` свойствах и `isMultiSelect` свойствах.  

### <a name="update-schema"></a>Обновление схемы

В схему добавлены следующие свойства, которые позволяют использовать выбор людей `Input.ChoiceSet` на карте:  

#### <a name="inputchoiceset-control"></a>Управление Input.ChoiceSet

|Свойство |Тип |Обязательный |Описание |
|----|----|----|----|
|**choices.data** |**Data.Query** |Нет |Включает динамическое автоматическое завершение для различных типов пользователей, извлекая результаты из указанного набором данных. |

#### <a name="dataquery"></a>Data.Query

|Свойство |Тип |Обязательный |Описание|
|--|--|--|--|
|**набор данных** |String |Да |Тип данных, которые необходимо получать динамически.|   

#### <a name="dataset"></a>набор данных
В следующей таблице предопределяются значения в качестве **наборов** данных для людей, которые выбирают:   

|набор данных|Область поиска
|--|--|
|**graph.microsoft.com/users** |Поиск всех участников по всей организации.|
|**graph.microsoft.com/users?scope=currentContext** |Поиск внутри участников текущего разговора, таких как чат или канал, в который отправляется конкретная карта.|        

### <a name="example"></a>Пример
Пример кода для создания выборщика людей с помощью поиска в организации:

```json 
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

На следующем изображении иллюстрируется выбор людей в адаптивных картах с помощью поиска в организации:

![Поиск оргвыбиратель людей](../../assets/images/cards/peoplepicker-org-search.png)

Чтобы включить поиск в списке участников беседы, используйте соответствующий набор данных, определенный в таблице [наборов](#dataset) данных. `isMultiSelect` свойство используется для обеспечения выбора нескольких пользователей в области управления. По умолчанию установлено значение false, и этот параметр позволяет выбрать только одного пользователя.

### <a name="data-submission"></a>Отправка данных

Вы можете использовать `Action.Submit` или `Action.Execute` отправлять выбранные данные в бот. Полезной `invoke` нагрузкой, полученной на боте, является список azure AD ID или ID, предоставляемых в статическом списке.
В подборщике людей, когда пользователь выбран в области управления, его значение `Azure AD ID` отослано обратно. Строка `Azure AD ID` и уникально идентифицирует пользователя в каталоге.

Формат значения, представленного боту, зависит от значения `isMultiSelect` свойства:

|значение `isMultiSelect`|Формат|
|--|--|
|false _(один выбор)_|<selected_Azure_AD_ID>|
|true _(multi select)_|<selected_Azure_AD_ID_1>,<selected_Azure_AD_ID_2> <selected_Azure_AD_ID_3>|  

С помощью предварительного предварительного выборщика людей `Azure AD ID` соответствующий пользователь. 

## <a name="preselection-of-user"></a>Предварительное отсев пользователя

Выбор людей поддерживает предварительную выборку пользователя в области управления при создании и отправке адаптивной карты. `Input.ChoiceSet` поддерживает `value` свойство, которое используется для предварительного предварительного отсеять пользователя. Формат этого свойства такой же, как и представленный формат значения `value` в [представлении данных.](#data-submission)  
В следующем списке содержится информация для предварительного отсеяний пользователей:

* Для одного пользователя в области управления укажите пользователя `Azure AD ID` в качестве `value` . 
* Для нескольких пользователей, таких как `isMultiSelect` `true` это, укажите строку s, разделенную `Azure AD ID` запятой.  

В следующем примере описаны предварительные действия одного пользователя:

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "value": "<Azure AD ID 1>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```  

В следующем примере описывается предварительное переизбрание нескольких пользователей:

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true,
            "value": "<Azure AD ID 1>,<Azure AD ID 2>,<Azure AD ID 3>"
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```
 
## <a name="static-choices"></a>Статические решения

Статические варианты поддерживают сценарии, в которых пользовательские профили должны быть вставлены в предопределяемые наборы данных. `Input.ChoiceSet` поддерживает `choices` статическое указание в json. Статичный выбор используется для создания выбора, из которого пользователь может выбрать.

> [!NOTE]
> Статический `choices` используется с динамическими наборами данных. 

Выбор состоит из `title` и `value` . При их использования вместе с выборщиком людей эти варианты переводятся на профили пользователей, которые имеют имя и `title` `value` идентификатор. Эти настраиваемые профили также являются частью результатов поиска, когда запрос поиска совпадает с указанным `title` .    
В следующем примере описываются статические варианты: 

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "size": "Medium",
            "weight": "Bolder",
            "text": "People Picker with Org search enabled"
        },
        {
            "type": "Input.ChoiceSet",
            "choices": [
                {
                    "title": "Custom Profile 1",
                    "value": "Profile1"
                },
                {
                    "title": "Custom Profile 2",
                    "value": "Profile2"
                }
            ],
            "choices.data": {
                "type": "Data.Query",
                "dataset": "graph.microsoft.com/users"
            },
            "id": "people-picker",
            "isMultiSelect": true
        }
    ],
    "actions": [
        {
            "type": "Action.Submit",
            "title": "Submit"
        }
    ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

На следующем изображении иллюстрируется выбор людей в адаптивных картах со статичными решениями в организации поиска:

![Статичный выбор выбора выбора людей](../../assets/images/cards/peoplepicker-static-choice.png)


Вы можете реализовать выбор людей для эффективного управления задачами в различных сценариях.  

## <a name="see-also"></a>См. также

[Справка по картам](cards-reference.md)
