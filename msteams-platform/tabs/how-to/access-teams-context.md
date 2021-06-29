---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
localization_priority: Normal
ms.topic: how-to
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 8c91cf5a65f13d9f58f6ae8aa2678266c37338c8
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179729"
---
# <a name="get-context-for-your-tab"></a><span data-ttu-id="f937d-104">Получение контекста для вкладки</span><span class="sxs-lookup"><span data-stu-id="f937d-104">Get context for your tab</span></span>

<span data-ttu-id="f937d-105">Для отображения соответствующего контента на вкладке требуются контекстные сведения:</span><span class="sxs-lookup"><span data-stu-id="f937d-105">Your tab requires contextual information to display relevant content:</span></span>

* <span data-ttu-id="f937d-106">Основные сведения о пользователе, команде или компании.</span><span class="sxs-lookup"><span data-stu-id="f937d-106">Basic information about the user, team, or company.</span></span>
* <span data-ttu-id="f937d-107">Сведения о locale и теме.</span><span class="sxs-lookup"><span data-stu-id="f937d-107">Locale and theme information.</span></span>
* <span data-ttu-id="f937d-108">Прочитайте `entityId` или `subEntityId` определяйте, что находится на этой вкладке.</span><span class="sxs-lookup"><span data-stu-id="f937d-108">Read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="f937d-109">Контекст пользователя</span><span class="sxs-lookup"><span data-stu-id="f937d-109">User context</span></span>

<span data-ttu-id="f937d-110">Контекст о пользователе, команде или компании может быть особенно полезен, когда:</span><span class="sxs-lookup"><span data-stu-id="f937d-110">Context about the user, team, or company can be especially useful when:</span></span>

* <span data-ttu-id="f937d-111">Вы создаете или связываете ресурсы в приложении с указанным пользователем или командой.</span><span class="sxs-lookup"><span data-stu-id="f937d-111">You create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="f937d-112">Вы инициируете поток проверки подлинности из Azure Active Directory (AAD) или другого поставщика удостоверений, и вам не требуется повторно вводить имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="f937d-112">You initiate an authentication flow from Azure Active Directory (AAD) or other identity provider, and you do not require the user to enter their username again.</span></span> <span data-ttu-id="f937d-113">Дополнительные сведения см. в записи проверки подлинности [пользователя на вкладке Microsoft Teams.](~/concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f937d-113">For more information, see [authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f937d-114">Хотя эта информация пользователя может помочь обеспечить плавный пользовательский опыт, вы не должны использовать его в качестве доказательства удостоверения.</span><span class="sxs-lookup"><span data-stu-id="f937d-114">Although this user information can help provide a smooth user experience, you must not use it as proof of identity.</span></span> <span data-ttu-id="f937d-115">Например, злоумышленник может загрузить страницу в браузер и отрисовки вредных сведений или запросов.</span><span class="sxs-lookup"><span data-stu-id="f937d-115">For example, an attacker can load your page in a browser and render harmful information or requests.</span></span>

## <a name="access-context-information"></a><span data-ttu-id="f937d-116">Доступ к данным контекста</span><span class="sxs-lookup"><span data-stu-id="f937d-116">Access context information</span></span>

<span data-ttu-id="f937d-117">Доступ к контекстной информации можно получить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="f937d-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="f937d-118">Вставьте значения местообнамерщика URL- адресов.</span><span class="sxs-lookup"><span data-stu-id="f937d-118">Insert URL placeholder values.</span></span>
* <span data-ttu-id="f937d-119">Используйте [SDK Microsoft Teams JavaScript.](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="f937d-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

### <a name="get-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="f937d-120">Получить контекст, вставив значения задатки URL-адресов</span><span class="sxs-lookup"><span data-stu-id="f937d-120">Get context by inserting URL placeholder values</span></span>

<span data-ttu-id="f937d-121">Используйте заполнители в конфигурации или в URL-адресах контента.</span><span class="sxs-lookup"><span data-stu-id="f937d-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="f937d-122">Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента.</span><span class="sxs-lookup"><span data-stu-id="f937d-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="f937d-123">Доступные держатели включают все поля на [объекте контекста.](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f937d-123">The available placeholders include all fields on the [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="f937d-124">Распространенные сценарии:</span><span class="sxs-lookup"><span data-stu-id="f937d-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="f937d-125">{entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="f937d-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="f937d-126">{subEntityId}: ID, который вы предоставили при создании глубокой ссылки для определенного элемента в этой вкладке. [](~/concepts/build-and-test/deep-links.md) Это необходимо использовать для восстановления определенного состояния в объекте; например, прокрутка или активация определенного фрагмента контента.</span><span class="sxs-lookup"><span data-stu-id="f937d-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item within this tab. This must be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="f937d-127">{LoginHint}: значение, подходящее в качестве подсказки входа для AAD.</span><span class="sxs-lookup"><span data-stu-id="f937d-127">{loginHint}: A value suitable as a login hint for AAD.</span></span> <span data-ttu-id="f937d-128">Обычно это имя входа текущего пользователя в домашнем клиенте.</span><span class="sxs-lookup"><span data-stu-id="f937d-128">This is usually the login name of the current user in their home tenant.</span></span>
* <span data-ttu-id="f937d-129">{userPrincipalName}: основное имя пользователя текущего пользователя в текущем клиенте.</span><span class="sxs-lookup"><span data-stu-id="f937d-129">{userPrincipalName}: The User Principal Name of the current user in the current tenant.</span></span>
* <span data-ttu-id="f937d-130">{userObjectId}: ID объекта AAD текущего пользователя текущего клиента.</span><span class="sxs-lookup"><span data-stu-id="f937d-130">{userObjectId}: The AAD object ID of the current user in the current tenant.</span></span>
* <span data-ttu-id="f937d-131">{theme}: текущая тема пользовательского интерфейса (пользовательского интерфейса), например `default` `dark` , или `contrast` .</span><span class="sxs-lookup"><span data-stu-id="f937d-131">{theme}: The current user interface (UI) theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="f937d-132">{groupId}: ID группы Office 365, в которой находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="f937d-132">{groupId}: The ID of the Office 365 group in which the tab resides.</span></span>
* <span data-ttu-id="f937d-133">{tid}: ID клиента AAD текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="f937d-133">{tid}: The AAD tenant ID of the current user.</span></span>
* <span data-ttu-id="f937d-134">{locale}: текущий локализ пользователя, форматированный как languageId-countryId.</span><span class="sxs-lookup"><span data-stu-id="f937d-134">{locale}: The current locale of the user formatted as languageId-countryId.</span></span> <span data-ttu-id="f937d-135">Например, en-ru.</span><span class="sxs-lookup"><span data-stu-id="f937d-135">For example, en-us.</span></span>

> [!NOTE]
> <span data-ttu-id="f937d-136">Предыдущий заполнитель `{upn}` теперь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="f937d-136">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="f937d-137">Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="f937d-137">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="f937d-138">Например, в манифесте вкладки вы за установите атрибут, чтобы пользователь, вписав его, получил `configURL` `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"` следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="f937d-138">For example, in your tab manifest you set the `configURL` attribute to `"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`, the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="f937d-139">Их имя пользователя **user@example.com**.</span><span class="sxs-lookup"><span data-stu-id="f937d-139">Their username is **user@example.com**.</span></span>
* <span data-ttu-id="f937d-140">Их ID клиента компании **e2653c-etc**.</span><span class="sxs-lookup"><span data-stu-id="f937d-140">Their company tenant ID is **e2653c-etc**.</span></span>
* <span data-ttu-id="f937d-141">Они являются членами группы Office 365 id **00209384-etc**.</span><span class="sxs-lookup"><span data-stu-id="f937d-141">They are a member of the Office 365 group with id **00209384-etc**.</span></span>
* <span data-ttu-id="f937d-142">Пользователь установил свою Teams **темную** тему.</span><span class="sxs-lookup"><span data-stu-id="f937d-142">The user has set their Teams theme to **dark**.</span></span>

<span data-ttu-id="f937d-143">При настройке вкладки Teams следующий URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="f937d-143">When they configure the tab, Teams calls the following URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="get-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="f937d-144">Получить контекст с помощью библиотеки Microsoft Teams JavaScript</span><span class="sxs-lookup"><span data-stu-id="f937d-144">Get context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="f937d-145">Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="f937d-145">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="f937d-146">В следующем коде приводится пример переменной контекста:</span><span class="sxs-lookup"><span data-stu-id="f937d-146">The following code provides an example of context variable:</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The principal name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates if the tab is in full-screen",
    "teamType": "The type of team",
    "teamSiteUrl": "The root SharePoint site associated with the team",
    "teamSiteDomain": "The domain of the root SharePoint site associated with the team",
    "teamSitePath": "The relative path to the SharePoint site associated with the team",
    "channelRelativeUrl": "The relative path to the SharePoint folder associated with the channel",
    "sessionId": "The unique ID for the current Teams session for use in correlating telemetry data",
    "userTeamRole": "The user's role in the team",
    "isTeamArchived": "Indicates if team is archived",
    "hostClientType": "The type of host client. Possible values are android, ios, web, desktop, rigel",
    "frameContext": "The context where tab URL is loaded (for example, content, task, setting, remove, sidePanel)",
    "sharepoint": "The SharePoint context is available only when hosted in SharePoint",
    "tenantSKU": "The license type for the current user tenant. Possible values are enterprise, free, edu, unknown",
    "userLicenseType": "The license type for the current user",
    "parentMessageId": "The parent message ID from which this task module is launched",
    "ringId": "The current ring ID",
    "appSessionId": "The unique ID for the current session used for correlating telemetry data",
    "isCallingAllowed": "Indicates if calling is allowed for the current logged in user",
    "isPSTNCallingAllowed": "Indicates if PSTN calling is allowed for the current logged in user",
    "meetingId": "The meeting ID used by tab when running in meeting context",
    "defaultOneNoteSectionId": "The OneNote section ID that is linked to the channel"
}
```

## <a name="retrieve-context-in-private-channels"></a><span data-ttu-id="f937d-147">Извлечение контекста в частных каналах</span><span class="sxs-lookup"><span data-stu-id="f937d-147">Retrieve context in private channels</span></span>

> [!Note]
> <span data-ttu-id="f937d-148">Закрытые каналы в настоящее время находятся в закрытой предварительной версии для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="f937d-148">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="f937d-149">Когда страница контента загружается в частный канал, данные, полученные от вызова, запутываются для защиты `getContext` конфиденциальности канала.</span><span class="sxs-lookup"><span data-stu-id="f937d-149">When your content page is loaded in a private channel, the data you receive from the `getContext` call is obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="f937d-150">Если страница контента находится в частном канале, меняются следующие поля:</span><span class="sxs-lookup"><span data-stu-id="f937d-150">The following fields are changed when your content page is in a private channel:</span></span>

* <span data-ttu-id="f937d-151">`groupId`: Неопределяемая для частных каналов</span><span class="sxs-lookup"><span data-stu-id="f937d-151">`groupId`: Undefined for private channels</span></span>
* <span data-ttu-id="f937d-152">`teamId`: Установите для threadId частного канала</span><span class="sxs-lookup"><span data-stu-id="f937d-152">`teamId`: Set to the threadId of the private channel</span></span>
* <span data-ttu-id="f937d-153">`teamName`: Установите имя частного канала</span><span class="sxs-lookup"><span data-stu-id="f937d-153">`teamName`: Set to the name of the private channel</span></span>
* <span data-ttu-id="f937d-154">`teamSiteUrl`: Установите URL-адрес отдельного уникального SharePoint для частного канала</span><span class="sxs-lookup"><span data-stu-id="f937d-154">`teamSiteUrl`: Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="f937d-155">`teamSitePath`: Установите путь отдельного, уникального SharePoint для частного канала</span><span class="sxs-lookup"><span data-stu-id="f937d-155">`teamSitePath`: Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="f937d-156">`teamSiteDomain`: Установите домен отдельного, уникального SharePoint для частного канала</span><span class="sxs-lookup"><span data-stu-id="f937d-156">`teamSiteDomain`: Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

<span data-ttu-id="f937d-157">Если на странице используется любое из этих значений, необходимо проверить поле, чтобы определить, загружена ли страница в частном канале, и ответить `channelType` соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="f937d-157">If your page makes use of any of these values, you must check the `channelType` field to determine if your page is loaded in a private channel and respond appropriately.</span></span>

> [!Note]
> <span data-ttu-id="f937d-158">`teamSiteUrl` также хорошо работает для стандартных каналов.</span><span class="sxs-lookup"><span data-stu-id="f937d-158">`teamSiteUrl` also works well for standard channels.</span></span>

## <a name="handle-theme-change"></a><span data-ttu-id="f937d-159">Обработка изменения темы</span><span class="sxs-lookup"><span data-stu-id="f937d-159">Handle theme change</span></span>

<span data-ttu-id="f937d-160">Вы можете зарегистрировать приложение, чтобы быть информированным, если тема изменяется по вызову `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="f937d-160">You can register your app to be informed if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="f937d-161">Аргументом `theme` в функции является строка со значением `default` , или `dark` `contrast` .</span><span class="sxs-lookup"><span data-stu-id="f937d-161">The `theme` argument in the function is a string with a value of `default`, `dark`, or `contrast`.</span></span>

## <a name="see-also"></a><span data-ttu-id="f937d-162">См. также</span><span class="sxs-lookup"><span data-stu-id="f937d-162">See also</span></span>

* [<span data-ttu-id="f937d-163">Рекомендации по разработке вкладок</span><span class="sxs-lookup"><span data-stu-id="f937d-163">Tab design guidelines</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="f937d-164">Teams вкладки</span><span class="sxs-lookup"><span data-stu-id="f937d-164">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="f937d-165">Создание личной вкладки</span><span class="sxs-lookup"><span data-stu-id="f937d-165">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="f937d-166">Создание вкладки канала или группы</span><span class="sxs-lookup"><span data-stu-id="f937d-166">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)

## <a name="next-step"></a><span data-ttu-id="f937d-167">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="f937d-167">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f937d-168">Создание вкладок с использованием адаптивных карточек</span><span class="sxs-lookup"><span data-stu-id="f937d-168">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)