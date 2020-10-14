---
title: Начало работы — Создание вкладки "канал" и "Группа"
author: heath-hamilton
description: Быстро создайте вкладку "канал и группа Microsoft Teams" с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: f890754cdf4ca43f39c25e3ba24fcf47b08c5a9f
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452857"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="51316-103">Создание вкладки "канал" и "Группа" для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="51316-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="51316-104">В этом руководстве описывается создание простой *вкладки канала* (также известной как *вкладка группы*), которая является полноэкранной страницей для канала команды или чата.</span><span class="sxs-lookup"><span data-stu-id="51316-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="51316-105">В отличие от вкладки личных сведений, пользователи могут настроить некоторые аспекты вкладки такого типа (например, переименовать вкладку, чтобы она была осмысленной для канала).</span><span class="sxs-lookup"><span data-stu-id="51316-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="51316-106">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="51316-106">Your assignment</span></span>

<span data-ttu-id="51316-107">Не давно, ваша организация создала вкладку команды со сведениями о том, как обращаться к важным функциям (служба технической поддержки, HR и т. д.).</span><span class="sxs-lookup"><span data-stu-id="51316-107">Not long ago, your organization created a Teams tab with information on how to contact important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="51316-108">Тем не менее, так как вкладка была создана только для личного использования, каждый пользователь должен установить эту вкладку, чтобы ее увидеть, а уровень внедрения меньше ожидаемого.</span><span class="sxs-lookup"><span data-stu-id="51316-108">However, since the tab was scoped only for personal use, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="51316-109">Другими словами, слишком много сотрудников по-прежнему не знают, как связаться со службой поддержки.</span><span class="sxs-lookup"><span data-stu-id="51316-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="51316-110">Вы можете упростить поиск этих сведений путем создания вкладки канала, которая будет изменять нагрузку, требующую от всех пользователей устанавливать приложение.</span><span class="sxs-lookup"><span data-stu-id="51316-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="51316-111">Вместо этого один пользователь может установить вкладку в канале или чат, чтобы воспользоваться преимуществами всей группы.</span><span class="sxs-lookup"><span data-stu-id="51316-111">Instead, one user can install the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="51316-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="51316-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="51316-113">Создание проекта приложения с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="51316-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="51316-114">Определение некоторых свойств манифеста приложения и формирование шаблонов, относящихся к вкладкам каналов и групп</span><span class="sxs-lookup"><span data-stu-id="51316-114">Identify some of the app manifest properties and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="51316-115">Локальное размещение приложения</span><span class="sxs-lookup"><span data-stu-id="51316-115">Host an app locally</span></span>
> * <span data-ttu-id="51316-116">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-116">Create tab content</span></span>
> * <span data-ttu-id="51316-117">Создание контента для страницы конфигурации вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-117">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="51316-118">Настройка и установка вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-118">Allow a tab to be configured and installed</span></span>
> * <span data-ttu-id="51316-119">Ввод предлагаемого имени вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-119">Provide a suggested tab name</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="51316-120">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="51316-120">1. Create your app project</span></span>

<span data-ttu-id="51316-121">Набор средств Microsoft Teams помогает настроить манифест приложения и формирование шаблонов, относящихся к вкладкам каналов и групп, включая основную страницу конфигурации и страницу содержимого, в которой отображается "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="51316-121">The Microsoft Teams Toolkit helps you set up the app manifest and scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="51316-122">Сообщение.</span><span class="sxs-lookup"><span data-stu-id="51316-122">message.</span></span>

> [!TIP]
> <span data-ttu-id="51316-123">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="51316-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="51316-125">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="51316-125">Enter a name for your Teams app.</span></span> <span data-ttu-id="51316-126">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="51316-126">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="51316-127">На экране **добавить возможности** выберите **вкладки** , а затем **группу или канал Teams**.</span><span class="sxs-lookup"><span data-stu-id="51316-127">On the **Add capabilities** screen, select **Tab** then **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="51316-128">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="51316-128">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="51316-129">2. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="51316-129">2. Identify relevant app project components</span></span>

<span data-ttu-id="51316-130">Большинство манифестов и шаблонов приложений настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="51316-130">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="51316-131">Рассмотрим основные компоненты для создания вкладки "канал" и "Группа".</span><span class="sxs-lookup"><span data-stu-id="51316-131">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="51316-132">Манифест приложения</span><span class="sxs-lookup"><span data-stu-id="51316-132">App manifest</span></span>

<span data-ttu-id="51316-133">В следующем фрагменте манифеста приложения показаны [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs) Свойства и значения по умолчанию, которые относятся к вкладкам каналов и групп.</span><span class="sxs-lookup"><span data-stu-id="51316-133">The following snippet from the app manifest shows [`configurableTabs`](../resources/schema/manifest-schema.md#configurabletabs), which includes the properties and default values relevant to channel and group tabs.</span></span>

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

* <span data-ttu-id="51316-134">`configurationUrl`: URL-адрес узла для страницы настройки вкладки (должен быть HTTPS).</span><span class="sxs-lookup"><span data-stu-id="51316-134">`configurationUrl`: The host URL for your tab configuration page (must be HTTPS).</span></span>
* <span data-ttu-id="51316-135">`canUpdateConfiguration`: Если задано значение `true` , пользователи могут изменять параметры вкладок, переименовывать вкладку или удалять ее из канала или чата.</span><span class="sxs-lookup"><span data-stu-id="51316-135">`canUpdateConfiguration`: If set to `true`, users can change tab settings, rename the tab, or remove it from a channel or chat.</span></span>
* <span data-ttu-id="51316-136">`scopes`: Указывает, могут ли пользователи устанавливать приложение в каналах ( `team` ) и чата ( `groupchat` ).</span><span class="sxs-lookup"><span data-stu-id="51316-136">`scopes`: Specifies if users can install the app in channels (`team`) and chats (`groupchat`).</span></span> <span data-ttu-id="51316-137">Необходимо указать по крайней мере одно значение.</span><span class="sxs-lookup"><span data-stu-id="51316-137">At least one value is required.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="51316-138">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="51316-138">App scaffolding</span></span>

<span data-ttu-id="51316-139">Формирование шаблонов приложений предоставляет `TabConfig.js` файл, расположенный в `src/components` каталоге проекта, для отображения страницы конфигурации вкладки (больше в скором времени).</span><span class="sxs-lookup"><span data-stu-id="51316-139">The app scaffolding provides a `TabConfig.js` file, located in the `src/components` directory of your project, for rendering your tab's configuration page (more on this soon).</span></span>

## <a name="3-run-your-app"></a><span data-ttu-id="51316-140">3. Запустите приложение.</span><span class="sxs-lookup"><span data-stu-id="51316-140">3. Run your app</span></span>

<span data-ttu-id="51316-141">В течение этого времени вы создадите и запустите свое приложение локально.</span><span class="sxs-lookup"><span data-stu-id="51316-141">In the interest of time, you'll build and run your app locally.</span></span>

1. <span data-ttu-id="51316-142">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="51316-142">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="51316-143">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="51316-143">Run `npm start`.</span></span>

<span data-ttu-id="51316-144">По завершении **компиляции успешно выполняется.**</span><span class="sxs-lookup"><span data-stu-id="51316-144">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="51316-145">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="51316-145">message in the terminal.</span></span>

## <a name="4-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="51316-146">4. Настройка безопасного туннеля для приложения</span><span class="sxs-lookup"><span data-stu-id="51316-146">4. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="51316-147">В целях тестирования давайте разместите вкладку на локальном веб-сервере (порт 3000).</span><span class="sxs-lookup"><span data-stu-id="51316-147">For testing purposes, let's host your tab on a local web server (port 3000).</span></span>

1. <span data-ttu-id="51316-148">В терминале запустите `ngrok http 3000` .</span><span class="sxs-lookup"><span data-stu-id="51316-148">In a terminal, run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="51316-149">Скопируйте предоставленный URL-адрес HTTPS.</span><span class="sxs-lookup"><span data-stu-id="51316-149">Copy the HTTPS URL you're provided.</span></span>
1. <span data-ttu-id="51316-150">В `.publish` каталоге откройте `Development.env` .</span><span class="sxs-lookup"><span data-stu-id="51316-150">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="51316-151">Замените `baseUrl0` значение скопированным URL-адресом.</span><span class="sxs-lookup"><span data-stu-id="51316-151">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="51316-152">(Например, замените `baseUrl0=http://localhost:3000` на `baseUrl0=https://85528b2b3ca5.ngrok.io` .)</span><span class="sxs-lookup"><span data-stu-id="51316-152">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ca5.ngrok.io`.)</span></span>

<span data-ttu-id="51316-153">Манифест приложения указывает на место размещения вкладки.</span><span class="sxs-lookup"><span data-stu-id="51316-153">Your app manifest is pointing to where you're hosting the tab.</span></span>

## <a name="5-customize-your-tab-content-page"></a><span data-ttu-id="51316-154">5. Настройка страницы контента вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-154">5. Customize your tab content page</span></span>

<span data-ttu-id="51316-155">Откройте манифест приложения ( `manifest.json` ) в `.publish` каталоге и задайте следующие свойства в разделе [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) , определяющем страницу содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="51316-155">Open the app manifest (`manifest.json`) in the `.publish` directory and set the following properties in [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which defines your tab's content page.</span></span>

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

<span data-ttu-id="51316-156">Скопируйте и обновите следующий фрагмент кода, используя сведения, которые относятся к вашей организации, или, в целях простоты, используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="51316-156">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="51316-157">Перейдите в `src/components` каталог и откройте его `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="51316-157">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="51316-158">Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="51316-158">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="51316-159">Добавьте следующее правило, чтобы `App.css` ссылки электронной почты легче читались независимо от того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="51316-159">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="6-create-your-tab-configuration-page"></a><span data-ttu-id="51316-160">6. Создание страницы конфигурации вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-160">6. Create your tab configuration page</span></span>

<span data-ttu-id="51316-161">У каждой вкладки в канале или в чате есть страница конфигурации, которая является модальной по крайней мере с одним параметром установки, который отображается при установке приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="51316-161">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users install your app.</span></span> <span data-ttu-id="51316-162">По умолчанию на странице конфигурации запрашиваются пользователи, хотят ли они уведомлять канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="51316-162">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="51316-163">Добавьте содержимое на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="51316-163">Add some content to your configuration page.</span></span> <span data-ttu-id="51316-164">Перейдите в `src/components` каталог проекта, откройте `TabConfig.js` и вставьте содержимое внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="51316-164">Go to your project's `src/components` directory, open `TabConfig.js`, and insert some content inside `return()` (as shown).</span></span>

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
> <span data-ttu-id="51316-165">Как минимум, укажите некоторые краткие сведения о приложении на этой странице, так как это может быть первый раз, когда пользователи узнают об этом.</span><span class="sxs-lookup"><span data-stu-id="51316-165">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="51316-166">Кроме того, можно включить настраиваемые параметры конфигурации или [Рабочий процесс проверки подлинности](../tabs/how-to/authentication/auth-aad-sso.md), который распространен на страницах настройки вкладок.</span><span class="sxs-lookup"><span data-stu-id="51316-166">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="7-allow-the-tab-to-be-configured-and-installed"></a><span data-ttu-id="51316-167">7. разрешить настройку и установку вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-167">7. Allow the tab to be configured and installed</span></span>

<span data-ttu-id="51316-168">Чтобы пользователи успешно настроили и установили вкладку, необходимо добавить [URL-адрес безопасного узла, настроенный](#4-set-up-a-secure-tunnel-to-your-app) на компонент страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="51316-168">For users to successfully configure and install the tab, you must add the [secure host URL you set up](#4-set-up-a-secure-tunnel-to-your-app) to the configuration page component.</span></span>

<span data-ttu-id="51316-169">Перейдите к разделу `TabConfig.js` и выберите `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="51316-169">Go to `TabConfig.js` and locate `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="51316-170">Для `"contentUrl"` замените `localhost:3000` часть URL-адреса на домен, в котором размещается содержимое вкладки (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="51316-170">For `"contentUrl"`, replace the `localhost:3000` part of the URL with the domain where you're hosting the tab content (as shown).</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab"
});
```

<span data-ttu-id="51316-171">Кроме того, убедитесь, что `microsoftTeams.settings.setValidityState(true);` .</span><span class="sxs-lookup"><span data-stu-id="51316-171">Also, make sure that `microsoftTeams.settings.setValidityState(true);`.</span></span> <span data-ttu-id="51316-172">По умолчанию он имеет значение, но если для этого параметра задано значение `false` , то кнопка **сохранить** на странице Конфигурация отключена.</span><span class="sxs-lookup"><span data-stu-id="51316-172">It is by default, but if set to `false`, the **Save** button is disabled on the configuration page.</span></span>

## <a name="8-provide-a-suggested-tab-name"></a><span data-ttu-id="51316-173">8. Введите предлагаемое имя вкладки.</span><span class="sxs-lookup"><span data-stu-id="51316-173">8. Provide a suggested tab name</span></span>

<span data-ttu-id="51316-174">При установке вкладки для личного использования отображаемым именем является `name` свойство в `staticTabs` части манифеста приложения (например, " **Мои контакты**").</span><span class="sxs-lookup"><span data-stu-id="51316-174">When you install a tab for personal use, the display name is the `name` property in the `staticTabs` portion of the app manifest (for example, **My Contacts**).</span></span> <span data-ttu-id="51316-175">При установке вкладки канал по умолчанию отображается имя приложения (например, **First-App**).</span><span class="sxs-lookup"><span data-stu-id="51316-175">When you install a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="51316-176">Это может быть разумно в зависимости от того, что вы назначите для вашего приложения, но вы можете указать имя, которое лучше в контексте совместной работы группы (например, " **Контакты группы**").</span><span class="sxs-lookup"><span data-stu-id="51316-176">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

<span data-ttu-id="51316-177">В `TabConfig.js` , вернитесь к `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="51316-177">In `TabConfig.js`, go back to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="51316-178">Добавьте `suggestedDisplayName` свойство с именем вкладки, которое будет отображаться по умолчанию (как показано).</span><span class="sxs-lookup"><span data-stu-id="51316-178">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="51316-179">Используйте предоставленное имя или создайте собственное.</span><span class="sxs-lookup"><span data-stu-id="51316-179">Use the provided name or create your own.</span></span> <span data-ttu-id="51316-180">Помните, что в манифесте вы можете разрешить пользователям изменять имя, если это необходимо.</span><span class="sxs-lookup"><span data-stu-id="51316-180">Remember, in the manifest you're allowing users to change the name if they want.</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://<MY_HOST_DOMAIN>/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="9-view-the-tab"></a><span data-ttu-id="51316-181">9. Просмотр вкладки</span><span class="sxs-lookup"><span data-stu-id="51316-181">9. View the tab</span></span>

<span data-ttu-id="51316-182">Чтобы просмотреть страницы конфигурации и контента вкладки, необходимо установить их в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="51316-182">To see your tab's configuration and content pages, you must install it in a channel or chat.</span></span>

1. <span data-ttu-id="51316-183">В клиенте Teams выберите **приложения**.</span><span class="sxs-lookup"><span data-stu-id="51316-183">In the Teams client, select **Apps**.</span></span>
1. <span data-ttu-id="51316-184">Выберите **Отправить настраиваемое приложение** и выберите приложение `Development.zip` .</span><span class="sxs-lookup"><span data-stu-id="51316-184">Select **Upload a custom app** and choose your app's `Development.zip`.</span></span>
1. <span data-ttu-id="51316-185">Выберите команду **Добавить в группу** или **Добавить в чат** , а затем выберите канал или чат, который вы можете использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="51316-185">Choose **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="51316-186">Выберите **Настройка вкладки**. Отобразится страница Конфигурация.</span><span class="sxs-lookup"><span data-stu-id="51316-186">Select **Set up a tab**. The configuration page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана: страница настройки вкладки каналов.":::
1. <span data-ttu-id="51316-188">Нажмите кнопку **сохранить** , чтобы настроить вкладку. Содержимое отображается.</span><span class="sxs-lookup"><span data-stu-id="51316-188">Select **Save** to configure the tab. The content displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана: страница настройки вкладки каналов.":::

## <a name="well-done"></a><span data-ttu-id="51316-190">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="51316-190">Well done</span></span>

<span data-ttu-id="51316-191">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="51316-191">Congratulations!</span></span> <span data-ttu-id="51316-192">У вас есть приложение Teams с вкладкой для отображения содержимого в каналах и беседах.</span><span class="sxs-lookup"><span data-stu-id="51316-192">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="51316-193">Подробнее</span><span class="sxs-lookup"><span data-stu-id="51316-193">Learn more</span></span>

* <span data-ttu-id="51316-194">[Проверка подлинности пользователей вкладки с единым входом](../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="51316-194">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="51316-195">[Внедрение контента из существующего веб-приложения или веб-страницы](../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="51316-195">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="51316-196">[Создайте простой интерфейс для вкладки](../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="51316-196">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="51316-197">[Создание вкладок для мобильных устройств](../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="51316-197">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="51316-198">Создание вкладки без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="51316-198">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="51316-199">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="51316-199">Next lesson</span></span>

<span data-ttu-id="51316-200">Вы знаете, как создать вкладку для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="51316-200">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="51316-201">Хотите попробовать создать другой тип приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="51316-201">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51316-202">Создание бота</span><span class="sxs-lookup"><span data-stu-id="51316-202">Build a bot</span></span>](../build-your-first-app/build-bot.md)
