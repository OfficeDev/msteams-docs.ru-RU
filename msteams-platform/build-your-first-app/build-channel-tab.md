---
title: Начало работы — Создание вкладки "канал" и "Группа"
author: heath-hamilton
description: Быстро создайте вкладку "канал и группа Microsoft Teams" с помощью набора инструментов Microsoft Teams.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 46b5410a1ae7c866f8998362765dfe5462df94cb
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931766"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="0cccb-103">Создание вкладки "канал" и "Группа" для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0cccb-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="0cccb-104">В этом руководстве описывается создание простой *вкладки канала* (также известной как *вкладка группы* ), которая является полноэкранной страницей для канала команды или чата.</span><span class="sxs-lookup"><span data-stu-id="0cccb-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab* ), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="0cccb-105">В отличие от вкладки личных сведений, пользователи могут настроить некоторые аспекты вкладки такого типа (например, переименовать вкладку, чтобы она была осмысленной для канала).</span><span class="sxs-lookup"><span data-stu-id="0cccb-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="0cccb-106">Ваше назначение</span><span class="sxs-lookup"><span data-stu-id="0cccb-106">Your assignment</span></span>

<span data-ttu-id="0cccb-107">Не давно, ваша организация создала приложение Teams, которое использует вкладку для отображения важных контактных сведений (служба технической поддержки, HR и т. д.).</span><span class="sxs-lookup"><span data-stu-id="0cccb-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="0cccb-108">Тем не менее, так как это личная вкладка, каждый пользователь должен установить эту вкладку, чтобы она была доступна, а внедрение ниже ожидаемого.</span><span class="sxs-lookup"><span data-stu-id="0cccb-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="0cccb-109">Другими словами, слишком много сотрудников по-прежнему не знают, как связаться со службой поддержки.</span><span class="sxs-lookup"><span data-stu-id="0cccb-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="0cccb-110">Вы можете упростить поиск этих сведений путем создания вкладки канала, которая будет изменять нагрузку, требующую от всех пользователей устанавливать приложение.</span><span class="sxs-lookup"><span data-stu-id="0cccb-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="0cccb-111">Вместо этого один пользователь может добавить вкладку в канал или чат для получения преимуществ целой группы.</span><span class="sxs-lookup"><span data-stu-id="0cccb-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="0cccb-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="0cccb-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="0cccb-113">Создание проекта приложения с помощью набора инструментов Microsoft Teams для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="0cccb-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="0cccb-114">Определите некоторые конфигурации приложений и формирование шаблонов, относящихся к вкладкам каналов и групп</span><span class="sxs-lookup"><span data-stu-id="0cccb-114">Identify some of the app configurations and scaffolding relevant to channel and group tabs</span></span>
> * <span data-ttu-id="0cccb-115">Создание содержимого вкладки</span><span class="sxs-lookup"><span data-stu-id="0cccb-115">Create tab content</span></span>
> * <span data-ttu-id="0cccb-116">Создание контента для страницы конфигурации вкладки</span><span class="sxs-lookup"><span data-stu-id="0cccb-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="0cccb-117">Ввод предлагаемого имени вкладки</span><span class="sxs-lookup"><span data-stu-id="0cccb-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="0cccb-118">Создание и запуск приложения на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="0cccb-118">Build and run your app locally</span></span>
> * <span data-ttu-id="0cccb-119">Загрузка неопубликованных ваше приложение в Teams для тестирования</span><span class="sxs-lookup"><span data-stu-id="0cccb-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0cccb-120">Перед началом работы</span><span class="sxs-lookup"><span data-stu-id="0cccb-120">Before you begin</span></span>

<span data-ttu-id="0cccb-121">Если вы еще не сделали это, убедитесь, что вы [знаете и установите необходимые компоненты для разработки Teams](build-first-app-overview.md#get-prerequisites).</span><span class="sxs-lookup"><span data-stu-id="0cccb-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="0cccb-122">1. Создайте проект приложения.</span><span class="sxs-lookup"><span data-stu-id="0cccb-122">1. Create your app project</span></span>

<span data-ttu-id="0cccb-123">Набор средств Microsoft Teams помогает настроить приложение и настроить формирование шаблонов, относящихся к вкладкам каналов и групп, включая основную страницу конфигурации и страницу контента, на которой отображается "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="0cccb-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="0cccb-124">Сообщение.</span><span class="sxs-lookup"><span data-stu-id="0cccb-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="0cccb-125">Если вы еще не создали проект приложения Teams, возможно, вам будет полезно выполнить приведенные [выше инструкции по](../build-your-first-app/build-and-run.md) более подробному объяснению проектов.</span><span class="sxs-lookup"><span data-stu-id="0cccb-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio Code выберите **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой панели активности и выберите **создать приложение Teams**.
1. <span data-ttu-id="0cccb-127">При появлении соответствующего запроса войдите в систему с помощью учетной записи разработчика Microsoft 365.</span><span class="sxs-lookup"><span data-stu-id="0cccb-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="0cccb-128">На экране **добавить возможности** выберите **вкладка** **Далее**.</span><span class="sxs-lookup"><span data-stu-id="0cccb-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="0cccb-129">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="0cccb-130">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)</span><span class="sxs-lookup"><span data-stu-id="0cccb-130">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="0cccb-131">Проверьте параметры вкладки " **Личные"** и " **Группа" или "канал Teams"** .</span><span class="sxs-lookup"><span data-stu-id="0cccb-131">Check the **Personal tab** and **Group or Teams channel tab** options.</span></span> <span data-ttu-id="0cccb-132">(Скоро вы узнаете, зачем нужны оба типа вкладок.)</span><span class="sxs-lookup"><span data-stu-id="0cccb-132">(You'll soon learn why you need both types of tabs.)</span></span>
1. <span data-ttu-id="0cccb-133">В нижней части экрана нажмите кнопку **Готово** , чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="0cccb-133">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="0cccb-134">2. определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="0cccb-134">2. Identify relevant app project components</span></span>

<span data-ttu-id="0cccb-135">Многие конфигурации приложений и формирование шаблонов настраиваются автоматически при создании проекта с помощью набора инструментов Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-135">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="0cccb-136">Рассмотрим основные компоненты для создания вкладки "канал" и "Группа".</span><span class="sxs-lookup"><span data-stu-id="0cccb-136">Let's look at the main components for building a channel and group tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="0cccb-137">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="0cccb-137">App configurations</span></span>

<span data-ttu-id="0cccb-138">Вы можете просматривать и обновлять конфигурации приложений с помощью App Studio, которая включена в набор средств.</span><span class="sxs-lookup"><span data-stu-id="0cccb-138">You can view and update your app configurations using App Studio, which is included in the toolkit.</span></span>

<span data-ttu-id="0cccb-139">Во время установки набор инструментов изначально настроил два основных компонента вкладок "канал" и "Группа":</span><span class="sxs-lookup"><span data-stu-id="0cccb-139">During setup, the toolkit initially configured two essential components of channel and group tabs:</span></span>

* <span data-ttu-id="0cccb-140">**Страница "Конфигурация** ": диалоговое окно для добавления вкладки в канал или чат.</span><span class="sxs-lookup"><span data-stu-id="0cccb-140">**Configuration page** : The dialog for adding a tab to a channel or chat.</span></span> <span data-ttu-id="0cccb-141">(В App Studio можно найти эту страницу, перейдя на **вкладки > вкладке Группа** ).</span><span class="sxs-lookup"><span data-stu-id="0cccb-141">(In App Studio, you can find this page by going to **Tabs > Team tab**.)</span></span>
* <span data-ttu-id="0cccb-142">**Страница содержимого** : где отображается основное содержимое.</span><span class="sxs-lookup"><span data-stu-id="0cccb-142">**Content page** : Where you display your primary content.</span></span> <span data-ttu-id="0cccb-143">(В App Studio можно найти эту страницу, перейдя на **вкладки > добавить личную вкладку** ).</span><span class="sxs-lookup"><span data-stu-id="0cccb-143">(In App Studio, you can find this page by going to **Tabs > Add a personal tab**.)</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="0cccb-144">Формирование шаблонов приложений</span><span class="sxs-lookup"><span data-stu-id="0cccb-144">App scaffolding</span></span>

<span data-ttu-id="0cccb-145">Формирование шаблонов приложений предоставляет компоненты для отображения вкладки "личные сведения" в Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-145">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="0cccb-146">Существует множество способов, с которыми вы можете работать, но теперь вам нужно сосредоточиться на следующих задачах:</span><span class="sxs-lookup"><span data-stu-id="0cccb-146">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="0cccb-147">Два файла, расположенные в `src/components` каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="0cccb-147">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="0cccb-148">`Tab.js` для отображения страницы содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="0cccb-148">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="0cccb-149">`TabConfig.js` для отображения страницы конфигурации вкладки.</span><span class="sxs-lookup"><span data-stu-id="0cccb-149">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="0cccb-150">Клиентский пакет SDK Microsoft Teams JavaScript, который предварительно загружен в интерфейсных компонентах проекта.</span><span class="sxs-lookup"><span data-stu-id="0cccb-150">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="0cccb-151">3. Настройка страницы контента вкладки</span><span class="sxs-lookup"><span data-stu-id="0cccb-151">3. Customize your tab content page</span></span>

<span data-ttu-id="0cccb-152">Скопируйте и обновите следующий фрагмент кода, используя сведения, которые относятся к вашей организации, или, в целях простоты, используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="0cccb-152">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="0cccb-153">Перейдите в `src/components` каталог и откройте его `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="0cccb-153">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="0cccb-154">Нахождение `render()` функции и вставка содержимого внутри `return()` (как показано на рисунке).</span><span class="sxs-lookup"><span data-stu-id="0cccb-154">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="0cccb-155">Добавьте следующее правило `App.css` (также размещено в `src/components` ), чтобы ссылки электронной почты легче читались независимо от того, какая тема используется.</span><span class="sxs-lookup"><span data-stu-id="0cccb-155">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="0cccb-156">4. Настройка страницы настройки вкладки</span><span class="sxs-lookup"><span data-stu-id="0cccb-156">4. Customize your tab configuration page</span></span>

<span data-ttu-id="0cccb-157">У каждой вкладки в канале или чата есть страница конфигурации, в которой по крайней мере один вариант установки, отображаемый при добавлении приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="0cccb-157">Every tab in a channel or chat has a configuration page, a dialog with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="0cccb-158">По умолчанию на странице конфигурации запрашиваются пользователи, хотят ли они уведомлять канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="0cccb-158">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="0cccb-159">Добавление настраиваемого контента на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="0cccb-159">Add some custom content to your configuration page.</span></span> <span data-ttu-id="0cccb-160">Перейдите в `src/components` каталог проекта, откройте `TabConfig.js` и обновите содержимое заполнителя в `return()` (как показано в следующем примере).</span><span class="sxs-lookup"><span data-stu-id="0cccb-160">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="0cccb-161">Как минимум, укажите некоторые краткие сведения о приложении на этой странице, так как это может быть первый раз, когда пользователи узнают об этом.</span><span class="sxs-lookup"><span data-stu-id="0cccb-161">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="0cccb-162">Кроме того, можно включить настраиваемые параметры конфигурации или [Рабочий процесс проверки подлинности](../tabs/how-to/authentication/auth-aad-sso.md), который распространен на страницах настройки вкладок.</span><span class="sxs-lookup"><span data-stu-id="0cccb-162">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="0cccb-163">5. Введите предлагаемое имя вкладки.</span><span class="sxs-lookup"><span data-stu-id="0cccb-163">5. Provide a suggested tab name</span></span>

<span data-ttu-id="0cccb-164">При добавлении вкладки "канал" или "Группа" по умолчанию отображается имя приложения (например, **First-App** ).</span><span class="sxs-lookup"><span data-stu-id="0cccb-164">When you add a channel or group tab, by default the app name displays (for example, **first-app** ).</span></span>

<span data-ttu-id="0cccb-165">Это может быть разумно в зависимости от того, что вы назначите для вашего приложения, но вы можете указать имя, которое лучше в контексте совместной работы группы (например, " **Контакты группы** ").</span><span class="sxs-lookup"><span data-stu-id="0cccb-165">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts** ).</span></span>

<span data-ttu-id="0cccb-166">В `TabConfig.js` перейдите на страницу `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="0cccb-166">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span> <span data-ttu-id="0cccb-167">Добавьте `suggestedDisplayName` свойство с именем вкладки, которое будет отображаться по умолчанию (как показано).</span><span class="sxs-lookup"><span data-stu-id="0cccb-167">Add the `suggestedDisplayName` property with the tab name you want to display by default (as shown).</span></span> <span data-ttu-id="0cccb-168">Используйте предоставленное имя или создайте собственное.</span><span class="sxs-lookup"><span data-stu-id="0cccb-168">Use the provided name or create your own.</span></span> <span data-ttu-id="0cccb-169">(По умолчанию при желании пользователи могут изменить имя.)</span><span class="sxs-lookup"><span data-stu-id="0cccb-169">(By default, users to change the name if they want.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="0cccb-170">6. Построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="0cccb-170">6. Build and run your app</span></span>

<span data-ttu-id="0cccb-171">В течение этого времени вы создадите и запустите свое приложение локально.</span><span class="sxs-lookup"><span data-stu-id="0cccb-171">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="0cccb-172">(Эти сведения также доступны в наборе инструментов `README` .)</span><span class="sxs-lookup"><span data-stu-id="0cccb-172">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="0cccb-173">В терминале перейдите к корневому каталогу проекта приложения и запустите его `npm install` .</span><span class="sxs-lookup"><span data-stu-id="0cccb-173">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="0cccb-174">Выполните команду `npm start` .</span><span class="sxs-lookup"><span data-stu-id="0cccb-174">Run `npm start`.</span></span>

<span data-ttu-id="0cccb-175">По завершении **компиляции успешно выполняется.**</span><span class="sxs-lookup"><span data-stu-id="0cccb-175">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="0cccb-176">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="0cccb-176">message in the terminal.</span></span> <span data-ttu-id="0cccb-177">Ваше приложение запущено `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="0cccb-177">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="0cccb-178">7. Загрузка неопубликованных ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="0cccb-178">7. Sideload your app in Teams</span></span>

<span data-ttu-id="0cccb-179">Ваше приложение готово к тестированию в Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-179">Your app is ready to test in Teams.</span></span> <span data-ttu-id="0cccb-180">Для этого необходимо иметь учетную запись, позволяющую выполнять загрузку неопубликованных приложений.</span><span class="sxs-lookup"><span data-stu-id="0cccb-180">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="0cccb-181">(Если вы не знаете этого, Узнайте о том, как получить [учетную запись разработки Teams](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span><span class="sxs-lookup"><span data-stu-id="0cccb-181">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="0cccb-182">В Visual Studio Code нажмите клавишу **F5** , чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-182">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="0cccb-183">Чтобы отобразить содержимое приложения в Teams, укажите, что приложение работает ( `localhost` ) является надежным:</span><span class="sxs-lookup"><span data-stu-id="0cccb-183">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="0cccb-184">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которое открывалось после нажатия клавиши **F5**.</span><span class="sxs-lookup"><span data-stu-id="0cccb-184">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="0cccb-185">Перейдите к `https://localhost:3000/tab` странице и перейдите к ней.</span><span class="sxs-lookup"><span data-stu-id="0cccb-185">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="0cccb-186">Вернитесь в Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-186">Go back to Teams.</span></span> <span data-ttu-id="0cccb-187">В диалоговом окне выберите команду **Добавить в группу** или **Добавить в чат** , а затем выберите канал или чат, который вы можете использовать для тестирования.</span><span class="sxs-lookup"><span data-stu-id="0cccb-187">In the dialog, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="0cccb-188">Выберите **Настройка вкладки**. Страница конфигурации отображается в диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="0cccb-188">Select **Set up a tab**. The configuration page displays in a dialog.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана: страница настройки вкладки каналов.":::
1. <span data-ttu-id="0cccb-190">Нажмите кнопку **сохранить** , чтобы настроить вкладку. Отображается страница содержимое.</span><span class="sxs-lookup"><span data-stu-id="0cccb-190">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана: вкладка _OL_QUOTE_PLACEHOLDER_канал_OL_QUOTE_PLACEHOLDER_ со статическим представлением контента.":::

## <a name="well-done"></a><span data-ttu-id="0cccb-192">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="0cccb-192">Well done</span></span>

<span data-ttu-id="0cccb-193">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="0cccb-193">Congratulations!</span></span> <span data-ttu-id="0cccb-194">У вас есть приложение Teams с вкладкой для отображения содержимого в каналах и беседах.</span><span class="sxs-lookup"><span data-stu-id="0cccb-194">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="0cccb-195">Подробнее</span><span class="sxs-lookup"><span data-stu-id="0cccb-195">Learn more</span></span>

* <span data-ttu-id="0cccb-196">[Проверка подлинности пользователей вкладки с единым входом](../tabs/how-to/authentication/auth-aad-sso.md): Если вы хотите, чтобы авторизованные пользователи просматривали вкладку, настройте единый вход (SSO) через Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="0cccb-196">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="0cccb-197">[Внедрение контента из существующего веб-приложения или веб-страницы](../tabs/how-to/add-tab.md#tab-requirements): мы показали, как создать новое содержимое для вкладки личных данных, но вы также можете загрузить контент с внешнего URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="0cccb-197">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="0cccb-198">[Создайте простой интерфейс для вкладки](../tabs/design/tabs.md): Ознакомьтесь с рекомендациями по проектированию вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="0cccb-198">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="0cccb-199">[Создание вкладок для мобильных устройств](../tabs/design/tabs-mobile.md): Узнайте, как создавать вкладки для телефонов и планшетов.</span><span class="sxs-lookup"><span data-stu-id="0cccb-199">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="0cccb-200">Использование данных Teams с API Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="0cccb-200">Utilize Teams data with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="0cccb-201">Создание вкладки без набора инструментов</span><span class="sxs-lookup"><span data-stu-id="0cccb-201">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="0cccb-202">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="0cccb-202">Next lesson</span></span>

<span data-ttu-id="0cccb-203">Вы знаете, как создать вкладку для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="0cccb-203">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="0cccb-204">Хотите попробовать создать другой тип приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="0cccb-204">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0cccb-205">Создание бота</span><span class="sxs-lookup"><span data-stu-id="0cccb-205">Build a bot</span></span>](../build-your-first-app/build-bot.md)
