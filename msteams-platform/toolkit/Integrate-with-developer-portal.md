---
title: Интеграция с порталом разработчика в Teams Toolkit
author: zyxiaoyuer
description: В этом модуле вы узнаете, как интегрироваться с порталом разработчика в Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
ms.openlocfilehash: b54e833f5c8292c0b426e859e63d858102860a47
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617336"
---
# <a name="integrate-with-developer-portal"></a>Интеграция с порталом разработчика

Вы можете настроить приложение и управлять этим приложением на портале разработчика в Teams Toolkit.

## <a name="to-publish-app-using-developer-portal"></a>Публикация приложения с помощью портала разработчика

Следующие действия помогут вам опубликовать приложение на портале разработчика:

1. Выберите **портал разработчика для Teams в** разделе **DEPLOYMENT**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/dev-portal-ttk.png" alt-text="Портал разработчика Teams":::

   Теперь в браузере откроется портал разработчика.

1. Войдите на портал [разработчика для Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
1. Импортируйте пакет приложения в ZIP-файле и выберите **приложение "** > **Импорт приложений"**.
1. Выберите **"Опубликовать** > **публикацию в организации"**.

## <a name="to-update-manifest-file-and-app-package"></a>Обновление файла манифеста и пакета приложения

При наличии каких-либо изменений, связанных с файлом манифеста приложения Teams, вы можете обновить манифест и снова опубликовать приложение Teams. Чтобы опубликовать приложение Teams вручную, вы можете использовать [Портал разработчика для Teams](https://dev.teams.microsoft.com/home).

1. Войдите на портал [разработчика для Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
1. Импортируйте пакет приложения в ZIP-файле и выберите **приложение "** > **Импорт приложений"**.<br>
   Необходимо заменить приложение, которое вы ранее отправили на портал разработчика.
1. Чтобы опубликовать приложение, выберите **"Опубликовать** > **публикацию в организации"**.

На портале разработчика можно выполнить следующую конфигурацию:

* Основные **сведения. В** этом разделе показано и разрешено изменять имя приложения, идентификатор приложения, описание, версию, сведения о разработчике, URL-адреса приложений, идентификатор приложения (клиента) и идентификатор Microsoft Partner Network.
* **Фирменная символика**: на этой странице отображаются сведения о значке приложения.
* **Функции** приложения: в приложение можно добавить следующие функции:
  * Личное приложение
  * Bot
  * Connector
  * Сцены
  * Приложение группы и канала
  * Расширение для обмена сообщениями
  * Расширение для собрания
  * Уведомление веб-канала действий
* **Разрешения.** В этом разделе вы можете предоставить устройствам разрешения, разрешения команды, разрешения чата или собрания, а также разрешения пользователя для вашего приложения.
* **Единый вход**. Вы можете настроить приложение для проверки подлинности пользователей с помощью единого входа.
* **Языки**: вы можете настроить или изменить язык приложения.
* **Домен**: вы можете добавить домены для загрузки приложений в клиент Teams (например, *.example.com).

## <a name="see-also"></a>См. также

* [Портал разработчика Teams](../concepts/build-and-test/teams-developer-portal.md)
* [Управление приложениями Microsoft Teams на Портале разработчика](../concepts/build-and-test/manage-your-apps-in-developer-portal.md)