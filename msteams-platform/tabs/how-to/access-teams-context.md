---
title: Получение контекста для вкладки
description: Сведения о получении контекста пользователя для вкладок
keywords: контекст пользователя вкладок Teams
ms.openlocfilehash: 01919999e38d6b659f014b0f05b76d3f332db9ab
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801222"
---
# <a name="get-context-for-your-microsoft-teams-tab"></a><span data-ttu-id="69295-104">Получение контекста для вкладки Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="69295-104">Get context for your Microsoft Teams tab</span></span>

<span data-ttu-id="69295-105">Для отображения соответствующего контента на вкладке может потребоваться Контекстная информация.</span><span class="sxs-lookup"><span data-stu-id="69295-105">Your tab might require contextual information to display relevant content.</span></span>

* <span data-ttu-id="69295-106">Для вкладки могут потребоваться основные сведения о пользователе, команде или компании.</span><span class="sxs-lookup"><span data-stu-id="69295-106">Your tab might need basic information about the user, team, or company.</span></span>
* <span data-ttu-id="69295-107">Для вкладки может потребоваться информация о языковых стандартах и теме.</span><span class="sxs-lookup"><span data-stu-id="69295-107">Your tab might need locale and theme information.</span></span>
* <span data-ttu-id="69295-108">На вкладке может потребоваться прочитать `entityId` или `subEntityId` определить, что находится на этой вкладке.</span><span class="sxs-lookup"><span data-stu-id="69295-108">Your tab might need to read the `entityId` or `subEntityId` that identifies what is in this tab.</span></span>

## <a name="user-context"></a><span data-ttu-id="69295-109">Контекст пользователя</span><span class="sxs-lookup"><span data-stu-id="69295-109">User context</span></span>

<span data-ttu-id="69295-110">Контекст пользователя, группы или компании особенно полезен при</span><span class="sxs-lookup"><span data-stu-id="69295-110">Context about the user, team or company can be especially useful when</span></span>

* <span data-ttu-id="69295-111">Необходимо создать или связать ресурсы в приложении с указанным пользователем или группой.</span><span class="sxs-lookup"><span data-stu-id="69295-111">You need to create or associate resources in your app with the specified user or team.</span></span>
* <span data-ttu-id="69295-112">Вы хотите инициировать процесс проверки подлинности для Azure Active Directory или другого поставщика удостоверений и не требовать от пользователя повторного ввода имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="69295-112">You want to initiate an authentication flow against Azure Active Directory or other identity provider, and you don't want to require the user to enter their username again.</span></span> <span data-ttu-id="69295-113">(Дополнительные сведения о проверке подлинности на вкладке Microsoft Teams можно найти [в разделе Проверка подлинности пользователя на вкладке Microsoft Teams](~/concepts/authentication/authentication.md).)</span><span class="sxs-lookup"><span data-stu-id="69295-113">(For more information on authenticating within your Microsoft Teams tab, see [Authenticate a user in your Microsoft Teams tab](~/concepts/authentication/authentication.md).)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="69295-114">Несмотря на то что эти сведения о пользователях помогают обеспечить гладкую работу пользователей, *не* следует использовать его для подтверждения подлинности.</span><span class="sxs-lookup"><span data-stu-id="69295-114">Although this user information can help provide a smooth user experience, you should *not* use it as proof of identity.</span></span> <span data-ttu-id="69295-115">Например, злоумышленник может загрузить страницу в «плохой браузер» и предоставить ей любую нужную информацию.</span><span class="sxs-lookup"><span data-stu-id="69295-115">For example, an attacker could you load your page in a "bad browser" and provide it with any information they want.</span></span>

## <a name="accessing-context"></a><span data-ttu-id="69295-116">Доступ к контексту</span><span class="sxs-lookup"><span data-stu-id="69295-116">Accessing context</span></span>

<span data-ttu-id="69295-117">Доступ к сведениям о контексте можно получить двумя способами:</span><span class="sxs-lookup"><span data-stu-id="69295-117">You can access context information in two ways:</span></span>

* <span data-ttu-id="69295-118">Вставка значений заполнителей URL-адресов</span><span class="sxs-lookup"><span data-stu-id="69295-118">Insert URL placeholder values</span></span>
* <span data-ttu-id="69295-119">Использование [пакета SDK клиента JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="69295-119">Use the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client)</span></span>

### <a name="getting-context-by-inserting-url-placeholder-values"></a><span data-ttu-id="69295-120">Извлечение контекста путем вставки значений заполнители URL-адресов</span><span class="sxs-lookup"><span data-stu-id="69295-120">Getting context by inserting URL placeholder values</span></span>

<span data-ttu-id="69295-121">Используйте заполнители в URL-адресах конфигурации или контента.</span><span class="sxs-lookup"><span data-stu-id="69295-121">Use placeholders in your configuration or content URLs.</span></span> <span data-ttu-id="69295-122">Microsoft Teams заменяет заполнители соответствующими значениями при определении фактической конфигурации или URL-адреса контента, к которому выполняется переход.</span><span class="sxs-lookup"><span data-stu-id="69295-122">Microsoft Teams replaces the placeholders with the relevant values when determining the actual configuration or content URL to navigate to.</span></span> <span data-ttu-id="69295-123">Доступные заполнители включают все поля в объекте [context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) .</span><span class="sxs-lookup"><span data-stu-id="69295-123">The available placeholders include all fields on the [Context](/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) object.</span></span> <span data-ttu-id="69295-124">Общие заполнители включают в себя следующее:</span><span class="sxs-lookup"><span data-stu-id="69295-124">Common placeholders include the following:</span></span>

* <span data-ttu-id="69295-125">{Ентитид}: идентификатор, указанный для элемента на этой вкладке при первой [настройке вкладки](~/tabs/how-to/create-tab-pages/configuration-page.md).</span><span class="sxs-lookup"><span data-stu-id="69295-125">{entityId}: The ID you supplied for the item in this tab when first [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>
* <span data-ttu-id="69295-126">{Субентитид}: идентификатор, указанный при создании [детальной ссылки](~/concepts/build-and-test/deep-links.md) для _определенного элемента на_ этой вкладке. Используется для восстановления в определенном состоянии в пределах объекта; Например, прокрутите или активируйте определенный фрагмент содержимого.</span><span class="sxs-lookup"><span data-stu-id="69295-126">{subEntityId}: The ID you supplied when generating a [deep link](~/concepts/build-and-test/deep-links.md) for a specific item _within_ this tab. This should be used to restore to a specific state within an entity; for example, scrolling to or activating a specific piece of content.</span></span>
* <span data-ttu-id="69295-127">{Логинхинт}: значение, которое подходит как подсказка для входа для Azure AD. Как правило, это имя входа текущего пользователя в его домашнем клиенте.</span><span class="sxs-lookup"><span data-stu-id="69295-127">{loginHint}: A value suitable as a login hint for Azure AD.This is usually the login name of the current user, in their home tenant.</span></span>
* <span data-ttu-id="69295-128">{userPrincipalName}: имя участника пользователя текущего пользователя в текущем клиенте.</span><span class="sxs-lookup"><span data-stu-id="69295-128">{userPrincipalName}: The User Principal Name of the current user, in the current tenant.</span></span>
* <span data-ttu-id="69295-129">{Усеробжектид}: идентификатор объекта Azure AD текущего пользователя в текущем клиенте.</span><span class="sxs-lookup"><span data-stu-id="69295-129">{userObjectId}: The Azure AD object ID of the current user, in the current tenant.</span></span>
* <span data-ttu-id="69295-130">{Theme}: текущие темы пользовательского интерфейса, такие как `default` , `dark` или `contrast` .</span><span class="sxs-lookup"><span data-stu-id="69295-130">{theme}: The current UI theme such as `default`, `dark`, or `contrast`.</span></span>
* <span data-ttu-id="69295-131">{groupId}: идентификатор группы Office 365, в которой находится вкладка.</span><span class="sxs-lookup"><span data-stu-id="69295-131">{groupId}: The ID of the Office 365 Group in which the tab resides.</span></span>
* <span data-ttu-id="69295-132">{TID}: идентификатор клиента Azure AD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="69295-132">{tid}: The Azure AD tenant ID of the current user.</span></span>
* <span data-ttu-id="69295-133">{locale}: текущий языковой стандарт пользователя, отформатированный как languageId-Каунтрид (например, EN-US).</span><span class="sxs-lookup"><span data-stu-id="69295-133">{locale}: The current locale of the user formatted as languageId-countryId (for example, en-us).</span></span>

>[!NOTE]
><span data-ttu-id="69295-134">Предыдущий `{upn}` заполнитель теперь не является устаревшим.</span><span class="sxs-lookup"><span data-stu-id="69295-134">The previous `{upn}` placeholder is now deprecated.</span></span> <span data-ttu-id="69295-135">Для обратной совместимости он в настоящее время является синонимом `{loginHint}` .</span><span class="sxs-lookup"><span data-stu-id="69295-135">For backward compatibility, it is currently a synonym for `{loginHint}`.</span></span>

<span data-ttu-id="69295-136">Например, предположим, что в манифесте вкладки атрибуту присвоено значение `configURL`</span><span class="sxs-lookup"><span data-stu-id="69295-136">For example, suppose in your tab manifest you set the `configURL` attribute to</span></span>

`"https://www.contoso.com/config?name={loginHint}&tenant={tid}&group={groupId}&theme={theme}"`

<span data-ttu-id="69295-137">И пользователь, вошедшего в систему, имеет следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="69295-137">And the signed-in user has the following attributes:</span></span>

* <span data-ttu-id="69295-138">Имя пользователя — "user@example.com"</span><span class="sxs-lookup"><span data-stu-id="69295-138">Their username is 'user@example.com'</span></span>
* <span data-ttu-id="69295-139">Идентификатор клиента компании — "e2653c-and-etc"</span><span class="sxs-lookup"><span data-stu-id="69295-139">Their company tenant ID is 'e2653c-etc'</span></span>
* <span data-ttu-id="69295-140">Они являются членами группы Office 365 с идентификатором ' 00209384 ' и т. д.</span><span class="sxs-lookup"><span data-stu-id="69295-140">They are a member of the Office 365 group with id '00209384-etc'</span></span>
* <span data-ttu-id="69295-141">Тема Teams пользователя задается "темная"</span><span class="sxs-lookup"><span data-stu-id="69295-141">The user has set their Teams theme to 'dark'</span></span>

<span data-ttu-id="69295-142">При настройке вкладки Teams вызывает этот URL-адрес:</span><span class="sxs-lookup"><span data-stu-id="69295-142">When they configure your tab, Teams calls this URL:</span></span>

`https://www.contoso.com/config?name=user@example.com&tenant=e2653c-etc&group=00209384-etc&theme=dark`

### <a name="getting-context-by-using-the-microsoft-teams-javascript-library"></a><span data-ttu-id="69295-143">Извлечение контекста с помощью библиотеки JavaScript для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="69295-143">Getting context by using the Microsoft Teams JavaScript library</span></span>

<span data-ttu-id="69295-144">Вы также можете получить приведенные выше сведения с помощью [пакета SDK для JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) , вызвав `microsoftTeams.getContext(function(context) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="69295-144">You can also retrieve the information listed above using the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client) by calling `microsoftTeams.getContext(function(context) { /* ... */ })`.</span></span>

<span data-ttu-id="69295-145">Переменная контекста будет выглядеть так, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="69295-145">The context variable will look like the following example.</span></span>

```json
{
    "teamId": "The Microsoft Teams ID in the format 19:[id]@thread.skype",
    "teamName": "The name of the current team",
    "channelId": "The channel ID in the format 19:[id]@thread.skype",
    "channelName": "The name of the current channel",
    "chatId": "The chat ID in the in the format 19:[id]@thread.skype",
    "locale": "The current locale of the user formatted as languageId-countryId (for example, en-us)",
    "entityId": "The developer-defined unique ID for the entity this content points to",
    "subEntityId": "The developer-defined unique ID for the sub-entity this content points to",
    "loginHint": "A value suitable as a login hint for Azure AD. This is usually the login name of the current user, in their home tenant",
    "userPrincipalName": "The User Principal Name of the current user, in the current tenant",
    "userObjectId": "The Azure AD object id of the current user, in the current tenant",
    "tid": "The Azure AD tenant ID of the current user",
    "groupId": "Guid identifying the current O365 Group ID",
    "theme": "The current UI theme: default | dark | contrast",
    "isFullScreen": "Indicates whether the tab is in full-screen mode",
    "userLicenseType": "Indicates the user licence type in the given SKU (for example, student or teacher)",
    "tenantSKU": "Indicates the SKU category of the tenant (for example, EDU)",
    "channelType": "microsoftTeams.ChannelType.Private | microsoftTeams.ChannelType.Regular"
}
```

## <a name="retrieving-context-in-private-channels"></a><span data-ttu-id="69295-146">Получение контекста в частных каналах</span><span class="sxs-lookup"><span data-stu-id="69295-146">Retrieving context in private channels</span></span>

> [!Note]
> <span data-ttu-id="69295-147">В настоящее время частные каналы находятся в предварительной версии для разработчиков личных версий.</span><span class="sxs-lookup"><span data-stu-id="69295-147">Private channels are currently in private developer preview.</span></span>

<span data-ttu-id="69295-148">Когда страница контента загружается в частном канале, данные, получаемые из `getContext` вызова, будут замаскированы для защиты конфиденциальности канала.</span><span class="sxs-lookup"><span data-stu-id="69295-148">When your content page is loaded in a private channel, the data you receive from the `getContext` call will be obfuscated to protect the privacy of the channel.</span></span> <span data-ttu-id="69295-149">Следующие поля изменяются, когда страница контента находится в частном канале.</span><span class="sxs-lookup"><span data-stu-id="69295-149">The following fields are changed when your content page is in a private channel.</span></span> <span data-ttu-id="69295-150">Если страница использует любое из указанных ниже значений, необходимо проверить `channelType` поле, чтобы определить, загружена ли страница в частном канале, и ответить соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="69295-150">If your page makes use of any of the values below, you'll need to check the `channelType` field to determine if your page is loaded in a private channel, and respond appropriately.</span></span>

* <span data-ttu-id="69295-151">`groupId`— Не определено для частных каналов</span><span class="sxs-lookup"><span data-stu-id="69295-151">`groupId` - Undefined for private channels</span></span>
* <span data-ttu-id="69295-152">`teamId`— Задает threadId для частного канала</span><span class="sxs-lookup"><span data-stu-id="69295-152">`teamId` - Set to the threadId of the private channel</span></span>
* <span data-ttu-id="69295-153">`teamName`— Укажите имя закрытого канала.</span><span class="sxs-lookup"><span data-stu-id="69295-153">`teamName` - Set to the name of the private channel</span></span>
* <span data-ttu-id="69295-154">`teamSiteUrl`-Задать URL-адрес уникального уникального сайта SharePoint для частного канала</span><span class="sxs-lookup"><span data-stu-id="69295-154">`teamSiteUrl` - Set to the URL of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="69295-155">`teamSitePath`-Задать путь к отдельному, уникальному сайту SharePoint для частного канала</span><span class="sxs-lookup"><span data-stu-id="69295-155">`teamSitePath` - Set to the path of a distinct, unique SharePoint site for the private channel</span></span>
* <span data-ttu-id="69295-156">`teamSiteDomain`— Укажите домен для частного канала в отдельном домене сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="69295-156">`teamSiteDomain` - Set to the domain of a distinct, unique SharePoint site domain for the private channel</span></span>

## <a name="theme-change-handling"></a><span data-ttu-id="69295-157">Обработка изменений темы</span><span class="sxs-lookup"><span data-stu-id="69295-157">Theme change handling</span></span>

<span data-ttu-id="69295-158">Вы можете зарегистрировать свое приложение, чтобы сообщить, изменяется ли тема с помощью вызова `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })` .</span><span class="sxs-lookup"><span data-stu-id="69295-158">You can register your app to be told if the theme changes by calling `microsoftTeams.registerOnThemeChangeHandler(function(theme) { /* ... */ })`.</span></span>

<span data-ttu-id="69295-159">`theme`Аргумент в функции будет строкой со значением `default` , `dark` или `contrast` .</span><span class="sxs-lookup"><span data-stu-id="69295-159">The `theme` argument in the function will be a string with a value of `default`, `dark`, or `contrast`.</span></span>