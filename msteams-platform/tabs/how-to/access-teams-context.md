---
title: Получение контекста для вкладки
description: В этой статье описывается, как получить контекст пользователя для вкладок
ms.topic: how-to
keywords: пользовательский контекст вкладок teams
ms.openlocfilehash: 88a9c8ac5b2bca539b931147e6f6feb1483a3b6c
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696481"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="a3582-104">Получение контекста для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a3582-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="a3582-105">Чтобы отображать соответствующее содержимое, вкладке может быть нужна контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="a3582-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="a3582-106">Или основные сведения о пользователе, группе или компании.</span><span class="sxs-lookup"><span data-stu-id="a3582-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="a3582-107">Вкладке также могут требоваться сведения о языковом стандарте и теме оформления.</span><span class="sxs-lookup"><span data-stu-id="a3582-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="a3582-108">Возможно, на вкладке нужно написать `entityId` или `subEntityId`, чтобы пользователи могли сразу понять, что на ней находится.</span><span class="sxs-lookup"><span data-stu-id="a3582-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="a3582-109">Контекст пользователя</span><span class="sxs-lookup"><span data-stu-id="a3582-109">User context</span></span>

<span data-ttu-id="a3582-110">Контекст, описывающий пользователя, группу или компанию, может быть особенно полезен, когда:</span><span class="sxs-lookup"><span data-stu-id="a3582-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="a3582-111">Необходимо создать ресурсы в приложении или связать их с указанным пользователем или группой.</span><span class="sxs-lookup"><span data-stu-id="a3582-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="a3582-112">Вы хотите инициировать поток проверки подлинности для Azure Active Directory или другого поставщика удостоверений и не хотите заставлять пользователя снова вводить логин</span><span class="sxs-lookup"><span data-stu-id="a3582-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="a3582-113">(Дополнительные сведения о проверке подлинности на вкладке Microsoft Teams см. в статье [Проверка подлинности пользователя на вкладке Microsoft Teams](~/concepts/authentication/authentication.md).)</span><span class="sxs-lookup"><span data-stu-id="a3582-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a3582-114">Хотя эти сведения о пользователях помогают обеспечить плавное взаимодействие с пользователем, *не надо* использовать их в качестве подтверждения личности.</span><span class="sxs-lookup"><span data-stu-id="a3582-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="a3582-115">Например, злоумышленник может загрузить страницу в "плохом браузере" и показать опасные сведения или ввести злонамеренные запросы.</span><span class="sxs-lookup"><span data-stu-id="a3582-115">For example, an attacker could load your page in a "bad browser" and render harmful information or requests.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="a3582-116">Доступ к контексту</span><span class="sxs-lookup"><span data-stu-id="a3582-116">Accessing context</span></span>

<span data-ttu-id="a3582-117">Доступ к контекстной информации можно получить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="a3582-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="a3582-118">Вставлять значения заполнителей в URL-адреса</span><span class="sxs-lookup"><span data-stu-id="a3582-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="a3582-119">Использовать [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="a3582-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="a3582-120">Получение контекста путем вставки значений-заполнителей в URL-адреса</span><span class="sxs-lookup"><span data-stu-id="a3582-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="a3582-121">Используйте заполнители в конфигурации или в URL-адресах контента.</span><span class="sxs-lookup"><span data-stu-id="a3582-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="a3582-122">Microsoft Teams заменяет заполнители соответствующими значениями, когда определяет фактическую конфигурацию или URL-адрес контента.</span><span class="sxs-lookup"><span data-stu-id="a3582-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL.</span></span> <span data-ttu-id="a3582-123">В число доступных заполнителей входят все поля объекта [Контекст](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true).</span><span class="sxs-lookup"><span data-stu-id="a3582-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) object.</span></span> <span data-ttu-id="a3582-124">Распространенные сценарии:</span><span class="sxs-lookup"><span data-stu-id="a3582-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="a3582-125">{entityId}: ИД, который вы предоставили для элемента на этой вкладке при [первоначальной настройке](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="a3582-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="a3582-126">{subEntityId}: ИД, предоставленный при создании [прямой ссылки](~/concepts/build-and-test/deep-links.md) для определенного элемента _внутри_ этой вкладки. Его следует использовать для восстановления определенного состояния объекта, например прокрутки или активации определенного фрагмента содержимого.</span><span class="sxs-lookup"><span data-stu-id="a3582-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="a3582-127">{loginHint}: значение, подходящее в качестве подсказки для входа в Azure AD. Обычно это логин текущего пользователя в его домашнем клиенте.</span><span class="sxs-lookup"><span data-stu-id="a3582-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="a3582-128">{userPrincipalName}: имя субъекта-пользователя данного пользователя в данном клиенте.</span><span class="sxs-lookup"><span data-stu-id="a3582-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="a3582-129">{userObjectId}: ИД объекта Azure AD данного пользователя в данном клиенте.</span><span class="sxs-lookup"><span data-stu-id="a3582-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="a3582-130">{theme}: текущая тема пользовательского интерфейса, например `default`, `dark` или `contrast`.</span><span class="sxs-lookup"><span data-stu-id="a3582-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="a3582-131">{groupId}: ИД группы Office 365, в которой находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="a3582-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="a3582-132">{tid}: ИД объекта Azure AD текущего пользователя в текущем клиенте</span><span class="sxs-lookup"><span data-stu-id="a3582-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="a3582-133">{locale}: текущий языковой стандарт пользователя, отформатированный как languageId-countryId (например, en-us).</span><span class="sxs-lookup"><span data-stu-id="a3582-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="a3582-134">Предыдущий заполнитель `{upn}` теперь не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a3582-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="a3582-135">Для обратной совместимости в настоящее время он является синонимом для `{loginHint}`.</span><span class="sxs-lookup"><span data-stu-id="a3582-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="a3582-136">Например, предположим, что в манифесте вкладки для атрибута `configURL` установлено значение</span><span class="sxs-lookup"><span data-stu-id="a3582-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="a3582-137">При этом у пользователя, вошедшего в систему, есть следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="a3582-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="a3582-138">Имя пользователя : "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="a3582-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="a3582-139">ИД клиента компании: "e2653c-etc"</span><span class="sxs-lookup"><span data-stu-id="a3582-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="a3582-140">Пользователь входит в группу Office 365 с ИД "00209384-etc"</span><span class="sxs-lookup"><span data-stu-id="a3582-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="a3582-141">Пользователь установил тему Teams "темный"</span><span class="sxs-lookup"><span data-stu-id="a3582-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="a3582-142">При настройке вкладки Teams вызывает этот URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="a3582-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="a3582-143">Получение контекста с помощью библиотеки JavaScript для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a3582-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="a3582-144">Вы также можете получить сведения, перечисленные выше, с помощью [клиентского SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client), вызвав `microsoftTeams.getContext(function(context) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="a3582-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="a3582-145">Контекстная переменная должна выглядеть приблизительно как в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="a3582-145">The context variable will look like the following example.</span></span>

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
    "tenantSKU": "The license type for the current user tenant",
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

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="a3582-146">Получение контекста в закрытых каналах</span><span class="sxs-lookup"><span data-stu-id="a3582-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="a3582-147">Закрытые каналы в настоящее время находятся в закрытой предварительной версии для разработчиков.</span><span class="sxs-lookup"><span data-stu-id="a3582-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="a3582-148">Когда страница содержимого загружается в закрытый канал, данные, полученные от вызова `getContext`, можно замаскировать для защиты конфиденциальности канала.</span><span class="sxs-lookup"><span data-stu-id="a3582-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="a3582-149">Следующие поля будут изменены, если страница содержимого находится в закрытом канале.</span><span class="sxs-lookup"><span data-stu-id="a3582-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="a3582-150">Если на странице используется любое из значений, указанных ниже, необходимо проверить поле `channelType`, чтобы определить, загружена ли страница в частном канале, и действовать соответственно.</span><span class="sxs-lookup"><span data-stu-id="a3582-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="a3582-151">`groupId` - Не определено для закрытых каналов</span><span class="sxs-lookup"><span data-stu-id="a3582-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="a3582-152">`teamId` - Присвоить в качестве значения threadId закрытого канала</span><span class="sxs-lookup"><span data-stu-id="a3582-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="a3582-153">`teamName` - Присвоить в качестве значения имя закрытого канала</span><span class="sxs-lookup"><span data-stu-id="a3582-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="a3582-154">`teamSiteUrl` - Присвоить в качестве значения URL-адрес отдельного уникального сайта SharePoint для закрытого канала</span><span class="sxs-lookup"><span data-stu-id="a3582-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="a3582-155">`teamSitePath` - Присвоить в качестве значения путь отдельного уникального сайта SharePoint для закрытого канала</span><span class="sxs-lookup"><span data-stu-id="a3582-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="a3582-156">`teamSiteDomain` - Присвоить в качестве значения домен отдельного уникального сайта SharePoint для закрытого канала</span><span class="sxs-lookup"><span data-stu-id="a3582-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

> [!Note]
>  <span data-ttu-id="a3582-157">Переменная teamSiteUrl также хорошо работает для стандартных каналов.</span><span class="sxs-lookup"><span data-stu-id="a3582-157">teamSiteUrl works well for standard channels also.</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="a3582-158">Обработка изменений темы</span><span class="sxs-lookup"><span data-stu-id="a3582-158">Theme change handling</span></span>

<span data-ttu-id="a3582-159">Вы можете зарегистрировать свое приложение — тогда вы сможете получать уведомления о том, что тема изменится, вызовом `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span><span class="sxs-lookup"><span data-stu-id="a3582-159">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="a3582-160">Аргумент `theme` функции будет строкой со значением `default`, `dark`или `contrast`.</span><span class="sxs-lookup"><span data-stu-id="a3582-160">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>
