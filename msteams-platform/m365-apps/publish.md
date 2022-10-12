---
title: Публикация приложений Teams для Microsoft 365
description: Узнайте, как сделать приложения Teams с поддержкой Microsoft 365 обнаруживаемыми для пользователей в Teams, Outlook и Office с помощью одного клиента и мультитенантного дистрибутива.
ms.date: 10/10/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: b225624970a380679b2b1a508bf3b4d2882de72e
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537523"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Публикация приложений Teams для Microsoft 365

Microsoft Teams поддерживает приложения Teams с поддержкой Microsoft 365 для рабочей среды. Вы можете распространять эти приложения для аудитории, использующей целевые выпуски (предварительная версия разработки) Outlook.com и Office.com, ** бета-версию канала Outlook для настольных компьютеров Windows и сборку Office Current Channel (предварительная версия для разработки) приложения Office для Android. **  Параметры распространения и процессы для приложений Teams с поддержкой Microsoft 365 совпадают с вариантами распространения для традиционных приложений Teams.

После публикации приложение будет обнаруживаться как устанавливаемое приложение из магазинов приложений Outlook и Office в дополнение к магазину Teams. Ваше приложение использует разрешения, определенные в Teams в Outlook и Office. Администраторы Teams могут [управлять доступом к приложениям Teams в Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) для пользователей в своей организации.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="На снимке экрана показан пример, на котором показаны экраны установки Outlook Office.com для приложений SurveyMonkey и MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Расширения сообщений с поддержкой Outlook можно распространять в тестовые и рабочие клиенты несколькими способами:

### <a name="teams-client"></a>Клиент Teams

В меню **"Приложения**" выберите **"Управление приложениями** > **" "Опубликовать** >  приложение **" "Отправить приложение в организацию"**. Для этого требуется утверждение от ИТ-администратора.

### <a name="teams-developer-portal"></a>Портал разработчика Teams

Используйте портал [разработчика Teams](https://dev.teams.microsoft.com/) для отправки и публикации приложения в организации. Для этого требуется утверждение от ИТ-администратора. Дополнительные сведения см. в статье ["Управление приложениями с помощью портала разработчика для Microsoft Teams"](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Администратор Teams может отправить и предварительно установить пакет приложения для клиента вашей организации из [Центра администрирования Teams](https://admin.teams.microsoft.com/). Дополнительные сведения см. в [статье "Отправка пользовательских приложений" в Центре администрирования Microsoft Teams](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор вы можете отправить и предварительно установить пакет приложения от [администратора Майкрософт](https://admin.microsoft.com/). Дополнительные сведения см. в разделе "[Тестирование и Приложения Microsoft 365 с помощью партнеров на портале интегрированных приложений"](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Мультиклиентское распределение

Процесс [отправки](https://appsource.microsoft.com/) на коммерческой платформе Майкрософт (Microsoft AppSource) для приложений Teams, включенных для Outlook и Office, совпадает с традиционными приложениями Teams. Единственным отличием является необходимость использовать манифест приложения Teams версии [1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, который предоставляет поддержку приложений Teams, которые работают в Microsoft 365.

> [!TIP]
> Используйте портал разработчика Teams для проверки пакета [приложения](https://dev.teams.microsoft.com/validation) для устранения ошибок или предупреждений перед отправкой в магазин Teams (через [Microsoft Partner Network](https://partner.microsoft.com/)).

Чтобы приступить к работе, [см. раздел "Распространение приложения Microsoft Teams"](../concepts/deploy-and-publish/apps-publish-overview.md).
