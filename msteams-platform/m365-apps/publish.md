---
title: Публикация приложений Teams для Microsoft 365
description: Узнайте, как сделать приложения Teams с поддержкой Microsoft 365 доступны для пользователей в Teams, Outlook и Office с помощью одного клиента и мультитенантного распространения.
ms.date: 10/10/2022
ms.topic: conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: cfe650e676252a16c1665f078938adbff0d4c7d7
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789886"
---
# <a name="publish-teams-apps-for-microsoft-365"></a>Публикация приложений Teams для Microsoft 365

Microsoft Teams поддерживает приложения Teams с поддержкой Microsoft 365 для рабочей среды. Эти приложения можно распространять среди пользователей, которые используют версии *целевого выпуска*  (предварительная версия разработки) Outlook.com и Office.com, сборку *Бета-канала* Outlook для классического компьютера Windows и сборку Office Current Channel (предварительная версия разработки) приложения Office для Android. Варианты распространения и процессы для приложений Teams с поддержкой Microsoft 365 такие же, как и для традиционных приложений Teams.

После публикации приложение можно будет обнаружить как устанавливаемое приложение из магазинов приложений Outlook и Office, а также из магазина Teams. Приложение использует разрешения, определенные в Teams в Outlook и Office. Администраторы Teams могут [управлять доступом к приложениям Teams в Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) для пользователей в своей организации.

:::image type="content" source="images/outlook-office-app-store.png" alt-text="На снимке экрана показан пример, на котором показаны экраны установки Outlook и Office.com для приложений SurveyMonkey и MURAL Teams.":::

## <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Расширения сообщений с поддержкой Outlook можно распространять среди тестовых и рабочих клиентов несколькими способами:

### <a name="teams-client"></a>Клиент Teams

В меню **Приложения** выберите **Управление приложениями** > **Публикация приложения** > **Отправка приложения в организацию**. Для отправки приложения требуется утверждение от ИТ-администратора.

### <a name="teams-developer-portal"></a>Портал разработчика Teams

Используйте [портал разработчика Teams](https://dev.teams.microsoft.com/) для отправки и публикации приложения для своей организации. Для отправки и публикации приложения требуется утверждение от ИТ-администратора. Дополнительные сведения см. в статье [Управление приложениями с помощью портала разработчика для Microsoft Teams](../concepts/build-and-test/teams-developer-portal.md).

### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Администратор Teams может отправить и предварительно установить пакет приложения для клиента вашей организации из [Центра администрирования Teams](https://admin.teams.microsoft.com/). Дополнительные сведения см [. в статье Отправка пользовательских приложений в Центр администрирования Microsoft Teams](/MicrosoftTeams/upload-custom-apps).

### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор вы можете отправить и предварительно установить пакет приложения от [администратора Майкрософт](https://admin.microsoft.com/). Дополнительные сведения см. [в статье Тестирование и развертывание Приложения Microsoft 365 от партнеров на портале интегрированных приложений](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

## <a name="multitenant-distribution"></a>Мультиклиентское распределение

Процесс отправки [Microsoft AppSource](https://appsource.microsoft.com/) (коммерческая платформа Майкрософт) для приложений Teams, включенных для Outlook и Office, совпадает с традиционными приложениями Teams. Единственное отличие заключается в том, что вам нужно использовать манифест приложения Teams [версии 1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, который предоставляет поддержку приложений Teams, работающих в Microsoft 365.

> [!TIP]
> Используйте портал разработчика Teams для [проверки пакета приложения](https://dev.teams.microsoft.com/validation) , чтобы устранить любые ошибки или предупреждения перед отправкой в магазин Teams (через [Microsoft Partner Network](https://partner.microsoft.com/)).

Чтобы приступить к работе, ознакомьтесь с [разделом Распространение приложения Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md).
