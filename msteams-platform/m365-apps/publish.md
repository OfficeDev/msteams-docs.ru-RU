---
title: Публикация Teams приложений для Microsoft 365
description: Сделайте Microsoft 365 приложения с поддержкой Teams обнаруживаемыми пользователями в Teams, Outlook и Office
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 66b5adb6162222da155318aeb818fd681a664816
ms.sourcegitcommit: 264d3cc84d6eec4ab025cf86a7a6f4865f1aed07
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65653711"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Публикация Teams приложений для Microsoft 365

Microsoft 365 приложения с Teams поддерживаются для использования в рабочей Microsoft Teams. Вы можете распространять эти приложения для аудиторий предварительной версии,  которые используют целевые версии выпусков outlook.com и office.com, а также сборку бета-канала  Outlook для Windows desktop. Параметры распространения и процессы для Microsoft 365 приложений с Teams так же, как и для традиционных Teams приложений.

После публикации приложение будет обнаруживаться как устанавливаемое приложение из Outlook и Приложение Office, а также из Teams магазина. Ваше приложение использует разрешения, определенные в Teams Outlook и Office. Teams администраторы могут управлять [доступом к Teams приложениям](/MicrosoftTeams/manage-third-party-teams-apps) в Microsoft 365 для пользователей в своей организации.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="Outlook и Office.com устанавливают экраны для приложений SurveyMonkey и MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Outlook сообщений с поддержкой функции можно распространять в тестовые и рабочие клиенты несколькими способами:

### <a name="teams-client"></a>Клиент Teams

В меню *"Приложения*" выберите *"Управление приложениями* > *" Для* публикации приложения  >  на **сайте организации**. Для этого требуется утверждение от ИТ-администратора.

### <a name="teams-developer-portal"></a>Teams портале разработчика

Используйте портал [Teams разработчика](https://dev.teams.microsoft.com/) для отправки и публикации приложения в организации. Для этого требуется утверждение от ИТ-администратора. Дополнительные сведения см. в статье ["Управление приложениями с помощью портала разработчика Microsoft Teams"](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Как администратор Teams вы можете отправить и предварительно установить пакет приложения для клиента вашей организации из [Teams центра администрирования](https://admin.teams.microsoft.com/). Дополнительные сведения см. в [статье "Отправка пользовательских приложений в Microsoft Teams администрирования"](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор вы можете отправить и предварительно установить пакет приложения от [администратора Майкрософт](https://admin.microsoft.com/). Дополнительные сведения см. в разделе "[Тестирование и Приложения Microsoft 365 с помощью партнеров на портале интегрированных приложений"](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Мультиклиентское распределение

Процесс отправки [Microsoft AppSource](https://appsource.microsoft.com/) (коммерческая платформа Майкрософт) для приложений Teams, включенных для Outlook и Office, совпадает с процессом отправки microsoft AppSource (коммерческая платформа Майкрософт) для приложений Outlook Teams и Office. Единственным отличием является необходимость использовать манифест приложения Teams версии [1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, что обеспечивает поддержку Teams  приложения, которые выполняются Microsoft 365.

> [!TIP]
> Используйте портал Teams для проверки пакета приложения[](https://dev.teams.microsoft.com/validation), чтобы устранить ошибки или предупреждения перед отправкой в хранилище Teams (через [Microsoft Partner Network](https://partner.microsoft.com/)).

Чтобы приступить к работе, см[. раздел "Распространение Microsoft Teams приложения"](../concepts/deploy-and-publish/apps-publish-overview.md).
