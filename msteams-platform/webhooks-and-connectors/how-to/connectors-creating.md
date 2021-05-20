---
title: Соединители Office 365
description: Описывает, как начать работу с Office 365 разъемами в Microsoft Teams
keywords: соединитель teams o365
localization_priority: Normal
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 9eaaedf88d907dd7a7422068ab5d20450345f0e7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566812"
---
# <a name="creating-office-365-connectors-for-microsoft-teams"></a><span data-ttu-id="23906-104">Создание Office 365 разъемов для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="23906-104">Creating Office 365 Connectors for Microsoft Teams</span></span>

><span data-ttu-id="23906-105">С Microsoft Teams приложениями вы можете добавить существующий Office 365 Connector или построить новый, который будет включен в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="23906-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one to include in Microsoft Teams.</span></span> <span data-ttu-id="23906-106">Для [получения дополнительной информации смотрите создать](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) свой собственный разъем.</span><span class="sxs-lookup"><span data-stu-id="23906-106">See [Build your own Connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector) for more information.</span></span>

## <a name="adding-a-connector-to-your-teams-app"></a><span data-ttu-id="23906-107">Добавление разъема в приложение Teams приложение</span><span class="sxs-lookup"><span data-stu-id="23906-107">Adding a Connector to your Teams App</span></span>

<span data-ttu-id="23906-108">Зарегистрированный соединитель можно распространять в составе пакета приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="23906-108">You can distribute your registered Connector as part of your Teams app package.</span></span> <span data-ttu-id="23906-109">Будь то автономное решение или [](~/concepts/extensibility-points.md) одна из нескольких возможностей, которые позволяет ваш опыт в Teams, [вы](~/concepts/build-and-test/apps-package.md) можете упаковать и [опубликовать](~/concepts/deploy-and-publish/apps-publish.md) ваш разъем как часть вашего представления AppSource, или вы можете предоставить его пользователям непосредственно для загрузки в течение Teams.</span><span class="sxs-lookup"><span data-stu-id="23906-109">Whether as a standalone solution, or one of several [capabilities](~/concepts/extensibility-points.md) that your experience enables in Teams, you can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your Connector as part of your AppSource submission, or you can provide it to users directly for uploading within Teams.</span></span>

<span data-ttu-id="23906-110">Для распространения разъема необходимо зарегистрироваться с помощью панели [разработчиков Connectors.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="23906-110">To distribute your Connector, you need to register by using the [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="23906-111">По умолчанию, после регистрации Коннектора, предполагается, что ваш разъем будет работать во всех Office 365 продуктах, которые их поддерживают, включая Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="23906-111">By default, once a Connector is registered, it's assumed that your Connector will work in all Office 365 products that support them, including Outlook and Teams.</span></span> <span data-ttu-id="23906-112">Если это _не так,_ и вам нужно создать разъем, который работает только в Microsoft Teams, свяжитесь с [нами непосредственно Microsoft Teams App Представлений](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="23906-112">If that is _not_ the case and you need to create a Connector that only works in Microsoft Teams, contact us directly at [Microsoft Teams App Submissions](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="23906-113">После выбора **Save in** the Connectors Developer Dashboard ваш разъем регистрируется.</span><span class="sxs-lookup"><span data-stu-id="23906-113">After you choose **Save** in the Connectors Developer Dashboard, your Connector is registered.</span></span> <span data-ttu-id="23906-114">Если вы хотите опубликовать свой разъем в AppSource, следуйте инструкциям [в Publish your Microsoft Teams приложение AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="23906-114">If you want to publish your Connector in AppSource, follow the instructions in [Publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="23906-115">Если вы не хотите публиковать свое приложение в AppSource, а просто распространять его только среди вашей организации, вы можете сделать это, [опубликовав в вашей организации.](#publish-connectors-for-your-organization)</span><span class="sxs-lookup"><span data-stu-id="23906-115">If you do not wish to publish your app in AppSource, and rather simply distribute it directly to your organization only, you can do so by [publishing to your organization](#publish-connectors-for-your-organization).</span></span> <span data-ttu-id="23906-116">Если вы хотите опубликовать информацию только в организации, никаких дальнейших действий на панели мониторинга Connector не требуется.</span><span class="sxs-lookup"><span data-stu-id="23906-116">If you only want to publish to your organization, no further action is necessary on the Connector dashboard.</span></span>

### <a name="integrating-the-configuration-experience"></a><span data-ttu-id="23906-117">Интеграция опыта конфигурации</span><span class="sxs-lookup"><span data-stu-id="23906-117">Integrating the configuration experience</span></span>

<span data-ttu-id="23906-118">Пользователи заверят весь процесс настройки Connector, не покидая Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="23906-118">Your users will complete the entire Connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="23906-119">Для достижения этой цели Teams встраивает страницу конфигурации непосредственно в iframe.</span><span class="sxs-lookup"><span data-stu-id="23906-119">To achieve this experience, Teams will embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="23906-120">Последовательность операций заключается в следующем:</span><span class="sxs-lookup"><span data-stu-id="23906-120">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="23906-121">Пользователь нажимает на разъем, чтобы начать процесс настройки.</span><span class="sxs-lookup"><span data-stu-id="23906-121">The user clicks on your connector to begin the configuration process.</span></span>
2. <span data-ttu-id="23906-122">Teams загрузит ваш опыт конфигурации в соответствии.</span><span class="sxs-lookup"><span data-stu-id="23906-122">Teams will load your configuration experience in line.</span></span>
3. <span data-ttu-id="23906-123">Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23906-123">The user interacts with your web experience to complete the configuration.</span></span>
4. <span data-ttu-id="23906-124">Пользователь нажимает "Сохранить", который вызывает обратный вызов в коде.</span><span class="sxs-lookup"><span data-stu-id="23906-124">The user presses "Save", which triggers a callback in your code.</span></span>
5. <span data-ttu-id="23906-125">Ваш код обработать событие сохранения путем извлечения параметров webhook (описано ниже).</span><span class="sxs-lookup"><span data-stu-id="23906-125">Your code will process the save event by retrieving the webhook settings (documented below).</span></span> <span data-ttu-id="23906-126">Ваш код должен хранить webhook для поста событий позже.</span><span class="sxs-lookup"><span data-stu-id="23906-126">Your code should then store the webhook to post events later.</span></span>

<span data-ttu-id="23906-127">Вы можете повторно использовать существующий веб-конфигурации опыт или создать отдельную версию, которая будет размещена специально в Teams.</span><span class="sxs-lookup"><span data-stu-id="23906-127">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="23906-128">Ваш код должен:</span><span class="sxs-lookup"><span data-stu-id="23906-128">Your code should:</span></span>

1. <span data-ttu-id="23906-129">Включите Microsoft Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="23906-129">Include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="23906-130">Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя/канала/команды и инициирование потоков аутентификации.</span><span class="sxs-lookup"><span data-stu-id="23906-130">This gives your code access to APIs to perform common operations like getting the current user/channel/team context and initiating authentication flows.</span></span> <span data-ttu-id="23906-131">Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="23906-131">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
2. <span data-ttu-id="23906-132">`microsoftTeams.settings.setValidityState(true)`Звоните, когда хотите включить кнопку Сохранения.</span><span class="sxs-lookup"><span data-stu-id="23906-132">Call `microsoftTeams.settings.setValidityState(true)` when you want to enable the Save button.</span></span> <span data-ttu-id="23906-133">Вы должны сделать это в ответ на действительный пользовательский ввод, например, выбор или обновление поля.</span><span class="sxs-lookup"><span data-stu-id="23906-133">You should do this as a response to valid user input, such as a selection or field update.</span></span>
3. <span data-ttu-id="23906-134">Зарегистрируйте обработчик `microsoftTeams.settings.registerOnSaveHandler()` событий, который вызывается при нажатии кнопки Save.</span><span class="sxs-lookup"><span data-stu-id="23906-134">Register a `microsoftTeams.settings.registerOnSaveHandler()` event handler, which gets called when the user clicks Save.</span></span>
4. <span data-ttu-id="23906-135">`microsoftTeams.settings.setSettings()`Звоните, чтобы сохранить настройки разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-135">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="23906-136">Здесь также сохраняется то, что будет показано в диалоге конфигурации, если пользователь попытается обновить существующую конфигурацию для вашего разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-136">What's saved here is also what will be shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
5. <span data-ttu-id="23906-137">`microsoftTeams.settings.getSettings()`Звоните, чтобы получить свойства webhook, включая сам URL.</span><span class="sxs-lookup"><span data-stu-id="23906-137">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL itself.</span></span> <span data-ttu-id="23906-138">Вы должны позвонить по этому вопросу В дополнение к событию сохранения, вы также должны позвонить по этому вопросу, когда ваша страница впервые загружена в случае повторной конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23906-138">You should call this  In addition to during the save event, you should also call this when your page is first loaded in the case of a re-configuration.</span></span>
6. <span data-ttu-id="23906-139">(По желанию) Зарегистрируйте обработчик `microsoftTeams.settings.registerOnRemoveHandler()` событий, который вызывается, когда пользователь удаляет ваш разъем.</span><span class="sxs-lookup"><span data-stu-id="23906-139">(Optional) Register a `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which gets called when the user removes your connector.</span></span> <span data-ttu-id="23906-140">Это событие дает вашему сервису возможность выполнять любые действия по очистке.</span><span class="sxs-lookup"><span data-stu-id="23906-140">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="23906-141">Вот пример HTML для создания страницы конфигурации Connector без CSS:</span><span class="sxs-lookup"><span data-stu-id="23906-141">Here's a sample HTML to create a Connector configuration page without the CSS:</span></span>

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

#### <a name="getsettings-response-properties"></a><span data-ttu-id="23906-142">`GetSettings()` свойства ответа</span><span class="sxs-lookup"><span data-stu-id="23906-142">`GetSettings()` response properties</span></span>

>[!Note]
><span data-ttu-id="23906-143">Параметры, возвращенные вызовом `getSettings` здесь, отличаются от тех, которые вы должны были вызвать этот метод из вкладки, и отличаются от тех, которые описаны [здесь.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="23906-143">The parameters returned by the `getSettings` call here are different than if you were to invoke this method from a tab, and differ from those documented [here](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

| <span data-ttu-id="23906-144">Параметр</span><span class="sxs-lookup"><span data-stu-id="23906-144">Parameter</span></span>   | <span data-ttu-id="23906-145">Сведения</span><span class="sxs-lookup"><span data-stu-id="23906-145">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="23906-146">Идентификатор сущности, установленный кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="23906-146">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="23906-147">Имя конфигурации, как установлено кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="23906-147">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="23906-148">URL страницы конфигурации, установленный кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="23906-148">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="23906-149">URL webhook, созданный для этого разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-149">The webhook URL created for this connector.</span></span> <span data-ttu-id="23906-150">Упорствуй webhook URL и использовать его для POST структурированных JSON для отправки карт на канал.</span><span class="sxs-lookup"><span data-stu-id="23906-150">Persist the webhook URL and use it to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="23906-151">Параметр `webhookUrl` возвращается только в том случае, если приложение возвращается успешно.</span><span class="sxs-lookup"><span data-stu-id="23906-151">The `webhookUrl` is returned only when application returns successfully.</span></span> |
| `appType` | <span data-ttu-id="23906-152">Возвращаемыми значениями могут быть `mail`, `groups` или `teams` (для почты Office 365, функции "Группы Office 365" и Microsoft Teams соответственно).</span><span class="sxs-lookup"><span data-stu-id="23906-152">The values returned can be `mail`, `groups` or `teams` corresponding to the Office 365 Mail, Office 365 Groups or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="23906-153">Это уникальный идентификатор, соответствующий Office 365, инициировавший настройку разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-153">This is the unique id corresponding to the Office 365 user who initiated setup of the connector.</span></span> <span data-ttu-id="23906-154">Этот параметр должен быть защищен.</span><span class="sxs-lookup"><span data-stu-id="23906-154">It should be secured.</span></span> <span data-ttu-id="23906-155">Это значение используется для сопоставления пользователя в Office 365, который настраивает конфигурацию, и пользователя в вашей службе.</span><span class="sxs-lookup"><span data-stu-id="23906-155">This value can be used to associate the user in Office 365 who set up the configuration to the user in your service.</span></span> |

<span data-ttu-id="23906-156">Если вам необходимо проверить подлинность пользователя в рамках загрузки страницы в шаге 2 выше, обратитесь к этой ссылке для [получения подробной](~/tabs/how-to/authentication/auth-flow-tab.md) информации о том, как вы можете интегрировать логин, когда ваша страница встроена.</span><span class="sxs-lookup"><span data-stu-id="23906-156">If you need to authenticate the user as part of loading your page in step 2 above, refer to [this link](~/tabs/how-to/authentication/auth-flow-tab.md) for details on how you can integrate login when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="23906-157">По причинам совместимости между клиентами, ваш код должен будет позвонить с URL и `microsoftTeams.authentication.registerAuthenticationHandlers()` методы возврата вызова успеха/неудачи перед вызовом. `authenticate()`</span><span class="sxs-lookup"><span data-stu-id="23906-157">Due to cross-client compatibility reasons, your code will need to call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success/failure callback methods before calling `authenticate()`.</span></span>

#### <a name="handling-edits"></a><span data-ttu-id="23906-158">Обработка правок</span><span class="sxs-lookup"><span data-stu-id="23906-158">Handling edits</span></span>

<span data-ttu-id="23906-159">Код должен обрабатывать пользователей, возвращающихся для изменения существующей конфигурации соединителя.</span><span class="sxs-lookup"><span data-stu-id="23906-159">Your code should handle users returning to edit an existing connector configuration.</span></span> <span data-ttu-id="23906-160">Для этого вызов в `microsoftTeams.settings.setSettings()` течение начальной конфигурации со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="23906-160">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="23906-161">`entityId` это пользовательский идентификатор, который понимается вашим сервисом и представляет то, что пользователь настроил.</span><span class="sxs-lookup"><span data-stu-id="23906-161">`entityId` is the custom ID that is understood by your service and represents what the user has configured.</span></span>
- <span data-ttu-id="23906-162">`configName` это дружелюбное имя, которое код конфигурации может получить</span><span class="sxs-lookup"><span data-stu-id="23906-162">`configName` is a friendly name that your configuration code can retrieve</span></span>
- <span data-ttu-id="23906-163">`contentUrl` это пользовательский URL-адрес, который загружается, когда пользователь редактирует существующую конфигурацию разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-163">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span> <span data-ttu-id="23906-164">Вы можете использовать этот URL, чтобы облегчить обработку кода в случае редактирования.</span><span class="sxs-lookup"><span data-stu-id="23906-164">You can use this URL to make it easier for your code to handle the edit case.</span></span>

<span data-ttu-id="23906-165">Как правило, этот вызов делается как часть обработчика событий сохранения.</span><span class="sxs-lookup"><span data-stu-id="23906-165">Typically, this call is made as part of your save event handler.</span></span> <span data-ttu-id="23906-166">Затем, когда `contentUrl` вышеуказанное загружено, код должен вызвать для `getSettings()` преднаселения любые настройки или формы в пользовательском интерфейсе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="23906-166">Then, when the `contentUrl` above is loaded, your code should call `getSettings()` to prepopulate any settings or forms in your configuration UI.</span></span>

#### <a name="handling-removals"></a><span data-ttu-id="23906-167">Обработка удалений</span><span class="sxs-lookup"><span data-stu-id="23906-167">Handling removals</span></span>

<span data-ttu-id="23906-168">Вы можете дополнительно выполнить обработчик событий, когда пользователь удаляет существующую конфигурацию разъема.</span><span class="sxs-lookup"><span data-stu-id="23906-168">You can optionally execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="23906-169">Вы регистрируете этот обработчик по телефону `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="23906-169">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="23906-170">Этот обработчик может быть использован для выполнения операций по очистке, таких как удаление записей из базы данных.</span><span class="sxs-lookup"><span data-stu-id="23906-170">This handler can be used to perform cleanup operations such as removing entries from a database.</span></span>

### <a name="including-the-connector-in-your-manifest"></a><span data-ttu-id="23906-171">Включение разъема в манифест</span><span class="sxs-lookup"><span data-stu-id="23906-171">Including the Connector in your Manifest</span></span>

<span data-ttu-id="23906-172">Вы можете скачать автоматически сгенерированный Teams манифест приложения с портала.</span><span class="sxs-lookup"><span data-stu-id="23906-172">You can download the auto-generated Teams app manifest from the portal.</span></span> <span data-ttu-id="23906-173">Однако, прежде чем использовать его для тестирования или публикации приложения, необходимо сделать следующее:</span><span class="sxs-lookup"><span data-stu-id="23906-173">Before you can use it to test or publish your app, though, you must do the following:</span></span>

- <span data-ttu-id="23906-174">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="23906-174">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
- <span data-ttu-id="23906-175">Измените раздел `icons` манифеста, чтобы он ссылался на имена файлов значков, а не на их URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="23906-175">Modify the `icons` portion of the manifest to refer to the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="23906-176">Приведенный ниже файл manifest.json содержит основные элементы, необходимые для тестирования и отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="23906-176">The following manifest.json file contains the basic elements needed to test and submit your app.</span></span>

> [!NOTE]
> <span data-ttu-id="23906-177">Замените `id` и `connectorId` в приведенном ниже примере на GUID соединителя.</span><span class="sxs-lookup"><span data-stu-id="23906-177">Replace `id` and `connectorId` in the following example with the GUID of your Connector.</span></span>

#### <a name="example-manifestjson-with-connector"></a><span data-ttu-id="23906-178">Пример файла manifest.json с соединителем</span><span class="sxs-lookup"><span data-stu-id="23906-178">Example manifest.json with Connector</span></span>

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

## <a name="testing-your-connector"></a><span data-ttu-id="23906-179">Тестирование соединителя</span><span class="sxs-lookup"><span data-stu-id="23906-179">Testing your Connector</span></span>

<span data-ttu-id="23906-180">Чтобы тестировать соединитель, отправьте его команде, как в любом другом приложении.</span><span class="sxs-lookup"><span data-stu-id="23906-180">To test your Connector, upload it to a team as you would with any other app.</span></span> <span data-ttu-id="23906-181">Вы можете создать ZIP-пакет, используя файл манифеста с панели администрирования для разработчиков соединителей (измененный согласно инструкциям из предыдущего раздела) и два файла значков.</span><span class="sxs-lookup"><span data-stu-id="23906-181">You can create a .zip package using the manifest file from the Connectors Developer Dashboard (modified as directed in the preceding section) and the two icon files.</span></span>

<span data-ttu-id="23906-182">После отправки приложения откройте список соединителей с любого канала.</span><span class="sxs-lookup"><span data-stu-id="23906-182">After you upload the app, open the Connectors list from any channel.</span></span> <span data-ttu-id="23906-183">Прокрутите вниз, чтобы найти свое приложение в разделе **Отправленные**.</span><span class="sxs-lookup"><span data-stu-id="23906-183">Scroll to the bottom to see your app in the **Uploaded** section.</span></span>

![Снимок экрана раздела отправленных приложений в диалоговом окне соединителя](~/assets/images/connectors/connector_dialog_uploaded.png)

<span data-ttu-id="23906-185">Теперь можно запустить среду настройки.</span><span class="sxs-lookup"><span data-stu-id="23906-185">You can now launch the configuration experience.</span></span> <span data-ttu-id="23906-186">Имейте в виду, что этот поток происходит Microsoft Teams в качестве размещены опыт.</span><span class="sxs-lookup"><span data-stu-id="23906-186">Be aware that this flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="23906-187">Чтобы убедиться, `HttpPOST` что действие работает правильно, отправьте сообщения в [разъем.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="23906-187">To verify that an `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-your-organization"></a><span data-ttu-id="23906-188">Публикация разъемов для вашей организации</span><span class="sxs-lookup"><span data-stu-id="23906-188">Publish Connectors for your organization</span></span>

<span data-ttu-id="23906-189">Иногда вы можете не публиковать приложение-разъем для общедоступных AppSource/Store, но хотели бы, чтобы оно было доступно только пользователям в вашей организации.</span><span class="sxs-lookup"><span data-stu-id="23906-189">Sometimes, you may not want to publish your connector app to the public AppSource/Store but would like it to be available only to the users in your organization.</span></span> <span data-ttu-id="23906-190">В таких случаях вы можете загрузить пользовательское приложение-разъем в [каталог приложений вашей организации.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="23906-190">In such cases, you can upload your custom connector app to your [organization's App Catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="23906-191">Таким образом, ваше приложение-разъем будет доступно только этой организации, и вам не нужно будет публиковать свой разъем в общедоступный магазин.</span><span class="sxs-lookup"><span data-stu-id="23906-191">This way, your connector app will be available only to that organization, and you will not need to publish your connector to the public store.</span></span>

<span data-ttu-id="23906-192">После загрузки пакета приложений для настройки и использования разъема в команде он может быть установлен из каталога приложений организации, следуя следующим шагам:</span><span class="sxs-lookup"><span data-stu-id="23906-192">Once you've uploaded your app package, to configure and use the connector in a Team it can be installed from the organization's app catalog by following these steps:</span></span>

1. <span data-ttu-id="23906-193">Выберите значок приложений из крайне левой вертикальной навигационной полосы.</span><span class="sxs-lookup"><span data-stu-id="23906-193">Select the apps icon from the far left vertical navigation bar.</span></span>
1. <span data-ttu-id="23906-194">В окне **Приложения** выберите **разъемы.**</span><span class="sxs-lookup"><span data-stu-id="23906-194">In the **Apps** window select **Connectors**.</span></span>
1. <span data-ttu-id="23906-195">Выберите разъем, который вы хотите добавить, и всплывающее окно диалога будет отображаться.</span><span class="sxs-lookup"><span data-stu-id="23906-195">Select the connector that you want to add and a pop-up dialog window will display.</span></span>
1. <span data-ttu-id="23906-196">Выберите **добавить в бар** команды.</span><span class="sxs-lookup"><span data-stu-id="23906-196">Select the **Add to a team** bar.</span></span>
1. <span data-ttu-id="23906-197">В следующем диалоговом окне ввемите имя команды или канала.</span><span class="sxs-lookup"><span data-stu-id="23906-197">In the next dialog window type a team or channel name.</span></span>
1. <span data-ttu-id="23906-198">Выберите **стойку разъема** из правого нижнего угла окна диалога.</span><span class="sxs-lookup"><span data-stu-id="23906-198">Select the **Set up a connector** bar from the bottom right corner of dialog window.</span></span>
1. <span data-ttu-id="23906-199">Разъем будет доступен в разделе, &#9679;&#9679;&#9679; и> *больше*  =>  *вариантов*  =>  *Разъемы*  =>  *Все разъемы для вас команда* для этой команды.</span><span class="sxs-lookup"><span data-stu-id="23906-199">The connector will be available in the  section &#9679;&#9679;&#9679; => *More options* => *Connectors* => *All* => *Connectors for you team* for that team.</span></span> <span data-ttu-id="23906-200">Вы можете перемещаться, прокручивая в этот раздел или искать разъем приложения.</span><span class="sxs-lookup"><span data-stu-id="23906-200">You can navigate by scrolling to this section or search for the connector app.</span></span>
1. <span data-ttu-id="23906-201">Для настройки или изменения разъема выберите **планку Configure.**</span><span class="sxs-lookup"><span data-stu-id="23906-201">To configure or modify the connector select the **Configure** bar.</span></span>

## <a name="code-sample"></a><span data-ttu-id="23906-202">Пример кода</span><span class="sxs-lookup"><span data-stu-id="23906-202">Code sample</span></span>
|<span data-ttu-id="23906-203">**Название образца**</span><span class="sxs-lookup"><span data-stu-id="23906-203">**Sample name**</span></span> | <span data-ttu-id="23906-204">**Описание**</span><span class="sxs-lookup"><span data-stu-id="23906-204">**Description**</span></span> | <span data-ttu-id="23906-205">**.NET**</span><span class="sxs-lookup"><span data-stu-id="23906-205">**.NET**</span></span> | <span data-ttu-id="23906-206">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="23906-206">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="23906-207">Соединители</span><span class="sxs-lookup"><span data-stu-id="23906-207">Connectors</span></span>    | <span data-ttu-id="23906-208">Пример Office 365 Connector, генерирующий уведомления для команд канала.</span><span class="sxs-lookup"><span data-stu-id="23906-208">Sample Office 365 Connector generating notifications to teams channel.</span></span>|   [<span data-ttu-id="23906-209">View</span><span class="sxs-lookup"><span data-stu-id="23906-209">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="23906-210">View</span><span class="sxs-lookup"><span data-stu-id="23906-210">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="23906-211">Общий образец разъемов</span><span class="sxs-lookup"><span data-stu-id="23906-211">Generic connectors sample</span></span> |<span data-ttu-id="23906-212">Пример кода для общего разъема, который легко настроить для любой системы, которая поддерживает webhooks.</span><span class="sxs-lookup"><span data-stu-id="23906-212">Sample code for a generic connector that's easy to customize for any system which supports webhooks.</span></span>|  | [<span data-ttu-id="23906-213">View</span><span class="sxs-lookup"><span data-stu-id="23906-213">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|
