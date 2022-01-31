---
title: Расширение Teams сообщений по всему Microsoft 365
description: Вот как обновить расширение обмена сообщениями на основе Teams для работы в Outlook
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: f019f82c4e617e3cf6aa7caa499e125dc448b1c3
ms.sourcegitcommit: abe5ccd61ba3e8eddc1bec01752fd949a7ba0cc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/31/2022
ms.locfileid: "62281744"
---
# <a name="extend-a-teams-messaging-extension-across-microsoft-365"></a>Расширение Teams сообщений по всему Microsoft 365

> [!NOTE]
> *Расширение расширения Teams для* Microsoft 365 в настоящее время доступно только в [предварительном просмотре общедоступных разработчиков](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

Расширения [обмена сообщениями на](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) основе поиска позволяют пользователям искать внешнюю систему и делиться результатами через область составить сообщение Microsoft Teams клиента. Расширив Teams приложений по [Microsoft 365 (](overview.md)предварительный просмотр), теперь можно Teams расширения обмена сообщениями на основе поиска Outlook для Windows настольных и веб-приложений.

Процесс обновления расширения обмена сообщениями на основе Teams на основе Outlook включает следующие действия:

> [!div class="checklist"]
> * Обновление манифеста приложения
> * Добавление канала Outlook для бота
> * Перезагрузите обновленное приложение в Teams

В остальном руководстве вы сможете просмотреть эти действия и показать, как просмотреть расширение обмена сообщениями как в Outlook для Windows, так и в Интернете.

## <a name="prerequisites"></a>Предварительные требования

Чтобы завершить этот учебник, вам потребуется:

 - Клиент Microsoft 365 программы разработчиков
 - Клиент песочницы, зарегистрированный *в Office 365 целевых выпусках*
 - Тестовая среда с Office приложениями, установленными с Приложения Microsoft 365 *бета-канала*
 - Visual Studio Code с расширением Teams набор средств (Предварительная версия) (необязательный)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>Подготовка расширения обмена сообщениями для обновления

Если у вас есть существующее расширение обмена сообщениями, сделайте копию или филиал производственного проекта для тестирования и обновления идентификатора приложения в манифесте приложения, чтобы использовать новый идентификатор (в отличие от идентификатора приложения производства).

Если вы хотите использовать пример кода для завершения этого руководства, выполните шаги установки в примере Teams [](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) расширения обмена сообщениями, чтобы быстро создать расширение обмена сообщениями на основе Microsoft Teams на основе поиска. Или вы можете начать с того же образца Teams расширения обмена сообщениями, обновленного для [TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365), и перейти к предварительному просмотру расширения обмена [сообщениями в Outlook](#preview-your-messaging-extension-in-outlook). Обновленный пример также доступен в Teams набор средств: *samplesNPM* >  Search **Connector** *DevelopmentView* > .

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Пример соединитетеля поиска NPM в Teams набор средств":::

## <a name="update-the-app-manifest"></a>Обновление манифеста приложения

Чтобы включить [](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `m365DevPreview` расширение Teams в Outlook, необходимо использовать схему предварительного просмотра Teams разработчика и версию манифеста.

У вас есть два варианта обновления манифеста приложения:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *палитру Команд*: `Ctrl+Shift+P`
1. Запустите команду `Teams: Upgrade Teams manifest to support Outlook and Office apps` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Действия вручную](#tab/manifest-manual)

Откройте манифест Teams приложения и обновите `$schema` следующие `manifestVersion` значения:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Если вы Teams набор средств для создания приложения расширения обмена сообщениями, вы можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру `Ctrl+Shift+P` команд и **Teams:** проверьте файл манифеста или выберите параметр из меню развертывания Teams набор средств (найдите значок Teams слева от Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams набор средств параметр &quot;Проверка файла манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавление канала Outlook для бота

В Microsoft Teams расширение обмена сообщениями состоит из веб-службы, на которой вы работаете, и манифеста приложения, который определяет, где находится веб-служба. Веб-служба воспользовалась схемой обмена сообщениями [Bot Framework SDK](/azure/bot-service/bot-service-overview) и протоколом безопасной связи Teams канала, зарегистрированного для вашего бота.

Чтобы пользователи могли взаимодействовать с расширением обмена сообщениями из Outlook, необходимо добавить в бот Outlook канал:

1. С [портала Azure](https://portal.azure.com) (или [портала Bot Framework](https://dev.botframework.com) , если вы зарегистрировались там ранее), перейдите на ресурс бота.

1. Из *Параметры* выберите **Каналы**.

1. Нажмите **кнопку Outlook**, выберите вкладку **Расширения** сообщений и нажмите кнопку **Сохранить**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Добавьте канал Outlook 'Расширения сообщений' для бота из области каналов Azure Bot":::

1. Подтвердите, Outlook канал указан вместе с Microsoft Teams в области каналов бота:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Области каналов ботов Azure с перечислением Microsoft Teams и Outlook каналов":::

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>Перезагрузите обновленное расширение обмена сообщениями в Teams

Последний шаг — загрузка обновленного расширения обмена [сообщениями (пакета](/microsoftteams/platform/concepts/build-and-test/apps-package) приложений) в Microsoft Teams. После завершения расширение обмена сообщениями появится в установленных *приложениях* из области составить сообщение.

1. Пакет Teams приложения (манифест [и значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложения) в почтовый файл. Если вы Teams набор средств для создания приложения, вы можете легко сделать это с помощью параметра пакета метаданных **zip Teams** в меню развертывания Teams набор средств:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр &quot;Пакет Teams метаданных&quot; в Teams набор средств для Visual Studio Code":::

1. Войдите Teams с учетной записью клиента в песочнице и убедитесь, что вы находитесь в общедоступных Developer Preview *,* нажав на меню ellipsis (**...**) в профиле пользователя и открыв  о том, чтобы проверить, что параметр предварительного просмотра разработчика переглушают.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Из Teams эллипсов откройте параметр &quot;About&quot; и убедитесь, что Developer Preview 'проверяется&quot;":::

1. Откройте области *Приложений* и **нажмите кнопку Upload настраиваемом** приложении, а затем **Upload для меня или моих команд**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка Upload настраиваемом приложении в области Teams &quot;Приложения&quot;":::

1. Выберите пакет приложения и нажмите кнопку *Открыть*.

После загрузки через Teams расширение обмена сообщениями будет доступно в Outlook в Интернете.

## <a name="preview-your-messaging-extension-in-outlook"></a>Просмотр расширения обмена сообщениями в Outlook

Теперь вы готовы протестировать расширение обмена сообщениями в Outlook на Windows и в Интернете. Несмотря на то, что обновленное расширение обмена сообщениями будет продолжать работать в Teams с полной поддержкой функций для расширений обмена [сообщениями, в](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) этом предварительном предварительном просмотре Outlook с включенной поддержкой есть ограничения:

* Расширения обмена сообщениями в Outlook ограничиваются контекстом [*композитной почты*](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если расширение Teams `commandBox` обмена сообщениями включается в качестве контекста в  манифесте, текущий предварительный просмотр ограничен параметром композиции почты`compose`. Запрос расширения обмена сообщениями из глобального Outlook *не* поддерживается.
* [Команды расширения обмена сообщениями](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) на основе действий не поддерживаются в Outlook. Если у приложения есть команды на основе поиска и действий, оно будет Outlook, но меню действий будет недоступным.
* Вставка более пяти [адаптивных карт](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) в электронной почте не поддерживается; Адаптивные карты v1.4 и более поздние не поддерживаются.
* [Действия карт](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) типа `messageBack`, `imBack`и `invoke``signin` не поддерживаются для вставленных карт. Поддержка ограничена `openURL`: по щелчку мыши пользователь будет перенаправлен на указанный URL-адрес на новой вкладке.

При проверке расширения обмена сообщениями можно определить источник (исходя из Teams и Outlook) запросов бота по [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, служба получает стандартный объект Bot Framework `Activity` . Одним из свойств в объекте Activity `channelId`является , `msteams` `outlook`которое будет иметь значение или , в зависимости от того, откуда возникает запрос бота. Дополнительные новости см.  [в тексте Расширения SDK на основе обмена сообщениями](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions) на основе поиска.

### <a name="outlook"></a>Outlook

Чтобы просмотреть ваше приложение, Outlook на Windows настольном компьютере, откройте Outlook войти с учетными данными для тест-клиента. Нажмите **кнопку Новая электронная почта**. Откройте меню **"Больше приложений** " на верхней ленте. Ваше расширение обмена сообщениями будет перечислены. Вы можете вызвать его оттуда и использовать его так же, как вы бы при сочинении сообщения в Teams.

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Для предварительного просмотра приложения, запущенного в Outlook в Интернете, войдите outlook.com с [помощью](https://www.outlook.com) учетных данных для тест-клиента. Щелкните **новое сообщение**. Откройте меню **"Больше приложений** " в нижней части окна композиции. Ваше расширение обмена сообщениями будет перечислены. Вы можете вызвать его оттуда и использовать его так же, как вы бы при сочинении сообщения в Teams.

## <a name="next-steps"></a>Дальнейшие действия

Outlook расширения Teams сообщений находятся в предварительном просмотре и не поддерживаются для использования в производстве. Ниже попросят распространить расширение Outlook с включенной поддержкой для предварительного просмотра аудитории для целей тестирования.

### <a name="single-tenant-distribution"></a>Распределение с одним клиентом

Outlook и Office личные вкладки с поддержкой Office могут быть распространены среди аудитории предварительного просмотра в клиенте тестовых (или производственных) одним из трех способов:

#### <a name="teams-client"></a>Teams клиента

Из меню *Apps* выберите *Управление приложениями* > **.** Для этого требуется утверждение от ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Центр администрирования

Как администратор Teams, вы можете загрузить и предварительно установить пакет приложений для клиента вашей организации из https://admin.teams.microsoft.com/. Подробные Upload в центре [администрирования Microsoft Teams пользовательских](/MicrosoftTeams/upload-custom-apps) приложений.

#### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

В качестве глобального администратора вы можете загрузить и предварительно установить пакет приложений из https://admin.microsoft.com/. Дополнительные сведения см. в Приложения Microsoft 365 и развертывании Приложения Microsoft 365 партнеров на [портале интегрированных](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) приложений.

### <a name="multi-tenant-distribution"></a>Распределение с несколькими арендаторами

Распространение в Microsoft AppSource еще не поддерживается во время предварительного предварительного просмотра Outlook с Teams сообщениями.
