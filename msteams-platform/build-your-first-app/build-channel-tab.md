---
title: 'Начало работы : создание канала и вкладки "Группа"'
author: heath-hamilton
description: Быстро создайте канал Microsoft Teams и вкладку группы с помощью набор средств.
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 0692d28653063c2f886db9a03e7136379edde9c3
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911879"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="93797-103">Создание канала и вкладки группы для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="93797-103">Build a channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="93797-104">В этом руководстве вы создайте базовую вкладку канала *(также* называется вкладками *группы),* которая является полноэкранной страницей для канала команды или чата.</span><span class="sxs-lookup"><span data-stu-id="93797-104">In this tutorial, you'll build a basic *channel tab* (also known as a *group tab*), which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="93797-105">В отличие от личной вкладки, пользователи могут настраивать некоторые аспекты этой вкладки (например, переименовать вкладку, чтобы она была осмысленной для их канала).</span><span class="sxs-lookup"><span data-stu-id="93797-105">Unlike a personal tab, users can configure some aspects of this kind of tab (for example, rename the tab so it's meaningful to their channel).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="93797-106">Назначение</span><span class="sxs-lookup"><span data-stu-id="93797-106">Your assignment</span></span>

<span data-ttu-id="93797-107">Не так давно ваша организация создала приложение Teams, которое использует вкладку для отображения важных контактных данных (службы поддержки, отдела кадров и т. д.).</span><span class="sxs-lookup"><span data-stu-id="93797-107">Not long ago, your organization created a Teams app that uses a tab to display important contact information (help desk, HR, etc.).</span></span> <span data-ttu-id="93797-108">Однако так как это личная вкладка, каждый пользователь должен установить вкладку, чтобы увидеть ее, а уровень внедрения ниже ожидаемого.</span><span class="sxs-lookup"><span data-stu-id="93797-108">However, since it's a personal tab, each user must install the tab to see it and adoption is lower than expected.</span></span> <span data-ttu-id="93797-109">Другими словами, слишком много сотрудников по-прежнему не знают, как связаться со службой поддержки.</span><span class="sxs-lookup"><span data-stu-id="93797-109">In other words, too many workers still don't know how to reach the help desk.</span></span>

<span data-ttu-id="93797-110">Вы можете упростить поиск этих сведений, построив вкладку канала, что устралит трудности с требованием установки приложения всеми.</span><span class="sxs-lookup"><span data-stu-id="93797-110">You can make this information easier to find by building a channel tab, which will remove the burden of requiring everyone to install an app.</span></span> <span data-ttu-id="93797-111">Вместо этого один пользователь может добавить вкладку в канал или чат для всей группы.</span><span class="sxs-lookup"><span data-stu-id="93797-111">Instead, one user can add the tab in a channel or chat for the benefit of an entire group.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="93797-112">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="93797-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="93797-113">Создание проекта приложения с помощью microsoft Teams набор средств для Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="93797-113">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="93797-114">Определение некоторых конфигураций приложения и скаолдинга, релевантного для вкладок канала</span><span class="sxs-lookup"><span data-stu-id="93797-114">Identify some of the app configurations and scaffolding relevant to channel tabs</span></span>
> * <span data-ttu-id="93797-115">Создание содержимого вкладок</span><span class="sxs-lookup"><span data-stu-id="93797-115">Create tab content</span></span>
> * <span data-ttu-id="93797-116">Создание контента для страницы конфигурации вкладки</span><span class="sxs-lookup"><span data-stu-id="93797-116">Create content for a tab's configuration page</span></span>
> * <span data-ttu-id="93797-117">Предоставление предложенного имени вкладки</span><span class="sxs-lookup"><span data-stu-id="93797-117">Provide a suggested tab name</span></span>
> * <span data-ttu-id="93797-118">Локальное построение и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="93797-118">Build and run your app locally</span></span>
> * <span data-ttu-id="93797-119">Загрузка неогрузки приложения в Teams для тестирования</span><span class="sxs-lookup"><span data-stu-id="93797-119">Sideload your app in Teams for testing</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="93797-120">Прежде чем начать</span><span class="sxs-lookup"><span data-stu-id="93797-120">Before you begin</span></span>

<span data-ttu-id="93797-121">Если вы еще не знаете и не установили необходимые условия для [разработки Teams.](build-first-app-overview.md#get-prerequisites)</span><span class="sxs-lookup"><span data-stu-id="93797-121">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="93797-122">1. Создайте проект приложения</span><span class="sxs-lookup"><span data-stu-id="93797-122">1. Create your app project</span></span>

<span data-ttu-id="93797-123">Microsoft Teams набор средств помогает настроить приложение и настроить скаолдинг, релевантный для вкладок каналов и групп, включая базовую страницу конфигурации и страницу содержимого, на которых отображается страница "Hello, World!"</span><span class="sxs-lookup"><span data-stu-id="93797-123">The Microsoft Teams Toolkit helps configure your app and set up scaffolding relevant to channel and group tabs, including a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="93797-124">Сообщение.</span><span class="sxs-lookup"><span data-stu-id="93797-124">message.</span></span>

> [!TIP]
> <span data-ttu-id="93797-125">Если вы еще не создавали проект приложения Teams, возможно, вам будет полезно следовать этим инструкциям, чтобы подробнее объяснить проекты. [](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="93797-125">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. <span data-ttu-id="93797-127">При запросе во sign in with your Microsoft 365 development account.</span><span class="sxs-lookup"><span data-stu-id="93797-127">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="93797-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span><span class="sxs-lookup"><span data-stu-id="93797-128">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
1. <span data-ttu-id="93797-129">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="93797-129">Enter a name for your Teams app.</span></span> <span data-ttu-id="93797-130">(Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.) Выберите **вкладку "Группа" или "Канал Teams".**</span><span class="sxs-lookup"><span data-stu-id="93797-130">(This is the default name for your app and also the name of the app project directory on your local machine.) Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="93797-131">Выберите **"Готово"** в нижней части экрана, чтобы настроить проект.</span><span class="sxs-lookup"><span data-stu-id="93797-131">Select **Finish** at the bottom of the screen to configure your project.</span></span>  

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="93797-132">2. Определение соответствующих компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="93797-132">2. Identify relevant app project components</span></span>

<span data-ttu-id="93797-133">Большая часть конфигураций и скафаолдинга приложений автоматически заданная при создании проекта с помощью набора средств.</span><span class="sxs-lookup"><span data-stu-id="93797-133">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="93797-134">Рассмотрим основные компоненты для создания вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="93797-134">Let's look at the main components for building a channel tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="93797-135">Конфигурации приложений</span><span class="sxs-lookup"><span data-stu-id="93797-135">App configurations</span></span>

<span data-ttu-id="93797-136">В наборе средств перейдите в **App Studio,** чтобы просмотреть и обновить конфигурации приложений.</span><span class="sxs-lookup"><span data-stu-id="93797-136">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="93797-137">Скафаолдинг приложений</span><span class="sxs-lookup"><span data-stu-id="93797-137">App scaffolding</span></span>

<span data-ttu-id="93797-138">Скафолдинг приложения предоставляет компоненты для отображения вкладки канала в Teams.</span><span class="sxs-lookup"><span data-stu-id="93797-138">The app scaffolding provides the components for rendering your channel tab in Teams.</span></span> <span data-ttu-id="93797-139">Вы можете работать с большим количеством работы, но на данный момент вам нужно сосредоточиться только на следующих темах:</span><span class="sxs-lookup"><span data-stu-id="93797-139">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="93797-140">Два файла, расположенных в `src/components` каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="93797-140">Two files located in the `src/components` directory of your project:</span></span>
  * <span data-ttu-id="93797-141">`Tab.js` для отображения страницы содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="93797-141">`Tab.js` for rendering your tab's content page.</span></span>
  * <span data-ttu-id="93797-142">`TabConfig.js` для отображения страницы конфигурации вкладки.</span><span class="sxs-lookup"><span data-stu-id="93797-142">`TabConfig.js` for rendering your tab's configuration page.</span></span>
* <span data-ttu-id="93797-143">Клиентский SDK JavaScript для Microsoft Teams, который предварительно загружается в клиентские компоненты вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="93797-143">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="93797-144">3. Настройка страницы содержимого вкладок</span><span class="sxs-lookup"><span data-stu-id="93797-144">3. Customize your tab content page</span></span>

<span data-ttu-id="93797-145">Скопируйте и обновите следующий фрагмент, внося сведения, релевантные для вашей организации, или используйте код как есть.</span><span class="sxs-lookup"><span data-stu-id="93797-145">Copy and update the following snippet with information that's relevant to your organization or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="93797-146">Перейдите в `src/components` каталог и откройте `Tab.js` .</span><span class="sxs-lookup"><span data-stu-id="93797-146">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="93797-147">Найдите `render()` функцию и в paste your content inside `return()` (как показано).</span><span class="sxs-lookup"><span data-stu-id="93797-147">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="93797-148">Добавьте в (также расположено) следующее правило, чтобы упростить чтение ссылок электронной почты независимо от `App.css` `src/components` используемой темы.</span><span class="sxs-lookup"><span data-stu-id="93797-148">Add the following rule to `App.css` (also located in `src/components`) so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="93797-149">4. Настройка страницы конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="93797-149">4. Customize your tab configuration page</span></span>

<span data-ttu-id="93797-150">Каждая вкладка в канале или чате имеет страницу конфигурации, модальный режим по крайней мере с одним параметром настройки, который отображается при добавлении приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="93797-150">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="93797-151">Страница конфигурации по умолчанию спросит пользователей, хотят ли они уведомить канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="93797-151">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span>

<span data-ttu-id="93797-152">Добавьте пользовательское содержимое на страницу конфигурации.</span><span class="sxs-lookup"><span data-stu-id="93797-152">Add some custom content to your configuration page.</span></span> <span data-ttu-id="93797-153">Перейдите в каталог проекта, откройте и обновите содержимое-подстановщик внутри (как показано `src/components` `TabConfig.js` в следующем `return()` примере).</span><span class="sxs-lookup"><span data-stu-id="93797-153">Go to your project's `src/components` directory, open `TabConfig.js`, and update the placeholder content inside `return()` (as shown in the following example).</span></span>

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
> <span data-ttu-id="93797-154">Как минимум, у вас есть краткая информация о вашем приложении на этой странице, так как это может быть первый раз, когда пользователи об этом узнали.</span><span class="sxs-lookup"><span data-stu-id="93797-154">At minimum, provide some brief information about your app on this page since this may be the first time users are learning about it.</span></span> <span data-ttu-id="93797-155">Вы также можете включить настраиваемые параметры конфигурации или рабочий процесс проверки [подлинности,](../tabs/how-to/authentication/auth-aad-sso.md)который часто используется на страницах конфигурации вкладок.</span><span class="sxs-lookup"><span data-stu-id="93797-155">You also could include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-provide-a-suggested-tab-name"></a><span data-ttu-id="93797-156">5. В качестве рекомендуемой вкладки в качестве имени</span><span class="sxs-lookup"><span data-stu-id="93797-156">5. Provide a suggested tab name</span></span>

<span data-ttu-id="93797-157">При добавлении вкладки канала по умолчанию отображается имя приложения (например, **first-app).**</span><span class="sxs-lookup"><span data-stu-id="93797-157">When you add a channel tab, by default the app name displays (for example, **first-app**).</span></span>

<span data-ttu-id="93797-158">Это может быть нормально в зависимости от того, что вы звоните вашему приложению, но вы можете предоставить имя, которое имеет больше смысла в контексте совместной работы групп (например, **"Контакты группы").**</span><span class="sxs-lookup"><span data-stu-id="93797-158">This may be fine depending on what you call your app, but you may want to provide a name that makes more sense in the context of group collaboration (for example, **Team Contacts**).</span></span>

1. <span data-ttu-id="93797-159">In `TabConfig.js` , go to `microsoftTeams.settings.setSettings` .</span><span class="sxs-lookup"><span data-stu-id="93797-159">In `TabConfig.js`, go to `microsoftTeams.settings.setSettings`.</span></span>
2. <span data-ttu-id="93797-160">Добавьте свойство `suggestedDisplayName` с именем вкладки, которое вы хотите отобразить по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="93797-160">Add the `suggestedDisplayName` property with the tab name you want to display by default.</span></span> 
3. <span data-ttu-id="93797-161">Используйте имя, предоставленное в следующем примере, или введите свое имя.</span><span class="sxs-lookup"><span data-stu-id="93797-161">Use the name provided in the following example or type your name.</span></span> <span data-ttu-id="93797-162">(По умолчанию пользователи могут изменить имя.)</span><span class="sxs-lookup"><span data-stu-id="93797-162">(By default, users can change the name.)</span></span>

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="93797-163">6. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="93797-163">6. Build and run your app</span></span>

<span data-ttu-id="93797-164">В интересах времени вы будете создавать и запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="93797-164">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="93797-165">(Эти сведения также доступны в наборе `README` средств.)</span><span class="sxs-lookup"><span data-stu-id="93797-165">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="93797-166">В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.</span><span class="sxs-lookup"><span data-stu-id="93797-166">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="93797-167">Запустите `npm start` .</span><span class="sxs-lookup"><span data-stu-id="93797-167">Run `npm start`.</span></span>

<span data-ttu-id="93797-168">После завершения компилятор **успешно скомпилироваться!**</span><span class="sxs-lookup"><span data-stu-id="93797-168">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="93797-169">сообщение в терминале.</span><span class="sxs-lookup"><span data-stu-id="93797-169">message in the terminal.</span></span> <span data-ttu-id="93797-170">Ваше приложение работает в `https://localhost:3000` .</span><span class="sxs-lookup"><span data-stu-id="93797-170">Your app is running on `https://localhost:3000`.</span></span>

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="93797-171">7. Загрузка нео sideload приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="93797-171">7. Sideload your app in Teams</span></span>

<span data-ttu-id="93797-172">Ваше приложение готово для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="93797-172">Your app is ready to test in Teams.</span></span> <span data-ttu-id="93797-173">Для этого необходимо иметь учетную запись, которая разрешает загрузку нео том же приложения.</span><span class="sxs-lookup"><span data-stu-id="93797-173">To do this, you must have an account that allows app sideloading.</span></span> <span data-ttu-id="93797-174">(Если вы не уверены в этом, узнайте о получении учетной записи [разработки Teams.)](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)</span><span class="sxs-lookup"><span data-stu-id="93797-174">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>

1. <span data-ttu-id="93797-175">В Visual Studio Code нажмите клавишу **F5,** чтобы запустить веб-клиент Teams.</span><span class="sxs-lookup"><span data-stu-id="93797-175">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="93797-176">Чтобы отобразить содержимое приложения в Teams, укажите, где работает ваше приложение ( `localhost` ) является надежным:</span><span class="sxs-lookup"><span data-stu-id="93797-176">To display your app content in Teams, specify that where your app is running (`localhost`) is trustworthy:</span></span>
   1. <span data-ttu-id="93797-177">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая была открыта после нажатия **F5.**</span><span class="sxs-lookup"><span data-stu-id="93797-177">Open a new tab in the same browser window (Google Chrome by default) which opened after pressing **F5**.</span></span>
   1. <span data-ttu-id="93797-178">Перейдите `https://localhost:3000/tab` на страницу и перейдите на нее.</span><span class="sxs-lookup"><span data-stu-id="93797-178">Go to `https://localhost:3000/tab` and proceed to the page.</span></span>
1. <span data-ttu-id="93797-179">Вернуться в Teams.</span><span class="sxs-lookup"><span data-stu-id="93797-179">Go back to Teams.</span></span> <span data-ttu-id="93797-180">In the modal, select **Add to a team** or Add to a **chat** and locate a channel or chat you can use for testing.</span><span class="sxs-lookup"><span data-stu-id="93797-180">In the modal, select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing.</span></span>
1. <span data-ttu-id="93797-181">Выберите **"Настройка вкладки"**. Страница конфигурации отображается в модальной области.</span><span class="sxs-lookup"><span data-stu-id="93797-181">Select **Set up a tab**. The configuration page displays in a modal.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана: страница конфигурации вкладки канала.":::
1. <span data-ttu-id="93797-183">Выберите **"Сохранить",** чтобы настроить вкладку. Отображается страница содержимого.</span><span class="sxs-lookup"><span data-stu-id="93797-183">Select **Save** to configure the tab. The content page displays.</span></span><br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана: вкладка канала со статическим представлением содержимого.":::

## <a name="well-done"></a><span data-ttu-id="93797-185">Прекрасно</span><span class="sxs-lookup"><span data-stu-id="93797-185">Well done</span></span>

<span data-ttu-id="93797-186">Поздравляем!</span><span class="sxs-lookup"><span data-stu-id="93797-186">Congratulations!</span></span> <span data-ttu-id="93797-187">У вас есть приложение Teams с вкладками для отображения полезного содержимого в каналах и чатах.</span><span class="sxs-lookup"><span data-stu-id="93797-187">You have a Teams app with a tab for displaying useful content in channels and chats.</span></span>

## <a name="learn-more"></a><span data-ttu-id="93797-188">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="93797-188">Learn more</span></span>

* <span data-ttu-id="93797-189">Следуйте [нашим рекомендациям по проектированию](../tabs/design/tabs.md) и создавайте [шаблоны](../concepts/design/design-teams-app-ui-templates.md) пользовательского интерфейса, готовые к выпуску, чтобы удобо поработать.</span><span class="sxs-lookup"><span data-stu-id="93797-189">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="93797-190">В [этой теме рассматриваются вопросы, которые следует учитывать при](../tabs/design/tabs-mobile.md) мобильных устройствах для вкладок.</span><span class="sxs-lookup"><span data-stu-id="93797-190">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="93797-191">[Добавьте проверку подлинности SSO на вкладку.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="93797-191">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="93797-192">Использование данных Teams с [Microsoft Graph.](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="93797-192">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* [<span data-ttu-id="93797-193">Создание вкладки без наборов средств</span><span class="sxs-lookup"><span data-stu-id="93797-193">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="93797-194">Следующий урок</span><span class="sxs-lookup"><span data-stu-id="93797-194">Next lesson</span></span>

<span data-ttu-id="93797-195">Вы знаете, как создать вкладку для совместной работы.</span><span class="sxs-lookup"><span data-stu-id="93797-195">You know how to build a tab for collaboration.</span></span> <span data-ttu-id="93797-196">Хотите попробовать разных видов приложения Teams?</span><span class="sxs-lookup"><span data-stu-id="93797-196">Want to try building a different kind of Teams app?</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="93797-197">Создание бота</span><span class="sxs-lookup"><span data-stu-id="93797-197">Build a bot</span></span>](../build-your-first-app/build-bot.md)
