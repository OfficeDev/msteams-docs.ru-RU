---
title: Публикация приложений Teams для Microsoft 365
description: Из этой статьи вы узнаете, как сделать приложения Teams с поддержкой Microsoft 365 обнаруживаемыми для пользователей в Teams, Outlook и Office.
ms.date: 05/24/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: c99114ed397b9c20f699ffee165189ec7c4fd26d
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919818"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Публикация приложений Teams для Microsoft 365

Приложения Teams с поддержкой Microsoft 365 поддерживаются для использования в рабочей области в Microsoft Teams. Вы можете распространять эти приложения для аудиторий предварительной версии,  которые используют целевые версии выпусков outlook.com и office.com, а также бета-канал сборки Outlook для windows desktop. Параметры распространения и процессы для приложений Teams с поддержкой Microsoft 365 совпадают с вариантами распространения для традиционных приложений Teams.

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

Процесс [отправки Microsoft AppSource](https://appsource.microsoft.com/) (коммерческая платформа Майкрософт) для приложений Teams, включенных для Outlook и Office, совпадает с традиционными приложениями Teams. Единственным отличием является необходимость использовать манифест приложения Teams версии [1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, который предоставляет поддержку приложений Teams, которые работают в Microsoft 365.

> [!TIP]
> Используйте портал разработчика Teams для проверки пакета [приложения](https://dev.teams.microsoft.com/validation) для устранения ошибок или предупреждений перед отправкой в магазин Teams (через [Microsoft Partner Network](https://partner.microsoft.com/)).

Чтобы приступить к работе, [см. раздел "Распространение приложения Microsoft Teams"](../concepts/deploy-and-publish/apps-publish-overview.md).
