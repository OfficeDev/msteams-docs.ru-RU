---
title: Тестирование разрешений на согласие для определенных ресурсов в Teams
description: Подробные сведения о тестировании согласия на использование ресурсов в Teams с помощью postman
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: команды авторизации OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 0d3d1c895c77bb417a9fdd84e319103485aa8944
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634711"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>Тестирование разрешений на согласие для определенных ресурсов в Teams

Согласие на использование ресурсов — это интеграция Microsoft Teams и Graph API, которая позволяет приложению использовать конечные точки API для управления определенными группами в организации. Дополнительные сведения см. в [сайте Resource-specific consent (RSC) — API Microsoft Teams Graph.](resource-specific-consent.md)

> [!NOTE]
> Чтобы проверить разрешения RSC, файл манифеста приложения Teams должен включать ключ **webApplicationInfo,** населённый следующими полями:
>
> - **id.** ID приложения Azure AD см. в приложении [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).
> - **ресурс.** Любая строка см. в заметке  [в манифесте приложения Update your Teams](resource-specific-consent.md#update-your-teams-app-manifest)
> - **Разрешения приложения:** разрешения RSC для вашего приложения см. в [приложении Resource-specific Permissions.](resource-specific-consent.md#resource-specific-permissions)

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

> [!IMPORTANT]
> В манифесте приложения включите только разрешения RSC, которые необходимо иметь вашему приложению.

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>Тестирование добавленных разрешений RSC с помощью приложения Postman

Чтобы проверить, чтят ли разрешения RSC полезной нагрузкой запроса API, необходимо скопировать тестовый код [RSC JSON](test-rsc-json-file.md) в локальной среде и обновить следующие значения:

* `azureADAppId`: ID приложения Azure AD вашего приложения
* `azureADAppSecret`: Секрет приложения Azure AD (пароль)
* `token_scope`. Область, необходимая для получения маркера — задай значение https://graph.microsoft.com/.default
* `teamGroupId`: Вы можете получить id группы группы из клиента Teams следующим образом:

  > [!div class="checklist"]
  >
  > * В клиенте Teams выберите **Teams из** левой панели навигации .
  > * Выберите команду, в которой установлено приложение из отсевного меню.
  > * Выберите **значок Дополнительные** параметры (&#8943;)
  > * Выберите **Получить ссылку на команду** 
  > * Скопируйте и сохраните **значение groupId** из строки.

### <a name="use-postman"></a>Использование Postman

1. Откройте [приложение Postman.](https://www.postman.com)
2. Выберите **файл импорта**  >    >  **файлов,** чтобы загрузить обновленный JSON-файл из среды.  
3. Выберите **вкладку Collections.** 
4. Выберите шеврон **>** рядом с **тестом RSC,** чтобы расширить представление сведений и просмотреть запросы API.

Выполните всю коллекцию разрешений для каждого вызова API. Разрешения, указанные в манифесте приложения, должны быть успешными, а те, которые не указаны, должны не работать с кодом состояния HTTP 403. Проверьте все коды состояния отклика, чтобы подтвердить, что поведение разрешений RSC в вашем приложении соответствует ожиданиям.

> [!NOTE]
> Чтобы протестировать конкретные вызовы DELETE и READ API, добавьте эти сценарии экземпляров в файл JSON.

## <a name="test-revoked-rsc-permissions-using-postman"></a>Тестирование отозванных разрешений RSC с помощью [Postman](https://www.postman.com/)

1. Удалить приложение из определенной группы.
2. Следуйте шагам [для тестовых добавленных разрешений RSC с помощью Postman](#test-added-rsc-permissions-using-the-postman-app).
3. Проверьте все коды состояния отклика, чтобы подтвердить, что конкретные вызовы API успешно сбой с **кодом состояния HTTP 403**.

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [API и команды Microsoft Graph](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

