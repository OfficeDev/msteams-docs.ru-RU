---
title: Upload пользовательское приложение
description: Узнайте, как перезагрузить приложение в Microsoft Teams. Боковая загрузка является обычной при тестировании и отладке приложения во время разработки.
ms.topic: how-to
author: KirtiPereira
ms.author: surbhigupta
ms.openlocfilehash: 39e94317ceb615ecd7d5481276ffafed5afe5cde
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565195"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Upload приложение в Microsoft Teams

Вы можете Microsoft Teams приложения без публикации в вашей организации или Teams магазине. Это имеет смысл в следующих сценариях:

* Вы хотите протестировать и отладить приложение локально самостоятельно или с другими разработчиками.
* Вы создали приложение только для себя. Например, автоматизировать рабочий процесс.
* Вы создали приложение для небольшого набора пользователей, например рабочей группы.

## <a name="prerequisites"></a>Предварительные требования

* Создайте пакет [приложений и](~/concepts/build-and-test/apps-package.md) [проверяйте его на](https://dev.teams.microsoft.com/appvalidation.html) ошибки.
* [Включите пользовательскую загрузку приложения](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) в Teams.
* Убедитесь, что ваше приложение работает и доступно через HTTPs.

## <a name="upload-your-app"></a>Отправка пакета приложения

Вы можете настроить приложение в группу, общаться, встречаться или для личного пользования в зависимости от того, как вы настроили область действия приложения.

1. Войдите в систему к Teams с вашей [учетной Microsoft 365 развития.](~/build-your-first-app/build-and-run.md#prerequisites)
1. Выберите **приложения** и **выберите Upload пользовательское приложение.**
1. Выберите пакет приложений .zip файл. Установка диалоговых дисплеев.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Скриншот, показывающий пример Teams установки диалога.":::
1. Добавьте приложение в Teams.

## <a name="troubleshoot-upload-issues"></a>Устранение неполадок при отправке

Если ваше приложение не может перегрузиться, сделайте следующее до тех пор, пока проблема не решится:

1. Вернитесь через инструкции [по созданию пакета приложений.](../../concepts/build-and-test/apps-package.md)
1. [Еще раз проиймите](https://dev.teams.microsoft.com/appvalidation.html) пакет приложений.
1. Убедитесь, что манифест приложения соответствует [последней схеме.](../../resources/schema/manifest-schema.md)

## <a name="access-your-app"></a>Доступ к приложению

Teams предоставляет несколько способов открытия приложений. Для получения дополнительной информации [смотрите доступ к приложениям в Teams.](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)

## <a name="update-your-app"></a>Обновление приложения

Вам больше не нужно снова входить в приложение, если вы внести изменения в код (они отражены в Teams в режиме реального времени). Однако необходимо переустановить настройки, если вы измените конфигурацию приложения.

## <a name="remove-your-app"></a>Удалить приложение

Чтобы удалить приложение, нажмите на значок приложения в Teams и **выберите Uninstall.**

> [!NOTE]
> Вы не можете удалить личную активность бота полностью. Если вы удалите приложение и добавите его снова, новая связь с ботом пристройки к предыдущему разговору с ним.

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Используйте свое Teams приложение](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
