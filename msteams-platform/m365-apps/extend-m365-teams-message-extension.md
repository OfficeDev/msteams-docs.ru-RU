---
title: Расширение Teams сообщений по всему Microsoft 365
description: Вот как обновить расширение обмена сообщениями на основе Teams для работы в Outlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 743181b11d595aabdd9d7972674e843b598826af
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/08/2022
ms.locfileid: "63356009"
---
# <a name="extend-a-teams-messaging-extension-across-microsoft-365"></a>Расширение Teams сообщений по всему Microsoft 365

> [!NOTE]
> *Расширение расширения Teams для* Microsoft 365 в настоящее время доступно только в [предварительном просмотре общедоступных разработчиков](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

Расширения обмена сообщениями [на](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) основе поиска позволяют пользователям искать внешнюю систему и делиться результатами через область составить сообщение Microsoft Teams клиента. Расширив Teams приложений Microsoft 365 (предварительный просмотр[)](overview.md), теперь вы можете Teams расширения обмена сообщениями на основе поиска в Outlook для Windows настольных и веб-приложений.

Процесс обновления расширения обмена сообщениями на основе Teams на основе Outlook включает следующие действия:

> [!div class="checklist"]
> * Обновление манифеста приложения
> * Добавление канала Outlook для бота
> * Перезагрузите обновленное приложение в Teams

В остальном руководстве вы сможете просмотреть эти действия и показать, как просмотреть расширение обмена сообщениями как в Outlook для Windows, так и в Интернете.

## <a name="prerequisites"></a>Предварительные требования

Чтобы завершить этот учебник, вам потребуется:

 - Клиент Microsoft 365 программы разработчиков
 - Клиент песочницы, зарегистрированный *в Office 365 целевых выпусков*
 - Тестовая среда с Office приложениями, установленными с Приложения Microsoft 365 *бета-канала*
 - Microsoft Visual Studio с расширением Teams набор средств (Preview) (необязательный)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-messaging-extension-for-the-upgrade"></a>Подготовка расширения обмена сообщениями для обновления

Если у вас есть существующее расширение обмена сообщениями, сделайте копию или филиал производственного проекта для тестирования и обновления идентификатора приложения в манифесте приложения, чтобы использовать новый идентификатор (в отличие от идентификатора приложения производства).

Если вы хотите использовать пример кода для завершения этого руководства, выполните действия по настройке в примере Teams расширения обмена сообщениями, чтобы быстро создать расширение обмена сообщениями на основе Microsoft Teams на основе поиска.[](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) Или вы можете начать с того же образца Teams расширения обмена сообщениями, обновленного для [TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365), и перейти к предварительному просмотру расширения обмена [сообщениями в Outlook](#preview-your-messaging-extension-in-outlook). Обновленный пример также доступен в Teams набор средств: *samplesNPM* >  Search **Connector** *DevelopmentView* > .

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

Если вы Teams набор средств для создания приложения расширения обмена сообщениями, вы можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру `Ctrl+Shift+P` команд и **найдите Teams:** Проверьте файл манифеста или выберите параметр из меню развертывания Teams набор средств (найдите значок Teams слева от Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams набор средств параметр &quot;Проверка файла манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавление канала Outlook для бота

В Microsoft Teams расширение обмена сообщениями состоит из веб-службы, на которой вы работаете, и манифеста приложения, который определяет, где находится ваша веб-служба. Веб-служба воспользовалась схемой обмена сообщениями [Bot Framework SDK](/azure/bot-service/bot-service-overview) и протоколом безопасной связи Teams канала, зарегистрированного для вашего бота.

Чтобы пользователи могли взаимодействовать с расширением обмена сообщениями из Outlook, необходимо добавить в бот Outlook канал:

1. С [Microsoft Azure](https://portal.azure.com) портала (или [портала Bot Framework](https://dev.botframework.com), если вы ранее там зарегистрировались), перейдите на ресурс бота.

1. Из *Параметры* выберите **Каналы**.

1. Нажмите **кнопку Outlook**, выберите вкладку **Расширения** сообщений и нажмите кнопку **Сохранить**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Добавление канала Outlook &quot;Расширения сообщений&quot; для бота из области каналов Azure Bot":::

1. Подтвердите, Outlook канал указан вместе с Microsoft Teams в области каналов бота:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Области каналов ботов Azure с перечислением Microsoft Teams и Outlook каналов":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Регистрация Microsoft Azure Active Directory приложения Azure AD для SSO

> [!NOTE]
> Вы можете пропустить этот шаг, если вы используете образец Teams расширения обмена [сообщениями, так](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) как сценарий не предполагает Azure Active Directory (AAD) Sign-On проверки подлинности.

Azure Active Directory однонастройка (SSO) для расширений обмена сообщениями работает так же, как и Outlook в [Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots) году, однако необходимо добавить несколько идентификаторов клиентских приложений в регистрацию приложения Azure AD бота на портале регистраций приложений клиента.

1. Во входе на [портал Azure](https://portal.azure.com) с учетной записью клиента в песочнице.
1. Откройте **регистрации приложений**.
1. Выберите имя приложения, чтобы открыть регистрацию приложения.
1. Выберите  **Expose aPI** (в *статье Управление*).

В разделе **Авторизованные клиентские приложения** убедитесь, `Client Id` что все перечисленные ниже значения:

|Microsoft 365 клиентского приложения | Идентификатор клиента |
|--|--|
|Teams и мобильный |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams веб |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-00000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-messaging-extension-in-teams"></a>Боковой загрузки обновленного расширения обмена сообщениями в Teams

Последний шаг — загрузка обновленного расширения обмена [сообщениями (пакета](/microsoftteams/platform/concepts/build-and-test/apps-package) приложений) в Microsoft Teams. После завершения расширение обмена сообщениями появится в установленных *приложениях* из области составить сообщение.

1. Пакет Teams приложения (манифест [и значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложений) в почтовый файл. Если вы Teams набор средств для создания приложения, вы можете легко сделать это с помощью параметра пакета метаданных **Teams Zip** в меню развертывания Teams набор средств:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Вариант пакета Teams zip в Teams набор средств для Visual Studio Code":::

1. Войдите Teams с учетной записью клиента в песочнице и убедитесь, что вы находитесь в общедоступных Developer Preview *,* нажав на меню ellipsis (**...**) в профиле пользователя и открыв  о том, чтобы проверить, что параметр предварительного просмотра разработчика переглушают.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Из Teams меню эллипсов откройте параметр &quot;About&quot; и убедитесь, что Developer Preview 'проверяется&quot;":::

1. Откройте области *приложений*, и **нажмите Upload настраиваемом** приложении, а затем **Upload для меня или моей команды**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка Upload настраиваемом приложении в области Teams &quot;Приложения&quot;":::

1. Выберите пакет приложения и нажмите кнопку *Открыть*.

После боковой загрузки Teams расширения обмена сообщениями будут доступны в Outlook в Интернете.

## <a name="preview-your-messaging-extension-in-outlook"></a>Просмотр расширения обмена сообщениями в Outlook

Теперь вы готовы протестировать расширение обмена сообщениями в Outlook на Windows и в Интернете. Несмотря на то, что обновленное расширение обмена сообщениями будет продолжать работать в Teams с полной поддержкой функций для расширений обмена [сообщениями, в](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) этом предварительном просмотре Outlook с включенной поддержкой есть ограничения:

* Расширения обмена сообщениями в Outlook ограничиваются контекстом [*композитной почты*](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если Teams `commandBox` расширения обмена сообщениями включается в качестве контекста в манифесте, текущий предварительный просмотр ограничен параметром состав почты ().`compose` Запрос расширения обмена сообщениями из глобального Outlook *не* поддерживается.
* [Команды расширения обмена сообщениями](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) на основе действий не поддерживаются в Outlook. Если у приложения есть команды на основе поиска и действий, оно будет Outlook, но меню действий будет недоступным.
* Вставка более пяти [адаптивных карт](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) в электронной почте не поддерживается; Адаптивные карты v1.4 и более поздние не поддерживаются.
* [Действия карт](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) типа `messageBack`, `imBack`и `invoke``signin` не поддерживаются для вставленных карт. Поддержка ограничена `openURL`: по щелчку мыши пользователь будет перенаправлен на указанный URL-адрес на новой вкладке.

При проверке расширения обмена сообщениями можно определить источник (исходя из Teams и Outlook) запросов бота по [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, служба получает стандартный объект Bot Framework `Activity` . Одним из свойств в объекте Activity `channelId`является , `msteams` `outlook`которое будет иметь значение или , в зависимости от того, откуда возникает запрос бота. Дополнительные новости см.  [в тексте Расширения SDK на основе обмена сообщениями](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions) на основе поиска.

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Предварительный просмотр приложения, запущенного в Outlook в Интернете:

1. Войдите в [outlook.com](https://www.outlook.com) с помощью учетных данных для тестовых клиентов.
1. Щелкните **новое сообщение**.
1. Откройте меню **"Больше приложений** " в нижней части окна композиции.

Ваше расширение обмена сообщениями будет перечислены. Вы можете вызвать его оттуда и использовать его так же, как вы бы при сочинении сообщения в Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Обратитесь к последним обновлениям в [блоге Microsoft Teams - Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) разработчика, чтобы проверить, Outlook ли Windows поддержка настольных Teams личных приложений доступна вашему тест-клиенту.

Предварительный просмотр приложения, запущенного в Outlook на Windows рабочем столе:

1. Запуск Outlook с учетными данными для тестового клиента. 1. Нажмите **кнопку Новая электронная почта**.
1. Откройте меню **"Больше приложений** " на верхней ленте.

Ваше расширение обмена сообщениями будет перечислены. Вы можете вызвать его оттуда и использовать его так же, как вы бы при сочинении сообщения в Teams.

## <a name="next-steps"></a>Дальнейшие действия

Outlook расширения Teams сообщений находятся в предварительном просмотре и не поддерживаются для использования в производстве. Вот как распределить расширение Outlook с включенной поддержкой для предварительного просмотра аудитории для тестирования.

### <a name="single-tenant-distribution"></a>Распределение с одним клиентом

Outlook и Office личные вкладки с включенной поддержкой можно распространять среди аудитории предварительного просмотра в клиенте тестовых (или производственных) одним из трех способов:

#### <a name="teams-client"></a>Teams клиента

Из меню *Apps* выберите *Управление приложениями* > **.** Для этого требуется утверждение от ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Центр администрирования

Как администратор Teams, вы можете загрузить и предварительно установить пакет приложений для клиента вашей организации из https://admin.teams.microsoft.com/. Подробные Upload в центре [Microsoft Teams администрирования Upload настраиваемые](/MicrosoftTeams/upload-custom-apps) приложения.

#### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

В качестве глобального администратора вы можете загрузить и предварительно установить пакет приложений из https://admin.microsoft.com/. [Дополнительные сведения см. в Приложения Microsoft 365 test and deploy by partners in the Integrated Apps portal](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

### <a name="multitenant-distribution"></a>Мультитенантное распространение

Распространение в Microsoft AppSource еще не поддерживается во время предварительного предварительного просмотра Outlook с Teams сообщениями.
