---
title: Создание страницы конфигурации
author: laujan
description: ''
keywords: вкладки Teams канал группы настраиваемого канала
ms.topic: conceptualF
ms.author: laujan
ms.openlocfilehash: c7b6b636a342c650667a1131e7899908744beedf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675172"
---
# <a name="create-a-configuration-page"></a><span data-ttu-id="e223c-103">Создание страницы конфигурации</span><span class="sxs-lookup"><span data-stu-id="e223c-103">Create a configuration page</span></span>

<span data-ttu-id="e223c-104">Страница конфигурации — это особый тип [страницы контента](content-page.md) , позволяющий пользователям настраивать некоторые аспекты приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="e223c-104">A configuration page is a special type of [content page](content-page.md) that allows your users to configure some aspect of your Teams app.</span></span> <span data-ttu-id="e223c-105">Обычно они используются в качестве части:</span><span class="sxs-lookup"><span data-stu-id="e223c-105">Typically these are used as part of:</span></span>

* <span data-ttu-id="e223c-106">Вкладка "канал" или "Группа чата" — страница настройки позволяет собирать сведения от пользователей и задавать `contentUrl` отображаемую страницу контента.</span><span class="sxs-lookup"><span data-stu-id="e223c-106">A channel or group chat tab - The configuration page allows you to collect information from your users and set the `contentUrl` of the content page to display.</span></span>
* <span data-ttu-id="e223c-107">[Расширение системы обмена сообщениями](~/messaging-extensions/what-are-messaging-extensions.md)</span><span class="sxs-lookup"><span data-stu-id="e223c-107">A [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md)</span></span>
* <span data-ttu-id="e223c-108">[Соединитель Office 365](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="e223c-108">A [Office 365 Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span></span>

## <a name="configuring-a-channel-or-group-chat-tab"></a><span data-ttu-id="e223c-109">Настройка вкладки канала или группового чата</span><span class="sxs-lookup"><span data-stu-id="e223c-109">Configuring a channel or group chat tab</span></span>

<span data-ttu-id="e223c-110">Страница конфигурации информирует страницу содержимого о том, как она должна отображаться.</span><span class="sxs-lookup"><span data-stu-id="e223c-110">A configuration page informs the content page how it should render.</span></span> <span data-ttu-id="e223c-111">Ваше приложение должно ссылаться `microsoft.initialize()`на [клиентский пакет SDK и вызов Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) .</span><span class="sxs-lookup"><span data-stu-id="e223c-111">Your application must reference the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and call `microsoft.initialize()`.</span></span> <span data-ttu-id="e223c-112">Кроме того, ваш URL-адрес должен быть защищенными конечными точками HTTPS и доступен в облаке.</span><span class="sxs-lookup"><span data-stu-id="e223c-112">Additionally, your URLs must be secure HTTPS endpoints and available from the cloud.</span></span> <span data-ttu-id="e223c-113">Ниже приведен пример страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e223c-113">Below is a configuration page example.</span></span>

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

<span data-ttu-id="e223c-114">Здесь у пользователя есть два переключателя, **выберите серый** или **красный** , чтобы отобразить содержимое вкладки с помощью значка красного или серого.</span><span class="sxs-lookup"><span data-stu-id="e223c-114">Here, the user is presented with two option buttons, **Select Gray** or **Select Red** to display the tab content with either a red or gray icon.</span></span> <span data-ttu-id="e223c-115">При нажатии кнопки `saveGray()` относитель `saveRed()` срабатывает или вызывается следующее:</span><span class="sxs-lookup"><span data-stu-id="e223c-115">Choosing the relative button fires `saveGray()` or `saveRed()` and invokes the following:</span></span>

1. <span data-ttu-id="e223c-116">Для `settings.setValidityState(true)` параметра задано значение true.</span><span class="sxs-lookup"><span data-stu-id="e223c-116">The `settings.setValidityState(true)` is set to true.</span></span>
1. <span data-ttu-id="e223c-117">Запускается `microsoftTeams.settings.registerOnSaveHandler()` обработчик событий.</span><span class="sxs-lookup"><span data-stu-id="e223c-117">The `microsoftTeams.settings.registerOnSaveHandler()` event handler is triggered.</span></span>
1. <span data-ttu-id="e223c-118">Кнопка **сохранить** на странице настройки приложения, отправленная в Teams, включена.</span><span class="sxs-lookup"><span data-stu-id="e223c-118">The **Save** button on the app's configuration page, uploaded in Teams, is enabled.</span></span>

<span data-ttu-id="e223c-119">С помощью этого кода Teams вы узнаете, что требования к конфигурации выполнены, и установка может быть продолжена.</span><span class="sxs-lookup"><span data-stu-id="e223c-119">This code lets Teams know that the configuration requirements have been satisfied and the installation can proceed.</span></span> <span data-ttu-id="e223c-120">При **сохранении**параметры `settings.setSettings()` задаются, как определено `Settings` интерфейсом, для текущего экземпляра (см. [интерфейс параметров](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span><span class="sxs-lookup"><span data-stu-id="e223c-120">On **Save**, the parameters of `settings.setSettings()` are set, as defined by the `Settings` interface, for the current instance (See [Settings interface](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest) ).</span></span> <span data-ttu-id="e223c-121">`saveEvent.notifySuccess()` Finally вызывается, чтобы показать, что URL-адрес контента успешно разрешен.</span><span class="sxs-lookup"><span data-stu-id="e223c-121">Finally, `saveEvent.notifySuccess()` is called to indicate that the content URL has successfully resolved.</span></span>

>[!NOTE]
>
>* <span data-ttu-id="e223c-122">Если обработчик сохранения зарегистрирован с помощью `microsoftTeams.settings.registerOnSaveHandler()`, обратный вызов должен вызвать `saveEvent.notifySuccess()` или `saveEvent.notifyFailure()` указать результат конфигурации.</span><span class="sxs-lookup"><span data-stu-id="e223c-122">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler()`, the callback must invoke `saveEvent.notifySuccess()` or `saveEvent.notifyFailure()` to indicate the outcome of the configuration.</span></span>
>* <span data-ttu-id="e223c-123">Если обработчик сохранения не зарегистрирован, `saveEvent.notifySuccess()` вызов автоматически выполняется сразу после нажатия кнопки **сохранить** .</span><span class="sxs-lookup"><span data-stu-id="e223c-123">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the **Save** button.</span></span>

### <a name="get-context-data-for-your-tab-settings"></a><span data-ttu-id="e223c-124">Получение данных контекста для параметров вкладки</span><span class="sxs-lookup"><span data-stu-id="e223c-124">Get context data for your tab settings</span></span>

<span data-ttu-id="e223c-125">Для отображения соответствующего контента на вкладке может потребоваться Контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="e223c-125">Your tab might require contextual information to display relevant content.</span></span> <span data-ttu-id="e223c-126">Контекстные сведения могут улучшить внешний вид вкладки, обеспечивая более настраиваемое взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="e223c-126">Contextual information can further enhance your tab's appeal by providing a more customized user experience.</span></span>

<span data-ttu-id="e223c-127">[Интерфейс контекста](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) Teams определяет свойства, которые можно использовать для настройки вкладки.</span><span class="sxs-lookup"><span data-stu-id="e223c-127">The Teams [Context interface](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) defines the properties that can be used for your tab configuration.</span></span> <span data-ttu-id="e223c-128">Вы можете собирать значения переменных контекстных данных двумя способами:</span><span class="sxs-lookup"><span data-stu-id="e223c-128">You can collect the values of context data variables in two ways:</span></span>

1. <span data-ttu-id="e223c-129">Вставьте в манифесте заполнители строки запроса URL- `configurationURL`адреса.</span><span class="sxs-lookup"><span data-stu-id="e223c-129">Insert URL query string placeholders in your manifest's `configurationURL`.</span></span>

1. <span data-ttu-id="e223c-130">Используйте метод [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` .</span><span class="sxs-lookup"><span data-stu-id="e223c-130">Use the [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) `microsoftTeams.getContext((context) =>{}` method.</span></span>

#### <a name="insert-placeholders-in-the-configurationurl"></a><span data-ttu-id="e223c-131">Вставьте заполнители в поле`configurationURL`</span><span class="sxs-lookup"><span data-stu-id="e223c-131">Insert placeholders in the `configurationURL`</span></span>

<span data-ttu-id="e223c-132">Заполнители интерфейса контекста можно добавлять к базе `configurationUrl`.</span><span class="sxs-lookup"><span data-stu-id="e223c-132">Context interface placeholders can be added to your base `configurationUrl`.</span></span> <span data-ttu-id="e223c-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="e223c-133">For example:</span></span>

##### <a name="base-url"></a><span data-ttu-id="e223c-134">Базовый URL-адрес</span><span class="sxs-lookup"><span data-stu-id="e223c-134">Base Url</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config",
...
```

#### <a name="base-url-with-query-strings"></a><span data-ttu-id="e223c-135">Базовый URL-адрес со строками запроса</span><span class="sxs-lookup"><span data-stu-id="e223c-135">Base URL with query strings</span></span>

```json
...
"configurationUrl": "https://yourWebsite/config?team={teamId}&channel={channelId}&{locale}"
...
```

<span data-ttu-id="e223c-136">После отправки страницы заполнители строки запроса будут обновлены в Teams с соответствующими значениями.</span><span class="sxs-lookup"><span data-stu-id="e223c-136">After your page has uploaded, the query string placeholders will be updated by Teams with the relevant values.</span></span> <span data-ttu-id="e223c-137">Вы можете включить логику на странице конфигурации, чтобы извлечь и использовать эти значения.</span><span class="sxs-lookup"><span data-stu-id="e223c-137">You can include logic in your configuration page to retrieve and use those values.</span></span> <span data-ttu-id="e223c-138">Дополнительные сведения о работе с строками запросов URL-адресов [урлсеарчпарамс](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) в веб-документах МДН. Ниже приведен пример того, как извлечь значение из вышеуказанного `configurationURL` свойства:</span><span class="sxs-lookup"><span data-stu-id="e223c-138">For more information on working with URL query strings see [URLSearchParams](https://developer.mozilla.org/en-US/docs/Web/API/URLSearchParams) in MDN web docs. Here is an example of how to extract a value from the above `configurationURL` property:</span></span>

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

### <a name="use-the-getcontext-function-to-retrieve-context"></a><span data-ttu-id="e223c-139">Использование `getContext()` функции для получения контекста</span><span class="sxs-lookup"><span data-stu-id="e223c-139">Use the `getContext()` function to retrieve context</span></span>

<span data-ttu-id="e223c-140">При вызове `microsoftTeams.getContext((context) => {})` функция получает [интерфейс контекста](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span><span class="sxs-lookup"><span data-stu-id="e223c-140">When invoked, the `microsoftTeams.getContext((context) => {})` function retrieves the [Context interface](/javascript/api/@microsoft/teams-js//microsoftteams.context?view=msteams-client-js-latest).</span></span> <span data-ttu-id="e223c-141">Вы можете добавить эту функцию на страницу конфигурации для получения значений контекста:</span><span class="sxs-lookup"><span data-stu-id="e223c-141">You can add this function to your configuration page to retrieve context values:</span></span>

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

## <a name="context-and-authentication"></a><span data-ttu-id="e223c-142">Контекст и проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="e223c-142">Context and Authentication</span></span>

<span data-ttu-id="e223c-143">Проверка подлинности может потребоваться, прежде чем разрешить пользователю настраивать приложение или контент может включать источники с собственными протоколами проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="e223c-143">You might require authentication before allowing a user to configure your app or your content might include sources that have their own authentication protocols.</span></span> <span data-ttu-id="e223c-144">Просмотреть [проверку подлинности пользователь в контексте вкладки Microsoft Teams](~/tabs/how-to/authentication/auth-flow-tab.md) можно использовать для создания URL-адресов страниц проверки подлинности и страниц авторизации.</span><span class="sxs-lookup"><span data-stu-id="e223c-144">See [Authenticate a user in a Microsoft Teams tab](~/tabs/how-to/authentication/auth-flow-tab.md) Context information can be used to help construct authentication requests and authorization page URLs.</span></span>
<span data-ttu-id="e223c-145">Убедитесь, что все домены, используемые на страницах вкладок, указаны в `manifest.json` `validDomains` массиве.</span><span class="sxs-lookup"><span data-stu-id="e223c-145">Make sure that all domains used in your tab pages are listed in the `manifest.json` `validDomains` array.</span></span>

## <a name="modify-or-remove-a-tab"></a><span data-ttu-id="e223c-146">Изменение или удаление вкладки</span><span class="sxs-lookup"><span data-stu-id="e223c-146">Modify or remove a tab</span></span>

<span data-ttu-id="e223c-147">Поддерживаемые варианты удаления могут дополнительно улучшить взаимодействие с пользователем.</span><span class="sxs-lookup"><span data-stu-id="e223c-147">Supported removal options can further refine the user experience.</span></span> <span data-ttu-id="e223c-148">Вы можете разрешить пользователям изменять, перенастраивать или переименовывать вкладки группа и канал, устанавливая для `canUpdateConfiguration` `true`свойства манифеста значение.</span><span class="sxs-lookup"><span data-stu-id="e223c-148">You can enable users to modify, reconfigure, or rename a group/channel tab by setting your manifest's `canUpdateConfiguration` property to `true`.</span></span>  <span data-ttu-id="e223c-149">Кроме того, вы можете указать, что происходит с содержимым при удалении вкладки, включив страницу параметров удаления в свое приложение и задав значение для `removeUrl` свойства в `setSettings()` конфигурации (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="e223c-149">In addition, you can designate what happens to the content when a tab is removed by including a removal options page in your app and setting a value for the `removeUrl` property in the  `setSettings()` configuration (see below).</span></span> <span data-ttu-id="e223c-150">Личные вкладки нельзя изменить, но можно удалить пользователя.</span><span class="sxs-lookup"><span data-stu-id="e223c-150">Personal tabs can't be modified but can be uninstalled by the user.</span></span> <span data-ttu-id="e223c-151">Дополнительные сведения можно найти [в разделе Создание страницы удаления для вкладки](~/tabs/how-to/create-tab-pages/removal-page.md).</span><span class="sxs-lookup"><span data-stu-id="e223c-151">For more information, see [Create a removal page for your tab](~/tabs/how-to/create-tab-pages/removal-page.md).</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="e223c-152">Мобильные приложения</span><span class="sxs-lookup"><span data-stu-id="e223c-152">Mobile clients</span></span>

<span data-ttu-id="e223c-153">Если вкладка канал и группа отображается в клиентах Teams для мобильных устройств, то `setSettings()` конфигурация должна иметь значение для `websiteUrl` свойства (см. ниже).</span><span class="sxs-lookup"><span data-stu-id="e223c-153">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="e223c-154">В ближайшее время будет выпущена полная поддержка вкладок на мобильных клиентах.</span><span class="sxs-lookup"><span data-stu-id="e223c-154">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="e223c-155">Чтобы подготовиться к обновлению, следуйте [указаниям для вкладок на странице Mobile](~/tabs/design/tabs-mobile.md) при создании вкладок.</span><span class="sxs-lookup"><span data-stu-id="e223c-155">To prepare for the update, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

<span data-ttu-id="e223c-156">Настройка Microsoft Teams Сетсеттингс () для страницы удаления и/или мобильных клиентов:</span><span class="sxs-lookup"><span data-stu-id="e223c-156">Microsoft Teams setSettings() configuration for removal page and/or mobile clients:</span></span>

```javascript
microsoftTeams.settings.setSettings({
    contentUrl: "add content page URL here",
    entityId: "add unique name here",
    suggestedDisplayName: "add name to display on tab here",
    websiteUrl: "URL REQUIRED FOR MOBILE CLIENTS",
    removeUrl: "ADD REMOVAL PAGE URL HERE"
});
```
