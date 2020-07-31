---
title: Тестирование согласия конкретного ресурса в Teams
description: Details проверка согласия конкретного ресурса в Teams с использованием POST
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: Диаграмма Microsoft Teams SSO единого входа OAuth RSC POST
ms.openlocfilehash: a7384222e5e4cba164f918186ce53b4c1b702016
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531268"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a>Проверка разрешений согласия для определенных ресурсов в Teams

Согласие с конкретными ресурсами (RSC) — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными командами в Организации. *Ознакомьтесь*с разделом[согласия для определенных ресурсов (RSC) — API Microsoft Teams Graph](resource-specific-consent.md).  

> [!NOTE]
>Для тестирования разрешений RSC файл манифеста приложения Teams должен содержать ключ **webApplicationInfo** , заполненный следующими полями:
>
> - **ID** — идентификатор приложения Azure AD, *см* . [Регистрация приложения на портале Azure AD](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ресурс** — любая строка, *просмотрев* заметку в [статье обновление манифеста приложения Teams](resource-specific-consent.md#update-your-teams-app-manifest)
> - **разрешения приложения** — сведения о разрешениях RSC для вашего *приложения: сведения* о разрешениях для [ресурсов](resource-specific-consent.md#resource-specific-permissions).

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

>[!IMPORTANT]
>В манифесте приложения включите только разрешения RSC, которые должно иметь ваше приложение.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Тестирование добавленных разрешений RSC с использованием почтовых приложений

Чтобы проверить, учитываются ли разрешения RSC в полезных данных запроса API, необходимо скопировать [код теста RSC JSON](test-rsc-json-file.md) в локальную среду и обновить следующие значения:

1. `azureADAppId`— Идентификатор приложения Azure AD в приложении.
1. `azureADAppSecret`— ваш секрет приложения Azure AD (пароль)
1. `token_scope`— область требуется для получения маркера, чтобы задать значениеhttps://graph.microsoft.com/.default
1. `teamGroupId`— Идентификатор группы Teams можно получить из клиента Teams следующим образом:

> [!div class="checklist"]
>
> * В клиенте Teams выберите **Teams (Teams** ) в крайней левой панели навигации.
> * Выберите из раскрывающегося меню команду, в которой установлено приложение.
> * Выбор значка " **Дополнительные параметры** " (&#8943;)
> * Выберите команду " **получить ссылку на группу** " 
> * Скопируйте и сохраните значение **groupId** из строки.

### <a name="using-postman"></a>Использование POST

> [!div class="checklist"]
>
> * Откройте приложение [POST](https://www.postman.com) .
> * Выберите **файл импорт файла**  =>  **Import**  =>  **импорта** , чтобы отправить обновленный файл JSON из вашей среды.  
> * Перейдите на вкладку **коллекции** . 
> * Выберите Шеврон (>) рядом с элементом **тест RSC** , чтобы развернуть представление сведений и просмотреть запросы API.

Выполните всю коллекцию разрешений для каждого вызова API. Разрешения, указанные в манифесте приложения, должны выполняться успешно, в то время как они не задаются должным образом, с кодом состояния HTTP 403. Проверьте все коды состояния ответа, чтобы убедиться в том, что поведение RSC в вашем приложении соответствует ожиданиям.

>[!NOTE]
>Чтобы протестировать конкретные вызовы API для удаления и чтения, добавьте эти сценарии в JSON-файл.

## <a name="test--revoked-rsc-permissions-using-postman"></a>Проверка отозванных разрешений RSC с помощью [POST](https://www.postman.com/)

> [!div class="checklist"]
>
> * Удаление приложения из определенной команды.
> * Выполните описанные выше действия для теста, чтобы [Добавить разрешения RSC с помощью POST](#test-added-rsc-permissions-using-the-postman-app).
> * Проверьте все коды состояния ответа, чтобы убедиться в том, что определенные вызовы API, которые завершились успешно, с кодом состояния HTTP 403.

> [!div class="nextstepaction"]
>
> [Дополнительные сведения о API Graph и Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
