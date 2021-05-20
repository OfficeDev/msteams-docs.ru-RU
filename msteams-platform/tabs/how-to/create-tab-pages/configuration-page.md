---
title: Создать страницу конфигурации
author: laujan
description: как создать страницу конфигурации
keywords: команды вкладки группы канал настраиваемый
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: aeab1cf96d1e875db79d9143fefd0e46348f585a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566686"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="c9219-104">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="c9219-104">Create a configuration page</span></span>

<span data-ttu-id="c9219-105">Страница конфигурации является особым типом страницы [содержимого.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="c9219-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="c9219-106">Пользователи настраивают некоторые аспекты приложения Microsoft Teams используя страницу конфигурации и используют эту конфигурацию как часть следующего:</span><span class="sxs-lookup"><span data-stu-id="c9219-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="c9219-107">Вкладка канала или группы чата: Соберите информацию от пользователей и `contentUrl` установите страницу содержимого для отображения.</span><span class="sxs-lookup"><span data-stu-id="c9219-107">A channel or group chat tab: Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="c9219-108">Расширение [обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md).</span><span class="sxs-lookup"><span data-stu-id="c9219-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>
* <span data-ttu-id="c9219-109">Разъем [Office 365 США](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="c9219-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="c9219-110">Настройка вкладки канала или группового чата</span><span class="sxs-lookup"><span data-stu-id="c9219-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="c9219-111">Приложение должно ссылаться на [Microsoft Teams JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и звонить. `microsoft.initialize()`</span><span class="sxs-lookup"><span data-stu-id="c9219-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="c9219-112">Кроме того, используемые URL-адреса должны быть защищены конечных точек HTTPS и доступны из облака.</span><span class="sxs-lookup"><span data-stu-id="c9219-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> 

### <a name="example"></a><span data-ttu-id="c9219-113">Пример</span><span class="sxs-lookup"><span data-stu-id="c9219-113">Example</span></span>

<span data-ttu-id="c9219-114">Пример страницы конфигурации показан на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="c9219-114">An example of a configuration page is shown in the following image:</span></span> 

<img src="~/assets/images/tab-images/configuration-page.png" alt="Configuration page" width="400"/>

<span data-ttu-id="c9219-115">Соответствующий код страницы конфигурации отображается в следующем разделе:</span><span class="sxs-lookup"><span data-stu-id="c9219-115">The corresponding code for configuration page is shown in the following section:</span></span>

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

<span data-ttu-id="c9219-116">Выберите **кнопку Select Gray** или Select **Red** на странице конфигурации, чтобы отобразить содержимое вкладки серым или красным значком.</span><span class="sxs-lookup"><span data-stu-id="c9219-116">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> 

<span data-ttu-id="c9219-117">Следующее изображение отображает содержимое вкладки с серым значком:</span><span class="sxs-lookup"><span data-stu-id="c9219-117">The following image displays the tab content with gray icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-gray.png" alt="Configure tab with select gray" width="400"/>

<span data-ttu-id="c9219-118">Следующее изображение отображает содержимое вкладки с красным значком:</span><span class="sxs-lookup"><span data-stu-id="c9219-118">The following image displays the tab content with red icon:</span></span>

<img src="~/assets/images/tab-images/configure-tab-with-red.png" alt="Configure tab with select red" width="400"/>

<span data-ttu-id="c9219-119">Выбор относительной кнопки вызывает `saveGray()` либо или , и вызывает `saveRed()` следующее:</span><span class="sxs-lookup"><span data-stu-id="c9219-119">Choosing the relative button triggers either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="c9219-120">Установлен `settings.setValidityState(true)` на реальность.</span><span class="sxs-lookup"><span data-stu-id="c9219-120">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="c9219-121">Обработчик `microsoftTeams.settings.registerOnSaveHandler()` событий срабатывает.</span><span class="sxs-lookup"><span data-stu-id="c9219-121">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="c9219-122">Кнопка **Сохранения** на странице конфигурации приложения, загруженная в Teams, включена.</span><span class="sxs-lookup"><span data-stu-id="c9219-122">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="c9219-123">Код страницы конфигурации информирует Teams, что требования к конфигурации удовлетворены и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="c9219-123">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="c9219-124">Когда пользователь выбирает **Сохранить**, параметры устанавливаются, `settings.setSettings()` как это определено `Settings` интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="c9219-124">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="c9219-125">Для получения дополнительной информации [с Параметры м.](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c9219-125">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="c9219-126">На последнем этапе `saveEvent.notifySuccess()` вызывается указать, что URL-адрес содержимого успешно решен.</span><span class="sxs-lookup"><span data-stu-id="c9219-126">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="c9219-127">При регистрации обработчика сохранения `microsoftTeams.settings.registerOnSaveHandler()` с помощью обратного вызова `saveEvent.notifySuccess()` необходимо `saveEvent.notifyFailure()` вызвать или указать результат конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9219-127">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="c9219-128">Если вы не регистрируете обработчик сохранения, `saveEvent.notifySuccess()` вызов делается автоматически, когда пользователь выбирает **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c9219-128">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="c9219-129">Получить контекстные данные для настроек вкладок</span><span class="sxs-lookup"><span data-stu-id="c9219-129">Get context data for your tab settings</span></span>

<span data-ttu-id="c9219-130">Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="c9219-130">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="c9219-131">Контекстная информация еще больше повышает привлекательность вашей вкладки, предоставляя более индивидуальный пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c9219-131">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="c9219-132">Для получения дополнительной информации о свойствах, используемых для конфигурации вкладок, [см.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c9219-132">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="c9219-133">Соберите значения переменных контекстных данных следующими двумя способами:</span><span class="sxs-lookup"><span data-stu-id="c9219-133">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="c9219-134">Вставьте держатели строк URL-запросов в `configurationURL` манифесте.</span><span class="sxs-lookup"><span data-stu-id="c9219-134">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="c9219-135">Используйте [Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` SDK.</span><span class="sxs-lookup"><span data-stu-id="c9219-135">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="c9219-136">Вставьте держатели в `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="c9219-136">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="c9219-137">Добавьте в базу держатели контекстных `configurationUrl` интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c9219-137">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="c9219-138">Пример:</span><span class="sxs-lookup"><span data-stu-id="c9219-138">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="c9219-139">Базовый URL</span><span class="sxs-lookup"><span data-stu-id="c9219-139">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="c9219-140">Базовый URL со строками запросов</span><span class="sxs-lookup"><span data-stu-id="c9219-140">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="c9219-141">После загрузки страницы веб-Teams строки запросов с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="c9219-141">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="c9219-142">Включите логику в страницу конфигурации для получения и использования этих значений.</span><span class="sxs-lookup"><span data-stu-id="c9219-142">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="c9219-143">Для получения дополнительной информации о работе со строками [запросов URL см.](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:</span><span class="sxs-lookup"><span data-stu-id="c9219-143">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="c9219-144">Используйте `getContext()` функцию для извлечения контекста</span><span class="sxs-lookup"><span data-stu-id="c9219-144">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="c9219-145">Функция `microsoftTeams.getContext((context) => {})` получает интерфейс Контекста при [вызовах.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="c9219-145">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="c9219-146">Добавьте эту функцию на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="c9219-146">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="c9219-147">Контекст и аутентификация</span><span class="sxs-lookup"><span data-stu-id="c9219-147">Context and authentication</span></span>

 <span data-ttu-id="c9219-148">Аутентичность, прежде чем разрешить пользователю настроить приложение.</span><span class="sxs-lookup"><span data-stu-id="c9219-148">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="c9219-149">В противном случае содержимое может включать источники, в которые есть протоколы проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c9219-149">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="c9219-150">Для получения дополнительной информации [см Microsoft Teams.](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстную информацию для построения URL-адресов запросов на проверку подлинности и авторизации страниц.</span><span class="sxs-lookup"><span data-stu-id="c9219-150">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="c9219-151">Убедитесь, что все домены, используемые на страницах вкладок, перечислены в `manifest.json` `validDomains` массиве и массиве.</span><span class="sxs-lookup"><span data-stu-id="c9219-151">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="c9219-152">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="c9219-152">Modify or remove a tab</span></span>

<span data-ttu-id="c9219-153">Поддерживаемые варианты удаления еще больше уточняют пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="c9219-153">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="c9219-154">Установите свойство вашего `canUpdateConfiguration` `true` манифеста, чтобы пользователи могли изменять, перенастраивать или переименовывать вкладку группы или канала. Кроме того, укажите, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в приложение и установив `removeUrl` значение для свойства в  `setSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="c9219-154">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="c9219-155">Пользователь может удалить Личные вкладки, но не может изменить их.</span><span class="sxs-lookup"><span data-stu-id="c9219-155">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="c9219-156">Для получения дополнительной информации [см. Создайте страницу удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="c9219-156">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

<span data-ttu-id="c9219-157">Microsoft Teams setSettings () конфигурация для удаления страницы:</span><span class="sxs-lookup"><span data-stu-id="c9219-157">Microsoft Teams setSettings() configuration for removal page:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "add website URL here //Required field for configurable tabs on Mobile Clients",
    removeUrl: "add removal page URL here"
});
```

## <a name="mobile-clients"></a><span data-ttu-id="c9219-158">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="c9219-158">Mobile clients</span></span>

<span data-ttu-id="c9219-159">Если вы решите, чтобы ваш канал или группа вкладка Teams мобильных клиентов, `setSettings()` конфигурация должна иметь значение для `websiteUrl` свойства.</span><span class="sxs-lookup"><span data-stu-id="c9219-159">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="c9219-160">Для получения дополнительной информации, [см. руководство для вкладок на мобильном телефоне](~/tabs/design/tabs-mobile.md).</span><span class="sxs-lookup"><span data-stu-id="c9219-160">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>
