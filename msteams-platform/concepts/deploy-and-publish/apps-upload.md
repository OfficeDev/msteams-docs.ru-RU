---
title: Загрузка пользовательского приложения
description: Узнайте, как загрузить неопубликованное приложение в Microsoft Teams. Загрузка неопубликованного приложения часто используется при тестировании и отладке приложения во время разработки.
ms.topic: how-to
author: surbhigupta
ms.author: surbhigupta
ms.localizationpriority: high
ms.openlocfilehash: ffa7cdb0fabf07254c90590fe94fe2347c35658c
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044681"
---
# <a name="upload-your-app-in-teams"></a>Отправка приложения в Microsoft Teams

Вы можете загрузить приложение в Microsoft Teams, не публикуя его в вашей организации или магазине Teams в следующих сценариях.

* Вы хотите протестировать и отладить приложение локально или с другими разработчиками.
* Вы создали приложение для себя, чтобы автоматизировать рабочий процесс.
* Вы создали приложение для небольшого набора пользователей, например рабочей группы.

> [!NOTE]
> При загрузке неопубликованного приложения расширения обмена сообщениями несколько раз отображается несколько экземпляров для расширений обмена сообщениями.

> [!IMPORTANT]
>
> * В настоящее время загрузка неопубликованных приложений возможна только в облаке сообщества для государственных организаций (GCC) и не поддерживается в GCC-High и Министерства обороны США (DOD).
> * Установка приложения поддерживается только в классических приложениях Teams.

## <a name="prerequisites"></a>Предварительные условия

* Создайте [пакет приложения](~/concepts/build-and-test/apps-package.md) и [проверьте его](https://dev.teams.microsoft.com/appvalidation.html) на наличие ошибок.
* [Включите загрузку пользовательских приложений](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) в Teams.
* Убедитесь, что приложение работает и доступно через HTTPS.

## <a name="upload-your-app"></a>Отправка пакета приложения

Вы можете загрузить приложение в команду, чат, собрание или для личного использования в зависимости от того, как вы настроили область приложения.

1. Войдите в клиент Teams с помощью [учетной записи разработчика Microsoft 365](https://developer.microsoft.com/en-us/microsoft-365/dev-program).
1. Выберите **Приложения** > **Управление приложениями** и **Опубликовать приложение**.

    :::image type="content" source="~/assets/images/publish-app/manage-apps.png" alt-text="Публикация приложения":::

1. Выберите **Отправить пользовательское приложение**.

   :::image type="content" source="~/assets/images/publish-app/publish-app.png" alt-text="Отправка пользовательского приложения":::.

1. Выберите ZIP-файл пакета приложения.
1. Добавьте приложение в Teams в качестве требования:</br>

   a. Select **Add** to add your personal app.</br>
   b. Use the dropdown menu to add your app to a Team or chat.

    :::image type="content" source="~/assets/images/publish-app/teams-app-detail.png" alt-text="Описание приложения":::

## <a name="troubleshoot"></a>Устранение неполадок

Если приложению не удается загрузить неопубликованный файл или возникают проблемы с отправкой, проверьте следующие параметры:

1. Проверьте правильность выполнения всех инструкций по [созданию пакета приложения](../../concepts/build-and-test/apps-package.md).
1. [Проверьте свой пакет приложения](https://dev.teams.microsoft.com/appvalidation.html).
1. Убедитесь, что манифест приложения соответствует последней [схеме](../../resources/schema/manifest-schema.md).

## <a name="manage-your-apps"></a>Управление приложениями

Manage your apps allows users to have a dedicated place to manage, update and remove their apps, permissions, and subscriptions on the Teams client. The users can install the apps from **Manage your apps**.

### <a name="access-your-app"></a>Откройте приложение

Чтобы получить доступ к приложениям из раздела **Управление приложениями**, выполните следующие действия:

1. Перейдите в раздел **Приложения** и выберите **Управление приложениями** в Teams, чтобы просмотреть установленные приложения во всех каналах или для личного использования в формате списка.

    :::image type="content" source="~/assets/images/publish-app/manage-apps-list.png" alt-text="Доступ к списку приложений Teams":::

1. Выберите раскрывающийся список приложений, чтобы просмотреть все области, в которых установлено приложение.

    :::image type="content" source="~/assets/images/publish-app/app-scopes.png" alt-text="Доступ к области приложения Teams":::

1. Выберите область приложения, чтобы перейти к приложению в канале или личном представлении. Список областей включает только личную область и область Teams. Приложения, установленные в области группового чата, в настоящее время не отображаются в этом представлении.

В Teams есть несколько способов открытия приложений. Дополнительные сведения см. в статье [об открытии приложений в Teams](https://support.microsoft.com/office/access-your-apps-in-teams-0758cb09-9e85-40e7-a974-51df7734646a).

### <a name="update-your-app"></a>Обновите приложение

При внесении изменений в код повторно загружать приложение не нужно (изменения отражаются в Teams в режиме реального времени). Однако при изменении конфигурации приложения необходимо переустановить приложение.

Если для вашего приложения доступно обновление, параметр **Доступно обновление** будет включен. Чтобы обновить, выполните следующие действия:

1. Выберите **Доступно обновление**, чтобы просмотреть обновление.

     :::image type="content" source="~/assets/images/publish-app/update-available.png" alt-text="Обновление приложения Teams.":::

1. Выберите **"Просмотреть обновление"**. Появится окно с параметром обновления.
1. Нажмите кнопку **Обновить**, чтобы обновить приложение.

     :::image type="content" source="~/assets/images/publish-app/update-window.png" alt-text="Обновление приложения Teams в разделе управления приложениями.":::

     :::image type="content" source="~/assets/images/publish-app/updated-app.png" alt-text="Приложение обновлено.":::

### <a name="remove-your-app"></a>Удаление приложения

Чтобы удалить приложение из Teams, выполните следующие действия:

1. Найдите приложение в разделе **Управление приложением**.

1. Выберите &nbsp;:::image type="content" source="~/assets/images/publish-app/bin-icon.png" alt-text="Удаление приложения из Teams.":::&nbsp; в области установленного приложения.

    :::image type="content" source="~/assets/images/publish-app/uninstall-from-channel.png" alt-text="Удаление приложения из канала.":::

1. Выберите **Удалить**, чтобы удалить приложение.

    :::image type="content" source="~/assets/images/publish-app/remove-app-teams.png" alt-text="Удаление приложения из Teams.":::

> [!NOTE]
>
> * You can't remove personal bot activity entirely. If you remove the app and add it again, new communication with the bot appends to the previous conversation with it.
> * В настоящее время вы не можете перенести свое пользовательское приложение в магазин Teams. Если вы хотите разместить свое приложение в магазине Teams, см. статью [Публикация приложения в магазине Microsoft Teams](appsource/publish.md).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
>[Создание приложений для собраний Teams](../../apps-in-teams-meetings/teams-apps-in-meetings.md)

## <a name="see-also"></a>См. также

* [Настройка параметров установки по умолчанию](~/concepts/deploy-and-publish/add-default-install-scope.md)
* [Поддержка опубликованного приложения Microsoft Teams](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)
* [Добавление приложения в чат](/graph/api/chat-post-installedapps)
