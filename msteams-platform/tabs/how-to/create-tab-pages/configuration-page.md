---
title: Создать страницу конфигурации
author: laujan
description: создание страницы конфигурации.
keywords: Настраиваемый канал группы вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: c041c311245bb5bfc5e2655ef8d596b2839fdb70
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731967"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="d4470-104">Создать страницу конфигурации</span><span class="sxs-lookup"><span data-stu-id="d4470-104">Create a configuration page</span></span>

<span data-ttu-id="d4470-105">Страница конфигурации — это специальный тип страницы [содержимого,](content-page.md) который позволяет пользователям настраивать некоторые аспекты приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="d4470-105">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="d4470-106">Как правило, они используются в составе:</span><span class="sxs-lookup"><span data-stu-id="d4470-106">Typically these are used as part of:</span></span>

* <span data-ttu-id="d4470-107">Вкладка канала или группового чата — страница конфигурации позволяет собирать сведения от пользователей и устанавливать отображаемую `contentUrl` страницу содержимого.</span><span class="sxs-lookup"><span data-stu-id="d4470-107">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="d4470-108">Расширение [для обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="d4470-108">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="d4470-109">[Соединители Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="d4470-109">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="d4470-110">Настройка вкладки чата канала или группы</span><span class="sxs-lookup"><span data-stu-id="d4470-110">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="d4470-111">Страница конфигурации информирует страницу содержимого о том, как она должна отрисовки.</span><span class="sxs-lookup"><span data-stu-id="d4470-111">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="d4470-112">Приложение должно ссылаться на [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) и вызывать `microsoft.initialize()` его.</span><span class="sxs-lookup"><span data-stu-id="d4470-112">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="d4470-113">Кроме того, URL-адреса должны быть защищены конечными точками HTTPS и доступны из облака.</span><span class="sxs-lookup"><span data-stu-id="d4470-113">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="d4470-114">Ниже приведен пример страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="d4470-114">Below is a configuration page example.</span></span>

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

<span data-ttu-id="d4470-115">Здесь пользователь получает две кнопки **выбора:** "Выбрать  серый" или "Красный" для отображения содержимого вкладки с помощью красного или серого значка.</span><span class="sxs-lookup"><span data-stu-id="d4470-115">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="d4470-116">При нажатии относительной кнопки активна или `saveGray()` `saveRed()` вызывается следующая кнопка:</span><span class="sxs-lookup"><span data-stu-id="d4470-116">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="d4470-117">За `settings.setValidityState(true)` установлено true.</span><span class="sxs-lookup"><span data-stu-id="d4470-117">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="d4470-118">`microsoftTeams.settings.registerOnSaveHandler()`Инициирует обработник событий.</span><span class="sxs-lookup"><span data-stu-id="d4470-118">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="d4470-119">**Кнопка** "Сохранить" на странице конфигурации приложения, загруженная в Teams, включена.</span><span class="sxs-lookup"><span data-stu-id="d4470-119">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="d4470-120">Этот код сообщает Teams, что требования к конфигурации выполнены и что установка может продолжиться.</span><span class="sxs-lookup"><span data-stu-id="d4470-120">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="d4470-121">При **сохранения** параметры заданы в зависимости от интерфейса `settings.setSettings()` для `Settings` текущего экземпляра.</span><span class="sxs-lookup"><span data-stu-id="d4470-121">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance.</span></span> <span data-ttu-id="d4470-122">Дополнительные сведения см. в [интерфейсе "Параметры".](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d4470-122">For more information, see [Settings interface](/javascript/api/@microsoft/teams-js/_settings?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="d4470-123">Наконец, `saveEvent.notifySuccess()` он вызван, чтобы указать, что URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="d4470-123">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="d4470-124">Если обработель сохранения был зарегистрирован с помощью этого обработка, то он должен вызвать или указать `microsoftTeams.settings.registerOnSaveHandler()` `saveEvent.notifySuccess()` результат `saveEvent.notifyFailure()` настройки.</span><span class="sxs-lookup"><span data-stu-id="d4470-124">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="d4470-125">Если обработка сохранения не зарегистрирована, вызов автоматически делается сразу после того, как пользователь `saveEvent.notifySuccess()` нажал кнопку **"Сохранить".**</span><span class="sxs-lookup"><span data-stu-id="d4470-125">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="d4470-126">Получить контекстные данные для параметров вкладок</span><span class="sxs-lookup"><span data-stu-id="d4470-126">Get context data for your tab settings</span></span>

<span data-ttu-id="d4470-127">Для отображения релевантной информации на вкладке может потребоваться контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="d4470-127">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="d4470-128">Контекстная информация может еще больше повысить привлекательность вкладки, обеспечивая более настраиваемый пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d4470-128">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="d4470-129">Контекстный [интерфейс](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) Teams определяет свойства, которые можно использовать для настройки вкладки.</span><span class="sxs-lookup"><span data-stu-id="d4470-129">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="d4470-130">Значения переменных данных контекста можно собирать двумя способами:</span><span class="sxs-lookup"><span data-stu-id="d4470-130">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="d4470-131">Вставьте в манифесте строки запроса `configurationURL` URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d4470-131">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="d4470-132">Используйте метод [Teams SDK.](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}`</span><span class="sxs-lookup"><span data-stu-id="d4470-132">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="d4470-133">Вставка в них заме- `configurationURL`</span><span class="sxs-lookup"><span data-stu-id="d4470-133">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="d4470-134">В базу можно добавить замессеры контекстного `configurationUrl` интерфейса.</span><span class="sxs-lookup"><span data-stu-id="d4470-134">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="d4470-135">Например:</span><span class="sxs-lookup"><span data-stu-id="d4470-135">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="d4470-136">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="d4470-136">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="d4470-137">Базовый URL-адрес со строками запроса</span><span class="sxs-lookup"><span data-stu-id="d4470-137">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="d4470-138">После отправки страницы в Teams будут добавлены соответствующие значения.</span><span class="sxs-lookup"><span data-stu-id="d4470-138">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="d4470-139">На странице конфигурации можно включить логику для извлечения и использования этих значений.</span><span class="sxs-lookup"><span data-stu-id="d4470-139">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="d4470-140">Дополнительные сведения о работе со строками запроса URL-адресов см. в [urlSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документы MDN. Вот пример извлечения значения из вышеуказанного `configurationURL` свойства:</span><span class="sxs-lookup"><span data-stu-id="d4470-140">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="d4470-141">Использование `getContext()` функции для извлечения контекста</span><span class="sxs-lookup"><span data-stu-id="d4470-141">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="d4470-142">При вызове функция `microsoftTeams.getContext((context) => {})` извлекает интерфейс [контекста.](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d4470-142">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span></span> <span data-ttu-id="d4470-143">Эту функцию можно добавить на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="d4470-143">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="d4470-144">Контекст и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="d4470-144">Context and Authentication</span></span>

<span data-ttu-id="d4470-145">Прежде чем разрешить пользователю настроить приложение, может потребоваться проверка подлинности, или содержимое может включать источники с собственными протоколами проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d4470-145">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="d4470-146">См. [статью "Проверка](~/tabs/how-to/authentication/auth-flow-tab.md) подлинности пользователя" на вкладке "Контекст" в Microsoft Teams. Сведения о контексте можно использовать для создания запросов проверки подлинности и URL-адресов страниц авторизации.</span><span class="sxs-lookup"><span data-stu-id="d4470-146">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="d4470-147">Убедитесь, что все домены, используемые на страницах вкладок, указаны в `manifest.json` `validDomains` массиве.</span><span class="sxs-lookup"><span data-stu-id="d4470-147">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="d4470-148">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="d4470-148">Modify or remove a tab</span></span>

<span data-ttu-id="d4470-149">Поддерживаемые параметры удаления могут дополнительно уточнить пользовательский интерфейс.</span><span class="sxs-lookup"><span data-stu-id="d4470-149">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="d4470-150">Вы можете позволить пользователям изменять, перенастройку или переименовывать вкладку группы или канала, задав свойству манифеста `canUpdateConfiguration` имя `true` .</span><span class="sxs-lookup"><span data-stu-id="d4470-150">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="d4470-151">Кроме того, вы можете узначить, что происходит с содержимым при удалении вкладки, включив в приложение страницу параметров удаления и задав значение свойства в конфигурации `removeUrl`  `setSettings()` (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="d4470-151">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="d4470-152">Личные вкладки не могут быть изменены, но могут быть выгрузлены пользователем.</span><span class="sxs-lookup"><span data-stu-id="d4470-152">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="d4470-153">Дополнительные сведения см. в [подсети "Создание страницы удаления".](~/tabs/how-to/create-tab-pages/removal-page.md)</span><span class="sxs-lookup"><span data-stu-id="d4470-153">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="d4470-154">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="d4470-154">Mobile clients</span></span>

<span data-ttu-id="d4470-155">Если вкладка "Канал/группа" будет отображаться на мобильных клиентах Teams, конфигурация должна иметь значение свойства `setSettings()` `websiteUrl` (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="d4470-155">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="d4470-156">См. [инструкции для вкладок на мобильных устройствах.](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="d4470-156">See [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md).</span></span>

<span data-ttu-id="d4470-157">Конфигурация Microsoft Teams setSettings() для страницы удаления и/или мобильных клиентов:</span><span class="sxs-lookup"><span data-stu-id="d4470-157">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
