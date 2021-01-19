---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации.
keywords: Настраиваемый канал группы вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2544454fd06348fa41269f3a8fd57cc71a07d140
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886739"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="34abf-104">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="34abf-104">Create a configuration page</span></span>

<span data-ttu-id="34abf-105">Страница конфигурации — это специальный тип страницы [контента.](content-page.md)</span><span class="sxs-lookup"><span data-stu-id="34abf-105">A configuration page is a special type of [content page](content-page.md).</span></span> <span data-ttu-id="34abf-106">Пользователи настраивают некоторые аспекты приложения Microsoft Teams на странице конфигурации и используют эту конфигурацию в составе следующих ключевых моментов:</span><span class="sxs-lookup"><span data-stu-id="34abf-106">The users configure some aspects of the Microsoft Teams app using the configuration page and use that configuration as part of the following:</span></span>

* <span data-ttu-id="34abf-107">Вкладка канала или группового чата — сбор сведений от пользователей и настройка `contentUrl` отображаемой страницы содержимого.</span><span class="sxs-lookup"><span data-stu-id="34abf-107">A channel or group chat tab - Collect information from the users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="34abf-108">Расширение [для обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="34abf-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="34abf-109">[Соединители Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="34abf-109">An [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="34abf-110">Настройка вкладки чата канала или группы</span><span class="sxs-lookup"><span data-stu-id="34abf-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="34abf-111">Приложение должно ссылаться на [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` его.</span><span class="sxs-lookup"><span data-stu-id="34abf-111">The application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="34abf-112">Кроме того, используемые URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака.</span><span class="sxs-lookup"><span data-stu-id="34abf-112">Also, the URLs used must be secured HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="34abf-113">Ниже приводится пример страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="34abf-113">The following code is an example of a configuration page:</span></span>

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

<span data-ttu-id="34abf-114">На странице конфигурации выберите "Выбрать **серый"** или "Красный", чтобы отобразить содержимое вкладки с серым или красным значком. </span><span class="sxs-lookup"><span data-stu-id="34abf-114">Choose either **Select Gray** or **Select Red** button in the configuration page, to display the tab content with a gray or red icon.</span></span> <span data-ttu-id="34abf-115">Если нажать относительную кнопку, будет либо активна, либо будет `saveGray()` `saveRed()` вызвано следующее:</span><span class="sxs-lookup"><span data-stu-id="34abf-115">Choosing the relative button fires either `saveGray()` or `saveRed()`, and invokes the following:</span></span>

1. <span data-ttu-id="34abf-116">За `settings.setValidityState(true)` установлено true.</span><span class="sxs-lookup"><span data-stu-id="34abf-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="34abf-117">`microsoftTeams.settings.registerOnSaveHandler()`Инициирует обработник событий.</span><span class="sxs-lookup"><span data-stu-id="34abf-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="34abf-118">**Кнопка** "Сохранить" на странице конфигурации приложения, загруженная в Teams, включена.</span><span class="sxs-lookup"><span data-stu-id="34abf-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="34abf-119">Код страницы конфигурации информирует Teams о том, что требования к конфигурации выполнены и установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="34abf-119">The configuration page code informs the Teams that the configuration requirements are satisfied and the installation can proceed.</span></span> <span data-ttu-id="34abf-120">Когда пользователь выбирает параметр **"Сохранить",** устанавливаются `settings.setSettings()` параметры, определенные `Settings` интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="34abf-120">When the user selects **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface.</span></span> <span data-ttu-id="34abf-121">Дополнительные сведения см. в [интерфейсе "Параметры".](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="34abf-121">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="34abf-122">На последнем этапе будет вызвано, чтобы указать, что `saveEvent.notifySuccess()` URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="34abf-122">In the last step, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="34abf-123">Если вы регистрируете обработчивель сохранения с помощью, то метод callback должен вызвать или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` настройки.</span><span class="sxs-lookup"><span data-stu-id="34abf-123">If you register a save handler using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="34abf-124">Если вы не зарегистрируете обработок сохранения, вызов будет выполнен автоматически, когда пользователь `saveEvent.notifySuccess()` наберет **"Сохранить".**</span><span class="sxs-lookup"><span data-stu-id="34abf-124">If you don't register a save handler, the `saveEvent.notifySuccess()` call is made automatically when the user selects **Save**.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="34abf-125">Получить контекстные данные для параметров вкладок</span><span class="sxs-lookup"><span data-stu-id="34abf-125">Get context data for your tab settings</span></span>

<span data-ttu-id="34abf-126">Для отображения релевантной информации на вкладке может потребоваться контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="34abf-126">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="34abf-127">Контекстная информация еще больше повышает привлекательность вкладки, обеспечивая более настраиваемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="34abf-127">Contextual information further enhances your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="34abf-128">Дополнительные сведения о свойствах, используемых для настройки вкладок, см. в [контекстных интерфейсах.](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="34abf-128">For more information on the properties used for tab configuration, see [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="34abf-129">Соберйте значения переменных данных контекста двумя способами:</span><span class="sxs-lookup"><span data-stu-id="34abf-129">Collect the values of context data variables in the following two ways:</span></span>

1. <span data-ttu-id="34abf-130">Вставьте в манифесте строки запроса `configurationURL` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="34abf-130">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="34abf-131">Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})`</span><span class="sxs-lookup"><span data-stu-id="34abf-131">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{})` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="34abf-132">Вставка в них заме- `configurationUrl`</span><span class="sxs-lookup"><span data-stu-id="34abf-132">Insert placeholders in the `configurationUrl`</span></span>

<span data-ttu-id="34abf-133">Добавьте в базу подстроки контекстного `configurationUrl` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="34abf-133">Add context interface placeholders to your base `configurationUrl`.</span></span> <span data-ttu-id="34abf-134">Например:</span><span class="sxs-lookup"><span data-stu-id="34abf-134">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="34abf-135">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="34abf-135">Base URL</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="34abf-136">Базовый URL-адрес со строками запроса</span><span class="sxs-lookup"><span data-stu-id="34abf-136">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="34abf-137">После отправки страницы Teams обновляет заметивые строки запроса соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="34abf-137">After your page uploads, the Teams updates the query string placeholders with relevant values.</span></span> <span data-ttu-id="34abf-138">Включить логику на странице конфигурации для получения и использования этих значений.</span><span class="sxs-lookup"><span data-stu-id="34abf-138">Include logic in the configuration page to retrieve and use those values.</span></span> <span data-ttu-id="34abf-139">Дополнительные сведения о работе со строками запросов URL-адресов см. в [urlSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документы MDN. В следующем примере описывается способ извлечения значения из `configurationUrl` свойства:</span><span class="sxs-lookup"><span data-stu-id="34abf-139">For more information on working with URL query strings, see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN Web Docs. The following example describes the way to extract a value from the `configurationUrl` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="34abf-140">Использование `getContext()` функции для извлечения контекста</span><span class="sxs-lookup"><span data-stu-id="34abf-140">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="34abf-141">Функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) при вызове.</span><span class="sxs-lookup"><span data-stu-id="34abf-141">The `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) when invoked.</span></span> <span data-ttu-id="34abf-142">Добавьте эту функцию на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="34abf-142">Add this function to the configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="34abf-143">Контекст и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="34abf-143">Context and authentication</span></span>

 <span data-ttu-id="34abf-144">Проверка подлинности перед разрешением пользователю настроить приложение.</span><span class="sxs-lookup"><span data-stu-id="34abf-144">Authenticate before allowing a user to configure your app.</span></span> <span data-ttu-id="34abf-145">В противном случае контент может включать источники с протоколами проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="34abf-145">Otherwise, your content might include sources that have their authentication protocols.</span></span> <span data-ttu-id="34abf-146">Дополнительные сведения см. в [записи "Проверка подлинности пользователя на вкладке Microsoft Teams".](~/tabs/how-to/authentication/auth-flow-tab.md) Используйте контекстные сведения для создания запросов проверки подлинности и URL-адресов страниц авторизации.</span><span class="sxs-lookup"><span data-stu-id="34abf-146">For more information, see [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md). Use context information to construct the authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="34abf-147">Убедитесь, что в массиве указаны все домены, используемые на страницах `manifest.json` `validDomains` вкладок.</span><span class="sxs-lookup"><span data-stu-id="34abf-147">Ensure that all domains used in your tab pages are listed in the `manifest.json` and `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="34abf-148">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="34abf-148">Modify or remove a tab</span></span>

<span data-ttu-id="34abf-149">Поддерживаемые варианты удаления дополнительно уточняют пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="34abf-149">Supported removal options further refine the user experience.</span></span> <span data-ttu-id="34abf-150">Задайте свойству манифеста свойство , которое позволяет пользователям изменять, перенастройку или переименовывать группу или `canUpdateConfiguration` `true` вкладку канала. Кроме того, указать, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в приложение и задав значение свойства `removeUrl` в  `setSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="34abf-150">Set your manifest's `canUpdateConfiguration` property to `true`, that enables the users to modify, reconfigure, or rename a group or channel tab. Also, indicate what happens to the content when a tab is removed, by including a removal options page in the app and setting a value for the `removeUrl` property in the  `setSettings()` configuration.</span></span> <span data-ttu-id="34abf-151">Дополнительные сведения см. в [мобильных клиентах.](#mobile-clients)</span><span class="sxs-lookup"><span data-stu-id="34abf-151">For more information, see [Mobile clients](#mobile-clients).</span></span> <span data-ttu-id="34abf-152">Пользователь может удалить личные вкладки, но не может изменять их.</span><span class="sxs-lookup"><span data-stu-id="34abf-152">The user can uninstall the Personal tabs but cannot modify them.</span></span> <span data-ttu-id="34abf-153">Дополнительные сведения см. в [подсети "Создание страницы удаления".](~/tabs/how-to/create-tab-pages/removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="34abf-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="34abf-154">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="34abf-154">Mobile clients</span></span>

<span data-ttu-id="34abf-155">Если вы хотите, чтобы вкладка канала или группы появлялась на мобильных клиентах Teams, конфигурация должна иметь значение `setSettings()` `websiteUrl` свойства.</span><span class="sxs-lookup"><span data-stu-id="34abf-155">If you choose to have your channel or group tab appear on the Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="34abf-156">Дополнительные сведения см. [в инструкциях для вкладок на мобильных устройствах.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="34abf-156">For more information, see [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="34abf-157">Конфигурация Microsoft Teams setSettings() для страницы удаления или мобильных клиентов:</span><span class="sxs-lookup"><span data-stu-id="34abf-157">Microsoft Teams setSettings() configuration for removal page or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
