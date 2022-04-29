---
title: Распространение расширения сообщений Teams в Microsoft 365
description: Вот как обновить расширение сообщений Teams на основе поиска для запуска в Outlook.
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 7e3a0d772367952c1726648fce2f10e1d8b885b2
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111376"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Распространение расширения сообщений Teams в Microsoft 365

> [!NOTE]
> *Распространение расширения сообщений Teams в Microsoft 365* сейчас доступна только в [предварительной версии для разработчиков](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

[Расширения сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) на основе поиска позволяют пользователям выполнять поиск во внешней системе и обмениваться результатами через область ввода сообщений клиента Microsoft Teams. [Расширив свои приложения Teams в Microsoft 365 (предварительная версия)](overview.md), вы теперь можете перенести расширения сообщений Teams на основе поиска в Outlook для настольных компьютеров Windows и Интернета.

Процесс обновления расширения сообщений Teams на основе поиска для запуска Outlook включает следующие шаги:

> [!div class="checklist"]
>
> * Обновите манифест вашего приложения
> * Добавьте канал Outlook для бота
> * Загрузите неопубликованное обновленное приложение в Teams

Остальная часть этого руководства покажет пошагово, как предварительно просмотреть расширение сообщений в Outlook для рабочего стола Windows и в Интернете.

## <a name="prerequisites"></a>Предварительные условия

Для выполнения этого руководства вам понадобятся:

* Клиент песочницы программы для разработчиков Microsoft 365
* Клиент песочницы зарегистрированный в *Office 365 Targeted Releases*
* Тестовая среда с приложениями Office, установленными из *бета-канала* приложений Microsoft 365.
* Microsoft Visual Studio Code с расширением Teams Toolkit (предварительная версия) (необязательно)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Подготовьте расширение сообщений для обновления

Если у вас есть существующее расширение сообщений, сделайте копию или ветку рабочего проекта для тестирования и обновите свой идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (отличный от рабочего идентификатора приложения).

Если вы хотите использовать пример кода для выполнения этого руководства, выполните действия по настройке в [примере поиска расширения сообщений Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), чтобы быстро создать расширение сообщений на основе поиска Microsoft Teams. Или вы можете начать с того же [образца поиска расширений сообщений Teams, обновленного до](https://github.com/OfficeDev/TeamsFx-Samples/tree/v2/NPM-search-connector-M365)предварительной версии TeamsJS SDK v2, и перейти к [Предварительному просмотру вашего расширения сообщений в Outlook](#preview-your-message-extension-in-outlook). Обновленный пример также доступен в расширении Teams Toolkit: *Разработка* > *Просмотреть примеры* > **Соединитель поиска NPM**.

:::image type="content" source="images/toolkit-search-sample.png" alt-text="Образец соединителя поиска NPM в наборе инструментов Teams":::

## <a name="update-the-app-manifest"></a>Обновите манифест приложения

Вам потребуется использовать [схему манифеста предварительной версии для разработчиков Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) и версию манифеста `m365DevPreview`, чтобы расширение сообщений Teams работало в Outlook.

Существует два варианта обновления манифеста приложения:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Запустите команду `Teams: Upgrade Teams manifest to support Outlook and Office apps` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Если вы использовали Teams Toolkit для создания приложения расширения сообщений, вы можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд`Ctrl+Shift+P` и найдите **Teams: проверьте файл манифеста** или выберите параметр в меню ''Развертывание'' набора инструментов Teams (найдите значок Teams в левой части кода Visual Studio).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Параметр Teams Toolkit &quot;Проверить файл манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавьте канал Outlook для бота

В Microsoft Teams расширение сообщений состоит из веб-службы, которую вы размещаете, и манифеста приложения, который определяет, где размещена ваша веб-служба. Веб-служба использует схему обмена сообщениями[Bot Framework SDK](/azure/bot-service/bot-service-overview) и безопасный протокол связи через зарегистрированный канал Teams для вашего бота.

Чтобы пользователи могли взаимодействовать с вашим расширением сообщений из Outlook, вам необходимо добавить канал Outlook к вашему боту:

1. На [Портале Microsoft Azure](https://portal.azure.com) (или на портале [Bot Framework](https://dev.botframework.com), если вы ранее там зарегистрировались), перейдите к ресурсу своего бота.

1. В *Параметрах* выберите **Каналы**.

1. Щелкните **Outlook**, выберите вкладку **Расширения сообщений**, затем щелкните **Сохранить**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Добавьте канал Outlook ''Расширения сообщений'' для бота на панели ''Каналы Azure Bot''.":::

1. Убедитесь, что ваш канал Outlook отображен вместе с Microsoft Teams на панели **Каналов** вашего бота:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Панель Azure Bot Channels со списком каналов Microsoft Teams и Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Microsoft Azure Active Directory (Azure AD) для единого входа

> [!NOTE]
> Вы можете пропустить этот шаг, если вы используете [образец поиска расширения сообщений Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), так как сценарий не включает проверку подлинности с единым входом Azure Active Directory (AAD).

Единый вход Azure Active Directory (SSO) для расширений сообщений работает в Outlook так же, [как и в Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots), но вам необходимо добавить несколько учетных данных клиентского приложения к регистрации приложения Azure AD вашего бота на портале *регистрации приложений* вашего клиента.

1. Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи клиента песочницы.
1. Откройте **Регистрации приложений**.
1. Выберите имя приложения, чтобы открыть его регистрацию.
1. Выберите **Открыть API** (в разделе *Управление*).

В разделе **Авторизованные клиентские приложения** убедитесь, что указаны все следующие `Client Id`значения:

|Клиентское приложение Microsoft 365 | Идентификатор клиента |
|--|--|
|Настольные компьютеры и мобильные устройства |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Веб-приложение Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Загрузите обновленное расширение сообщений в Teams

Последний шаг — загрузить обновленное расширение сообщений ([пакет приложения](/microsoftteams/platform/concepts/build-and-test/apps-package)) в Microsoft Teams. После завершения ваше расширение сообщений появится в ваших установленных *Приложениях* в области создания сообщения.

1. Упакуйте приложение Teams (манифест и [значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложений) в ZIP-файл. Если вы использовали Teams Toolkit для создания своего приложения, вы можете легко сделать это с помощью параметра **пакета метаданных Zip Teams** в меню *Развертывание* Teams Toolkit:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр ''Zip Teams metadata package'' в расширении Teams Toolkit для Visual Studio Code":::

1. Войдите в Teams со своей учетной записью клиента песочницы и убедитесь, что вы находитесь в *Общедоступной предварительной версии для разработчиков*, щелкнув меню с многоточием (**...**) в своем профиле пользователя и открыв **О программе**, чтобы убедиться, что параметр *Предварительная версия для разработчиков* включен.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="В меню с многоточием Teams откройте ''О программе'' и убедитесь, что установлен флажок ''Предварительный просмотр для разработчиков''.":::

1. Откройте панель *Приложения* и щелкните **Загрузить пользовательское приложение**, а затем **Загрузить для меня или моей группы**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка ''Отправить пользовательское приложение'' на панели ''Приложения'' Teams":::

1. Выберите пакет приложения и нажмите *Открыть*.

После загрузки через Teams ваше расширение сообщений будет доступно в Outlook в Интернете.

## <a name="preview-your-message-extension-in-outlook"></a>Предварительный просмотр расширения сообщений в Outlook

Теперь вы готовы протестировать расширение сообщений, работающее в Outlook на рабочем столе Windows и в Интернете. Хотя ваше обновленное расширение сообщений будет по-прежнему работать в Teams с полной[поддержкой расширений сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), в этой ранней предварительной версии интерфейса с поддержкой Outlook существуют ограничения, о которых следует знать:

* Расширения сообщений в Outlook ограничены контекстом [*создания* почты](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если ваше расширение сообщений Teams включает`commandBox` *контекст* в свой манифест, текущий предварительный просмотр ограничен параметром составления почты (`compose`). Вызов расширения сообщений из глобального поля *Поиска* Outlook не поддерживается.
* Команды [расширения сообщений на основе действий](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) не поддерживаются в Outlook. Если в вашем приложении есть команды, основанные на поиске и действиях, оно появится в Outlook, но меню действий будет недоступно.
* Вставка более пяти [Адаптивных карточек](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design)в электронное письмо не поддерживается. Адаптивные карточки версии 1.4 и выше не поддерживаются
* [Действия с карточками](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) типа`messageBack`, `imBack`, `invoke` и `signin` не поддерживаются для вставленных карточек. Поддержка ограничена `openURL`: при щелчке пользователь будет перенаправлен на указанный URL-адрес в новой вкладке.

При тестировании расширения сообщений вы можете определить источник (исходящий из Teams или Outlook) запросов ботов с помощью [идентификатора канала ](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, ваша служба получает стандартный объект Bot Framework.`Activity`. Одним из свойств объекта Activity является `channelId`, которое будет иметь значение `msteams` или `outlook`, в зависимости от того, откуда исходит запрос бота. Подробнее в статье [SDK расширения сообщений на основе поиска.](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы предварительно просмотреть приложение, работающее в Outlook в Интернете, выполните следующее.

1. Войдите в [outlook.com](https://www.outlook.com), используя учетные данные для своего тестового клиента.
1. Выберите **Создать сообщение**.
1. Откройте всплывающее меню **Дополнительные приложения** в нижней части окна композиции.

:::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Нажмите на меню ''Дополнительные приложения'' в нижней части окна составления письма, чтобы использовать ваше расширение сообщений.":::

Ваше расширение сообщений будет в списке. Вы можете вызвать его оттуда и использовать так же, как при создании сообщения в Teams.

### <a name="outlook"></a>Outlook

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями в [Microsoft Teams — блог разработчиков Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли для вашего тестового клиента поддержка настольных компьютеров Outlook для Windows для личных приложений Teams.

Чтобы предварительно просмотреть приложение, работающее в Outlook на рабочем столе Windows, выполните следующее:

1. Запустите Outlook, войдя в систему с учетными данными для вашего тестового клиента. 1. Щелкните **Новое письмо**.
1. Откройте всплывающее меню **Дополнительные приложения** на верхней ленте.

Ваше расширение сообщений будет в списке. Вы можете вызвать его оттуда и использовать так же, как при создании сообщения в Teams.

## <a name="next-steps"></a>Дальнейшие действия

Расширения сообщений Teams с поддержкой Outlook находятся в предварительной версии и не поддерживаются для использования в рабочей среде. Вот как можно распространить расширение сообщений с поддержкой Outlook для предварительного просмотра аудитории в целях тестирования.

### <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Персональные вкладки с поддержкой Outlook и Office можно распространять среди аудитории предварительного просмотра в тестовом (или рабочем) клиенте одним из трех способов:

#### <a name="teams-client"></a>Клиент Teams

В меню *Приложения* выберите *Управление приложениями* > **Отправить приложение в вашу организацию**. Для этого требуется одобрение вашего ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Как администратор Teams, вы можете отправить и предварительно установить пакет приложения для клиента вашей организации из [Администратора Teams](https://admin.teams.microsoft.com/). Подробнее в статье [Загрузка пользовательских приложений в центре администрирования Microsoft Teams.](/MicrosoftTeams/upload-custom-apps)

#### <a name="microsoft-admin-center"></a>Центр администрирования Microsoft

Как глобальный администратор, вы можете загрузить и предварительно установить пакет приложения из [Администратора Microsoft](https://admin.microsoft.com/). Подробнее в разделе [Тестирование и развертывание приложений Microsoft 365 партнерами на портале интегрированных приложений](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

### <a name="multitenant-distribution"></a>Мультиклиентское распределение

Распространение в Microsoft AppSource еще не поддерживается во время этой предварительной версии для разработчиков расширений сообщений Teams, включенных для Outlook.
