---
title: Публикация приложений Teams для Microsoft 365
description: Сделайте Microsoft 365 приложения с поддержкой Teams обнаруживаемыми пользователями в Teams, Outlook и Office
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 78a2d0354028426f4de98759a501e66530cf1166
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668062"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Публикация приложений Teams для Microsoft 365

Microsoft 365 приложения с Teams поддерживаются для использования в рабочей Microsoft Teams. Вы можете распространять эти приложения для аудиторий предварительной версии,  которые используют целевые версии выпусков outlook.com и office.com, а также сборку бета-канала  Outlook для Windows desktop. Параметры распространения и процессы для Microsoft 365 приложений с Teams так же, как и для традиционных Teams приложений.

После публикации приложение будет обнаруживаться как устанавливаемое приложение из Outlook и Приложение Office, а также из Teams магазина. Ваше приложение использует разрешения, определенные в Teams Outlook и Office. Teams администраторы могут управлять [доступом к Teams приложениям](/MicrosoftTeams/manage-third-party-teams-apps) в Microsoft 365 для пользователей в своей организации.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="Outlook и Office.com устанавливают экраны для приложений SurveyMonkey и MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Outlook сообщений с поддержкой функции можно распространять в тестовые и рабочие клиенты несколькими способами:

### <a name="teams-client"></a>Клиент Teams

В меню **"Приложения**" выберите **"Управление приложениями** > **" "Опубликовать** >  приложение **" "Отправить приложение в организацию"**. Для этого требуется утверждение от ИТ-администратора.

### <a name="teams-developer-portal"></a>Teams портале разработчика

Используйте портал [Teams разработчика](https://dev.teams.microsoft.com/) для отправки и публикации приложения в организации. Для этого требуется утверждение от ИТ-администратора. Дополнительные сведения см. в статье ["Управление приложениями с помощью портала разработчика Microsoft Teams"](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Как администратор Teams вы можете отправить и предварительно установить пакет приложения для клиента вашей организации из [Teams центра администрирования](https://admin.teams.microsoft.com/). Дополнительные сведения см. в [статье "Отправка пользовательских приложений в Microsoft Teams администрирования"](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор вы можете отправить и предварительно установить пакет приложения от [администратора Майкрософт](https://admin.microsoft.com/). Дополнительные сведения см. в разделе "[Тестирование и Приложения Microsoft 365 с помощью партнеров на портале интегрированных приложений"](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Мультиклиентское распределение

Процесс [отправки Microsoft AppSource](https://appsource.microsoft.com/) (коммерческая платформа Майкрософт) для Teams приложений, включенных для Outlook и Office, совпадает с традиционными Teams приложениями. Единственным отличием является необходимость использовать манифест приложения Teams [версии 1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, который предоставляет поддержку Teams приложений, которые выполняются в Microsoft 365.

> [!TIP]
> Используйте портал Teams для проверки пакета приложения[](https://dev.teams.microsoft.com/validation), чтобы устранить ошибки или предупреждения перед отправкой в хранилище Teams (через [Microsoft Partner Network](https://partner.microsoft.com/)).

Чтобы приступить к работе, см[. раздел "Распространение Microsoft Teams приложения"](../concepts/deploy-and-publish/apps-publish-overview.md).
