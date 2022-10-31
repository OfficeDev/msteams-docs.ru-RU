---
title: Распространение расширения сообщений Teams в Microsoft 365
description: Узнайте, как обновить расширение сообщений на основе поиска для запуска в Outlook в дополнение к Microsoft Teams.
ms.date: 10/10/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: high
ms.openlocfilehash: 9b153eaaaa4cf3eb59d1a7b34122b569ae0d0d1a
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789946"
---
# <a name="extend-a-teams-message-extension-across-microsoft-365"></a>Распространение расширения сообщений Teams в Microsoft 365

[Расширения сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions) на основе поиска позволяют пользователям выполнять поиск во внешней системе и обмениваться результатами через область ввода сообщений клиента Microsoft Teams. Теперь вы можете использовать расширения сообщений Teams для предварительного просмотра в классическом приложении Outlook для Windows и outlook.com, [расширив приложения Teams в Microsoft 365](overview.md).

Процесс обновления расширения сообщений Teams на основе поиска включает в себя следующие действия.

> [!div class="checklist"]
>
> * Обновите манифест приложения
> * Добавьте канал Outlook для бота.
> * Загрузите неопубликованное обновленное приложение в Teams

В оставшейся части этого руководства показано, как предварительно просмотреть расширение сообщений в Outlook для настольных компьютеров и Веб-приложений Windows.

## <a name="prerequisites"></a>Предварительные требования

Чтобы завершить работу с этим руководством, вам потребуется:

* Клиент изолированной программы для разработчиков Microsoft 365.
* Регистрация в *целевых выпусках Office 365* для изолированного клиента.
* Тестовая среда с приложениями Office, установленными из *бета-канала* приложений Microsoft 365.
* Microsoft Visual Studio Code с расширением Teams Toolkit (необязательно)

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="link-unfurling"></a>Развертывание ссылки

Если расширение сообщений на основе поиска поддерживает [распаковку ссылок](../messaging-extensions/how-to/link-unfurling.md) в Teams, то при выполнении действий, описанных в этом руководстве, вы также включаете распаковку ссылок в средах рабочего стола Outlook в Интернете и Windows. В разделе [Примеры кода](#code-sample) ниже представлено простое приложение для распаковки ссылок для тестирования.

## <a name="prepare-your-message-extension-for-the-upgrade"></a>Подготовьте расширение сообщений для обновления

Если у вас есть существующее расширение сообщений в рабочей среде, сделайте копию или ветку проекта для тестирования и обновите свой идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (отличный от рабочего идентификатора приложения, для тестирования).

Если вы хотите использовать пример кода для выполнения полного руководства по обновлению существующего приложения Teams, выполните действия по настройке в [примере поиска расширения сообщения Teams](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/50.teams-messaging-extensions-search), чтобы быстро создать расширение сообщения Microsoft Teams на основе поиска.

Кроме того, можно использовать готовое приложение с поддержкой Outlook в следующем разделе и пропустить часть [*обновления манифеста приложения*](#update-the-app-manifest) в этом руководстве.

### <a name="quickstart"></a>Быстрый запуск

Чтобы начать с [примера расширения сообщения](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365), которое уже включено для запуска в Outlook, используйте расширение Teams Toolkit для Visual Studio Code.

1. В Visual Studio Code откройте палитру команд (`Ctrl+Shift+P`), введите `Teams: Create a new Teams app`.
1. Выберите **Создать новое приложение Teams**.
1. Выберите **Расширение сообщения на основе поиска**, чтобы скачать пример кода для расширения сообщения Teams с помощью последнего манифеста приложения Teams (версия `1.13`).

    :::image type="content" source="images/toolkit-palatte-search-sample.png" alt-text="На снимке экрана показан пример палитры команд VS Code type 'Create a new Teams app' (Тип &quot;Создание нового приложения Teams&quot;) для перечисления примеров параметров Teams.":::

    Этот образец также доступен под названием *Соединитель поиска NPM* в коллекции образцов Teams Toolkit. В области Teams Toolkit выберите *Разработка* > *Просмотреть образцы* > **Соединитель поиска NPM**.

    :::image type="content" source="images/toolkit-search-sample.png" alt-text="На снимке экрана показан пример соединителя поиска NPM в коллекции примеров набора средств Teams.":::

1. Выберите предпочтительный язык программирования.
1. Выберите расположение на локальном компьютере для папки рабочей области и введите имя приложения.
1. Откройте палитру команд (`Ctrl+Shift+P`) и введите `Teams: Provision in the cloud`, чтобы создать необходимые ресурсы для приложения (Служба приложений Azure, план службы приложений, бот Azure и управляемое удостоверение) в вашей учетной записи Azure.
1. Выберите подписку и группу ресурсов.
1. Выберите **Подготовка**.
1. Откройте палитру команд (`Ctrl+Shift+P`) и введите `Teams: Deploy to the cloud`, чтобы развернуть образец кода на подготовленных ресурсах в Azure и запустить приложение.
1. Нажмите **Развернуть**.

Оттуда можно сразу перейти к [добавлению канала Outlook для бота](#add-an-outlook-channel-for-your-bot), чтобы завершить последний этап включения расширения для сообщений Teams в Outlook. (Манифест приложения уже ссылается на правильную версию, поэтому обновления не требуется.

## <a name="update-the-app-manifest"></a>Обновите манифест приложения

Чтобы разрешить запуск расширения сообщений Teams в Outlook, необходимо использовать версию схемы `1.13` [манифеста разработчика Teams](../resources/schema/manifest-schema.md).

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

Если вы использовали Teams Toolkit для создания приложения расширения сообщений, вы можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд (`Ctrl+Shift+P`) и найдите **Teams: Проверить файл манифеста**.

## <a name="add-an-outlook-channel-for-your-bot"></a>Добавьте канал Outlook для бота

В Microsoft Teams расширение сообщений состоит из веб-службы, которую вы размещаете, и манифеста приложения, который определяет, где размещена ваша веб-служба. Веб-служба использует схему обмена сообщениями[Bot Framework SDK](/azure/bot-service/bot-service-overview) и безопасный протокол связи через зарегистрированный канал Teams для вашего бота.

Чтобы пользователи взаимодействовали с расширением сообщений из Outlook, необходимо добавить канал Outlook в бот:

1. На [портале Microsoft портал Azure](https://portal.azure.com) (или [портале Bot Framework](https://dev.botframework.com), если вы там ранее зарегистрировались) перейдите к ресурсу бота.

1. В *Параметрах* выберите **Каналы**.

1. В разделе *Доступные каналы* выберите **Outlook**. Выберите вкладку **Расширения для сообщений** и выберите **Применить**.

    :::image type="content" source="images/azure-bot-channel-message-extensions.png" alt-text="На снимках экрана показан пример канала Outlook &quot;Расширения сообщений&quot; для бота из области &quot;Каналы Azure Bot&quot;.":::

1. Убедитесь, что ваш канал Outlook указан вместе с Teams на панели **каналов** вашего бота.

    :::image type="content" source="images/azure-bot-channels.png" alt-text="На снимок экрана показан пример, на котором показана панель &quot;Каналы Azure Bot&quot;, в которой перечислены каналы Teams и Outlook.":::

## <a name="update-microsoft-azure-active-directory-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Microsoft Azure Active Directory (Azure AD) для единого входа

> [!NOTE]
> Этот шаг можно пропустить, если вы используете [пример приложения](#quickstart) , представленный в этом руководстве, так как сценарий не включает проверку подлинности Azure Active Directory (AAD) с одним Sign-On.

Единый вход Azure Active Directory (AD) для расширений сообщений работает так же, [как и в Teams](/microsoftteams/platform/bots/how-to/authentication/auth-aad-sso-bots). Однако необходимо добавить несколько идентификаторов клиентских приложений в Azure AD регистрации приложения бота на *портале Регистрация приложений* клиента.

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

Последним шагом является загрузка обновленного расширения сообщений ([пакета приложения](/microsoftteams/platform/concepts/build-and-test/apps-package)) в Teams. После завершения в установленных *приложениях* в области создания сообщений появится расширение сообщения.

1. Упакуйте приложение Teams (манифест и [значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложений) в ZIP-файл. Если вы использовали Teams Toolkit для создания приложения, это легко сделать с помощью параметра **пакета метаданных Zip Teams** в меню *Развертывание* Teams Toolkit:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="На снимке экрана показан пример параметра &quot;Пакет метаданных Zip Teams&quot; в расширении набора средств Teams для Visual Studio Code.":::

1. Войдите в Teams с помощью учетной записи клиента песочницы и переключитесь в режим *предварительной версии для разработчиков*. Выберите меню с многоточием (**...**) рядом с профилем пользователя, затем выберите: **О программе** > **Предварительная версия для разработчиков**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="На снимку экрана показан пример параметра &quot;Предварительная версия для разработчиков&quot;.":::

1. Выберите **Приложения**, чтобы открыть область **Управление приложениями**. Затем выберите **Отправить приложение**.

    :::image type="content" source="../assets/images/teams-manage-your-apps.png" alt-text="На снимку экрана показан пример параметра &quot;Отправить приложение&quot;.":::

1. Выберите **Параметр Отправить настраиваемое приложение** , выберите пакет приложения и установите (*Добавить*) в клиент Teams.

    :::image type="content" source="../assets/images/teams-upload-custom-app.png" alt-text="На снимке экрана показан пример параметра &quot;Отправить настраиваемое приложение&quot; в Teams.":::

После загрузки неопубликованного приложения в Teams расширение сообщений будет доступно в Outlook для классических приложений Windows и в Интернете.

## <a name="preview-your-message-extension-in-outlook"></a>Предварительный просмотр расширения сообщений в Outlook

Протестировать ваше расширение для сообщений, работающее в классическом приложении Outlook для Windows и в Интернете, можно следующим образом. 

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы предварительно просмотреть приложение, работающее в Outlook в Интернете, выполните следующее.

1. Войдите в [outlook.com](https://www.outlook.com) , используя учетные данные тестового клиента.
1. Выберите **Создать сообщение**.
1. Откройте всплывающее меню **Дополнительные приложения** в нижней части окна композиции.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="На снимку экрана показан пример меню &quot;Дополнительные приложения&quot; в нижней части окна композиции почты для использования расширения сообщений.":::

Your message extension is listed. You can invoke it from there and use it just as you would while composing a message in Teams.

### <a name="outlook"></a>Outlook

Чтобы предварительно просмотреть приложение, работающее в Outlook на рабочем столе Windows, выполните следующее:

1. Запустите Outlook и войдите с учетными данными тестового клиента.
1. Выберите **Создать сообщение**.
1. Откройте всплывающее меню **Дополнительные приложения** на верхней ленте.

    :::image type="content" source="images/outlook-desktop-compose-more-apps.png" alt-text="На снимок экрана показан пример &quot;Дополнительные приложения&quot; на ленте окна композиции для использования расширения сообщения.":::

Расширение сообщения отображается в списке. Откроется соседняя панель для отображения результатов поиска.

## <a name="troubleshooting"></a>Устранение неполадок

 Хотя ваше обновленное расширение сообщений будет по-прежнему работать в Teams с полной[поддержкой расширений сообщений](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions), в этой ранней предварительной версии интерфейса с поддержкой Outlook существуют ограничения, о которых следует знать:

* Расширения сообщений в Outlook ограничены контекстом [*создания* почты](/microsoftteams/platform/resources/schema/manifest-schema#composeextensions). Даже если ваше расширение сообщений Teams включает`commandBox` *контекст* в свой манифест, текущий предварительный просмотр ограничен параметром составления почты (`compose`). Вызов расширения сообщений из глобального поля *Поиска* в Outlook не поддерживается.
* Команды [расширения сообщений на основе действий](/microsoftteams/platform/messaging-extensions/how-to/action-commands/define-action-command?tabs=AS) не поддерживаются в Outlook. Если приложение содержит команды на основе поиска и действий, оно появится в Outlook, но меню действий будет недоступно.
* В каждое сообщение электронной почты можно вставлять не более пяти [адаптивных карточек](/microsoftteams/platform/task-modules-and-cards/cards/design-effective-cards?tabs=design). Адаптивные карточки версии 1.4 и более поздних версий не поддерживаются.
* [Действия с карточками](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json) типа`messageBack`, `imBack`, `invoke` и `signin` не поддерживаются для вставленных карточек. Поддержка ограничена `openURL`: при выборе этого параметра пользователь перенаправляется на указанный URL-адрес на новой вкладке.

Используйте [каналы сообщества разработчиков Microsoft Teams](/microsoftteams/platform/feedback), чтобы сообщать о проблемах и оставлять отзывы.

### <a name="debugging"></a>Отладка

При тестировании расширения сообщений вы можете определить источник (исходящий из Teams или Outlook) запросов ботов с помощью [идентификатора канала ](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md#channel-id) объекта [Activity](https://github.com/Microsoft/botframework-sdk/blob/main/specs/botframework-activity/botframework-activity.md). Когда пользователь выполняет запрос, ваша служба получает стандартный объект Bot Framework.`Activity`. Одним из свойств объекта Activity является `channelId`, которое будет иметь значение `msteams` или `outlook`, в зависимости от того, откуда исходит запрос бота. Дополнительные сведения см. в разделе [Пакет SDK для расширений сообщений на основе поиска](/microsoftteams/platform/resources/messaging-extension-v3/search-extensions).

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **Node.js** |
|---------------|--------------|--------|
| Соединитель поиска NPM | Используйте Teams Toolkit, чтобы создать приложение расширения для сообщений. Работает в Teams и в Outlook. |  [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/NPM-search-connector-M365) |
| Разблокирование ссылок Teams | Простое приложение Teams для демонстрации распаковки ссылок. Работает в Teams и в Outlook. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/55.teams-link-unfurling)

## <a name="next-step"></a>Следующий этап

Опубликуйте приложение, чтобы его можно было обнаруживать в Teams, в Outlook и в Office:

> [!div class="nextstepaction"]
> [Публикация приложений Teams для Outlook и Office](publish.md)
