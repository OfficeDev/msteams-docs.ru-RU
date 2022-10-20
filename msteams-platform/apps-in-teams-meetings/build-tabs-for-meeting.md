---
title: Создание вкладок для собрания
author: surbhigupta
description: Узнайте, как создавать вкладки для чата собрания, боковой панели собрания и этапа собрания в собрании Microsoft Teams.
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: d86f0931cb6338ef331f2afe3a4a5fdb217bb316
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615433"
---
# <a name="build-tabs-for-meeting"></a>Создание вкладок для собрания

У каждой команды есть разные способы взаимодействия и совместной работы. Для выполнения различных задач настройте Teams с использованием приложений для собраний. Включите приложения для собраний Teams и настройте их доступность в области собраний в манифесте приложения.

## <a name="tabs-in-teams-meetings"></a>Вкладки в собраниях Teams

Вкладки позволяют участникам собрания получать доступ к службам и содержимому в определенном пространстве собрания. Если вы еще не знакомы с разработкой вкладок Microsoft Teams, см. вкладки ["Сборка" для Teams](/microsoftteams/platform/tabs/what-are-tabs).

Перед созданием вкладки собрания важно узнать о поверхностях, доступных для представления чата собрания, представления сведений о собрании, представления на боковой панели собрания и представления стадии собрания.

### <a name="meeting-details-view"></a>Представление сведений о собрании

1. В календаре выберите собрание, для которого нужно добавить вкладку.
1. Select the **Details** tab and select :::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::. Появится галерея приложений.

   :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="На этом снимке экрана показан интерфейс приложения для предварительного собрания в собрании Teams.":::

1. В коллекции приложений выберите приложение, которое вы хотите добавить, и выполните необходимые действия. Вкладка добавляется на страницу сведений о собрании.

# <a name="desktop"></a>[Компьютер](#tab/desktop)

На следующем рисунке показана вкладка, добавленная на страницу сведений о собрании в настольном клиенте Teams:

   :::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="На снимке экрана показаны классические вкладки Teams в представлении сведений о собрании в собрании Teams.":::

# <a name="mobile"></a>[Мобильные устройства](#tab/mobile)

На следующем рисунке показана вкладка, добавленная на страницу сведений о собрании в мобильном клиенте Teams:

   :::image type="content" source="../assets/images/mobile-tab.png" alt-text="На снимке экрана показаны мобильные вкладки Teams в представлении сведений о собрании в собрании Teams.":::

---

### <a name="meeting-chat-view"></a>Представление чата собрания

1. На панели чата Teams выберите представление чата собрания.

1. Выберите :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: и отобразится галерея приложений.

1. В коллекции приложений выберите приложение, которое вы хотите добавить, и выполните необходимые действия. Вкладка добавляется в чат собрания.

   :::image type="content" source="../assets/images/apps-in-meetings/meeting-chat-view.png" alt-text="Снимок экрана: представление чата собрания в собрании Teams.":::

### <a name="meeting-side-panel-view"></a>Представление боковой панели собрания

1. Во время собрания можно **выбрать "** :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: Приложения" в окне собрания Teams, чтобы добавить приложения к собранию.

   :::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="На этом снимке экрана показано, как добавить приложение в окне собрания Teams.":::

1. В коллекции приложений выберите приложение, которое вы хотите добавить, и выполните необходимые действия. Приложение добавляется на панель на стороне собрания.

   :::image type="content" source="../assets/images/side-panel-view.png" alt-text="На этом снимке экрана показано представление боковой панели со списком приложений.":::

### <a name="meeting-stage-view"></a>Представление стадии собрания

1. После добавления вкладки на панель на стороне собрания теперь можно согласиться на глобальный общий доступ к приложениям.

1. Это приводит к отрисовке вкладки на этапе для каждого участника собрания.

   :::image type="content" source="../assets/images/meeting-stage-view.png" alt-text="На этом снимке экрана показано представление этапа собрания приложения, которое вы предоставили собранию.":::

### <a name="apps-in-channel-meeting"></a>Приложения на собрании канала

Собрание общедоступного запланированного канала содержит тот же список приложений, что и его родительская команда. Установка приложения на собрание канала также делает его доступным в родительской команде и наоборот.

Однако экземпляры вкладок в собрании канала отделены от вкладок в самом канале. Например, предположим, что канал *разработки* имеет *вкладку Polly* . Если вы создаете *в* этом канале резервное собрание, на этом собрании не будет вкладки *Polly* , пока вы не добавите вкладку [в собрание явным образом](#meeting-details-view).

На собраниях общедоступного запланированного канала после добавления вкладки собрания можно выбрать объект собрания на странице сведений о собрании, чтобы получить доступ к вкладке.

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="После собрания":::

> [!NOTE]
> На мобильных устройствах анонимные пользователи не могут получить доступ к приложениям на запланированных собраниях общедоступного канала.

### <a name="app-manifest-settings-for-tabs-in-meeting"></a>Параметры манифеста приложения для вкладок на собрании

[Обновите манифест приложения](/microsoftteams/platform/resources/schema/manifest-schema), используя соответствующее свойство контекста, чтобы настроить различные представления вкладок. Возможности приложения для собраний объявляются в манифесте приложения с помощью областей и массивов контекста в разделе configurableTabs.

#### <a name="scope"></a>Область

Область определяет, кто может получить доступ к приложениям.

* `groupchat` Область  делает приложение доступным в области группы и позволяет добавлять его в звонок или собрание (запланированное частное собрание или мгновенные собрания).

* `team` Область  делает ваше приложение доступным в области группы и позволяет добавить приложение в группу, канал или запланированное собрание канала.

#### <a name="context"></a>Context

Свойство `context` определяет, доступно ли приложение в определенном представлении после установки и настройки. Ниже приведены значения для свойства `context` , из которого можно использовать все или некоторые значения:

|Значение|Описание|
|---|---|
| **channelTab** | Вкладка в заголовке канала команды. |
| **privateChatTab** | Вкладка в заголовке группового чата между группой пользователей, а не в контексте команды или собрания. |
| **meetingChatTab** | Вкладка в заголовке группового чата между группой пользователей для запланированного собрания. Вы можете указать **meetingChatTab** или **meetingDetailsTab**, чтобы убедиться, что приложения работают на мобильных устройствах. |
| **meetingDetailsTab** | Вкладка в заголовке представления сведений о собрании календаря. Вы можете указать **meetingChatTab** или **meetingDetailsTab**, чтобы убедиться, что приложения работают на мобильных устройствах. |
| **meetingSidePanel** | Панель на собрании, открытая через единую панель (панель U-bar). |
| **meetingStage** | Приложение из `meetingSidePanel` можно продемонстрировать на сцене собрания. Это приложение нельзя использовать в клиентах на мобильных устройствах или клиентах комнат Teams. |

#### <a name="configure-tab-app-for-a-meeting"></a>Настройка приложения табуляции для собрания

Приложения на собраниях могут использовать следующие контексты: `meetingChatTab`, `meetingDetailsTab`, `meetingSidePanel` и `meetingStage`. После того как участник собрания установит приложение и настроит вкладку в собрании, все целевые другие контексты приложения для данного собрания начинают отображать вкладку.

Следующий фрагмент кода является примером настраиваемой вкладки, используемой в приложении для собраний Teams:

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```

---

#### <a name="other-examples"></a>Другие примеры

Контекст по умолчанию для вкладок (если не указан) имеет значение:  

```json
"context":[ 
  "channelTab", 
  "privateChatTab", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Чтобы приложение не отображались в чатах, не включаемом в группу собраний, необходимо задать следующий контекст:

```json
"context":[ 
  "meetingSidePanel", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

Только для работы с панелью на стороне собрания:  

```json
"context":[ 
  "meetingSidePanel" 
     ] 
```

### <a name="advanced-tab-sdk-apis"></a>API-интерфейсы пакета SDK для расширенных вкладок

Клиентский пакет SDK JavaScript для Microsoft Teams — это полнофункциональный пакет SDK, используемый для создания вкладок с помощью JavaScript. Используйте последнюю версию TeamsJS (версии 2.0 или более поздней) для работы в Teams, Office и Outlook. Дополнительные сведения см. в статье [Пакет SDK клиента JavaScript для Teams](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit).

### <a name="frame-context"></a>Контекст фрейма

Библиотека JavaScript Microsoft Teams предоставляет frameContext, в котором URL-адрес вкладки собрания загружается в API getContext. Возможные значения frameContext: content, task, setting, remove, sidePanel и meetingStage. Это позволяет создавать настраиваемые интерфейсы в зависимости от того, где отображается приложение. Например, отображение определенного пользовательского интерфейса `meetingStage` , ориентированного на совместную работу, в пользовательском интерфейсе подготовки собрания и другом пользовательском интерфейсе на вкладке чата (`content`). Дополнительные сведения см. в [разделе getContext API](/microsoftteams/platform/tabs/how-to/access-teams-context?tabs=teamsjs-v2).

## <a name="code-sample"></a>Пример кода

|Название примера | Описание | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| Приложение для собраний | Демонстрирует, как использовать приложение генератора маркеров собраний для запроса маркера. Маркер создается последовательно, чтобы каждый участник обладал равными возможностями участия в собрании. Маркер удобен в таких сценариях, как собрания Scrum и сеансы вопросов с ответами. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| Пример сцены собрания | Пример приложения для отображения вкладки на сцене собрания для совместной работы | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| Боковая панель собрания | Пример приложения для демонстрации добавления повестки дня на боковой панели во время собрания | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|
| Уведомление на собрании | Демонстрирует реализацию уведомлений на собрании с помощью бота. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| Подписывание документа на собрании | Демонстрирует реализацию приложения Teams для подписи документов. Включает предоставление общего доступа к определенному содержимому приложения на этапе, единый вход Teams и представление стадии для конкретного пользователя. | [Просмотр](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | Н/Д |

> [!NOTE]
>
> * Приложения для собраний (боковая панель и этап собрания) поддерживаются в настольном клиенте Teams.
> * Приложения для собраний (боковая панель и этап собрания) в веб-клиенте Teams поддерживаются только в том случае, если [включена предварительная версия для разработчиков](/microsoftteams/platform/resources/dev-preview/developer-preview-intro#enable-developer-preview).

## <a name="step-by-step-guides"></a>Пошаговые руководства

* Следуйте [пошаговым инструкциям](../sbs-meeting-token-generator.yml), чтобы создать маркер собрания в своем собрании Teams.
* Следуйте [пошаговое руководство,](../sbs-meetings-sidepanel.yml) чтобы создать панель на стороне собрания в собрании Teams.
* Следуйте [пошаговым инструкциям](../sbs-meetings-stage-view.yml), чтобы поделиться представлением сцены собрания в своем собрании Teams.
* Следуйте [пошаговое руководство,](../sbs-meeting-content-bubble.yml) чтобы создать уведомление о собрании в собрании Teams.

## <a name="see-also"></a>См. также

* [Рекомендации по проектированию уведомлений на собрании](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Поток проверки подлинности Teams для вкладок](../tabs/how-to/authentication/auth-flow-tab.md)
* [Руководства по проектированию общего интерфейса сцены собрания](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [Добавление приложений для собраний с помощью Microsoft Graph](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
