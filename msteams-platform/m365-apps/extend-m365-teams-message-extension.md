---
title: Распространение расширения сообщений Teams в Microsoft 365
description: Вот как обновить расширение сообщений Teams на основе поиска для запуска в Outlook.
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: f9c4b342a0be797a1ac20f9f195ae969b51a0187
ms.sourcegitcommit: 1e77573e47fad51a19545949fdac1241b13052e2
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656147"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Распространение расширения сообщений Teams в Microsoft 365

[Расширения сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) на основе поиска позволяют пользователям выполнять поиск во внешней системе и обмениваться результатами через область ввода сообщений клиента Microsoft Teams. Развертывание [приложений Teams в Microsoft 365](overview.md) дает возможность расширения для сообщений Teams на основе рабочей среды для пользователей предварительных версий классического приложения Outlook для Windows и outlook.com.

Процесс обновления расширения сообщений Teams на основе поиска для запуска Outlook включает следующие шаги:

> [!div class="checklist"]
>
> * Обновите манифест вашего приложения
> * Добавьте канал Outlook для бота
> * Загрузите неопубликованное обновленное приложение в Teams

Остальная часть этого руководства покажет пошагово, как предварительно просмотреть расширение сообщений в Outlook для рабочего стола Windows и в outlook.com.

## <a name="prerequisites"></a>Предварительные условия

Для следования этому руководству вам понадобятся:

* Клиент изолированной программной среды Microsoft 365 Developer Program
* Регистрация в *целевых выпусках Office 365* для вашего клиента песочницы
* Тестовая среда с приложениями Office, установленными из *бета-канала* приложений Microsoft 365.
* Microsoft Visual Studio Code с расширением Teams Toolkit (необязательно)

> [!div class="nextstepaction"]
> [Публикация приложений Teams для Microsoft 365](publish.md)

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Подготовьте расширение сообщений для обновления

Если у вас есть существующее расширение сообщений в рабочей среде, сделайте копию или ветку проекта для тестирования и обновите свой идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (отличный от рабочего идентификатора приложения, для тестирования).

Если вы хотите использовать пример кода для выполнения полного руководства по обновлению существующего приложения Teams, выполните действия по настройке в [примере поиска расширения сообщения Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), чтобы быстро создать расширение сообщения Microsoft Teams на основе поиска.

Кроме того, можно использовать готовое приложение с поддержкой Outlook в следующем разделе и пропустить часть [*обновления манифеста приложения*](#update-the-app-manifest) в этом руководстве.

### <a name="quickstart"></a>Быстрый запуск

Чтобы начать с [примера расширения сообщения](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365), которое уже включено для запуска в Outlook, используйте расширение Teams Toolkit для Visual Studio Code.

1. В Visual Studio Code откройте палитру команд (`Ctrl+Shift+P`), введите `Teams: Create a new Teams app`.
1. Выберите **Создать новое приложение Teams**.
1. Выберите **Расширение сообщения на основе поиска**, чтобы скачать пример кода для расширения сообщения Teams с помощью последнего манифеста приложения Teams (версия `1.13`).

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="Введите «Создать новое приложение Teams» в палитре команд VS Code, чтобы просмотреть примеры параметров Teams":::

    Этот образец также доступен под названием *Соединитель поиска NPM* в коллекции образцов Teams Toolkit. В области Teams Toolkit выберите *Разработка* > *Просмотреть образцы* > **Соединитель поиска NPM**.

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="Образец соединителя поиска NPM в коллекции образцов Teams Toolkit":::

1. Выберите расположение папки рабочей области на локальном компьютере.
1. Откройте палитру команд (`Ctrl+Shift+P`) и введите `Teams: Provision in the cloud`, чтобы создать необходимые ресурсы для приложения (Служба приложений Azure, план службы приложений, бот Azure и управляемое удостоверение) в вашей учетной записи Azure.
1. Откройте палитру команд (`Ctrl+Shift+P`) и введите `Teams: Deploy to the cloud`, чтобы развернуть образец кода на подготовленных ресурсах в Azure и запустить приложение.

Оттуда можно сразу перейти к [добавлению канала Outlook для бота](#add-an-outlook-channel-for-your-bot), чтобы завершить последний этап включения расширения для сообщений Teams в Outlook. (Манифест приложения уже ссылается на нужную версию, поэтому не требуется ничего менять.)

## <a name="update-the-app-manifest"></a>Обновите манифест приложения

Вам потребуется использовать версию схемы [манифеста для разработчиков Teams](../resources/schema/manifest-schema.md) `1.13`, чтобы расширение сообщений Teams работало в Outlook.

Существует два варианта обновления манифеста приложения:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте палитру команд: `Ctrl+Shift+P`.
1. Запустите команду `Teams: Upgrade Teams manifest` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Если вы использовали Teams Toolkit для создания приложения расширения сообщений, вы можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд `Ctrl+Shift+P` и найдите **Teams: проверка файла манифеста**.

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавьте канал Outlook для бота

В Microsoft Teams расширение сообщений состоит из веб-службы, которую вы размещаете, и манифеста приложения, который определяет, где размещена ваша веб-служба. Веб-служба использует схему обмена сообщениями[Bot Framework SDK](/azure/bot-service/bot-service-overview) и безопасный протокол связи через зарегистрированный канал Teams для вашего бота.

Чтобы пользователи могли взаимодействовать с вашим расширением сообщений из Outlook, вам необходимо добавить канал Outlook к вашему боту:

1. На [Портале Microsoft Azure](https://portal.azure.com) (или на портале [Bot Framework](https://dev.botframework.com), если вы ранее там зарегистрировались), перейдите к ресурсу своего бота.

1. В *Параметрах* выберите **Каналы**.

1. В разделе *Доступные каналы* выберите **Outlook**. Выберите вкладку **Расширения для сообщений** и выберите **Применить**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="Добавьте канал Outlook ''Расширения сообщений'' для бота на панели ''Каналы Azure Bot''.":::

1. Убедитесь, что ваш канал Outlook отображен вместе с Microsoft Teams на панели **Каналов** вашего бота:

    :::image type="content" source="images/azure-bot-channels.png" alt-text="Панель Azure Bot Channels со списком каналов Microsoft Teams и Outlook":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Microsoft Azure Active Directory (Azure AD) для единого входа

> [!NOTE]
> Этот шаг можно пропустить, если вы используете [образец приложения](#quickstart), предоставленный в этом учебном руководстве, поскольку этот сценарий не включает проверку подлинности Azure Active Directory (AAD) с единым входом.

Единый вход (SSO) Azure Active Directory (AAD) для расширений сообщений работает в Outlook так же, [как в Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots). При этом необходимо добавить несколько идентификаторов клиентского приложения к регистрации приложения вашего бота в Azure AD на портале *Регистрация приложений* вашего клиента.

1. Войдите на [портал Azure](https://portal.azure.com) с помощью учетной записи клиента песочницы.
1. Откройте **Регистрации приложений**.
1. Выберите имя приложения, чтобы открыть его регистрацию.
1. Выберите **Открыть API** (в разделе *Управление*).
1. В разделе **Авторизованные клиентские приложения** убедитесь, что указаны все следующие `Client Id`значения:

|Клиентское приложение Microsoft 365 | Идентификатор клиента |
|--|--|
|Настольные компьютеры и мобильные устройства |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Веб-приложение Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-updated-message-extension-in-teams"></a>Загрузите обновленное расширение сообщений в Teams

Последний шаг — загрузить обновленное расширение сообщений ([пакет приложения](/microsoftteams/platform/concepts/build-and-test/apps-package)) в Microsoft Teams. После завершения ваше расширение сообщений появится в ваших установленных *Приложениях* в области создания сообщения.

1. Упакуйте приложение Teams (манифеcт и [значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложения) в ZIP-файл. Если вы использовали Teams Toolkit для создания приложения, это можно сделать с помощью параметра **Упаковка пакета метаданных Teams** в меню *Развертывание* в Teams Toolkit.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр ''Zip Teams metadata package'' в расширении Teams Toolkit для Visual Studio Code":::

1. Войдите в Teams с помощью учетной записи клиента песочницы и переключитесь в режим *предварительной версии для разработчиков*. Выберите меню с многоточием (**...**) рядом с профилем пользователя, затем выберите: О программе > **Предварительная версия для разработчиков**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="В меню с многоточием Teams откройте «О программе» и выберите параметр «Предварительная версия для разработчиков»":::

1. Выберите *Приложения*, чтобы открыть область **Управление приложениями**. Затем выберите **Опубликовать приложение**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="Откройте панель «Управление приложениями» и выберите «Опубликовать приложение»":::

1. Выберите **Отправить настраиваемое приложение**, выберите пакет приложения и нажмите *Добавить*, чтобы установить приложение в ваш клиент Teams.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="«Отправить настраиваемое приложение» в Teams":::

После загрузки через Teams ваше расширение для сообщений будет доступно в outlook.com и в классическом приложении Outlook для Windows.

## <a name="preview-your-message-extension-in-outlook"></a>Предварительный просмотр расширения сообщений в Outlook

Протестировать ваше расширение для сообщений, работающее в классическом приложении Outlook для Windows и в Интернете, можно следующим образом. 

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы предварительно просмотреть приложение, работающее в Outlook в Интернете, выполните следующее.

1. Выполните вход на сайте [outlook.com](https://www.outlook.com), используя учетные данные тестового клиента.
1. Выберите **Создать сообщение**.
1. Откройте всплывающее меню **Дополнительные приложения** в нижней части окна композиции.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Нажмите на меню ''Дополнительные приложения'' в нижней части окна составления письма, чтобы использовать ваше расширение сообщений.":::

Ваше расширение для сообщений содержится в списке. Его можно вызвать и использовать таким же образом, как при создании сообщений в Teams.

### <a name="outlook"></a>Outlook

Чтобы предварительно просмотреть приложение, работающее в Outlook на рабочем столе Windows, выполните следующее:

1. Запустите Outlook, войдя в систему с учетными данными для вашего тестового клиента.
1. Выберите **Создать сообщение**.
1. Откройте всплывающее меню **Дополнительные приложения** на верхней ленте.

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="Щелкните «Другие приложения» на ленте окна составления сообщений, чтобы использовать ваше расширение для сообщений.":::

Расширение сообщения отображается в списке. Откроется соседняя панель для отображения результатов поиска.

## <a name="troubleshooting"></a>Устранение неполадок

 Хотя ваше обновленное расширение сообщений будет по-прежнему работать в Teams с полной[поддержкой расширений сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), в этой ранней предварительной версии интерфейса с поддержкой Outlook существуют ограничения, о которых следует знать:

* Расширения сообщений в Outlook ограничены контекстом [*создания* почты](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если ваше расширение сообщений Teams включает`commandBox` *контекст* в свой манифест, текущий предварительный просмотр ограничен параметром составления почты (`compose`). Вызов расширения сообщений из глобального поля *Поиска* в Outlook не поддерживается.
* Команды [расширения для сообщений на основе действий](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) не поддерживаются в Outlook. Если в вашем приложении есть команды на основе поиска и действий, оно появится в Outlook, но меню действий будет недоступно.
* В каждое сообщение электронной почты можно вставлять не более пяти [адаптивных карточек](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design). Адаптивные карточки версии 1.4 и более поздних версий не поддерживаются.
* [Действия с карточками](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) типа`messageBack`, `imBack`, `invoke` и `signin` не поддерживаются для вставленных карточек. Поддержка ограничена `openURL`: при щелчке пользователь будет перенаправлен на указанный URL-адрес в новой вкладке.

Используйте [каналы сообщества разработчиков Microsoft Teams](/microsoftteams/platform/feedback), чтобы сообщать о проблемах и оставлять отзывы.

### <a name="debugging"></a>Отладка

При тестировании расширения сообщений вы можете определить источник (исходящий из Teams или Outlook) запросов ботов с помощью [идентификатора канала ](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, ваша служба получает стандартный объект Bot Framework.`Activity`. Одним из свойств объекта Activity является `channelId`, которое будет иметь значение `msteams` или `outlook`, в зависимости от того, откуда исходит запрос бота. Дополнительные сведения см. в статье [SDK расширений для сообщений на базе поиска](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **Node.js** |
|---------------|--------------|--------|
| Соединитель поиска NPM | Используйте Teams Toolkit, чтобы создать приложение расширения для сообщений. Работает в Teams и в Outlook. |  [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |

## <a name="next-step"></a>Следующий этап

Опубликуйте приложение, чтобы его можно было обнаруживать в Teams, в Outlook и в Office:

> [!div class="nextstepaction"]
> [Публикация приложений Teams для Outlook и Office](publish.md)
