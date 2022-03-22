---
title: Загрузка пользовательского приложения
description: Узнайте, как загрузить неопубликованное приложение в Microsoft Teams. Загрузка неопубликованного приложения часто используется при тестировании и отладке приложения во время разработки.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: 1db2f2933f2da47310468c5374b1b6a27b7fffbc
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/20/2022
ms.locfileid: "63675008"
---
# <a name="upload-your-app-in-microsoft-teams"></a>Отправка приложения в Microsoft Teams

Вы можете загрузить приложение в Microsoft Teams, не публикуя его в вашей организации или магазине Teams в следующих сценариях.

* Вы хотите протестировать и отладить приложение локально или с другими разработчиками.
* Вы создали приложение для себя, чтобы автоматизировать рабочий процесс.
* Вы создали приложение для небольшого набора пользователей, например рабочей группы.

> [!IMPORTANT]
> В настоящее время загрузка неопубликованного приложения доступна в облаке сообщества для государственных организаций (GCC), но недоступны для GCC-High и Министерства обороны (DOD).

## <a name="prerequisites"></a>Предварительные условия

* Создайте [пакет приложения](~/concepts/build-and-test/apps-package.md) и [проверьте его](https://dev.teams.microsoft.com/appvalidation.html) на наличие ошибок.
* [Включите загрузку пользовательских приложений](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) в Teams.
* Убедитесь, что приложение работает и доступно через HTTPS.

## <a name="upload-your-app"></a>Отправка пакета приложения

Вы можете загрузить приложение в команду, чат, собрание или для личного использования в зависимости от того, как вы настроили область приложения.

1. Войдите в клиент Teams с помощью [учетной записи разработчика Microsoft 365](~/build-your-first-app/build-and-run.md#prerequisites).
1. Выберите **Приложения** и нажмите **Управление приложениями**.
1. Выберите **Отправить пользовательское приложение**.
1. Выберите ZIP-файл своего пакета приложения. Появится следующий экран.

    :::image type="content" source="~/assets/images/build-your-first-app/add-teams-app.png" alt-text="Снимок экрана с примером диалогового окна установки приложения Teams.":::

1. Выберите **Добавить**, чтобы добавить приложение в Teams.

    > [!NOTE]
    > Метод `onInstallationUpdateActivityAsync()` используется для получения языкового стандарты Microsoft Teams при добавлении бота в Microsoft Teams.

## <a name="troubleshooting"></a>Устранение неполадок

Если не удается загрузить неопубликованное приложение или возникают проблемы с отправкой, проверьте следующие параметры.

1. Проверьте правильность выполнения всех инструкций по [созданию пакета приложения](../../concepts/build-and-test/apps-package.md).
1. [Проверьте свой пакет приложения](https://dev.teams.microsoft.com/appvalidation.html).
1. Убедитесь, что манифест приложения соответствует последней версии [схемы](../../resources/schema/manifest-schema.md).

## <a name="access-your-app"></a>Откройте приложение

В Teams есть несколько способов открытия приложений. Дополнительные сведения см. в статье [об открытии приложений в Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

## <a name="update-your-app"></a>Обновите приложение

При внесении изменений в код повторно загружать приложение не нужно (изменения отражаются в Teams в режиме реального времени). Однако при изменении конфигурации приложения необходимо переустановить приложение.

## <a name="remove-your-app"></a>Удаление приложения

Чтобы удалить приложение, щелкните правой кнопкой мыши значок приложения в Teams и выберите **Удалить**.

> [!NOTE]
> Вы не можете полностью удалить действия бота для личных целей. Если вы удалите приложение и добавите его снова, новое взаимодействие с ботом будет добавлено к предыдущей беседе с ним.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Использование приложения Teams](https://support.microsoft.com/office/apps-and-services-cc1fba57-9900-4634-8306-2360a40c665b)

## <a name="see-also"></a>См. также

* [Настройка параметров установки по умолчанию](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Поддержка опубликованного приложения Microsoft Teams](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
