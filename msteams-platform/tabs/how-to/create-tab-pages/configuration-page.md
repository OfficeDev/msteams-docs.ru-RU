---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации
keywords: команды вкладки группового канала настраиваются
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 0866d11442f79cee33d4454dbd4ed4d6b4b1a840
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019596"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="0c51f-104">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="0c51f-104">Create a configuration page</span></span>

<span data-ttu-id="0c51f-105">Страница конфигурации — это особый тип [страницы контента.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="0c51f-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="0c51f-106">Пользователи настраивают некоторые аспекты приложения Microsoft Teams с помощью страницы конфигурации и используют эту конфигурацию в следующем:</span><span class="sxs-lookup"><span data-stu-id="0c51f-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="0c51f-107">Вкладка чата канала или группы — сбор сведений от пользователей и отображение страницы `contentUrl` контента.</span><span class="sxs-lookup"><span data-stu-id="0c51f-107">A channel or group chat tab - Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="0c51f-108">Расширение [обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="0c51f-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="0c51f-109">[Соединители Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="0c51f-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="0c51f-110">Настройка вкладки чата канала или группы</span><span class="sxs-lookup"><span data-stu-id="0c51f-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="0c51f-111">Приложение должно ссылаться на [SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) клиента Microsoft Teams JavaScript и вызывать `microsoft.initialize()` .</span><span class="sxs-lookup"><span data-stu-id="0c51f-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="0c51f-112">Кроме того, используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны в облаке.</span><span class="sxs-lookup"><span data-stu-id="0c51f-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="0c51f-113">Пример</span><span class="sxs-lookup"><span data-stu-id="0c51f-113">Example</span></span>

<span data-ttu-id="0c51f-114">Пример страницы конфигурации показан на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="0c51f-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="0c51f-115">Соответствующий код страницы конфигурации показан в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="0c51f-115">The corresponding code for configuration page is shown in the following section:</span></span>

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

<span data-ttu-id="0c51f-116">Выберите **кнопку Выберите серый** или **красный** на странице конфигурации, чтобы отобразить содержимое вкладки с серым или красным значком.</span><span class="sxs-lookup"><span data-stu-id="0c51f-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="0c51f-117">На следующем изображении отображается содержимое вкладки с серым значком:</span><span class="sxs-lookup"><span data-stu-id="0c51f-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="0c51f-118">На следующем изображении отображается содержимое вкладки с красным значком:</span><span class="sxs-lookup"><span data-stu-id="0c51f-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="0c51f-119">Выбор относительной кнопки вызывает или `saveGray()` вызывает `saveRed()` следующее:</span><span class="sxs-lookup"><span data-stu-id="0c51f-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="0c51f-120">`settings.setValidityState(true)`Установлено, что это верно.</span><span class="sxs-lookup"><span data-stu-id="0c51f-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="0c51f-121">Запускается `microsoftTeams.settings.registerOnSaveHandler()` обработник событий.</span><span class="sxs-lookup"><span data-stu-id="0c51f-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="0c51f-122">Кнопка **Сохранить** на странице конфигурации приложения, загруженная в Teams, включена.</span><span class="sxs-lookup"><span data-stu-id="0c51f-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="0c51f-123">Код страницы конфигурации сообщает teams, что требования к конфигурации удовлетворены и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="0c51f-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="0c51f-124">Когда пользователь выбирает **Сохранить,** параметры заданы, `settings.setSettings()` как определено `Settings` интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="0c51f-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="0c51f-125">Дополнительные сведения см. в [интерфейсе Settings.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="0c51f-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="0c51f-126">На последнем шаге `saveEvent.notifySuccess()` вызвано, чтобы указать, что URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="0c51f-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="0c51f-127">Если вы регистрируете обработчивель сохранения с помощью, он должен вызвать вызов или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0c51f-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="0c51f-128">Если обработник сохранения не регистрируется, вызов делается автоматически, когда пользователь `saveEvent.notifySuccess()` выбирает **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0c51f-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="0c51f-129">Получите контекстные данные для параметров вкладки</span><span class="sxs-lookup"><span data-stu-id="0c51f-129">Get context data for your tab settings</span></span>

<span data-ttu-id="0c51f-130">Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="0c51f-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="0c51f-131">Контекстная информация еще больше повышает привлекательность вкладки, предоставляя более настраиваемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0c51f-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="0c51f-132">Дополнительные сведения о свойствах, используемых для конфигурации вкладок, см. в [интерфейсе Context.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="0c51f-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="0c51f-133">Собирайте значения переменных данных контекста следующими способами:</span><span class="sxs-lookup"><span data-stu-id="0c51f-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="0c51f-134">Вставьте в манифесте строки строки URL-адресов. `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="0c51f-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="0c51f-135">Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="0c51f-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="0c51f-136">Вставьте местообладатели в `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="0c51f-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="0c51f-137">Добавьте в базу местообладатели интерфейса `configurationUrl` контекста.</span><span class="sxs-lookup"><span data-stu-id="0c51f-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="0c51f-138">Например:</span><span class="sxs-lookup"><span data-stu-id="0c51f-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="0c51f-139">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="0c51f-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="0c51f-140">Базовый URL-адрес со строками запросов</span><span class="sxs-lookup"><span data-stu-id="0c51f-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="0c51f-141">После загрузки страницы Teams обновляет местообладатели строки запросов соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="0c51f-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="0c51f-142">Включай логику на странице конфигурации для получения и использования этих значений.</span><span class="sxs-lookup"><span data-stu-id="0c51f-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="0c51f-143">Дополнительные сведения о работе со строками запросов URL-адресов см. в [странице URLSearchParams в](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) веб-docs MDN. В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:</span><span class="sxs-lookup"><span data-stu-id="0c51f-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="0c51f-144">Использование `getContext()` функции для получения контекста</span><span class="sxs-lookup"><span data-stu-id="0c51f-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="0c51f-145">Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [Context при](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) вызове.</span><span class="sxs-lookup"><span data-stu-id="0c51f-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="0c51f-146">Добавьте эту функцию на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="0c51f-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="0c51f-147">Контекст и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="0c51f-147">Context and authentication</span></span>

 <span data-ttu-id="0c51f-148">Проверка подлинности перед разрешением пользователю настроить приложение.</span><span class="sxs-lookup"><span data-stu-id="0c51f-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="0c51f-149">В противном случае содержимое может включать источники, у них есть протоколы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0c51f-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="0c51f-150">Дополнительные сведения см. в вкладке Проверка подлинности пользователя [на вкладке Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов на проверку подлинности и URL-адресов страниц авторизации.</span><span class="sxs-lookup"><span data-stu-id="0c51f-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="0c51f-151">Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.</span><span class="sxs-lookup"><span data-stu-id="0c51f-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="0c51f-152">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="0c51f-152">Modify or remove a tab</span></span>

<span data-ttu-id="0c51f-153">Поддерживаемые параметры удаления дополнительно уточняют пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="0c51f-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="0c51f-154">Задайте свойству манифеста свойство , которое позволяет пользователям изменять, перенастроять или переименовывать `canUpdateConfiguration` `true` вкладку группы или канала. Кроме того, указать, что происходит с контентом при удалении вкладки, включив страницу параметры удаления в приложение и установив значение для свойства `removeUrl` в  `setSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0c51f-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="0c51f-155">Пользователь может удалить вкладки Personal, но не может изменить их.</span><span class="sxs-lookup"><span data-stu-id="0c51f-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="0c51f-156">Дополнительные сведения см. в [странице Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="0c51f-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="0c51f-157">Конфигурация Microsoft Teams setSettings() для страницы удаления:</span><span class="sxs-lookup"><span data-stu-id="0c51f-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="0c51f-158">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="0c51f-158">Mobile clients</span></span>

<span data-ttu-id="0c51f-159">Если вы хотите, чтобы вкладка канала или группы появлялась на мобильных клиентах Teams, конфигурация должна иметь значение `setSettings()` `websiteUrl` для свойства.</span><span class="sxs-lookup"><span data-stu-id="0c51f-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="0c51f-160">Дополнительные сведения см. [в руководстве по вкладке на мобильных устройствах.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="0c51f-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
