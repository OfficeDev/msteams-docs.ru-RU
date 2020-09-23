---
author: heath-hamilton
description: Узнайте, как создать вкладку канала для первого приложения Microsoft Teams.
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
title: Создание вкладки "канал Teams"
ms.openlocfilehash: d0846c3af23fd9df6013f989e9f455f711d05a5f
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210344"
---
# <a name="build-a-teams-channel-tab"></a><span data-ttu-id="ab929-103">Создание вкладки "канал Teams"</span><span class="sxs-lookup"><span data-stu-id="ab929-103">Build a Teams channel tab</span></span>

<span data-ttu-id="ab929-104">В этом руководстве рассказывается, как создать базовую *вкладку канала*, страницу содержимого в полноэкранном режиме для канала команды или чата.</span><span class="sxs-lookup"><span data-stu-id="ab929-104">In this tutorial, you'll build a basic *channel tab*, a full-screen content page for a team channel or chat.</span></span> <span data-ttu-id="ab929-105">В отличие от вкладки личных сведений, пользователи могут настроить некоторые аспекты вкладки канала (например, переименовать вкладку, чтобы она была осмысленной для канала).</span><span class="sxs-lookup"><span data-stu-id="ab929-105">Unlike a personal tab, users can configure some aspects of a channel tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ab929-106">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="ab929-106">Before you begin</span></span>

<span data-ttu-id="ab929-107">Чтобы начать работу, вам потребуется базовое работающее приложение.</span><span class="sxs-lookup"><span data-stu-id="ab929-107">You need a basic running app to get started.</span></span> <span data-ttu-id="ab929-108">Если у вас его нет, выполните [Построение и выполните инструкции Teams в первом приложении](../build-your-first-app/build-and-run.md).</span><span class="sxs-lookup"><span data-stu-id="ab929-108">If you don't have one, follow the [build and run your Teams first app instructions](../build-your-first-app/build-and-run.md).</span></span> <span data-ttu-id="ab929-109">При создании проекта приложения выберите параметр только **вкладка "Группа" или "канал Teams"** .</span><span class="sxs-lookup"><span data-stu-id="ab929-109">When you create your app project, choose only the **Group or Teams channel tab** option.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="ab929-110">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="ab929-110">Your assignment</span></span>

<span data-ttu-id="ab929-111">Не давно, ваша организация создала вкладку команды со сведениями о том, как обращаться к важным функциям (служба технической поддержки, HR и т. д.).</span><span class="sxs-lookup"><span data-stu-id="ab929-111">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="ab929-112">Тем не менее, так как вкладка была создана только для личного использования, каждый пользователь должен установить эту вкладку, чтобы ее увидеть, а уровень внедрения меньше ожидаемого.</span><span class="sxs-lookup"><span data-stu-id="ab929-112">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="ab929-113">Другими словами, слишком много сотрудников по-прежнему не знают, как связаться со службой поддержки.</span><span class="sxs-lookup"><span data-stu-id="ab929-113">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="ab929-114">Вы можете упростить поиск этих сведений путем создания вкладки канала, которая будет изменять нагрузку, требующую от всех пользователей устанавливать приложение.</span><span class="sxs-lookup"><span data-stu-id="ab929-114">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="ab929-115">Вместо этого один пользователь может установить вкладку в канале или чат, чтобы воспользоваться преимуществами всей группы.</span><span class="sxs-lookup"><span data-stu-id="ab929-115">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="ab929-116">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="ab929-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="ab929-117">Определение некоторых свойств манифеста приложения и формирование шаблонов, связанных с вкладками канала</span><span class="sxs-lookup"><span data-stu-id="ab929-117">Identify some of the app manifest properties and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="ab929-118">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-118">Create tab content</span></span>
> * <span data-ttu-id="ab929-119">Создание контента для страницы конфигурации вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-119">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="ab929-120">Настройка и установка вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-120">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="ab929-121">Ввод предлагаемого имени вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-121">Provide a suggested tab name</span></span>

## <a name="identify-relevant-app-project-components"></a><span data-ttu-id="ab929-122">Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="ab929-122">Identify relevant app project components</span></span>

<span data-ttu-id="ab929-123">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="ab929-123">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="ab929-124">Рассмотрим основные компоненты для создания вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="ab929-124">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="ab929-125">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="ab929-125">App manifest</span></span>

<span data-ttu-id="ab929-126">В следующем фрагменте манифеста приложения показано [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) , в том числе свойства и значения по умолчанию, относящиеся к вкладкам канала.</span><span class="sxs-lookup"><span data-stu-id="ab929-126">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel tabs.</span></span>

```JSON
"configurableTabs": [
    {
        "configurationUrl": "{baseUrl0}/config",
        "canUpdateConfiguration": true,
        "scopes": [
            "team",
            "groupchat"
        ]
    }
],
```

* <span data-ttu-id="ab929-127">`configurationUrl`: URL-адрес узла для страницы настройки вкладки (должен быть HTTPS).</span><span class="sxs-lookup"><span data-stu-id="ab929-127">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="ab929-128">`canUpdateConfiguration`: Если задано значение `true` , пользователи могут изменять параметры вкладок, переименовывать вкладку или удалять ее из канала или чата.</span><span class="sxs-lookup"><span data-stu-id="ab929-128">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="ab929-129">`scopes`: Указывает, могут ли пользователи устанавливать приложение в каналах ( `team` ) и чата ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="ab929-129">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="ab929-130">Необходимо указать по крайней мере одно значение.</span><span class="sxs-lookup"><span data-stu-id="ab929-130">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="ab929-131">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="ab929-131">App scaffolding</span></span>

<span data-ttu-id="ab929-132">Формирование шаблонов приложений предоставляет `TabConfig.js` файл, расположенный в `src/components` каталоге проекта, для отображения страницы конфигурации вкладки (больше в скором времени).</span><span class="sxs-lookup"><span data-stu-id="ab929-132">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="create-your-tab-content"></a><span data-ttu-id="ab929-133">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-133">Create your tab content</span></span>

<span data-ttu-id="ab929-134">Откройте манифест приложения ( `manifest.json` ) в `.publish` каталоге и задайте следующие свойства в разделе [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , определяющем страницу содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="ab929-134">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "My Contacts",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

<span data-ttu-id="ab929-135">Скопируйте и обновите следующий фрагмент кода, используя сведения, которые относятся к вашей организации, или, в целях простоты, используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="ab929-135">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="ab929-136">Перейдите в `src/components` каталог и откройте его `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="ab929-136">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="ab929-137">Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="ab929-137">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="ab929-138">Добавьте следующее правило, чтобы `App.css` ссылки электронной почты легче читались независимо от того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="ab929-138">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="create-your-tab-configuration-page"></a><span data-ttu-id="ab929-139">Страница "Создание конфигурации вкладки"</span><span class="sxs-lookup"><span data-stu-id="ab929-139">Create your tab configuration page</span></span>

<span data-ttu-id="ab929-140">На каждой вкладке канала есть страница конфигурации, которая является модальной и по крайней мере с одним параметром установки, который отображается при установке приложения.</span><span class="sxs-lookup"><span data-stu-id="ab929-140">Every channel tab has a configuration page, a modal with at least one setup option that displays when installing the app.</span></span> <span data-ttu-id="ab929-141">По умолчанию на странице конфигурации запрашиваются пользователи, хотят ли они уведомлять канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="ab929-141">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="ab929-142">Добавьте содержимое на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab929-142">Add some content to your configuration page.</span></span> <span data-ttu-id="ab929-143">Перейдите в `src/components` каталог проекта, откройте `TabConfig.js` и вставьте содержимое внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="ab929-143">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

```JavaScript
return (
    <div>
      <h1>Add My Contoso Contacts</h1>
      <div>
        Select <b>Save</b> to add our organization's important contacts to this workspace.
      </div>
    </div>
);
```
 
> [!TIP]
> <span data-ttu-id="ab929-144">Как минимум, укажите некоторые краткие сведения о приложении на этой странице, так как это может быть первый раз, когда пользователи узнают об этом.</span><span class="sxs-lookup"><span data-stu-id="ab929-144">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="ab929-145">Кроме того, можно включить настраиваемые параметры конфигурации или [Рабочий процесс проверки подлинности](../tabs/how-to/authentication/auth-aad-sso.md), который распространен на страницах настройки вкладок.</span><span class="sxs-lookup"><span data-stu-id="ab929-145">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="ab929-146">Настройка и установка вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-146">Allow the tab to be configured and installed</span></span>

<span data-ttu-id="ab929-147">Для успешной настройки и установки вкладки канала необходимо добавить URL-адрес узла, который вы настроили при [создании и запуске первого приложения](../build-your-first-app/build-and-run.md) в компоненте страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ab929-147">For users to successfully configure and install the channel tab, you must add the host URL you set up when [creating and running your first app](../build-your-first-app/build-and-run.md) to the configuration page component.</span></span>

<span data-ttu-id="ab929-148">Перейдите к разделу `TabConfig.js` и выберите `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="ab929-148">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="ab929-149">Для `"contentUrl"` замените `localhost:3000` часть URL-адреса на домен, в котором размещается содержимое вкладки (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="ab929-149">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="ab929-150">Кроме того, убедитесь, что `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="ab929-150">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="ab929-151">По умолчанию он имеет значение, но если для этого параметра задано значение `false` , то кнопка **сохранить** на странице Конфигурация отключена.</span><span class="sxs-lookup"><span data-stu-id="ab929-151">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="provide-a-suggested-tab-name"></a><span data-ttu-id="ab929-152">Ввод предлагаемого имени вкладки</span><span class="sxs-lookup"><span data-stu-id="ab929-152">Provide a suggested tab name</span></span>

<span data-ttu-id="ab929-153">При установке вкладки для личного использования отображаемым именем является `name` свойство в `staticTabs` части манифеста приложения (например, " **Мои контакты**").</span><span class="sxs-lookup"><span data-stu-id="ab929-153">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="ab929-154">При установке вкладки канал по умолчанию отображается имя приложения (например, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="ab929-154">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="ab929-155">Это может быть разумно в зависимости от того, что вы назначите для вашего приложения, но вы можете указать имя, которое лучше в контексте совместной работы группы (например, " **Контакты группы**").</span><span class="sxs-lookup"><span data-stu-id="ab929-155">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="ab929-156">В `TabConfig.js` , вернитесь к `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="ab929-156">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="ab929-157">Добавьте `suggestedDisplayName` свойство с именем вкладки, которое будет отображаться по умолчанию (как показано).</span><span class="sxs-lookup"><span data-stu-id="ab929-157">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="ab929-158">Используйте предоставленное имя или создайте собственное.</span><span class="sxs-lookup"><span data-stu-id="ab929-158">Use the provided name or create your own.</span></span> <span data-ttu-id="ab929-159">Помните, что в манифесте вы можете разрешить пользователям изменять имя, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="ab929-159">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="view-the-channel-tab"></a><span data-ttu-id="ab929-160">Просмотр вкладки "канал"</span><span class="sxs-lookup"><span data-stu-id="ab929-160">View the channel tab</span></span>

<span data-ttu-id="ab929-161">Чтобы просмотреть страницы конфигурации и контента на вкладке канала, необходимо установить его в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="ab929-161">To see your channel tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="ab929-162">В клиенте Teams выберите **приложения**.</span><span class="sxs-lookup"><span data-stu-id="ab929-162">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="ab929-163">Выберите **Отправить настраиваемое приложение** и выберите приложение `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="ab929-163">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="ab929-164">Выберите команду **Добавить в группу** или **Добавить в чат** , а затем выберите канал или чат, который вы можете использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="ab929-164">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="ab929-165">Выберите **Настройка вкладки**. Отобразится страница Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="ab929-165">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана: страница настройки вкладки каналов.":::
1. <span data-ttu-id="ab929-167">Нажмите кнопку **сохранить** , чтобы настроить вкладку. Содержимое отображается.</span><span class="sxs-lookup"><span data-stu-id="ab929-167">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана: вкладка "канал" со статическим представлением контента.":::

## <a name="well-done"></a><span data-ttu-id="ab929-169">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="ab929-169">Well done</span></span>

<span data-ttu-id="ab929-170">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="ab929-170">Congratulations!</span></span> <span data-ttu-id="ab929-171">У вас есть приложение Teams с вкладкой канал для отображения содержимого в каналах и беседах.</span><span class="sxs-lookup"><span data-stu-id="ab929-171">You have a Teams app with a channel tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="ab929-172">Подробнее</span><span class="sxs-lookup"><span data-stu-id="ab929-172">Learn more</span></span>

* <span data-ttu-id="ab929-173">[Проверка подлинности пользователей вкладки с единым входом](../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="ab929-173">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="ab929-174">[Внедрение контента из существующего веб-приложения или веб-страницы](../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="ab929-174">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="ab929-175">[Создайте простой интерфейс для вкладки](../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="ab929-175">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="ab929-176">[Создание вкладок для мобильных устройств](../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="ab929-176">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="ab929-177">Создание вкладки без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="ab929-177">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="ab929-178">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="ab929-178">Next lesson</span></span>

<span data-ttu-id="ab929-179">Вы знаете, как создать вкладку для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="ab929-179">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="ab929-180">Хотите попробовать создать другой тип приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="ab929-180">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ab929-181">Создание ленты</span><span class="sxs-lookup"><span data-stu-id="ab929-181">Build a bot</span></span>](../build-your-first-app/build-bot.md)
