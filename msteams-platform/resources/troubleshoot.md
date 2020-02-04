---
title: Устранение неполадок в приложении
description: Устранение проблем и ошибок при создании приложений для Microsoft Teams
keywords: Устранение неполадок при разработке приложений Teams
ms.date: 07/09/2018
ms.openlocfilehash: f7fe42e7c1f3ff2c4d8d1cbe81ed8f71e6c04384
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675189"
---
# <a name="troubleshoot-your-microsoft-teams-app"></a><span data-ttu-id="8974c-104">Устранение неполадок в приложении Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="8974c-104">Troubleshoot your Microsoft Teams app</span></span>

## <a name="troubleshooting-tabs"></a><span data-ttu-id="8974c-105">Вкладки устранения неполадок</span><span class="sxs-lookup"><span data-stu-id="8974c-105">Troubleshooting tabs</span></span>

### <a name="accessing-the-devtools"></a><span data-ttu-id="8974c-106">Доступ к Девтулс</span><span class="sxs-lookup"><span data-stu-id="8974c-106">Accessing the DevTools</span></span>

<span data-ttu-id="8974c-107">Вы можете открыть [девтулс в клиенте Teams](~/tabs/how-to/developer-tools.md) для аналогичной функции, нажав клавишу F12 (в Windows) или Command-Option-I (on MacOS) в браузере.</span><span class="sxs-lookup"><span data-stu-id="8974c-107">You can open [DevTools in the Teams client](~/tabs/how-to/developer-tools.md) for a similar experience as pressing F12 (on Windows) or Command-Option-I (on MacOS) in a browser.</span></span>

### <a name="blank-tab-screen"></a><span data-ttu-id="8974c-108">Экран пустой вкладки</span><span class="sxs-lookup"><span data-stu-id="8974c-108">Blank tab screen</span></span>

<span data-ttu-id="8974c-109">Если вы не видите контент в представлении вкладок, может быть:</span><span class="sxs-lookup"><span data-stu-id="8974c-109">If you are not seeing your content in the tab view, it could be:</span></span>

* <span data-ttu-id="8974c-110">контент не может быть отображен в файле `<iframe>`.</span><span class="sxs-lookup"><span data-stu-id="8974c-110">your content cannot be displayed in an `<iframe>`.</span></span>
* <span data-ttu-id="8974c-111">домен контента не входит в список [валиддомаинс](~/resources/schema/manifest-schema.md#validdomains) в манифесте.</span><span class="sxs-lookup"><span data-stu-id="8974c-111">the content domain is not in the [validDomains](~/resources/schema/manifest-schema.md#validdomains) list in the manifest.</span></span>

### <a name="the-save-button-isnt-enabled-on-the-settings-dialog"></a><span data-ttu-id="8974c-112">Кнопка "Сохранить" недоступна в диалоговом окне "Параметры"</span><span class="sxs-lookup"><span data-stu-id="8974c-112">The Save button isn't enabled on the settings dialog</span></span>

<span data-ttu-id="8974c-113">Обязательно звоните `microsoftTeams.settings.setValidityState(true)` , когда пользователь настроил ввод или выбрал все необходимые данные на странице параметров, чтобы включить кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="8974c-113">Be sure to call `microsoftTeams.settings.setValidityState(true)` once the user has input or selected all required data on your settings page to enable the save button.</span></span>

### <a name="after-selecting-the-save-button-the-tab-settings-cannot-be-saved"></a><span data-ttu-id="8974c-114">После нажатия кнопки сохранить параметры вкладки невозможно сохранить</span><span class="sxs-lookup"><span data-stu-id="8974c-114">After selecting the Save button, the tab settings cannot be saved</span></span>

<span data-ttu-id="8974c-115">Если при добавлении вкладки нажать кнопку Сохранить, но отображается сообщение об ошибке с указанием на то, что параметры не могут быть сохранены, проблема может быть одним из двух классов проблем:</span><span class="sxs-lookup"><span data-stu-id="8974c-115">When adding a tab, if you click the save buttons but are presented with an error message indicating the settings cannot be saved, the problem could be one of two classes of issues:</span></span>

* <span data-ttu-id="8974c-116">Сообщение о сохранении успешности не было получено.</span><span class="sxs-lookup"><span data-stu-id="8974c-116">The save success message was never received.</span></span> <span data-ttu-id="8974c-117">Если обработчик сохранения зарегистрирован с помощью `microsoftTeams.settings.registerOnSaveHandler(handler)`, обратный вызов должен вызываться `saveEvent.notifySuccess()`.</span><span class="sxs-lookup"><span data-stu-id="8974c-117">If a save handler was registered using `microsoftTeams.settings.registerOnSaveHandler(handler)`, the callback must call `saveEvent.notifySuccess()`.</span></span> <span data-ttu-id="8974c-118">Если обратный вызов не вызывает его в течение 30 секунд или `saveEvent.notifyFailure(reason)` вызовов, отображается эта ошибка.</span><span class="sxs-lookup"><span data-stu-id="8974c-118">If the callback doesn't call this within 30 seconds or calls `saveEvent.notifyFailure(reason)` instead, this error will be shown.</span></span>

* <span data-ttu-id="8974c-119">Если обработчик сохранения не зарегистрирован, `saveEvent.notifySuccess()` вызов автоматически выполняется сразу после нажатия кнопки Сохранить.</span><span class="sxs-lookup"><span data-stu-id="8974c-119">If no save handler was registered, the `saveEvent.notifySuccess()` call is automatically made immediately upon the user selecting the save button.</span></span>

* <span data-ttu-id="8974c-120">Указаны недопустимые параметры.</span><span class="sxs-lookup"><span data-stu-id="8974c-120">The provided settings were invalid.</span></span> <span data-ttu-id="8974c-121">Другая причина, по которой эти параметры могут не сохраняться, заключается в `microsoftTeams.setSettings(settings)` том, что вызов предоставил недопустимый объект параметров, или вызов не был выполнен вообще.</span><span class="sxs-lookup"><span data-stu-id="8974c-121">The other reason the settings may not be saved is if the call to `microsoftTeams.setSettings(settings)` provided an invalid settings object, or the call wasn't made at all.</span></span> <span data-ttu-id="8974c-122">В следующем разделе представлены распространенные проблемы с объектом Settings.</span><span class="sxs-lookup"><span data-stu-id="8974c-122">See the next section, Common problems with the settings object.</span></span>

### <a name="common-problems-with-the-settings-object"></a><span data-ttu-id="8974c-123">Распространенные проблемы с объектом Settings</span><span class="sxs-lookup"><span data-stu-id="8974c-123">Common problems with the settings object</span></span>

* <span data-ttu-id="8974c-124">`settings.entityId`отсутствует.</span><span class="sxs-lookup"><span data-stu-id="8974c-124">`settings.entityId` is missing.</span></span> <span data-ttu-id="8974c-125">Это поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="8974c-125">This field is required.</span></span>
* <span data-ttu-id="8974c-126">`settings.contentUrl`отсутствует.</span><span class="sxs-lookup"><span data-stu-id="8974c-126">`settings.contentUrl` is missing.</span></span> <span data-ttu-id="8974c-127">Это поле является обязательным.</span><span class="sxs-lookup"><span data-stu-id="8974c-127">This field is required.</span></span>
* <span data-ttu-id="8974c-128">`settings.contentUrl`необязательные `settings.removeUrl`или необязательные или `settings.websiteUrl` предоставленные, но недопустимые.</span><span class="sxs-lookup"><span data-stu-id="8974c-128">`settings.contentUrl` or the optional `settings.removeUrl`, or `settings.websiteUrl` are provided but not valid.</span></span> <span data-ttu-id="8974c-129">URL-адреса должны использовать HTTPS, а также должны быть того же домена, что и на странице параметров или в `validDomains` списке манифеста.</span><span class="sxs-lookup"><span data-stu-id="8974c-129">The URLs must use HTTPS and also must either be the same domain as the settings page or specified in the manifest's `validDomains` list.</span></span>

### <a name="cant-authenticate-the-user-or-display-your-auth-provider-in-your-tab"></a><span data-ttu-id="8974c-130">Не удается проверить подлинность пользователя или отобразить поставщика проверки подлинности на вкладке</span><span class="sxs-lookup"><span data-stu-id="8974c-130">Can't authenticate the user or display your auth provider in your tab</span></span>

<span data-ttu-id="8974c-131">Если вы не выполняете автоматическую проверку подлинности, необходимо соблюдать процесс проверки подлинности, предоставляемый [клиентским пакетом SDK для Microsoft Teams JavaScript](/javascript/api/overview/msteams-client.md).</span><span class="sxs-lookup"><span data-stu-id="8974c-131">Unless you are doing silent authentication, you must follow the authentication process provided by the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client.md).</span></span>

> [!NOTE]
><span data-ttu-id="8974c-132">Необходимо, чтобы весь процесс проверки подлинности был запущен и завершен для вашего домена, который должен `validDomains` быть указан в объекте в манифесте.</span><span class="sxs-lookup"><span data-stu-id="8974c-132">We require all authentication flow to start and end on your domain, which must be listed in the `validDomains` object in your manifest.</span></span>

<span data-ttu-id="8974c-133">Для получения дополнительных сведений о проверке подлинности обратитесь к разделу Проверка [подлинности пользователя](~/concepts/authentication/authentication.md).</span><span class="sxs-lookup"><span data-stu-id="8974c-133">For more information about authentication, please see [Authenticate a user](~/concepts/authentication/authentication.md).</span></span>

### <a name="static-tabs-not-showing-up"></a><span data-ttu-id="8974c-134">Не отображаются статические вкладки</span><span class="sxs-lookup"><span data-stu-id="8974c-134">Static tabs not showing up</span></span>

<span data-ttu-id="8974c-135">Существует известная ошибка, из-за которой при обновлении существующего приложения-робота с помощью новой или обновленной статической вкладки не будет показано изменение вкладки при доступе к приложению из беседы личного чата.</span><span class="sxs-lookup"><span data-stu-id="8974c-135">There is a known issue where updating an existing bot app with a new or updated static tab will not show that tab change when accessing the app from a personal chat conversation.</span></span>  <span data-ttu-id="8974c-136">Чтобы просмотреть изменения, необходимо проверить нового пользователя или тестового экземпляра или получить доступ к Bot из всплывающего меню приложения.</span><span class="sxs-lookup"><span data-stu-id="8974c-136">To see the change, you should test on a new user or test instance, or access the bot from the Apps flyout.</span></span>

## <a name="troubleshooting-bots"></a><span data-ttu-id="8974c-137">Устранение неполадок Боты</span><span class="sxs-lookup"><span data-stu-id="8974c-137">Troubleshooting bots</span></span>

### <a name="cant-add-my-bot"></a><span data-ttu-id="8974c-138">Не удается добавить мой Bot</span><span class="sxs-lookup"><span data-stu-id="8974c-138">Can't add my bot</span></span>

<span data-ttu-id="8974c-139">Приложения должны быть включены администратором клиента Office 365, чтобы они загружались конечными пользователями.</span><span class="sxs-lookup"><span data-stu-id="8974c-139">Apps must be enabled by the Office 365 tenant admin for them to be loaded by end users.</span></span> <span data-ttu-id="8974c-140">Обратите внимание, что в некоторых случаях у клиента Office 365 может быть связано несколько номеров SKU, и для работы боты в любом случае он должен быть включен во всех SKU.</span><span class="sxs-lookup"><span data-stu-id="8974c-140">Note that in some cases, the Office 365 tenant might have multiple SKUs associated with it, and for bots to work in any, they must be enabled in all SKUs.</span></span> <span data-ttu-id="8974c-141">Более подробную информацию можно найти [в статье Подготовка клиента Office 365](~/concepts/build-and-test/prepare-your-o365-tenant.md) .</span><span class="sxs-lookup"><span data-stu-id="8974c-141">See [Prepare your Office 365 tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for more information.</span></span>

### <a name="cant-add-bot-as-a-member-of-a-team"></a><span data-ttu-id="8974c-142">Не удается добавить Bot в качестве участника команды</span><span class="sxs-lookup"><span data-stu-id="8974c-142">Can't add bot as a member of a team</span></span>

<span data-ttu-id="8974c-143">Сначала необходимо отправить боты в команду, чтобы она была доступна в любом канале этой команды.</span><span class="sxs-lookup"><span data-stu-id="8974c-143">Bots must first be upload into a team before it is accessible within any channel of that team.</span></span> <span data-ttu-id="8974c-144">Изучите [отправку своего приложения в команду, чтобы](~/concepts/deploy-and-publish/apps-upload.md) получить дополнительные сведения об этом процессе.</span><span class="sxs-lookup"><span data-stu-id="8974c-144">Please review [Uploading your app in a team](~/concepts/deploy-and-publish/apps-upload.md) for more information on this process.</span></span>

### <a name="my-bot-doesnt-get-my-message-in-a-channel"></a><span data-ttu-id="8974c-145">Мой робот не получает сообщение в канале</span><span class="sxs-lookup"><span data-stu-id="8974c-145">My bot doesn't get my message in a channel</span></span>

<span data-ttu-id="8974c-146">Боты в каналах получают сообщения только в том случае, если они явно @mentioned, даже если вы отвечаете на предыдущее сообщение Bot.</span><span class="sxs-lookup"><span data-stu-id="8974c-146">Bots in channels receive messages only when they are explicitly @mentioned, even if you are replying to a previous bot message.</span></span> <span data-ttu-id="8974c-147">Единственное исключение, в котором имя Bot может отсутствовать в сообщении, состоит в том, что Bot получает `imBack` действие в результате кардактион.</span><span class="sxs-lookup"><span data-stu-id="8974c-147">The only exception where you might not see the bot name in a message is if the bot receives an `imBack` action as a result of a CardAction that it originally sent.</span></span>

### <a name="my-bot-doesnt-understand-my-commands-when-in-a-channel"></a><span data-ttu-id="8974c-148">Мой Bot не распознает команды в канале</span><span class="sxs-lookup"><span data-stu-id="8974c-148">My bot doesn't understand my commands when in a channel</span></span>

<span data-ttu-id="8974c-149">Так как боты в каналах получают сообщения, только когда они @mentioned, все сообщения, которые поступают в канале от канала почтовых роботов, включают @mention в текстовое поле.</span><span class="sxs-lookup"><span data-stu-id="8974c-149">Because bots in channels only receive messages when they are @mentioned, all messages that your bot receives in a channel include that @mention in the text field.</span></span> <span data-ttu-id="8974c-150">Рекомендуется извлекать само имя Bot из всех входящих текстовых сообщений, прежде чем передавать логику синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="8974c-150">It is a best practice to strip the bot name itself out of all incoming text messages before passing along to your parsing logic.</span></span> <span data-ttu-id="8974c-151">Просмотрите [упоминания](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) , чтобы узнать, как справиться с этим обращением.</span><span class="sxs-lookup"><span data-stu-id="8974c-151">Review [Mentions](~/bots/how-to/conversations/channel-and-group-conversations.md#working-with--mentions) for tips on how to handle this case.</span></span>

## <a name="issues-with-packaging-and-uploading"></a><span data-ttu-id="8974c-152">Проблемы с упаковкой и отправкой</span><span class="sxs-lookup"><span data-stu-id="8974c-152">Issues with packaging and uploading</span></span>

### <a name="error-while-reading-manifestjson"></a><span data-ttu-id="8974c-153">Ошибка при чтении манифеста. JSON</span><span class="sxs-lookup"><span data-stu-id="8974c-153">Error while reading manifest.json</span></span>

<span data-ttu-id="8974c-154">Большинство ошибок манифеста содержит подсказку о том, что конкретное поле отсутствует или не является допустимым.</span><span class="sxs-lookup"><span data-stu-id="8974c-154">Most  manifest errors will provide a hint at what specific field is missing or invalid.</span></span> <span data-ttu-id="8974c-155">Тем не менее, если JSON-файл не может быть прочитан как JSON вообще, используется это общее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="8974c-155">However, if the JSON file cannot be read as JSON at all, this generic error message is used.</span></span>

<span data-ttu-id="8974c-156">Распространенные причины ошибок чтения манифеста:</span><span class="sxs-lookup"><span data-stu-id="8974c-156">Common reasons for manifest read errors:</span></span>

* <span data-ttu-id="8974c-157">Недопустимый формат JSON.</span><span class="sxs-lookup"><span data-stu-id="8974c-157">Invalid JSON.</span></span> <span data-ttu-id="8974c-158">Используйте IDE, например [Visual Studio Code](https://code.visualstudio.com) или [Visual Studio](https://www.visualstudio.com/vs/) , которая автоматически проверяет синтаксис JSON.</span><span class="sxs-lookup"><span data-stu-id="8974c-158">Use an IDE such as [Visual Studio Code](https://code.visualstudio.com) or [Visual Studio](https://www.visualstudio.com/vs/) that automatically validates the JSON syntax.</span></span>
* <span data-ttu-id="8974c-159">Проблемы кодирования.</span><span class="sxs-lookup"><span data-stu-id="8974c-159">Encoding issues.</span></span> <span data-ttu-id="8974c-160">Используйте кодировку UTF – 8 для файла *manifest. JSON* .</span><span class="sxs-lookup"><span data-stu-id="8974c-160">Use UTF-8 for the *manifest.json* file.</span></span> <span data-ttu-id="8974c-161">Другие кодировки, в частности, с КОМПЛЕКТом, могут быть недоступны для чтения.</span><span class="sxs-lookup"><span data-stu-id="8974c-161">Other encodings, specifically with the BOM, may not be readable.</span></span>
* <span data-ttu-id="8974c-162">Неправильно сформированный ZIP-пакет.</span><span class="sxs-lookup"><span data-stu-id="8974c-162">Malformed .zip package.</span></span> <span data-ttu-id="8974c-163">Файл *manifest. JSON* должен находиться на верхнем уровне ZIP-файла.</span><span class="sxs-lookup"><span data-stu-id="8974c-163">The *manifest.json* file must be at the top level of the .zip file.</span></span> <span data-ttu-id="8974c-164">Обратите внимание на то, что сжатие файлов Mac по умолчанию может поместить файл *manifest. JSON* в подкаталог, который не будет загружаться должным образом в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="8974c-164">Note that default Mac file compression might place the *manifest.json* in a subdirectory, which will not properly load in Microsoft Teams.</span></span>

### <a name="another-extension-with-same-id-exists"></a><span data-ttu-id="8974c-165">Существует другой добавочный номер с таким же идентификатором</span><span class="sxs-lookup"><span data-stu-id="8974c-165">Another extension with same ID exists</span></span>

<span data-ttu-id="8974c-166">Если вы пытаетесь повторно отправить обновленный пакет с тем же ИДЕНТИФИКАТОРом, выберите значок **заменить** в конце строки таблицы вкладки, а не кнопку **Отправить** .</span><span class="sxs-lookup"><span data-stu-id="8974c-166">If you're attempting to re-upload an updated package with the same ID, choose the **Replace** icon at the end of the tab's table row rather than the **Upload** button.</span></span>

<span data-ttu-id="8974c-167">Если вы не отправляете обновленный пакет повторно, убедитесь, что этот идентификатор уникален.</span><span class="sxs-lookup"><span data-stu-id="8974c-167">If you're not re-uploading an updated package, ensure that the ID is unique.</span></span>