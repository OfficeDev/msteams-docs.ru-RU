---
title: Начало работы - Создание канала и вкладки группы
author: girliemac
description: Быстро создайте Microsoft Teams канал и групповую вкладку с помощью Microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: ff9cfbfb7d099db52966f119add4ce8729929aa1
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566070"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="6a0a4-103">Создайте свой первый канал и групповую вкладку для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6a0a4-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="6a0a4-104">Этот учебник научит вас строить основные вкладки *канала также* известный как группа *вкладка*, которая является полноэкранной страницей для командного канала или чата.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="6a0a4-105">Вы также можете настроить некоторые аспекты такого рода вкладок, например, переименовать вкладку, чтобы она была значимой для их канала, что вы не можете сделать в личной вкладке.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="6a0a4-106">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="6a0a4-106">What you'll learn</span></span>

* <span data-ttu-id="6a0a4-107">Создайте проект приложения, используя Microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="6a0a4-108">Поймите конфигурации приложений и леса, относящиеся к вкладок канала.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="6a0a4-109">Создание содержимого вкладок и конфигурации вкладок.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="6a0a4-110">Создавайте и запускайте приложение в командах для тестирования.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a0a4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="6a0a4-111">Prerequisites</span></span>

<span data-ttu-id="6a0a4-112">Убедитесь, что вы понимаете, как настроить и построить простой Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="6a0a4-113">Для получения дополнительной [информации, см Microsoft Teams.](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="6a0a4-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="6a0a4-114">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="6a0a4-114">1. Create your app project</span></span>

<span data-ttu-id="6a0a4-115">Проект Microsoft Teams набор средств вам настроить приложение и настроить леса, имеющие отношение к вкладок канала и группы.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="6a0a4-116">Он также содержит основную страницу конфигурации и содержание страницы, которая отображает "Здравствуйте, мир!"</span><span class="sxs-lookup"><span data-stu-id="6a0a4-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="6a0a4-117">Сообщение.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-117">message.</span></span>

<span data-ttu-id="6a0a4-118">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-118">**To create your app project**</span></span>

1. Перейдите Visual Studio Code и **выберите Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: на левой стойке активности.
1. <span data-ttu-id="6a0a4-120">Вопишитесь в свой аккаунт Microsoft 365 разработки, когда вам будет предложено это сделать.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="6a0a4-121">На **экране проекта Select** выберите **JS** (JavaScript) под **приложением Channel и group.**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="6a0a4-122">Введите имя для вашего Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="6a0a4-123">Это имя по умолчанию для вашего приложения, а также название каталога проекта приложения на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="6a0a4-124">Выберите **вкладку Teams канала.**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="6a0a4-125">**Выберите** отделку в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="6a0a4-126">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="6a0a4-126">2. Understand your app project components</span></span>

<span data-ttu-id="6a0a4-127">Большая часть конфигураций приложений и строительных лесов настроены автоматически при создании проекта с помощью инструментария.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="6a0a4-128">Рассмотрим основные компоненты для построения вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="6a0a4-129">**Конфигурации приложений**: Open **App Studio** в наборе инструментов для просмотра и обновления конфигураций приложений.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="6a0a4-130">**App леса :** приложение леса предоставляет компоненты, необходимые для рендеринга вашего канала вкладку в Teams.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="6a0a4-131">Там очень много вы можете работать, однако, на данный момент давайте сосредоточимся на следующем:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="6a0a4-132">Файлы, на которые `src/components` находится каталог вашего проекта:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="6a0a4-133">`Tab.js` для рендеринга страницы содержимого вкладки.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="6a0a4-134">`TabConfig.js` для визуализации страницы конфигурации вкладки.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="6a0a4-135">Microsoft Teams JavaScript клиент SDK, который поставляется предварительно загружены в передней части компонентов вашего проекта.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="6a0a4-136">3. Настройка страницы содержимого вкладок</span><span class="sxs-lookup"><span data-stu-id="6a0a4-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="6a0a4-137">Копировать и изменять следующий образец кода с информацией, относящейся к вашей организации.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="6a0a4-138">Вы также можете использовать фрагмент, как он есть:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-138">You can also use the snippet as it is:</span></span>
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
    
1. <span data-ttu-id="6a0a4-139">Зайдите в `src/components` каталог и откройте `Tab.js` файл.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="6a0a4-140">Найдите `render()` функцию и вставьте код `return()` внутрь, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
    
1. <span data-ttu-id="6a0a4-141">Перейдите в `src/components` каталог и обновите файл со следующим кодом, чтобы сделать `App.css` ссылки электронной почты легче читать в любой теме, которая используется:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="6a0a4-142">4. Настройка страницы конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="6a0a4-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="6a0a4-143">Каждая вкладка в канале или чате имеет страницу конфигурации, модал с по крайней мере одним вариантом настройки, который отображается при использовании приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="6a0a4-144">Страница конфигурации по умолчанию запрашивает пользователей, хотят ли они уведомить канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="6a0a4-145">Вы можете настроить страницу конфигурации, добавив пользовательский контент.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="6a0a4-146">Чтобы добавить пользовательский контент, откройте `TabConfig.js` файл из `src/components` каталога и обновив содержимое заполнителя `return()` внутри, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="6a0a4-147">Дайте краткую информацию о вашем приложении на этой странице, так как это будет первый раз, когда пользователи читают об этом.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="6a0a4-148">Вы также можете включить пользовательские параметры конфигурации или рабочий [процесс проверки подлинности,](../tabs/how-to/authentication/auth-aad-sso.md)который является общим на страницах конфигурации вкладок.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="6a0a4-149">5. Настроили имя вкладки</span><span class="sxs-lookup"><span data-stu-id="6a0a4-149">5. Customize your tab name</span></span>

<span data-ttu-id="6a0a4-150">При добавление вкладки канала имя приложения отображается по умолчанию, например, **первым приложением.**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="6a0a4-151">Вы также можете узнать имя, которое имеет больше смысла в контексте совместной работы группы, например, **Контакты группы:**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="6a0a4-152">Зайдите в `src/components` каталог и откройте `TabConfig.js` файл.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="6a0a4-153">Добавьте `suggestedDisplayName` свойство с именем вкладки, которое вы хотите отобразить по умолчанию, `microsoftTeams.settings.setSettings` как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

    ```JavaScript
        microsoftTeams.settings.setSettings({
        "contentUrl": "https://localhost:3000/tab",
        "suggestedDisplayName": "Team Contacts"
      });
      ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="6a0a4-154">6. Создание и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="6a0a4-154">6. Build and run your app</span></span>

<span data-ttu-id="6a0a4-155">Этот учебник научит вас создавать и запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="6a0a4-156">Перейдите в корневой каталог проекта приложения в Терминале.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="6a0a4-157">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="6a0a4-157">Run `npm install`.</span></span>
1. <span data-ttu-id="6a0a4-158">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="6a0a4-158">Run `npm start`.</span></span>

<span data-ttu-id="6a0a4-159">Эта информация также представлена `README` в разделе инструментария.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="6a0a4-160">Ваше приложение работает после `https://localhost:3000` **успешного составления!**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="6a0a4-161">сообщение отображается в терминале.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="6a0a4-162">7. Sideload ваше приложение в Teams</span><span class="sxs-lookup"><span data-stu-id="6a0a4-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="6a0a4-163">Ваше приложение готово к тестированию в Teams.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="6a0a4-164">Для этого необходимо иметь учетную запись, которая позволяет перезагрузить приложение.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="6a0a4-165">Откройте Teams веб-клиента Visual Studio Code с помощью **ключа F5.**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="6a0a4-166">Добавить `localhost` () в качестве надежного, следуя этим шагам, чтобы содержимое приложения отображаться в Teams:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="6a0a4-167">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась с **ключом F5.**</span><span class="sxs-lookup"><span data-stu-id="6a0a4-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="6a0a4-168">Откройте `https://localhost:3000/tab` и перейти к странице.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="6a0a4-169">Выберите **Добавить в команду** или Добавить в чат **и** найти канал или чат можно использовать для тестирования от модала в Teams.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="6a0a4-170">Выберите **настройку вкладки**. Страница конфигурации отображается в моде.</span><span class="sxs-lookup"><span data-stu-id="6a0a4-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Скриншот страницы конфигурации вкладки канала.":::

1. <span data-ttu-id="6a0a4-172">Выберите **Сохранить** для настройки вкладки. Отображается следующая страница содержимого:</span><span class="sxs-lookup"><span data-stu-id="6a0a4-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Скриншот вкладки канала со статическим представлением содержимого.":::

## <a name="see-also"></a><span data-ttu-id="6a0a4-174">См. также</span><span class="sxs-lookup"><span data-stu-id="6a0a4-174">See also</span></span>

* [<span data-ttu-id="6a0a4-175">Создание и запуск первого Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="6a0a4-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="6a0a4-176">Клиентский SDK JavaScript для Teams</span><span class="sxs-lookup"><span data-stu-id="6a0a4-176">Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="6a0a4-177">Проектирование вкладки для Microsoft Teams и веб-страниц</span><span class="sxs-lookup"><span data-stu-id="6a0a4-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="6a0a4-178">Проектирование приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="6a0a4-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="6a0a4-179">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="6a0a4-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="6a0a4-180">Поддержка вкладок с одним ва-пом (SSO)</span><span class="sxs-lookup"><span data-stu-id="6a0a4-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="6a0a4-181">Обзор API Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6a0a4-181">Microsoft Teams API overview</span></span>](/graph/teams-concept-overview)
* [<span data-ttu-id="6a0a4-182">Создайте пользовательскую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6a0a4-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="6a0a4-183">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="6a0a4-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a0a4-184">Создание бота</span><span class="sxs-lookup"><span data-stu-id="6a0a4-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a0a4-185">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="6a0a4-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
