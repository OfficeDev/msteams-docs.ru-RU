---
title: Upload настраиваемом приложении
description: Узнайте, как перегрузить приложение в Microsoft Teams. При тестировании и отладке приложения во время разработки часто используется боковая загрузка.
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

Вы можете Microsoft Teams приложения без публикации в организации или Teams магазине. Это имеет смысл в следующих сценариях:

* Вы хотите протестировать и отчудить приложение локально самостоятельно или с другими разработчиками.
* Вы создали приложение только для себя. Например, автоматизировать рабочий процесс.
* Вы создали приложение для небольшого набора пользователей, например рабочей группы.

## <a name="prerequisites"></a>Предварительные условия

* Создайте [пакет приложения](~/concepts/build-and-test/apps-package.md) и проверьте его [на](https://dev.teams.microsoft.com/appvalidation.html) ошибки.
* [Включить настраиваемую загрузку](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) приложения в Teams.
* Убедитесь, что ваше приложение работает и доступно с помощью HTTP.

## <a name="upload-your-app"></a>Отправка пакета приложения

Вы можете перегрузить приложение в команду, чат, собрание или для личного использования в зависимости от настройки области приложения.

1. Войдите в Teams клиент с Microsoft 365 [учетной записью разработки.](~/build-your-first-app/build-and-run.md#prerequisites)
1. Выберите **Приложения** и **выберите Upload настраиваемом приложении.**
1. Выберите пакет приложений .zip файл. Отображает диалоговое окно установки.
:::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Снимок экрана, показывающий пример диалогового Teams установки приложения.":::
1. Добавьте приложение в Teams.

## <a name="troubleshoot-upload-issues"></a>Устранение неполадок при отправке

Если приложение не перегрузит, сделайте следующее, пока проблема не решится:

1. Возвращайся к инструкциям по созданию [пакета приложений.](../../concepts/build-and-test/apps-package.md)
1. [Проверка пакета приложений снова.](https://dev.teams.microsoft.com/appvalidation.html)
1. Убедитесь, что манифест приложения соответствует последней [схеме.](../../resources/schema/manifest-schema.md)

## <a name="access-your-app"></a>Доступ к приложению

Teams предоставляет несколько способов открытия приложений. Дополнительные сведения см. [в Teams.](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a)

## <a name="update-your-app"></a>Обновление приложения

При внесении изменений кода (они отражаются в Teams в режиме реального времени) не нужно снова перегружать приложение. Однако при изменении конфигураций приложений необходимо переустановить.

## <a name="remove-your-app"></a>Удаление приложения

Чтобы удалить приложение, нажмите правой кнопкой мыши значок приложения в Teams и выберите **Uninstall**.

> [!NOTE]
> Полностью удалить личную активность бота нельзя. Если удалить приложение и добавить его еще раз, новое общение с ботом добавляется к предыдущему разговору с ним.

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Используйте приложение Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b?ui=en-us&rs=en-us&ad=us)
