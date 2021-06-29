---
title: Создание соединителей Office 365
author: laujan
description: Описывает, как начать работу с Office 365 соединители в Microsoft Teams
keywords: соединитель teams o365
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/16/2021
ms.openlocfilehash: 28a2b35e868baf34e35a11a00e10b30b0f09c236
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179757"
---
# <a name="create-office-365-connectors"></a><span data-ttu-id="f2fdf-104">Создание соединителей Office 365</span><span class="sxs-lookup"><span data-stu-id="f2fdf-104">Create Office 365 Connectors</span></span>

<span data-ttu-id="f2fdf-105">С Microsoft Teams приложениями можно добавить существующие Office 365 соединителю или создать новый в Teams.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-105">With Microsoft Teams apps, you can add your existing Office 365 Connector or build a new one within Teams.</span></span> <span data-ttu-id="f2fdf-106">Дополнительные сведения см. [в дополнительных сведениях о создании собственного соединитетеля.](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-106">For more information, see [build your own connector](/outlook/actionable-messages/connectors-dev-dashboard#build-your-own-connector).</span></span>

## <a name="add-a-connector-to-teams-app"></a><span data-ttu-id="f2fdf-107">Добавление соединителю в Teams приложение</span><span class="sxs-lookup"><span data-stu-id="f2fdf-107">Add a connector to Teams app</span></span>

<span data-ttu-id="f2fdf-108">Вы можете [упаковать](~/concepts/build-and-test/apps-package.md) [и опубликовать](~/concepts/deploy-and-publish/apps-publish.md) соединители в рамках отправки AppSource.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-108">You can [package](~/concepts/build-and-test/apps-package.md) and [publish](~/concepts/deploy-and-publish/apps-publish.md) your connector as part of your AppSource submission.</span></span> <span data-ttu-id="f2fdf-109">Вы можете распространять зарегистрированный соединитатель как часть пакета Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-109">You can distribute your registered connector as part of your Teams app package.</span></span> <span data-ttu-id="f2fdf-110">Сведения о точках входа для Teams приложения см. [в таблице capabilities.](~/concepts/extensibility-points.md)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-110">For information on entry points for Teams app, see [capabilities](~/concepts/extensibility-points.md).</span></span> <span data-ttu-id="f2fdf-111">Вы также можете предоставить пакет пользователям непосредственно для загрузки в Teams.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-111">You can also provide the package to users directly for uploading within Teams.</span></span>

<span data-ttu-id="f2fdf-112">Для распространения соединитетеля необходимо зарегистрироваться через [панель мониторинга разработчиков соединители.](https://outlook.office.com/connectors/home/login/#/publish)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-112">To distribute your connector, you must register through [Connectors Developer Dashboard](https://outlook.office.com/connectors/home/login/#/publish).</span></span> <span data-ttu-id="f2fdf-113">При регистрации соединитетеля предполагается, что он работает во всех Office 365, поддерживаюх приложения, включая Outlook и Teams.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-113">When a connector is registered, it is assumed that it works in all Office 365 products that support applications, including Outlook and Teams.</span></span> <span data-ttu-id="f2fdf-114">Если это не так, и необходимо создать соединителя, который работает только в Microsoft Teams, свяжитесь: Microsoft Teams отправки приложений по [электронной почте](mailto:teamsubm@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f2fdf-114">If that is not the case and you must create a connector that only works in Microsoft Teams, contact: [Microsoft Teams App Submissions email](mailto:teamsubm@microsoft.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2fdf-115">Соединитель регистрируется после выбора **сохранить** в панели мониторинга разработчика соединители.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-115">Your connector is registered after you select **Save** in the Connectors Developer Dashboard.</span></span> <span data-ttu-id="f2fdf-116">Если вы хотите опубликовать соединителе в AppSource, следуйте инструкциям в публикации [Microsoft Teams приложения в AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span><span class="sxs-lookup"><span data-stu-id="f2fdf-116">If you want to publish your connector in AppSource, follow the instructions in [publish your Microsoft Teams app to AppSource](~/concepts/deploy-and-publish/apps-publish.md).</span></span> <span data-ttu-id="f2fdf-117">Если вы не хотите публиковать приложение в AppSource, раздайте его непосредственно организации.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-117">If you do not want to publish your app in AppSource, distribute it directly to the organization.</span></span> <span data-ttu-id="f2fdf-118">После [публикации соединители для организации](#publish-connectors-for-the-organization)никаких дополнительных действий на панели мониторинга соединители не требуется.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-118">After [publishing connectors for your organization](#publish-connectors-for-the-organization), no further action is required on the Connector Dashboard.</span></span>

### <a name="integrate-the-configuration-experience"></a><span data-ttu-id="f2fdf-119">Интеграция опытом настройки</span><span class="sxs-lookup"><span data-stu-id="f2fdf-119">Integrate the configuration experience</span></span>

<span data-ttu-id="f2fdf-120">Пользователи могут выполнить весь процесс настройки соединитетеля, не покидая Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-120">Users can complete the entire connector configuration experience without having to leave the Teams client.</span></span> <span data-ttu-id="f2fdf-121">Чтобы получить опыт, Teams встраить страницу конфигурации непосредственно в iframe.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-121">To get the experience, Teams can embed your configuration page directly within an iframe.</span></span> <span data-ttu-id="f2fdf-122">Последовательность операций следующим образом:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-122">The sequence of operations is as follows:</span></span>

1. <span data-ttu-id="f2fdf-123">Для начала процесса настройки пользователь выбирает соединител.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-123">The user selects the connector to begin the configuration process.</span></span>
1. <span data-ttu-id="f2fdf-124">Пользователь взаимодействует с веб-интерфейсом для завершения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-124">The user interacts with the web experience to complete the configuration.</span></span>
1. <span data-ttu-id="f2fdf-125">Пользователь выбирает **сохранить ,** который вызывает вызов в коде.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-125">The user selects **Save**, which triggers a callback in code.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="f2fdf-126">Код может обработать событие сохранения путем восстановления параметров веб-ок.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-126">The code can process the save event by retrieving the webhook settings.</span></span> <span data-ttu-id="f2fdf-127">Код хранит веб-сайт для публикации событий позже.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-127">Your code stores the webhook to post events later.</span></span>
    > * <span data-ttu-id="f2fdf-128">В пределах Teams загружается Teams.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-128">The configuration experience is loaded inline within Teams.</span></span>

<span data-ttu-id="f2fdf-129">Вы можете повторно использовать существующие возможности веб-конфигурации или создать отдельную версию, которая будет организована в Teams.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-129">You can reuse your existing web configuration experience or create a separate version to be hosted specifically in Teams.</span></span> <span data-ttu-id="f2fdf-130">Код должен включать Microsoft Teams JavaScript SDK.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-130">Your code must include the Microsoft Teams JavaScript SDK.</span></span> <span data-ttu-id="f2fdf-131">Это дает коду доступ к API для выполнения общих операций, таких как получение текущего контекста пользователя, канала или группы и начало потоков проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-131">This gives your code access to APIs to perform common operations, such as getting the current user, channel, or team context and initiate authentication flows.</span></span>

<span data-ttu-id="f2fdf-132">**Интеграция опытом конфигурации**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-132">**To integrate the configuration experience**</span></span>

1. <span data-ttu-id="f2fdf-133">Инициализация SDK происходит путем вызова `microsoftTeams.initialize()`.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-133">Initialize the SDK by calling `microsoftTeams.initialize()`.</span></span>
1. <span data-ttu-id="f2fdf-134">Вызов, `microsoftTeams.settings.setValidityState(true)` чтобы включить **сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-134">Call `microsoftTeams.settings.setValidityState(true)` to enable **Save**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2fdf-135">Вы должны вызвать `microsoftTeams.settings.setValidityState(true)` в качестве ответа на выбор пользователя или обновление поля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-135">You must call `microsoftTeams.settings.setValidityState(true)` as a response to user selection or field update.</span></span>

1. <span data-ttu-id="f2fdf-136">Регистрируйте  `microsoftTeams.settings.registerOnSaveHandler()` обработник событий, который называется, когда пользователь выбирает **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-136">Register  `microsoftTeams.settings.registerOnSaveHandler()` event handler, which is called when the user selects **Save**.</span></span>
1. <span data-ttu-id="f2fdf-137">Вызов `microsoftTeams.settings.setSettings()` для сохранения параметров соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-137">Call `microsoftTeams.settings.setSettings()` to save the connector settings.</span></span> <span data-ttu-id="f2fdf-138">Сохраненные параметры также показаны в диалоговом окне конфигурации, если пользователь пытается обновить существующую конфигурацию для соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-138">The saved settings are also shown in the configuration dialog if the user tries to update an existing configuration for your connector.</span></span>
1. <span data-ttu-id="f2fdf-139">Вызов `microsoftTeams.settings.getSettings()` для получения свойств веб-сайта, включая URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-139">Call `microsoftTeams.settings.getSettings()` to fetch webhook properties, including the URL.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f2fdf-140">При первой загрузке страницы в случае перенастройки необходимо вызвать `microsoftTeams.settings.getSettings()` вызов.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-140">You must call `microsoftTeams.settings.getSettings()` when your page is first loaded in case of reconfiguration.</span></span>

1. <span data-ttu-id="f2fdf-141">Регистрируйте `microsoftTeams.settings.registerOnRemoveHandler()` обработчик событий, который называется, когда пользователь удаляет соединители.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-141">Register `microsoftTeams.settings.registerOnRemoveHandler()` event handler, which is called when the user removes connector.</span></span>

<span data-ttu-id="f2fdf-142">Это событие предоставляет службе возможность выполнять любые действия по очистке.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-142">This event gives your service an opportunity to perform any cleanup actions.</span></span>

<span data-ttu-id="f2fdf-143">В следующем коде содержится пример HTML для создания страницы конфигурации соединителя без обслуживания и поддержки клиентов:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-143">The following code provides a sample HTML to create a connector configuration page without the customer service and support:</span></span>

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

<span data-ttu-id="f2fdf-144">Чтобы проверить подлинность пользователя в рамках загрузки страницы, см. поток проверки подлинности для вкладки для интеграции в систему при вложении страницы. [](~/tabs/how-to/authentication/auth-flow-tab.md)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-144">To authenticate the user as part of loading your page, see [authentication flow for tabs](~/tabs/how-to/authentication/auth-flow-tab.md) to integrate sign in when your page is embedded.</span></span>

> [!NOTE]
> <span data-ttu-id="f2fdf-145">В связи с перекрестной совместимостью клиента перед вызовом код должен звонить с URL-адресом и методами успешного или неудачного `microsoftTeams.authentication.registerAuthenticationHandlers()` `authenticate()` вызова.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-145">Due to cross client compatibility reasons, your code must call `microsoftTeams.authentication.registerAuthenticationHandlers()` with the URL and success or failure callback methods before calling `authenticate()`.</span></span>

#### <a name="getsettings-response-properties"></a><span data-ttu-id="f2fdf-146">`GetSettings` Свойства ответа</span><span class="sxs-lookup"><span data-stu-id="f2fdf-146">`GetSettings` response properties</span></span>

>[!NOTE]
><span data-ttu-id="f2fdf-147">Параметры, возвращенные вызовом, отличаются при вызове этого метода из вкладки и отличаются от параметров `getSettings` [js.](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-147">The parameters returned by the `getSettings` call are different when you invoke this method from a tab and differ from those documented in [js settings](/javascript/api/%40microsoft/teams-js/settings.settings?view=msteams-client-js-latest&preserve-view=true).</span></span>

<span data-ttu-id="f2fdf-148">В следующей таблице параметров и сведений о свойствах `GetSetting` отклика:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-148">The following table provides the parameters and the details of `GetSetting` response properties:</span></span>

| <span data-ttu-id="f2fdf-149">Параметры</span><span class="sxs-lookup"><span data-stu-id="f2fdf-149">Parameters</span></span>   | <span data-ttu-id="f2fdf-150">Сведения</span><span class="sxs-lookup"><span data-stu-id="f2fdf-150">Details</span></span> |
|-------------|---------|
| `entityId`       | <span data-ttu-id="f2fdf-151">Код сущности, задаваемый кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-151">The entity ID, as set by your code when calling `setSettings()`.</span></span> |
| `configName`  | <span data-ttu-id="f2fdf-152">Имя конфигурации, заданная кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-152">The configuration name, as set by your code when calling `setSettings()`.</span></span> |
| `contentUrl` | <span data-ttu-id="f2fdf-153">URL-адрес страницы конфигурации, заданная кодом при `setSettings()` вызове.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-153">The URL of the configuration page, as set by your code when calling `setSettings()`.</span></span> |
| `webhookUrl` | <span data-ttu-id="f2fdf-154">URL-адрес веб-страницы, созданный для соединителя.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-154">The webhook URL created for the connector.</span></span> <span data-ttu-id="f2fdf-155">Для отправки карт на канал используйте URL-адрес веб-сайта POST, структурированный JSON.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-155">Use the webhook URL to POST structured JSON to send cards to the channel.</span></span> <span data-ttu-id="f2fdf-156">Возвращается `webhookUrl` только тогда, когда приложение возвращает данные успешно.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-156">The `webhookUrl` is returned only when the application returns data successfully.</span></span> |
| `appType` | <span data-ttu-id="f2fdf-157">Возвращенные значения могут быть `mail` `groups` соответствующими Office 365, Office 365 группам или Microsoft Teams `teams` соответственно.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-157">The values returned can be `mail`, `groups`, or `teams` corresponding to the Office 365 Mail, Office 365 Groups, or Microsoft Teams respectively.</span></span> |
| `userObjectId` | <span data-ttu-id="f2fdf-158">Уникальный ID, соответствующий Office 365, который инициировал настройка соединиттеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-158">The unique ID corresponding to the Office 365 user who initiated the set up of the connector.</span></span> <span data-ttu-id="f2fdf-159">Она должна быть защищена.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-159">It must be secured.</span></span> <span data-ttu-id="f2fdf-160">Это значение можно использовать для связи пользователя в Office 365, который настроил конфигурацию в службе.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-160">This value can be used to associate the user in Office 365, who has set up the configuration in your service.</span></span> |

#### <a name="handle-edits"></a><span data-ttu-id="f2fdf-161">Обработка изменений</span><span class="sxs-lookup"><span data-stu-id="f2fdf-161">Handle edits</span></span>

<span data-ttu-id="f2fdf-162">Код должен обрабатывать пользователей, которые возвращаются, чтобы изменить существующую конфигурацию соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-162">Your code must handle users who return to edit an existing connector configuration.</span></span> <span data-ttu-id="f2fdf-163">Для этого необходимо вызвать `microsoftTeams.settings.setSettings()` во время начальной конфигурации со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-163">To do this, call `microsoftTeams.settings.setSettings()` during the initial configuration with the following parameters:</span></span>

- <span data-ttu-id="f2fdf-164">`entityId` это пользовательский ID, который представляет то, что пользователь настроил и понял в вашей службе.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-164">`entityId` is the custom ID that represents what the user has configured and understood by your service.</span></span>
- <span data-ttu-id="f2fdf-165">`configName` это имя, которое код конфигурации может получить.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-165">`configName` is a name that configuration code can retrieve.</span></span>
- <span data-ttu-id="f2fdf-166">`contentUrl` это настраиваемый URL-адрес, загружаемый при редактировании существующей конфигурации соединителя.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-166">`contentUrl` is a custom URL that gets loaded when a user edits an existing connector configuration.</span></span>

<span data-ttu-id="f2fdf-167">Этот вызов выполнен в рамках обработки событий сохранения.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-167">This call is made as part of your save event handler.</span></span> <span data-ttu-id="f2fdf-168">Затем при загрузке кода необходимо вызвать для предварительного заполнения любых параметров или форм `contentUrl` `getSettings()` в пользовательском интерфейсе конфигурации.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-168">Then, when the `contentUrl` is loaded, your code must call `getSettings()` to pre populate any settings or forms in your configuration user interface.</span></span>

#### <a name="handle-removals"></a><span data-ttu-id="f2fdf-169">Обработка удалений</span><span class="sxs-lookup"><span data-stu-id="f2fdf-169">Handle removals</span></span>

<span data-ttu-id="f2fdf-170">Обработчик событий можно выполнить, если пользователь удаляет существующую конфигурацию соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-170">You can execute an event handler when the user removes an existing connector configuration.</span></span> <span data-ttu-id="f2fdf-171">Этот обработок регистрируется по вызову `microsoftTeams.settings.registerOnRemoveHandler()` .</span><span class="sxs-lookup"><span data-stu-id="f2fdf-171">You register this handler by calling `microsoftTeams.settings.registerOnRemoveHandler()`.</span></span> <span data-ttu-id="f2fdf-172">Этот обработок используется для выполнения операций очистки, например для удаления записей из базы данных.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-172">This handler is used to perform cleanup operations, such as removing entries from a database.</span></span>

### <a name="include-the-connector-in-your-manifest"></a><span data-ttu-id="f2fdf-173">Включите соединители в манифест</span><span class="sxs-lookup"><span data-stu-id="f2fdf-173">Include the connector in your Manifest</span></span>

<span data-ttu-id="f2fdf-174">Скачайте авто, `Teams app manifest` сгенерированную с портала.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-174">Download the auto generated `Teams app manifest` from the portal.</span></span> <span data-ttu-id="f2fdf-175">Выполните следующие действия перед тестированием или публикацией приложения:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-175">Perform the following steps, before testing or publishing the app:</span></span>

1. <span data-ttu-id="f2fdf-176">[Включение двух значков](../../concepts/build-and-test/apps-package.md#app-icons).</span><span class="sxs-lookup"><span data-stu-id="f2fdf-176">[Include two icons](../../concepts/build-and-test/apps-package.md#app-icons).</span></span>
1. <span data-ttu-id="f2fdf-177">Измените `icons` часть манифеста, чтобы включить имена файлов значков вместо URL-адресов.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-177">Modify the `icons` portion of the manifest to include the file names of the icons instead of URLs.</span></span>

<span data-ttu-id="f2fdf-178">В следующем manifest.jsфайле содержатся элементы, необходимые для тестирования и отправки приложения:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-178">The following manifest.json file contains the elements needed to test and submit the app:</span></span>

> [!NOTE]
> <span data-ttu-id="f2fdf-179">Замените `id` `connectorId` и в следующем примере guID соединитетеля.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-179">Replace `id` and `connectorId` in the following example with the GUID of the connector.</span></span>

#### <a name="example-of-manifestjson-with-connector"></a><span data-ttu-id="f2fdf-180">Пример manifest.jsс соединитетелем</span><span class="sxs-lookup"><span data-stu-id="f2fdf-180">Example of manifest.json with connector</span></span>

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
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="enable-or-disable-connectors-in-teams"></a><span data-ttu-id="f2fdf-181">Включить или отключить соединители в Teams</span><span class="sxs-lookup"><span data-stu-id="f2fdf-181">Enable or disable connectors in Teams</span></span>

<span data-ttu-id="f2fdf-182">Модуль Exchange Online PowerShell V2 использует современную проверку подлинности и работает с многофакторной проверкой подлинности под названием MFA для подключения Exchange связанных сред PowerShell в Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-182">The Exchange Online PowerShell V2 module uses modern authentication and works with multi factor authentication, called MFA for connecting to all Exchange related PowerShell environments in Microsoft 365.</span></span> <span data-ttu-id="f2fdf-183">Администраторы могут использовать Exchange Online PowerShell для отключения соединители для всего клиента или определенного почтового ящика группы, затрагивая всех пользователей в этом клиенте или почтовом ящике.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-183">Admins can use Exchange Online PowerShell to disable connectors for an entire tenant or a specific group mailbox, affecting all users in that tenant or mailbox.</span></span> <span data-ttu-id="f2fdf-184">Отключение для одних и не для других невозможно.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-184">It is not possible to disable for some and not others.</span></span> <span data-ttu-id="f2fdf-185">Кроме того, соединители отключены по умолчанию для облако сообщества для государственных организаций, называемых GCC клиентов.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-185">Also, connectors are disabled by default for Government Community Cloud, called GCC tenants.</span></span>

<span data-ttu-id="f2fdf-186">Параметр уровня клиента переопределяет параметр группового уровня.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-186">The tenant level setting overrides the group level setting.</span></span> <span data-ttu-id="f2fdf-187">Например, если администратор включает соединители для группы и отключает их в клиенте, соединители для группы отключены.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-187">For example, if an admin enables connectors for the group and disables them on the tenant, connectors for the group is disabled.</span></span> <span data-ttu-id="f2fdf-188">Чтобы включить соединитель в Teams, подключите Exchange Online [PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) с помощью современной проверки подлинности с помощью MFA или без него.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-188">To enable a connector in Teams, [connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell?view=exchange-ps#connect-to-exchange-online-powershell-using-modern-authentication-with-or-without-mfa&preserve-view=true) using modern authentication with or without MFA.</span></span>

### <a name="commands-to-enable-or-disable-connectors"></a><span data-ttu-id="f2fdf-189">Команды, позволяющие включить или отключить соединители</span><span class="sxs-lookup"><span data-stu-id="f2fdf-189">Commands to enable or disable connectors</span></span>

<span data-ttu-id="f2fdf-190">В Exchange Online PowerShell выполните следующие команды.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-190">Run the following commands in Exchange Online PowerShell:</span></span>

* <span data-ttu-id="f2fdf-191">Отключение соединители для клиента: `Set-OrganizationConfig -ConnectorsEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="f2fdf-191">To disable connectors for the tenant: `Set-OrganizationConfig -ConnectorsEnabled:$false`.</span></span>
* <span data-ttu-id="f2fdf-192">Отключение действий для клиента: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false` .</span><span class="sxs-lookup"><span data-stu-id="f2fdf-192">To disable actionable messages for the tenant: `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$false`.</span></span>
* <span data-ttu-id="f2fdf-193">Чтобы включить соединители для Teams, запустите следующие команды:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-193">To enable connectors for Teams, run the following commands:</span></span>
  * `Set-OrganizationConfig -ConnectorsEnabled:$true `
  * `Set-OrganizationConfig -ConnectorsEnabledForTeams:$true`
  * `Set-OrganizationConfig -ConnectorsActionableMessagesEnabled:$true`

<span data-ttu-id="f2fdf-194">Дополнительные сведения об обмене модулями PowerShell см. в [сайте Set-OrganizationConfig.](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-194">For more information on PowerShell module exchange, see [Set-OrganizationConfig](/powershell/module/exchange/Set-OrganizationConfig?view=exchange-ps&preserve-view=true).</span></span> <span data-ttu-id="f2fdf-195">Чтобы включить или отключить Outlook соединители, [подключите приложения к](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us)группам в Outlook.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-195">To enable or disable Outlook connectors, [connect apps to your groups in Outlook](https://support.microsoft.com/topic/connect-apps-to-your-groups-in-outlook-ed0ce547-038f-4902-b9b3-9e518ae6fbab?ui=en-us&rs=en-us&ad=us).</span></span>

## <a name="test-your-connector"></a><span data-ttu-id="f2fdf-196">Тестирование соединитетеля</span><span class="sxs-lookup"><span data-stu-id="f2fdf-196">Test your connector</span></span>

<span data-ttu-id="f2fdf-197">Чтобы проверить соединители, загрузите его в команду с любым другим приложением.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-197">To test your connector, upload it to a team with any other app.</span></span> <span data-ttu-id="f2fdf-198">Вы можете создать пакет .zip с помощью файла манифеста из двух файлов значков и соединителов Панели мониторинга разработчика, измененных как указано в Включите соединитетель в [манифесте](#include-the-connector-in-your-manifest).</span><span class="sxs-lookup"><span data-stu-id="f2fdf-198">You can create a .zip package using the manifest file from the two icon files and connectors Developer Dashboard, modified as directed in [Include the connector in your Manifest](#include-the-connector-in-your-manifest).</span></span>

<span data-ttu-id="f2fdf-199">После отправки приложения откройте список соединитений из любого канала.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-199">After you upload the app, open the connectors list from any channel.</span></span> <span data-ttu-id="f2fdf-200">Прокрутите вниз, чтобы просмотреть приложение в разделе **Uploaded:**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-200">Scroll to the bottom to see your app in the **Uploaded** section:</span></span>

![Снимок экрана загруженного раздела в диалоговом окне соединитель](~/assets/images/connectors/connector_dialog_uploaded.png)

> [!NOTE]
> <span data-ttu-id="f2fdf-202">Поток происходит полностью в пределах Microsoft Teams в качестве хозяйского опыта.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-202">The flow occurs entirely within Microsoft Teams as a hosted experience.</span></span>

<span data-ttu-id="f2fdf-203">Чтобы убедиться, что действие работает правильно, отправьте сообщения в `HttpPOST` [соединителю.](~/webhooks-and-connectors/how-to/connectors-using.md)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-203">To verify that `HttpPOST` action is working correctly, [send messages to your connector](~/webhooks-and-connectors/how-to/connectors-using.md).</span></span>

## <a name="publish-connectors-for-the-organization"></a><span data-ttu-id="f2fdf-204">Публикация соединители для организации</span><span class="sxs-lookup"><span data-stu-id="f2fdf-204">Publish connectors for the organization</span></span>

<span data-ttu-id="f2fdf-205">Если вы хотите, чтобы соединители были доступны только пользователям в организации, вы можете загрузить свое настраиваемое приложение соединители в каталог [приложений организации.](~/concepts/deploy-and-publish/apps-publish.md)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-205">If you want the connector to be available only to the users in your organization, you can upload your custom connector app to your [organization's app catalog](~/concepts/deploy-and-publish/apps-publish.md).</span></span>

<span data-ttu-id="f2fdf-206">После отправки пакета приложений для настройки и использования соединителя в команде установите соединители из каталога приложений организации.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-206">After uploading the app package to configure and use the connector in a team, install the connector from the organization's app catalog.</span></span>

<span data-ttu-id="f2fdf-207">**Настройка соединитетеля**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-207">**To set up a connector**</span></span>

1. <span data-ttu-id="f2fdf-208">Выберите **Приложения** из левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-208">Select **Apps** from the left navigation bar.</span></span>
1. <span data-ttu-id="f2fdf-209">В разделе **Приложения** выберите **соединители**.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-209">In the **Apps** section, select **Connectors**.</span></span>
1. <span data-ttu-id="f2fdf-210">Выберите соединителю, который необходимо добавить.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-210">Select the connector that you want to add.</span></span> <span data-ttu-id="f2fdf-211">Появляется всплывающее диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-211">A pop up dialog window appears.</span></span>
1. <span data-ttu-id="f2fdf-212">В меню dropdown выберите **Добавить в команду**.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-212">From the dropdown menu, select **Add to a team**.</span></span>
1. <span data-ttu-id="f2fdf-213">В поле поиска введите команду или имя канала.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-213">In the search box, type a team or channel name.</span></span>
1. <span data-ttu-id="f2fdf-214">Выберите **Настройка соединителя из** выпадаемого меню в правом нижнем углу окна диалогов.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-214">Select **Set up a Connector** from the dropdown menu in the bottom right corner of the dialog window.</span></span>

<span data-ttu-id="f2fdf-215">Соединитектор доступен в разделе &#9679;&#9679;&#9679; > **Дополнительные** параметры  >  **Соединители**  >  **Все**  >  **соединители для вашей команды** для этой группы.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-215">The connector is available in the section &#9679;&#9679;&#9679; > **More options** > **Connectors** > **All** > **Connectors for your team** for that team.</span></span> <span data-ttu-id="f2fdf-216">Вы можете перемещаться путем прокрутки в этот раздел или поиска соединитеного приложения.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-216">You can navigate by scrolling to this section or search for the connector app.</span></span> <span data-ttu-id="f2fdf-217">Чтобы настроить или изменить соединители, выберите **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-217">To configure or modify the connector, select **Configure**.</span></span>

## <a name="distribute-webhook-and-connector"></a><span data-ttu-id="f2fdf-218">Распространение веб-ок и соединители</span><span class="sxs-lookup"><span data-stu-id="f2fdf-218">Distribute webhook and connector</span></span>

1. <span data-ttu-id="f2fdf-219">[Настройка входящих веб-ок непосредственно](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) для вашей команды.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-219">[Set up an Incoming Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md?branch=pr-en-us-3076#create-incoming-webhook) directly for your team.</span></span>
1. <span data-ttu-id="f2fdf-220">Добавьте [страницу конфигурации](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) [и опубликуйте входящий веб-сайт](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) в соединителю O365.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-220">Add a [configuration page](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#integrate-the-configuration-experience) and [publish your Incoming Webhook](~/webhooks-and-connectors/how-to/connectors-creating.md?branch=pr-en-us-3076#publish-connectors-for-the-organization) in a O365 Connector.</span></span>
1. <span data-ttu-id="f2fdf-221">Пакет и публикация соединитетеля в рамках отправки [AppSource.](~/concepts/deploy-and-publish/office-store-guidance.md)</span><span class="sxs-lookup"><span data-stu-id="f2fdf-221">Package and publish your connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="code-sample"></a><span data-ttu-id="f2fdf-222">Пример кода</span><span class="sxs-lookup"><span data-stu-id="f2fdf-222">Code sample</span></span>

<span data-ttu-id="f2fdf-223">В следующей таблице приводится пример имени и его описания:</span><span class="sxs-lookup"><span data-stu-id="f2fdf-223">The following table provides the sample name and its description:</span></span>

|<span data-ttu-id="f2fdf-224">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-224">**Sample name**</span></span> | <span data-ttu-id="f2fdf-225">**Описание**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-225">**Description**</span></span> | <span data-ttu-id="f2fdf-226">**.NET**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-226">**.NET**</span></span> | <span data-ttu-id="f2fdf-227">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="f2fdf-227">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="f2fdf-228">Соединители</span><span class="sxs-lookup"><span data-stu-id="f2fdf-228">Connectors</span></span>    | <span data-ttu-id="f2fdf-229">Пример Office 365 соединители, генерирующие уведомления для Teams канала.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-229">Sample Office 365 Connector generating notifications to Teams channel.</span></span>|   [<span data-ttu-id="f2fdf-230">View</span><span class="sxs-lookup"><span data-stu-id="f2fdf-230">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-todo-notification/csharp) | [<span data-ttu-id="f2fdf-231">View</span><span class="sxs-lookup"><span data-stu-id="f2fdf-231">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-github-notification/nodejs)|
| <span data-ttu-id="f2fdf-232">Общий пример соединители</span><span class="sxs-lookup"><span data-stu-id="f2fdf-232">Generic connectors sample</span></span> |<span data-ttu-id="f2fdf-233">Пример кода для общего соединители, который легко настроить для любой системы, поддерживающую веб-сайты.</span><span class="sxs-lookup"><span data-stu-id="f2fdf-233">Sample code for a generic connector that is easy to customize for any system that supports webhooks.</span></span>|  | [<span data-ttu-id="f2fdf-234">View</span><span class="sxs-lookup"><span data-stu-id="f2fdf-234">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/connector-generic/nodejs)|

## <a name="see-also"></a><span data-ttu-id="f2fdf-235">См. также</span><span class="sxs-lookup"><span data-stu-id="f2fdf-235">See also</span></span>

* [<span data-ttu-id="f2fdf-236">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="f2fdf-236">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
* [<span data-ttu-id="f2fdf-237">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="f2fdf-237">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="f2fdf-238">Создание соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="f2fdf-238">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
