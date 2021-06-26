---
title: Создать страницу конфигурации
author: surbhigupta
description: создание страницы конфигурации
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 00aac64465dcc0c59a0146ea37f863f16c976a52
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140224"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="b7b33-104">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="b7b33-104">Create a configuration page</span></span>

<span data-ttu-id="b7b33-105">Страница конфигурации — это особый тип [страницы контента.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="b7b33-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="b7b33-106">Пользователи настраивают некоторые аспекты приложения Microsoft Teams, используя страницу конфигурации, и используют эту конфигурацию в следующем:</span><span class="sxs-lookup"><span data-stu-id="b7b33-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="b7b33-107">Вкладка чата канала или группы: сбор сведений от пользователей и отображение страницы `contentUrl` контента.</span><span class="sxs-lookup"><span data-stu-id="b7b33-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to be displayed.</span></span>
* <span data-ttu-id="b7b33-108">Расширение [обмена сообщениями.](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="b7b33-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="b7b33-109">Соедините [Office 365.](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="b7b33-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configure-a-channel-or-group-chat-tab"></a><span data-ttu-id="b7b33-110">Настройка вкладки чата канала или группы</span><span class="sxs-lookup"><span data-stu-id="b7b33-110">Configure a channel or group chat tab</span></span>

<span data-ttu-id="b7b33-111">Приложение должно ссылаться на [Microsoft Teams клиента JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="b7b33-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="b7b33-112">Используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны в облаке.</span><span class="sxs-lookup"><span data-stu-id="b7b33-112">The URLs used must be secured HTTPS endpoints and available from the cloud.</span></span>

### <a name="example"></a><span data-ttu-id="b7b33-113">Пример</span><span class="sxs-lookup"><span data-stu-id="b7b33-113">Example</span></span>

<span data-ttu-id="b7b33-114">Пример страницы конфигурации показан на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="b7b33-114">An example of a configuration page is shown in the following image:</span></span>

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="b7b33-115">Следующий код — пример соответствующего кода для страницы конфигурации:</span><span class="sxs-lookup"><span data-stu-id="b7b33-115">The following code is an example of corresponding code for the configuration page:</span></span>

```html
<head>
<script src='https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
</head>
    <body>
        <button onclick="(document.getElementById('icon').src = '/images/iconGray.png'); colorClickGray()">Select Gray</button>
        <img id="icon" src="/images/teamsIcon.png" alt="icon" style="width:100px" />
        <button onclick="(document.getElementById('icon').src = '/images/iconRed.png'); colorClickRed()">Select Red</button>

        <script>
            microsoftTeams.initialize();
            let saveGray = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/gray",
                        entityId: "grayIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }
            let saveRed = () => {
                microsoftTeams.settings.registerOnSaveHandler((saveEvent) => {
                    microsoftTeams.settings.setSettings({
                        websiteUrl: "https://yourWebsite.com",
                        contentUrl: "https://yourWebsite.com/red",
                        entityId: "redIconTab",
                        suggestedDisplayName: "MyNewTab"
                    });
                    saveEvent.notifySuccess();
                });
            }

            let gr = document.getElementById("gray").style;
            let rd = document.getElementById("red").style;

            const colorClickGray = () => {
                gr.display = "block";
                rd.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveGray()
            }

            const colorClickRed = () => {
                rd.display = "block";
                gr.display = "none";
                microsoftTeams.settings.setValidityState(true);
                saveRed();
            }
        </script>
    </body>
...
```

<span data-ttu-id="b7b33-116">Выберите **кнопку Выберите серый** или **красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.</span><span class="sxs-lookup"><span data-stu-id="b7b33-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span>

<span data-ttu-id="b7b33-117">На следующем изображении отображается содержимое вкладки с серым значком:</span><span class="sxs-lookup"><span data-stu-id="b7b33-117">The following image displays the tab content with a gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="b7b33-118">На следующем изображении отображается содержимое вкладки с красным значком:</span><span class="sxs-lookup"><span data-stu-id="b7b33-118">The following image displays the tab content with a red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="b7b33-119">Выбор соответствующей кнопки запускает или `saveGray()` вызывает `saveRed()` следующее:</span><span class="sxs-lookup"><span data-stu-id="b7b33-119">Choosing the appropriate button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

* <span data-ttu-id="b7b33-120">Установите `settings.setValidityState(true)` для true.</span><span class="sxs-lookup"><span data-stu-id="b7b33-120">Set `settings.setValidityState(true)` to true.</span></span> 
* <span data-ttu-id="b7b33-121">Запускается `microsoftTeams.settings.registerOnSaveHandler()` обработник событий.</span><span class="sxs-lookup"><span data-stu-id="b7b33-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
* <span data-ttu-id="b7b33-122">**Сохранение** на странице конфигурации приложения включено.</span><span class="sxs-lookup"><span data-stu-id="b7b33-122">**Save** on the app's configuration page, is enabled.</span></span>

<span data-ttu-id="b7b33-123">Код страницы конфигурации информирует Teams, что требования к конфигурации удовлетворены и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="b7b33-123">The configuration page code informs Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="b7b33-124">Когда пользователь выбирает **Сохранить,** параметры заданы, `settings.setSettings()` как определено `Settings` интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="b7b33-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="b7b33-125">Дополнительные сведения см. в [интерфейсе параметров.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b7b33-125">For more information, see [settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="b7b33-126">`saveEvent.notifySuccess()` называется, чтобы указать, что URL-адрес контента успешно решен.</span><span class="sxs-lookup"><span data-stu-id="b7b33-126">`saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="b7b33-127">Если вы регистрируете обработчивель сохранения с помощью, он должен вызвать вызов или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7b33-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="b7b33-128">Если обработник сохранения не зарегистрирован, вызов делается автоматически, когда пользователь `saveEvent.notifySuccess()` выбирает **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b7b33-128">If you do not register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="b7b33-129">Получите контекстные данные для параметров вкладки</span><span class="sxs-lookup"><span data-stu-id="b7b33-129">Get context data for your tab settings</span></span>

<span data-ttu-id="b7b33-130">Для отображения соответствующего контента на вкладке требуются контекстные сведения.</span><span class="sxs-lookup"><span data-stu-id="b7b33-130">Your tab requires contextual information to display relevant content.</span></span> <span data-ttu-id="b7b33-131">Контекстная информация еще больше повышает привлекательность вкладки, предоставляя более настраиваемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="b7b33-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="b7b33-132">Дополнительные сведения о свойствах, используемых для конфигурации вкладок, см. в [интерфейсе контекста.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b7b33-132">For more information on the properties used for tab configuration, see [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="b7b33-133">Собирайте значения переменных данных контекста следующими способами:</span><span class="sxs-lookup"><span data-stu-id="b7b33-133">Collect the values of context data variables in the following two ways:</span></span>

* <span data-ttu-id="b7b33-134">Вставьте в манифесте строки строки URL-адресов. `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="b7b33-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

* <span data-ttu-id="b7b33-135">Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="b7b33-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="b7b33-136">Вставьте местообладатели в `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="b7b33-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="b7b33-137">Добавьте в базу местообладатели интерфейса `configurationUrl` контекста.</span><span class="sxs-lookup"><span data-stu-id="b7b33-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="b7b33-138">Например:</span><span class="sxs-lookup"><span data-stu-id="b7b33-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="b7b33-139">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="b7b33-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="b7b33-140">Базовый URL-адрес со строками запросов</span><span class="sxs-lookup"><span data-stu-id="b7b33-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="b7b33-141">После загрузки страницы Teams строки запросов с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="b7b33-141">After your page uploads, Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="b7b33-142">Включай логику на странице конфигурации для получения и использования этих значений.</span><span class="sxs-lookup"><span data-stu-id="b7b33-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="b7b33-143">Дополнительные сведения о работе со строками запросов URL-адресов см. в [странице URLSearchParams в](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) веб-docs MDN. В следующем примере кода приводится способ извлечения значения из `configurationUrl` свойства:</span><span class="sxs-lookup"><span data-stu-id="b7b33-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following code example provides the way to extract a value from the `configurationUrl` property:</span></span>

```html
<script>
   microsoftTeams.initialize();
   const getId = () => {
        let urlParams = new URLSearchParams(document.location.search.substring(1));
        let blueTeamId = urlParams.get('team');
        return blueTeamId
    }
//For testing, you can invoke the following to view the pertinent value:
document.write(getId());
</script>
```

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="b7b33-144">Использование `getContext()` функции для получения контекста</span><span class="sxs-lookup"><span data-stu-id="b7b33-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="b7b33-145">Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста при](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) вызове.</span><span class="sxs-lookup"><span data-stu-id="b7b33-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span>

<span data-ttu-id="b7b33-146">В следующем коде приводится пример добавления этой функции на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="b7b33-146">The following code provides an example of adding this function to the configuration page to retrieve context values:</span></span>

```html
<!-- `userPrincipalName` will render in the span with the id "user". -->

<span id="user"></span>
...
<script>
    microsoftTeams.getContext((context) =>{
        let userId = document.getElementById('user');
        userId.innerHTML = context.userPrincipalName;
    });
</script>
...
```

## <a name="context-and-authentication"></a><span data-ttu-id="b7b33-147">Контекст и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="b7b33-147">Context and authentication</span></span>

<span data-ttu-id="b7b33-148">Проверка подлинности перед разрешением пользователю настроить приложение.</span><span class="sxs-lookup"><span data-stu-id="b7b33-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="b7b33-149">В противном случае содержимое может включать источники, у них есть протоколы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="b7b33-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="b7b33-150">Дополнительные сведения см. в записи проверки подлинности [пользователя на вкладке Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов на проверку подлинности и URL-адресов страниц авторизации.</span><span class="sxs-lookup"><span data-stu-id="b7b33-150">For more information, see [authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span> <span data-ttu-id="b7b33-151">Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.</span><span class="sxs-lookup"><span data-stu-id="b7b33-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="b7b33-152">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="b7b33-152">Modify or remove a tab</span></span>

<span data-ttu-id="b7b33-153">Установите свойство манифеста, которое позволяет пользователям изменять, перенастроять или переименовывать вкладку канала `canUpdateConfiguration` `true` или группы. Кроме того, указать, что происходит с контентом при удалении вкладки, включив страницу параметры удаления в приложение и установив значение для свойства `removeUrl` в  `setSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="b7b33-153">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a channel or group tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="b7b33-154">Пользователь может удалить личные вкладки, но не может изменить их.</span><span class="sxs-lookup"><span data-stu-id="b7b33-154">The user can uninstall personal tabs but cannot modify them.</span></span> <span data-ttu-id="b7b33-155">Дополнительные сведения см. [в странице создание страницы удаления для вкладки.](~/tabs/how-to/create-tab-pages/removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="b7b33-155">For more information, see [create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="b7b33-156">`setSettings()`Microsoft Teams конфигурация для удаления страницы:</span><span class="sxs-lookup"><span data-stu-id="b7b33-156">Microsoft Teams `setSettings()` configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="b7b33-157">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="b7b33-157">Mobile clients</span></span>

<span data-ttu-id="b7b33-158">Если вы хотите, чтобы вкладка канала или группы Teams мобильных клиентов, конфигурация должна иметь `setSettings()` значение `websiteUrl` для .</span><span class="sxs-lookup"><span data-stu-id="b7b33-158">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for `websiteUrl`.</span></span> <span data-ttu-id="b7b33-159">Дополнительные сведения см. [в руководстве по вкладке на мобильных устройствах.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="b7b33-159">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b7b33-160">См. также</span><span class="sxs-lookup"><span data-stu-id="b7b33-160">See also</span></span>

* [<span data-ttu-id="b7b33-161">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="b7b33-161">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="b7b33-162">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="b7b33-162">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="b7b33-163">Создать личную вкладку</span><span class="sxs-lookup"><span data-stu-id="b7b33-163">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="b7b33-164">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="b7b33-164">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="b7b33-165">Создать страницу контента</span><span class="sxs-lookup"><span data-stu-id="b7b33-165">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="b7b33-166">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="b7b33-166">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="b7b33-167">Получение контекста для вкладки</span><span class="sxs-lookup"><span data-stu-id="b7b33-167">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="b7b33-168">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="b7b33-168">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="b7b33-169">Предварительный просмотр для ссылки "Вкладки" и представление стадий</span><span class="sxs-lookup"><span data-stu-id="b7b33-169">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)
* [<span data-ttu-id="b7b33-170">Создание вкладок бесед</span><span class="sxs-lookup"><span data-stu-id="b7b33-170">Create conversational tabs</span></span>](~/tabs/how-to/conversational-tabs.md)
* [<span data-ttu-id="b7b33-171">Изменения полей вкладок</span><span class="sxs-lookup"><span data-stu-id="b7b33-171">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)

## <a name="next-step"></a><span data-ttu-id="b7b33-172">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="b7b33-172">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7b33-173">Создание страницы удаления для вкладки</span><span class="sxs-lookup"><span data-stu-id="b7b33-173">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
