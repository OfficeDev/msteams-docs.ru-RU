---
title: Расширение Teams сообщений в Microsoft 365
description: Вот как обновить расширение сообщений на основе Teams поиска для запуска в Outlook
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.openlocfilehash: 3bab70d85d071763ffbbae7cb1dae11534d0e812
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104541"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Расширение Teams сообщений в Microsoft 365

> [!NOTE]
> *Расширение Teams сообщений в Microsoft 365* сейчас доступно только в общедоступной предварительной [версии разработчика](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

Расширения сообщений [на](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) основе поиска позволяют пользователям выполнять поиск во внешней системе и предоставлять общий доступ к результатам в области создания сообщений Microsoft Teams клиента. Расширив Teams приложения в [Microsoft 365 (](overview.md)предварительная версия), вы можете перенести расширения сообщений Teams на основе поиска в Outlook для Windows рабочего стола и веб-интерфейса.

Процесс обновления расширения сообщений на основе Teams поиска для запуска Outlook состоит из следующих этапов:

> [!div class="checklist"]
>
> * Обновление манифеста приложения
> * Добавление канала Outlook для бота
> * Загрузка неопубликованного приложения в Teams

В оставшейся части этого руководства вы узнаете, как просмотреть расширение сообщения в Outlook для Windows и в Интернете.

## <a name="prerequisites"></a>Предварительные требования

Для работы с этим руководством вам потребуется:

* Клиент песочницы Microsoft 365 developer Program
* Клиент песочницы, зарегистрированный *в Office 365 целевых выпусках*
* Тестовая среда с Office приложениями, установленными из Приложения Microsoft 365 *бета-версии.*
* Microsoft Visual Studio code с расширением Teams набор средств (предварительная версия) (необязательно)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Подготовка расширения сообщения к обновлению

Если у вас есть расширение сообщения, создайте копию или ветвь рабочего проекта для тестирования и обновите идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (не относящуюся к рабочему идентификатору приложения).

Если вы хотите использовать пример кода для работы с этим руководством, выполните действия по настройке в [](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) примере Teams поиска сообщений, чтобы быстро создать расширение Microsoft Teams сообщений на основе поиска. Вы также можете начать с того же примера Teams поиска расширений сообщений, обновленного для пакета [SDK TeamsJS версии 2](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365) (предварительная версия), и перейти к предварительной версии расширения [сообщения в Outlook](#preview-your-message-extension-in-outlook). Обновленный пример также доступен в расширении Teams набор средств *DevelopmentView* >  *samplesNPM* >  **Search Connector**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Пример соединителя поиска NPM в Teams набор средств":::

## <a name="update-the-app-manifest"></a>Обновление манифеста приложения

Вам потребуется использовать схему [](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `m365DevPreview` манифеста предварительной версии Teams разработчика и версию манифеста, чтобы расширение Teams сообщений запускались в Outlook.

У вас есть два варианта обновления манифеста приложения:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *палитру команд*: `Ctrl+Shift+P`
1. Выполните команду `Teams: Upgrade Teams manifest to support Outlook and Office apps` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Действия, которые необходимо выполнить вручную](#tab/manifest-manual)

Откройте манифест Teams приложения и обновите `$schema` его`manifestVersion`, указав следующие значения:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Если вы использовали Teams набор средств для создания приложения расширения сообщений, его можно использовать для проверки изменений в файле манифеста и выявления ошибок. `Ctrl+Shift+P` Откройте палитру команд и **найдите Teams:** проверка файла манифеста или выберите параметр в меню развертывания Teams набор средств (найдите значок Teams слева от Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams набор средств &quot;Проверить файл манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавление канала Outlook для бота

В Microsoft Teams расширение сообщения состоит из размещенной веб-службы и манифеста приложения, который определяет, где размещена веб-служба. Веб-служба использует схему обмена сообщениями пакета [SDK Bot Framework](/azure/bot-service/bot-service-overview) и протокол безопасного обмена данными через Teams, зарегистрированный для бота.

Чтобы пользователи могли взаимодействовать с расширением сообщения из Outlook, необходимо добавить Outlook в бот:

1. На [Microsoft Azure портале](https://portal.azure.com) (или на [портале Bot Framework](https://dev.botframework.com), если вы ранее зарегистрировались на этом портале) перейдите к ресурсу бота.

1. В *Параметры* выберите **"Каналы"**.

1. Щелкните **Outlook**, перейдите на вкладку **"** Расширения сообщений" и нажмите кнопку "**Сохранить"**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Добавление Outlook &quot;Расширения сообщений&quot; для бота из области каналов Azure Bot":::

1. Убедитесь, Outlook канал указан вместе с Microsoft Teams в области каналов **бота**:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Панель каналов Azure Bot со списком Microsoft Teams и Outlook каналов":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Обновление Microsoft Azure Active Directory приложения (Azure AD) для единого входа

> [!NOTE]
> Этот шаг можно пропустить, если вы используете пример Teams расширения сообщений[, так](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search) как сценарий не включает Azure Active Directory (AAD) Sign-On проверку подлинности.

Azure Active Directory единый вход (SSO) для расширений сообщений работает так же, как в Outlook, как и в [Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), однако необходимо добавить несколько идентификаторов клиентских приложений в регистрацию приложения Azure AD бота на портале *Регистрация приложений* клиента.

1. Войдите [в портал Azure](https://portal.azure.com) с помощью учетной записи клиента песочницы.
1. Откройте **Регистрация приложений**.
1. Выберите имя приложения, чтобы открыть регистрацию приложения.
1. Выберите  **"Предоставить API"** (в разделе *"Управление"*).

Убедитесь **,** `Client Id` что в разделе "Авторизованные клиентские приложения" перечислены все указанные ниже значения.

|Клиентское приложение Microsoft 365 | Идентификатор клиента |
|--|--|
|Teams и мобильные устройства |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Веб-приложение Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Загрузка неопубликованного расширения сообщения в Teams

Последним шагом является загрузка неопубликованного расширения сообщения (пакета [приложения](/microsoftteams/platform/concepts/build-and-test/apps-package)) в Microsoft Teams. После завершения расширение сообщения появится в установленных приложениях *из области* создания сообщения.

1. Упакуйте Teams приложения (манифест и значки [приложения](/microsoftteams/platform/resources/schema/manifest-schema#icons)) в ZIP-файл. Если вы использовали Teams набор средств для создания приложения, это можно легко сделать с помощью параметра zip **Teams** пакета метаданных в меню развертывания Teams набор средств:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр Zip Teams metadata package в Teams набор средств для Visual Studio Code":::

1. Войдите в Teams с помощью учетной записи клиента песочницы и убедитесь, что  вы используете общедоступную предварительную версию разработчика, щелкнув меню с многоточием  (**...**) профиля пользователя  и открыв "О программе", чтобы проверить, включен ли параметр предварительной версии разработчика.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="В Teams меню с многоточием откройте &quot;О программе&quot; и убедитесь, что установлен флажок &quot;Предварительная версия для разработчиков&quot;":::

1. Откройте область *"* Приложения" и **щелкните Upload пользовательское** приложение, а затем Upload **для меня или моих команд**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка Upload настраиваемого приложения в области Teams &quot;Приложения&quot;":::

1. Выберите пакет приложения и нажмите кнопку " *Открыть"*.

После загрузки неопубликованного Teams расширение сообщения будет доступно в Outlook в Интернете.

## <a name="preview-your-message-extension-in-outlook"></a>Предварительный просмотр расширения сообщения в Outlook

Теперь можно протестировать расширение сообщения, работающее в Outlook на Windows и в Интернете. Хотя обновленное расширение сообщений будет продолжать работать в Teams с полной поддержкой функций для расширений сообщений[,](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) существуют ограничения в этой ранней предварительной версии Outlook интерфейса с поддержкой Outlook, которые следует учитывать:

* Расширения сообщений в Outlook ограничены контекстом создания [*почты*](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если расширение Teams `commandBox` сообщений включается в манифест в качестве контекста, текущая предварительная версия ограничена параметром композиции почты ().`compose` Вызов расширения сообщения из глобального Outlook *не* поддерживается.
* [Команды расширения сообщений на](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) основе действий не поддерживаются в Outlook. Если в приложении есть команды на основе поиска и действий, оно будет отображаться в Outlook но меню действий будет недоступно.
* Вставка более пяти [адаптивных карточек](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design) в сообщение электронной почты не поддерживается. Адаптивные карточки версии 1.4 и более поздних версий не поддерживаются.
* [Действия с](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) карточками типа `messageBack`, `imBack`и `invoke`не `signin` поддерживаются для вставленных карточек. Поддержка ограничена `openURL`: при щелчке пользователь будет перенаправлен на указанный URL-адрес на новой вкладке.

При проверке расширения сообщения можно определить источник (исходя из Teams или Outlook) запросов бота по [channelId](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, служба получает стандартный объект Bot Framework `Activity` . Одно из свойств в объекте Activity `channelId``msteams` `outlook`имеет значение или , в зависимости от того, откуда поступает запрос бота. Дополнительные сведения см. в пакете  [SDK для расширений сообщений на основе поиска](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы просмотреть приложение, работающее в Outlook в Интернете:

1. Войдите в [outlook.com](https://www.outlook.com) , используя учетные данные тестового клиента.
1. Выберите **"Новое сообщение"**.
1. **Всплывающее меню** "Открыть другие приложения" в нижней части окна композиции.

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Щелкните меню &quot;Другие приложения&quot; в нижней части окна композиции почты, чтобы использовать расширение сообщения.":::

Расширение сообщения будет указано в списке. Вы можете вызвать его и использовать так же, как и при создании сообщения в Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями в Microsoft Teams [— Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли Outlook на Windows desktop поддержка Teams личных приложений для тестового клиента.

Чтобы просмотреть приложение, работающее Outlook на Windows компьютере:

1. Запустите Outlook входа с учетными данными для тестового клиента. 1. Щелкните " **Новый адрес электронной почты"**.
1. Откройте **всплывающее меню** "Другие приложения" на верхней ленте.

Расширение сообщения будет указано в списке. Вы можете вызвать его и использовать так же, как и при создании сообщения в Teams.

## <a name="next-steps"></a>Дальнейшие действия

Outlook расширения Teams сообщений находятся в предварительной версии и не поддерживаются для использования в рабочей области. Ниже описано, как распространить расширение Outlook сообщений для аудиторий предварительной версии в целях тестирования.

### <a name="single-tenant-distribution"></a>Распределение с одним клиентом

Outlook и Office с поддержкой личных вкладок можно распространять среди аудитории предварительной версии в тестовом (или производственном) клиенте одним из трех способов:

#### <a name="teams-client"></a>Клиент Teams

В меню *"Приложения* " выберите *"Управление приложениями* > **. Отправьте приложение в организацию"**. Для этого требуется утверждение от ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Центра администрирования

Как администратор Teams вы можете отправить и предварительно установить пакет приложения для клиента вашей организации от [Teams администратора](https://admin.teams.microsoft.com/). [Дополнительные Upload в центре администрирования Microsoft Teams настраиваемых](/MicrosoftTeams/upload-custom-apps) приложений.

#### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор вы можете отправить и предварительно установить пакет приложения от [администратора Майкрософт](https://admin.microsoft.com/). [Дополнительные сведения см. в статье Приложения Microsoft 365 тестирования](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) и развертывания приложений партнерами на портале интегрированных приложений.

### <a name="multitenant-distribution"></a>Мультитенантное распределение

Распространение в Microsoft AppSource пока не поддерживается в этой предварительной версии Outlook с Teams сообщений.
