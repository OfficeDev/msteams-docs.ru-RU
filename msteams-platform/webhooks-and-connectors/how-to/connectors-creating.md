---
title: Соединители Office 365
description: Описывает, как начать работу с Office 365 соединители в Microsoft Teams
keywords: соединитель teams o365
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 1598b84fc1c36547aa4c814cdf03404a3833779e
ms.sourcegitcommit: c55b0d2a4c1f8945e49b0b7c0b08c0eb3da3d2be
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646327"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="410a1-104">Создание Office 365 соединители для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="410a1-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

<span data-ttu-id="410a1-105">С Microsoft Teams приложениями можно добавить существующие Office 365 соединителю или создать новый, чтобы включить Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="410a1-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="410a1-106">Дополнительные [сведения см. в "Сборке](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) собственного соединитетеля".</span><span class="sxs-lookup"><span data-stu-id="410a1-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="410a1-107">Добавление соединитетеля в Teams App</span><span class="sxs-lookup"><span data-stu-id="410a1-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="410a1-108">Зарегистрированный соединитель можно распространять в составе пакета приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="410a1-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="410a1-109">Независимо от того, является ли это автономным решением или одним из нескольких [](~/concepts/build-and-test/apps-package.md) возможностей, [](~/concepts/deploy-and-publish/apps-publish.md) которые вы можете использовать в Teams, вы можете упаковать и опубликовать соединитель в составе отправки AppSource или предоставить его пользователям непосредственно для загрузки в Teams. [](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="410a1-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="410a1-110">Для распространения соединитетеля необходимо зарегистрироваться с помощью панели мониторинга разработчиков [соединители.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="410a1-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="410a1-111">По умолчанию после регистрации соединительщика предполагается, что соединительщик будет работать во всех продуктах Office 365, которые их поддерживают, включая Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="410a1-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="410a1-112">Если это _не_ так, и вам нужно создать соединителя, который работает только в Microsoft Teams, свяжитесь с нами непосредственно в Microsoft Teams [отправки приложений](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="410a1-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="410a1-113">После выбора **сохранить в** панели мониторинга разработчиков соединители, соединитель зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="410a1-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="410a1-114">Если вы хотите опубликовать свой соединититель в AppSource, следуйте инструкциям в [Публикации Microsoft Teams приложения в AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="410a1-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="410a1-115">Если вы не хотите публиковать свое приложение в AppSource, а просто распространять его только в организации, вы можете сделать это, опубликовав [в организации](#publish-connectors-for-your-organization).</span><span class="sxs-lookup"><span data-stu-id="410a1-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="410a1-116">Если требуется только опубликовать в организации, никаких дополнительных действий на панели мониторинга Connector не требуется.</span><span class="sxs-lookup"><span data-stu-id="410a1-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="410a1-117">Интеграция работы с конфигурацией</span><span class="sxs-lookup"><span data-stu-id="410a1-117">Integrating the configuration experience</span></span>

<span data-ttu-id="410a1-118">Пользователи завершят весь процесс настройки соединители, не покидая Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="410a1-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="410a1-119">Чтобы добиться этого, Teams встраит страницу конфигурации непосредственно в iframe.</span><span class="sxs-lookup"><span data-stu-id="410a1-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="410a1-120">Последовательность операций следующим образом:</span><span class="sxs-lookup"><span data-stu-id="410a1-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="410a1-121">Пользователь щелкает соединитетелем, чтобы начать процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="410a1-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="410a1-122">Teams загрузит ваш опыт настройки в строку.</span><span class="sxs-lookup"><span data-stu-id="410a1-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="410a1-123">Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="410a1-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="410a1-124">Пользователь нажимает кнопку "Сохранить", которая вызывает вызов в коде.</span><span class="sxs-lookup"><span data-stu-id="410a1-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="410a1-125">Код обработать событие сохранения путем восстановления параметров веб-ок (описано ниже).</span><span class="sxs-lookup"><span data-stu-id="410a1-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="410a1-126">Затем код должен хранить веб-сайт для публикации событий позже.</span><span class="sxs-lookup"><span data-stu-id="410a1-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="410a1-127">Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет организована в Teams.</span><span class="sxs-lookup"><span data-stu-id="410a1-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="410a1-128">Код должен:</span><span class="sxs-lookup"><span data-stu-id="410a1-128">Your code should:</span></span>

1. <span data-ttu-id="410a1-129">Включай Microsoft Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="410a1-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="410a1-130">Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя/канала или группы и начало потоков проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="410a1-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="410a1-131">Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="410a1-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="410a1-132">Вызов, `microsoftTeams.settings.setValidityState(true)` когда необходимо включить кнопку Сохранить.</span><span class="sxs-lookup"><span data-stu-id="410a1-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="410a1-133">Это необходимо сделать в качестве ответа на допустимые входные данные пользователей, такие как выбор или обновление поля.</span><span class="sxs-lookup"><span data-stu-id="410a1-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="410a1-134">Зарегистрируйте `microsoftTeams.settings.registerOnSaveHandler()` обработник событий, который будет вызван при нажатии пользователем кнопки Сохранить.</span><span class="sxs-lookup"><span data-stu-id="410a1-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="410a1-135">Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="410a1-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="410a1-136">Сохранено также то, что будет показано в диалоговом окне конфигурации, если пользователь попытается обновить существующую конфигурацию для соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="410a1-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="410a1-137">Вызов `microsoftTeams.settings.getSettings()` для получения свойств webhook, включая сам URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="410a1-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="410a1-138">Вы должны вызвать это в дополнение к во время события сохранения, вы также должны вызвать это, когда ваша страница впервые загружена в случае повторной настройки.</span><span class="sxs-lookup"><span data-stu-id="410a1-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="410a1-139">(Необязательный) Зарегистрируйте `microsoftTeams.settings.registerOnRemoveHandler()` обработчик событий, который будет вызван после удаления соединитетелем пользователя.</span><span class="sxs-lookup"><span data-stu-id="410a1-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="410a1-140">Это событие предоставляет службе возможность выполнять любые действия по очистке.</span><span class="sxs-lookup"><span data-stu-id="410a1-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="410a1-141">Вот пример HTML для создания страницы конфигурации соединителя без CSS:</span><span class="sxs-lookup"><span data-stu-id="410a1-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

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
            alert("Removed" + JSON.stringify(removeEvent));
        });

</script>
```

#### <a name="getsettings-response-properties"></a><span data-ttu-id="410a1-142">`GetSettings()` Свойства ответа</span><span class="sxs-lookup"><span data-stu-id="410a1-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="410a1-143">Параметры, возвращенные здесь вызовом, отличаются от тех, которые вы должны были вызвать этот метод со вкладки, и отличаются от параметров, задокументированных `getSettings` [здесь.](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="410a1-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/@microsoft/teams-js/microsoftteams.settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="410a1-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="410a1-144">Parameter</span></span>   | <span data-ttu-id="410a1-145">Сведения</span><span class="sxs-lookup"><span data-stu-id="410a1-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="410a1-146">Код сущности, задаваемый кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="410a1-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="410a1-147">Имя конфигурации, заданная кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="410a1-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="410a1-148">URL-адрес страницы конфигурации, заданная кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="410a1-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="410a1-149">URL-адрес веб-страницы, созданный для этого соединителя.</span><span class="sxs-lookup"><span data-stu-id="410a1-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="410a1-150">Сохраните URL-адрес веб-страницы и используйте его в структуре POST JSON для отправки карт на канал.</span><span class="sxs-lookup"><span data-stu-id="410a1-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="410a1-151">Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно.</span><span class="sxs-lookup"><span data-stu-id="410a1-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="410a1-152">Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно).</span><span class="sxs-lookup"><span data-stu-id="410a1-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="410a1-153">Это уникальный id, соответствующий Office 365, который инициировал установку соединиттеля.</span><span class="sxs-lookup"><span data-stu-id="410a1-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="410a1-154">Этот параметр должен быть защищен.</span><span class="sxs-lookup"><span data-stu-id="410a1-154">It should be secured.</span></span> <span data-ttu-id="410a1-155">Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе.</span><span class="sxs-lookup"><span data-stu-id="410a1-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="410a1-156">Если необходимо проверить подлинность пользователя в рамках загрузки страницы на шаге 2 выше, обратитесь к этой ссылке, чтобы узнать, как интегрировать вход при вложении страницы. [](~/tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="410a1-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="410a1-157">В связи с причинами совместимости между клиентами перед вызовом коду необходимо звонить с помощью URL-адреса и методов вызова успешного `microsoftTeams.authentication.registerAuthenticationHandlers()` и неудачного `authenticate()` вызова.</span><span class="sxs-lookup"><span data-stu-id="410a1-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="410a1-158">Обработка изменений</span><span class="sxs-lookup"><span data-stu-id="410a1-158">Handling edits</span></span>

<span data-ttu-id="410a1-159">Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединителя.</span><span class="sxs-lookup"><span data-stu-id="410a1-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="410a1-160">Для этого необходимо вызвать `microsoftTeams.settings.setSettings()` во время начальной конфигурации со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="410a1-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="410a1-161">`entityId` это пользовательский ID, который понимается службой и представляет то, что пользователь настроил.</span><span class="sxs-lookup"><span data-stu-id="410a1-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="410a1-162">`configName` это удобное имя, которое код конфигурации может получить</span><span class="sxs-lookup"><span data-stu-id="410a1-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="410a1-163">`contentUrl` это настраиваемый URL-адрес, загружаемый при редактировании существующей конфигурации соединителя.</span><span class="sxs-lookup"><span data-stu-id="410a1-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="410a1-164">Этот URL-адрес можно использовать, чтобы упростить обработку дела редактирования для кода.</span><span class="sxs-lookup"><span data-stu-id="410a1-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="410a1-165">Как правило, этот вызов проводится в рамках обработки событий сохранения.</span><span class="sxs-lookup"><span data-stu-id="410a1-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="410a1-166">Затем при загрузке кода должен вызываться предварительная загрузка параметров или форм в пользовательском интерфейсе `contentUrl` `getSettings()` конфигурации.</span><span class="sxs-lookup"><span data-stu-id="410a1-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="410a1-167">Обработка удалений</span><span class="sxs-lookup"><span data-stu-id="410a1-167">Handling removals</span></span>

<span data-ttu-id="410a1-168">Обработчик событий можно выполнить, если пользователь удаляет существующую конфигурацию соединителю.</span><span class="sxs-lookup"><span data-stu-id="410a1-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="410a1-169">Этот обработок регистрируется по вызову `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="410a1-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="410a1-170">Этот обработок можно использовать для выполнения операций очистки, таких как удаление записей из базы данных.</span><span class="sxs-lookup"><span data-stu-id="410a1-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="410a1-171">В том числе соединители в манифесте</span><span class="sxs-lookup"><span data-stu-id="410a1-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="410a1-172">Вы можете скачать автогенерированную Teams с портала.</span><span class="sxs-lookup"><span data-stu-id="410a1-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="410a1-173">Однако прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="410a1-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="410a1-174">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="410a1-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="410a1-175">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="410a1-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="410a1-176">Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="410a1-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="410a1-177">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="410a1-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="410a1-178">Пример файла manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="410a1-178">Example manifest.json with Connector</span></span>

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

## <a name="disable-or-enable-connectors-in-teams"></a><span data-ttu-id="410a1-179">Отключить или включить соединители в Teams</span><span class="sxs-lookup"><span data-stu-id="410a1-179">Disable or enable connectors in Teams</span></span>

<span data-ttu-id="410a1-180">Модуль Exchange Online PowerShell V2 использует современную проверку подлинности и работает с многофакторной проверкой подлинности (MFA) для подключения Exchange связанных с powerShell сред в Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="410a1-180">The Exchange Online PowerShell V2 module uses modern authentication and works with multi-factor authentication (MFA) for connecting to all Exchange-related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="410a1-181">Администраторы могут использовать Exchange Online PowerShell для отключения соединители для всего клиента или определенного почтового ящика группы, затрагивая всех пользователей в этом клиенте или почтовом ящике.</span><span class="sxs-lookup"><span data-stu-id="410a1-181">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="410a1-182">Отключение для одних и не для других невозможно.</span><span class="sxs-lookup"><span data-stu-id="410a1-182">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="410a1-183">Кроме того, соединители отключены по умолчанию для GCC клиентов.</span><span class="sxs-lookup"><span data-stu-id="410a1-183">Also, connectors are disabled by default for GCC tenants.</span></span>

<span data-ttu-id="410a1-184">Параметр на уровне клиента переопределяет параметр группового уровня.</span><span class="sxs-lookup"><span data-stu-id="410a1-184">The tenant-level setting overrides the group-level setting.</span></span> <span data-ttu-id="410a1-185">Например, если администратор включает соединители для группы и отключает их в клиенте, соединители для группы будут отключены.</span><span class="sxs-lookup"><span data-stu-id="410a1-185">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group will be disabled.</span></span> <span data-ttu-id="410a1-186">Чтобы включить соединитель в Teams, подключите Exchange Online [PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) с помощью современной проверки подлинности с помощью MFA или без него.</span><span class="sxs-lookup"><span data-stu-id="410a1-186">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-disable-or-enable-connectors"></a><span data-ttu-id="410a1-187">Команды по отключению или включении соединители</span><span class="sxs-lookup"><span data-stu-id="410a1-187">Commands to disable or enable connectors</span></span>

<span data-ttu-id="410a1-188">**Запустите команду в Exchange Online PowerShell**</span><span class="sxs-lookup"><span data-stu-id="410a1-188">**Run the command in Exchange Online PowerShell**</span></span>

* <span data-ttu-id="410a1-189">Отключение соединители для клиента: `Set-OrganizationConfig -ConnectorsEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="410a1-189">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="410a1-190">Отключение действий для клиента: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="410a1-190">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="410a1-191">Чтобы включить соединители для Teams, запустите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="410a1-191">To enable connectors for Teams, run the following commands:</span></span>
    * `Set-OrganizationConfig -ConnectorsEnabled:$true `
    * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
    * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="410a1-192">Дополнительные сведения об обмене модулями PowerShell см. в [сайте Set-OrganizationConfig.](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="410a1-192">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="410a1-193">Чтобы включить или отключить Outlook соединители, [подключите приложения к](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)группам в Outlook.</span><span class="sxs-lookup"><span data-stu-id="410a1-193">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="testing-your-connector"></a><span data-ttu-id="410a1-194">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="410a1-194">Testing your Connector</span></span>

<span data-ttu-id="410a1-195">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="410a1-195">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="410a1-196">Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.</span><span class="sxs-lookup"><span data-stu-id="410a1-196">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="410a1-197">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="410a1-197">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="410a1-198">Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.</span><span class="sxs-lookup"><span data-stu-id="410a1-198">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="410a1-200">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="410a1-200">You can now launch the configuration experience.</span></span> <span data-ttu-id="410a1-201">Следует помнить, что этот поток происходит полностью в Microsoft Teams в качестве хозяйского опыта.</span><span class="sxs-lookup"><span data-stu-id="410a1-201">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="410a1-202">Чтобы убедиться, `HttpPOST` что действие работает правильно, отправьте сообщения в [соединителю.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="410a1-202">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="410a1-203">Публикация соединители для организации</span><span class="sxs-lookup"><span data-stu-id="410a1-203">Publish Connectors for your organization</span></span>

<span data-ttu-id="410a1-204">Иногда может не потребоваться публиковать приложение соединители в общедоступный AppSource/Store, но вы хотите, чтобы оно было доступно только пользователям в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="410a1-204">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="410a1-205">В таких случаях вы можете загрузить свое настраиваемое соединитеное приложение в каталог [приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="410a1-205">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="410a1-206">Таким образом, приложение соединители будет доступно только этой организации, и вам не потребуется публиковать соединители в общедоступный магазин.</span><span class="sxs-lookup"><span data-stu-id="410a1-206">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="410a1-207">После загрузки пакета приложений для настройки и использования соединители в команде его можно установить из каталога приложений организации, следуя следующим шагам:</span><span class="sxs-lookup"><span data-stu-id="410a1-207">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="410a1-208">Выберите значок приложений из левой панели вертикальной навигации.</span><span class="sxs-lookup"><span data-stu-id="410a1-208">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="410a1-209">В **окне Приложения** выберите **соединители**.</span><span class="sxs-lookup"><span data-stu-id="410a1-209">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="410a1-210">Выберите соединителю, который необходимо добавить, и будет отображаться всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="410a1-210">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="410a1-211">Выберите **добавить в планку команды.**</span><span class="sxs-lookup"><span data-stu-id="410a1-211">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="410a1-212">В следующем диалоговом окне введите команду или имя канала.</span><span class="sxs-lookup"><span data-stu-id="410a1-212">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="410a1-213">Выберите **строку Настройка соединитетеля** в правом нижнем углу окна диалогов.</span><span class="sxs-lookup"><span data-stu-id="410a1-213">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="410a1-214">Соединители будут доступны в разделе &#9679;&#9679;&#9679; => дополнительные параметры Соединители Все соединители для вас  =>    =>    =>  *команда* для этой группы.</span><span class="sxs-lookup"><span data-stu-id="410a1-214">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="410a1-215">Вы можете перемещаться путем прокрутки в этот раздел или поиска соединитеного приложения.</span><span class="sxs-lookup"><span data-stu-id="410a1-215">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="410a1-216">Чтобы настроить или изменить соединители, выберите **планку Configure.**</span><span class="sxs-lookup"><span data-stu-id="410a1-216">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="410a1-217">Пример кода</span><span class="sxs-lookup"><span data-stu-id="410a1-217">Code sample</span></span>
|<span data-ttu-id="410a1-218">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="410a1-218">**Sample name**</span></span> | <span data-ttu-id="410a1-219">**Описание**</span><span class="sxs-lookup"><span data-stu-id="410a1-219">**Description**</span></span> | <span data-ttu-id="410a1-220">**.NET**</span><span class="sxs-lookup"><span data-stu-id="410a1-220">**.NET**</span></span> | <span data-ttu-id="410a1-221">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="410a1-221">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="410a1-222">Соединители</span><span class="sxs-lookup"><span data-stu-id="410a1-222">Connectors</span></span>    | <span data-ttu-id="410a1-223">Пример Office 365 соединители, генерирующие уведомления для канала teams.</span><span class="sxs-lookup"><span data-stu-id="410a1-223">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="410a1-224">View</span><span class="sxs-lookup"><span data-stu-id="410a1-224">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="410a1-225">View</span><span class="sxs-lookup"><span data-stu-id="410a1-225">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="410a1-226">Общий пример соединители</span><span class="sxs-lookup"><span data-stu-id="410a1-226">Generic connectors sample</span></span> |<span data-ttu-id="410a1-227">Пример кода для общего соединители, который легко настроить для любой системы, поддерживающую веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="410a1-227">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="410a1-228">View</span><span class="sxs-lookup"><span data-stu-id="410a1-228">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
