---
title: Соединители Office 365
description: Описание начала работы с соединитетелями Office 365 в Microsoft Teams
keywords: соединитель teams o365
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 62a27e8f7b218491682ff0b9216e428f51264d0a
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739051"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="9c5a2-104">Создание соединители Office 365 для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="9c5a2-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="9c5a2-105">С помощью приложений Microsoft Teams вы можете добавить существующий соединителю Office 365 или создать новый, чтобы включить его в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="9c5a2-106">Дополнительные [сведения см.](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) в подключении "Создание собственного соединитела".</span><span class="sxs-lookup"><span data-stu-id="9c5a2-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="9c5a2-107">Добавление соединители в приложение Teams</span><span class="sxs-lookup"><span data-stu-id="9c5a2-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="9c5a2-108">Вы можете распространять зарегистрированный соединитатель в составе пакета приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="9c5a2-109">Независимо от того, является ли приложение автономным решением или одной из [](~/concepts/build-and-test/apps-package.md) нескольких [](~/concepts/deploy-and-publish/apps-publish.md) возможностей Teams, вы можете упаковать и опубликовать соединитель в составе отправки в AppSource или предоставить его пользователям непосредственно для отправки в Teams. [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="9c5a2-110">Чтобы распространять соединители, необходимо зарегистрироваться с помощью панели мониторинга [разработчика соединитеителей.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="9c5a2-111">По умолчанию после регистрации соединитела предполагается, что он будет работать во всех продуктах Office 365, которые их поддерживают, включая Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="9c5a2-112">Если это _не так_ и вам нужно создать соединителя, который работает только в Microsoft Teams, свяжитесь с нами непосредственно на веб-сайте "Отправки приложений Microsoft [Teams".](mailto:teamsubm@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c5a2-113">После выбора **"Сохранить"** в информационной панели разработчика соединитеителей соединитель будет зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="9c5a2-114">Если вы хотите опубликовать соединители в AppSource, следуйте инструкциям в публикации приложения [Microsoft Teams в AppSource.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="9c5a2-115">Если вы не хотите публиковать приложение в AppSource, а просто распространяете его непосредственно в вашей организации, это можно сделать, опубликуя приложение [в своей организации.](#publish-connectors-for-your-organization)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="9c5a2-116">Если вы хотите опубликовать только в своей организации, никаких дополнительных действий на панели мониторинга соединители не требуется.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="9c5a2-117">Интеграция работы с конфигурацией</span><span class="sxs-lookup"><span data-stu-id="9c5a2-117">Integrating the configuration experience</span></span>

<span data-ttu-id="9c5a2-118">Пользователи будут полностью работать с конфигурацией соединители, не покидая клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="9c5a2-119">Для этого Teams встраит страницу конфигурации непосредственно в iframe.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="9c5a2-120">Последовательность операций:</span><span class="sxs-lookup"><span data-stu-id="9c5a2-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="9c5a2-121">Чтобы начать процесс настройки, пользователь щелкает соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="9c5a2-122">Teams загрузит ваш опыт настройки в строке.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="9c5a2-123">Пользователь взаимодействует с веб-интерфейсом для завершения настройки.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="9c5a2-124">Пользователь нажал кнопку "Сохранить", что вызывает в коде вызов.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="9c5a2-125">Код обрабатывает событие сохранения, искомые параметры веб-hook (задокументированы ниже).</span><span class="sxs-lookup"><span data-stu-id="9c5a2-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="9c5a2-126">Затем в коде должен храниться веб-сайт для публикации событий позже.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="9c5a2-127">Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет предназначена специально для Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="9c5a2-128">Код должен:</span><span class="sxs-lookup"><span data-stu-id="9c5a2-128">Your code should:</span></span>

1. <span data-ttu-id="9c5a2-129">Включит в него SDK JavaScript для Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="9c5a2-130">Это дает коду доступ к API для выполнения распространенных операций, таких как получение текущего контекста пользователя, канала или группы и инициирование потоков проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="9c5a2-131">Инициализировать SDK с помощью `microsoftTeams.initialize()` вызова.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="9c5a2-132">Вызовите `microsoftTeams.settings.setValidityState(true)` этот вызов, если нужно включить кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="9c5a2-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="9c5a2-133">Это следует сделать в ответ на допустимые данные пользователя, такие как выбор или обновление поля.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="9c5a2-134">`microsoftTeams.settings.registerOnSaveHandler()`Зарегистрируйте обработок событий, который будет вызван, когда пользователь нажмет кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="9c5a2-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="9c5a2-135">Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="9c5a2-136">Здесь также будет показано, что будет показано в диалоговом окне конфигурации, если пользователь попытается обновить существующую конфигурацию для соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="9c5a2-137">Вызов `microsoftTeams.settings.getSettings()` для получения свойств веб-hook, включая сам URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="9c5a2-138">Этот вызов следует вызывать не только во время события сохранения, но и при первой загрузке страницы при повторной настройке.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="9c5a2-139">(Необязательно) `microsoftTeams.settings.registerOnRemoveHandler()` Зарегистрируйте обработчик событий, который будет вызван, когда пользователь удалит соединитер.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="9c5a2-140">Это событие предоставляет службе возможность выполнять любые действия по очистке.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="9c5a2-141">Вот пример HTML для создания страницы конфигурации соединителя без CSS:</span><span class="sxs-lookup"><span data-stu-id="9c5a2-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

```html
<h2>Send notifications when tasks are:</h2>
<div class="col-md-8">
    <section id="configSection">
        <form id="configForm">
            <input type="radio" name="notificationType" value="Create" onclick="onClick()"> Created
            <br>
            <br>
            <input type="radio" name="notificationType" value="Update" onclick="onClick()"> Updated
        </form>
    </section>
</div>

<script src="https://statics.teams.microsoft.com/sdk/v1.5.2/js/MicrosoftTeams.min.js" crossorigin="anonymous"></script>
<script src="/Scripts/jquery-1.10.2.js"></script>

<script type="text/javascript">

        function onClick() {
            microsoftTeams.settings.setValidityState(true);
        }

        microsoftTeams.initialize();
        microsoftTeams.settings.registerOnSaveHandler(function (saveEvent) {
            var radios = document.getElementsByName('notificationType');

            var eventType = '';
            if (radios[0].checked) {
                eventType = radios[0].value;
            } else {
                eventType = radios[1].value;
            }

            microsoftTeams.settings.setSettings({
                 entityId: eventType,
                contentUrl: "https://YourSite/Connector/Setup",
                removeUrl:"https://YourSite/Connector/Setup",
                 configName: eventType
                });

            microsoftTeams.settings.getSettings(function (settings) {
                // We get the Webhook URL in settings.webhookUrl which needs to be saved. 
                // This can be used later to send notification.
            });

            saveEvent.notifySuccess();
        });

        microsoftTeams.settings.registerOnRemoveHandler(function (removeEvent) {
            var removeCalled = true;
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="9c5a2-142">`GetSettings()` свойства ответа</span><span class="sxs-lookup"><span data-stu-id="9c5a2-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="9c5a2-143">Параметры, возвращенные здесь вызовом, отличаются от параметров, которые были бы вызваны этим методом на вкладке, и отличаются от параметров, задокументированных `getSettings` [здесь.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="9c5a2-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="9c5a2-144">Parameter</span></span>   | <span data-ttu-id="9c5a2-145">Сведения</span><span class="sxs-lookup"><span data-stu-id="9c5a2-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="9c5a2-146">ИД сущности, задаваемой кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="9c5a2-147">Имя конфигурации, заданная кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="9c5a2-148">URL-адрес страницы конфигурации, заданная кодом при вызове `setSettings()`</span><span class="sxs-lookup"><span data-stu-id="9c5a2-148">The URL of the configuration page, as set by your code when calling `setSettings()`</span></span> |
| `webhookUrl` | <span data-ttu-id="9c5a2-149">URL-адрес веб-hook, созданный для этого соединителя.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="9c5a2-150">Сохраните URL-адрес веб-hook и используйте его в post структурированной JSON для отправки карточек в канал.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="9c5a2-151">Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="9c5a2-152">Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно).</span><span class="sxs-lookup"><span data-stu-id="9c5a2-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="9c5a2-153">Это уникальный ид, соответствующий пользователю Office 365, который инициировал настройку соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="9c5a2-154">Этот параметр должен быть защищен.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-154">It should be secured.</span></span> <span data-ttu-id="9c5a2-155">Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="9c5a2-156">Если вам нужно проверить подлинность пользователя при загрузке страницы на шаге 2 выше, обратитесь к этой ссылке, чтобы получить подробные сведения о том, как интегрировать вход при внедрении страницы. [](~/tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="9c5a2-157">В связи с причинами совместимости между клиентами код должен будет вызываться с URL-адресом и методами успешного или неудачного вызова. `microsoftTeams.authentication.registerAuthenticationHandlers()` `authenticate()`</span><span class="sxs-lookup"><span data-stu-id="9c5a2-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="9c5a2-158">Обработка изменений</span><span class="sxs-lookup"><span data-stu-id="9c5a2-158">Handling edits</span></span>

<span data-ttu-id="9c5a2-159">Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="9c5a2-160">Для этого вызовите `microsoftTeams.settings.setSettings()` во время начальной настройки следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="9c5a2-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="9c5a2-161">`entityId` — это пользовательский ИД, который понимается службой и представляет настроенные пользователем данные.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="9c5a2-162">`configName` — это удобное имя, которое может получить код конфигурации</span><span class="sxs-lookup"><span data-stu-id="9c5a2-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="9c5a2-163">`contentUrl` это настраиваемый URL-адрес, который загружается при редактировании пользователем существующей конфигурации соединителя.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="9c5a2-164">Этот URL-адрес можно использовать, чтобы упростить обработку дела редактирования в коде.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="9c5a2-165">Как правило, этот вызов является частью обработки события сохранения.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="9c5a2-166">Затем при загрузке выше код должен вызвать предварительное переполнение любых параметров или форм в пользовательском интерфейсе `contentUrl` `getSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="9c5a2-167">Обработка удалений</span><span class="sxs-lookup"><span data-stu-id="9c5a2-167">Handling removals</span></span>

<span data-ttu-id="9c5a2-168">При желании обработчик событий можно выполнить, когда пользователь удаляет существующую конфигурацию соединителю.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="9c5a2-169">Этот обработок регистрируется путем `microsoftTeams.settings.registerOnRemoveHandler()` вызова.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="9c5a2-170">Этот обработок можно использовать для выполнения операций очистки, таких как удаление записей из базы данных.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="9c5a2-171">Включите соединители в манифест</span><span class="sxs-lookup"><span data-stu-id="9c5a2-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="9c5a2-172">Вы можете скачать автоматически созданный манифест приложения Teams с портала.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="9c5a2-173">Однако прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="9c5a2-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="9c5a2-174">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="9c5a2-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="9c5a2-175">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="9c5a2-176">Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="9c5a2-177">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="9c5a2-178">Пример файла manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="9c5a2-178">Example manifest.json with Connector</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a sample manifest for an app with a connector with an inline configuration experience.",
    "short": "This is a sample manifest for an app with a connector."
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "configurationUrl": "https://teamstodoappconnectorwithinlineconfig.azurewebsites.net/Connector/Setup",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App Long Name"
  },
  "accentColor": "#FFFFFF"
}
```

## <a name="testing-your-connector"></a><span data-ttu-id="9c5a2-179">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="9c5a2-179">Testing your Connector</span></span>

<span data-ttu-id="9c5a2-180">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="9c5a2-181">Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="9c5a2-182">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="9c5a2-183">Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="9c5a2-185">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="9c5a2-186">Следует помнить, что этот поток полностью проходит в Microsoft Teams в качестве ведущего.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="9c5a2-187">Чтобы убедиться, что действие работает правильно, отправьте `HttpPOST` сообщения [соединителю.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="9c5a2-188">Публикация соединители для организации</span><span class="sxs-lookup"><span data-stu-id="9c5a2-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="9c5a2-189">Иногда может не потребоваться публиковать приложение соединители в общедоступных AppSource или Store, но вы хотите, чтобы оно было доступно только пользователям в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="9c5a2-190">В таких случаях вы можете отправить приложение настраиваемого соединитела в каталог [приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="9c5a2-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="9c5a2-191">Таким образом, приложение соединители будет доступно только для этой организации, и вам не потребуется публиковать соединители в общедоступных магазинах.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="9c5a2-192">После отправки пакета приложения для настройки и использования соединители в команде его можно установить из каталога приложений организации, вы предприняв указанные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="9c5a2-193">Выберите значок приложений на левой вертикальной панели навигации.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="9c5a2-194">В **окне "Приложения"** выберите **соединители.**</span><span class="sxs-lookup"><span data-stu-id="9c5a2-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="9c5a2-195">Выберите соединитель, который нужно добавить, и отобразит всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="9c5a2-196">Выберите **"Добавить на панели группы".**</span><span class="sxs-lookup"><span data-stu-id="9c5a2-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="9c5a2-197">В следующем диалоговом окне введите имя команды или канала.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="9c5a2-198">Выберите **строку соединители** в правом нижнем углу диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="9c5a2-199">Соединители будут доступны в разделе &#9679;&#9679;&#9679; => Дополнительные параметры Соединители Все соединители для команды  =>    =>    =>   для этой команды.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="9c5a2-200">Вы можете перейти к этому разделу или найти приложение соединители.</span><span class="sxs-lookup"><span data-stu-id="9c5a2-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="9c5a2-201">Чтобы настроить или изменить соединители, выберите **"Настроить** планку".</span><span class="sxs-lookup"><span data-stu-id="9c5a2-201">To configure or modify the connector select the **Configure** bar.</span></span>
