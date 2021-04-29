---
title: Начало работы — создание вкладки канала и группы
author: girliemac
description: Быстро создайте канал Microsoft Teams и вкладку группы с помощью microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068754"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a><span data-ttu-id="3a5f9-103">Создание вкладки первого канала и группы для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-103">Build your first channel and group tab for Microsoft Teams</span></span>

<span data-ttu-id="3a5f9-104">В этом руководстве рассказывается  о создании базовой вкладки канала, также известной как вкладка *группы,* которая является полноэкранной страницей для канала или чата группы.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-104">This tutorial teaches you to build a basic *channel tab* also known as a *group tab*, which is a full-screen page for a team channel or chat.</span></span> <span data-ttu-id="3a5f9-105">Вы также можете настроить некоторые аспекты вкладки такого типа, например, переименовать вкладку, чтобы она была значимой для канала, что невозможно сделать в личной вкладке.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-105">You can also configure some aspects of this kind of tab, for example, rename the tab so it's meaningful to their channel, which you cannot do in a Personal Tab.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="3a5f9-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="3a5f9-106">What you'll learn</span></span>

* <span data-ttu-id="3a5f9-107">Создайте проект приложения с помощью microsoft Teams набор средств для Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-107">Create an app project using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="3a5f9-108">Разберем конфигурации приложений и леса, соответствующие вкладке канала.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-108">Understand the app configurations and scaffolding relevant to channel tabs.</span></span>
* <span data-ttu-id="3a5f9-109">Создание конфигурации контента и вкладок.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-109">Create tab content and tab configuration.</span></span>
* <span data-ttu-id="3a5f9-110">Создайте и запустите приложение в командах для тестирования.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-110">Build and run your app in teams for testing.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a5f9-111">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="3a5f9-111">Prerequisites</span></span>

<span data-ttu-id="3a5f9-112">Убедитесь, что вы понимаете, как настроить и создать простое приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-112">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="3a5f9-113">Дополнительные сведения см. в [вашем первом приложении Microsoft Teams "Hello, World!".](../build-your-first-app/build-and-run.md)</span><span class="sxs-lookup"><span data-stu-id="3a5f9-113">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="3a5f9-114">1. Создание проекта приложения</span><span class="sxs-lookup"><span data-stu-id="3a5f9-114">1. Create your app project</span></span>

<span data-ttu-id="3a5f9-115">Программа Microsoft Teams набор средств настроить приложение и настроить леса, соответствующие вкладке канала и группы.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-115">The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs.</span></span> <span data-ttu-id="3a5f9-116">В нем также содержится базовая страница конфигурации и страница контента, на которую отображается "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="3a5f9-116">It also contains a basic configuration page and content page that displays a "Hello, World!"</span></span> <span data-ttu-id="3a5f9-117">Сообщение.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-117">message.</span></span>

<span data-ttu-id="3a5f9-118">**Создание проекта приложения**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-118">**To create your app project**</span></span>

1. Перейдите Visual Studio код и выберите **Microsoft Teams** в левой :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: панели действий.
1. <span data-ttu-id="3a5f9-120">Во входе в учетную запись разработки Microsoft 365 при запросе на это.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-120">Sign in with your Microsoft 365 development account when prompted to do so.</span></span>
1. <span data-ttu-id="3a5f9-121">На экране **Выберите проект** выберите **JS** (JavaScript) в **приложении Channel и group.**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-121">On the **Select project** screen, select **JS** (JavaScript) under **Channel and group app**.</span></span>
1. <span data-ttu-id="3a5f9-122">Введите имя приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-122">Enter a name for your Teams app.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3a5f9-123">Это имя по умолчанию для вашего приложения, а также имя каталога проектов приложений на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-123">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>

1. <span data-ttu-id="3a5f9-124">Выберите **вкладку канала Group или Teams.**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-124">Select **Group or Teams channel tab**.</span></span>
1. <span data-ttu-id="3a5f9-125">Выберите **Готово** в нижней части экрана, чтобы настроить проект и сохранить проект на локальной машине.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-125">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="3a5f9-126">2. Понимание компонентов проекта приложения</span><span class="sxs-lookup"><span data-stu-id="3a5f9-126">2. Understand your app project components</span></span>

<span data-ttu-id="3a5f9-127">Большая часть конфигураций приложений и строительных лесов создается автоматически при создании проекта с помощью набора инструментов.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-127">Much of the app configurations and scaffolding are set up automatically when you create your project with the toolkit.</span></span> <span data-ttu-id="3a5f9-128">Рассмотрим основные компоненты для создания вкладки канала.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-128">Let's look at the main components for building a channel tab.</span></span>

* <span data-ttu-id="3a5f9-129">**Конфигурации приложений:** Откройте **App Studio** в наборе инструментов для просмотра и обновления конфигураций приложений.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-129">**App configurations**: Open **App Studio** in the toolkit to view and update your app configurations.</span></span>
* <span data-ttu-id="3a5f9-130">**Строительные леса** приложений. Строительные леса приложений предоставляют компоненты, необходимые для отрисовки вкладки канала в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-130">**App scaffolding**: The app scaffolding provides the components needed for rendering your channel tab in Teams.</span></span> <span data-ttu-id="3a5f9-131">Тем не менее, вы можете много работать, но теперь давайте сосредоточимся на следующем:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-131">There's a lot you can work with, however, for now let's focus on the following:</span></span>
  * <span data-ttu-id="3a5f9-132">Файлы, расположенные в `src/components` каталоге проекта:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-132">The files located in the `src/components` directory of your project:</span></span>
    * <span data-ttu-id="3a5f9-133">`Tab.js` для отрисовки страницы контента вкладки.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-133">`Tab.js` for rendering your tab's content page.</span></span>
    * <span data-ttu-id="3a5f9-134">`TabConfig.js` для отрисовки страницы конфигурации вкладки.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-134">`TabConfig.js` for rendering your tab's configuration page.</span></span>
  * <span data-ttu-id="3a5f9-135">Клиент Microsoft Teams JavaScript SDK, который поставляется с предварительной загрузкой в передние компоненты проекта.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-135">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="3-customize-your-tab-content-page"></a><span data-ttu-id="3a5f9-136">3. Настройка страницы контента вкладок</span><span class="sxs-lookup"><span data-stu-id="3a5f9-136">3. Customize your tab content page</span></span>

1. <span data-ttu-id="3a5f9-137">Скопируйте и измените следующий пример кода с помощью сведений, соответствующих организации.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-137">Copy and modify the following code sample with information that's relevant to your organization.</span></span> <span data-ttu-id="3a5f9-138">Фрагмент можно также использовать так, как это:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-138">You can also use the snippet as it is:</span></span>
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
1. <span data-ttu-id="3a5f9-139">Перейдите в `src/components` каталог и откройте `Tab.js` файл.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-139">Go to the `src/components` directory and open the `Tab.js` file.</span></span> <span data-ttu-id="3a5f9-140">Найдите `render()` функцию и вклейте код `return()` внутри, как показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-140">Locate the `render()` function and paste your code inside `return()` as shown in the following example:</span></span>
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
1. <span data-ttu-id="3a5f9-141">Перейдите в каталог и обнови файл следующим кодом, чтобы упростить чтение ссылок электронной почты в любой `src/components` `App.css` используемой теме:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-141">Go to the `src/components` directory and update the `App.css` file with the following code to make the email links easier to read in any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a><span data-ttu-id="3a5f9-142">4. Настройка страницы конфигурации вкладок</span><span class="sxs-lookup"><span data-stu-id="3a5f9-142">4. Customize your tab configuration page</span></span>

<span data-ttu-id="3a5f9-143">Каждая вкладка в канале или чате имеет страницу конфигурации, модал с по крайней мере одним параметром настройки, отображаемой при добавлении приложения пользователями.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-143">Every tab in a channel or chat has a configuration page, a modal with at least one setup option that displays when users add your app.</span></span> <span data-ttu-id="3a5f9-144">Страница конфигурации по умолчанию спрашивает пользователей, хотят ли они уведомить канал или чат при установке вкладки.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-144">The configuration page by default asks users if they want to notify the channel or chat when the tab is installed.</span></span> <span data-ttu-id="3a5f9-145">Вы можете настроить страницу конфигурации, добавив настраиваемый контент.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-145">You can customize the configuration page by adding custom content.</span></span>

<span data-ttu-id="3a5f9-146">Чтобы добавить настраиваемый контент, откройте файл из каталога и обновив содержимое держателя внутри, как показано `TabConfig.js` `src/components` в следующем `return()` примере:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-146">To add custom content, open `TabConfig.js` file from the `src/components` directory and update the placeholder content inside `return()` as shown in the following example:</span></span>

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
> <span data-ttu-id="3a5f9-147">Дайте краткую информацию о вашем приложении на этой странице, так как это будет первый раз, когда пользователи читают об этом.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-147">Give a brief information about your app on this page since this would be the first time users are reading about it.</span></span> <span data-ttu-id="3a5f9-148">Вы также можете включить настраиваемые параметры конфигурации или рабочий процесс проверки [подлинности,](../tabs/how-to/authentication/auth-aad-sso.md)который распространен на страницах конфигурации вкладок.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-148">You can also include custom configuration options or an [authentication workflow](../tabs/how-to/authentication/auth-aad-sso.md), which is common on tab configuration pages.</span></span>

## <a name="5-customize-your-tab-name"></a><span data-ttu-id="3a5f9-149">5. Настройка имени вкладки</span><span class="sxs-lookup"><span data-stu-id="3a5f9-149">5. Customize your tab name</span></span>

<span data-ttu-id="3a5f9-150">При добавлении вкладки канала имя приложения отображает по умолчанию, например, **первое приложение.**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-150">When you add a channel tab, the app name displays by default, for example, **first-app**.</span></span> <span data-ttu-id="3a5f9-151">Вы также можете предоставить имя, которое имеет больше смысла в контексте групповой совместной работы, например, **Team Contacts:**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-151">You can also provide a name that makes more sense in the context of group collaboration, for example, **Team Contacts**:</span></span>

1. <span data-ttu-id="3a5f9-152">Перейдите в `src/components` каталог и откройте `TabConfig.js` файл.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-152">Go to the `src/components` directory and open the `TabConfig.js` file.</span></span>
1. <span data-ttu-id="3a5f9-153">Добавьте свойство с именем вкладки, которое необходимо отобразить по умолчанию, как `suggestedDisplayName` `microsoftTeams.settings.setSettings` показано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-153">Add the `suggestedDisplayName` property with the tab name you want to display by default under `microsoftTeams.settings.setSettings` as shown in the following example:</span></span>

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a><span data-ttu-id="3a5f9-154">6. Сборка и запуск приложения</span><span class="sxs-lookup"><span data-stu-id="3a5f9-154">6. Build and run your app</span></span>

<span data-ttu-id="3a5f9-155">Этот учебник учит создавать и запускать приложение локально.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-155">This tutorial teaches you to build and run your app locally.</span></span> 

1. <span data-ttu-id="3a5f9-156">Перейдите в корневой каталог проекта приложения в Терминале.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-156">Go to the root directory of your app project in Terminal.</span></span>
1. <span data-ttu-id="3a5f9-157">Запуск `npm install` .</span><span class="sxs-lookup"><span data-stu-id="3a5f9-157">Run `npm install`.</span></span>
1. <span data-ttu-id="3a5f9-158">Запуск `npm start` .</span><span class="sxs-lookup"><span data-stu-id="3a5f9-158">Run `npm start`.</span></span>

<span data-ttu-id="3a5f9-159">Эти сведения также представлены в `README` разделе набор инструментов.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-159">This information is also present in the `README` section of the toolkit.</span></span>
<span data-ttu-id="3a5f9-160">Ваше приложение работает после `https://localhost:3000` **успешного компилировать!**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-160">Your app is running on `https://localhost:3000` after the **Compiled successfully!**</span></span> <span data-ttu-id="3a5f9-161">сообщение отображается в терминале.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-161">message appears in the terminal.</span></span> 

## <a name="7-sideload-your-app-in-teams"></a><span data-ttu-id="3a5f9-162">7. Боковое загрузка приложения в Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-162">7. Sideload your app in Teams</span></span>

<span data-ttu-id="3a5f9-163">Ваше приложение готово для тестирования в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-163">Your app is ready to test in Teams.</span></span> <span data-ttu-id="3a5f9-164">Для этого необходимо иметь учетную запись, позволяющую загрузку приложений.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-164">To do this, you must have an account that allows app sideloading.</span></span> 

1. <span data-ttu-id="3a5f9-165">Откройте веб-клиент Teams в Visual Studio коде с **ключом F5.**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-165">Open a Teams web client in Visual Studio Code with the **F5** key.</span></span>
1. <span data-ttu-id="3a5f9-166">Добавление () в качестве надежного, следуя этим шагам, чтобы включить отображение контента приложения `localhost` в Teams:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-166">Add (`localhost`) as trustworthy by following these steps to enable your app content to display in Teams:</span></span>

   1. <span data-ttu-id="3a5f9-167">Откройте новую вкладку в том же окне браузера (Google Chrome по умолчанию), которая открылась с помощью **клавиши F5.**</span><span class="sxs-lookup"><span data-stu-id="3a5f9-167">Open a new tab in the same browser window (Google Chrome by default) which opened with the **F5** key.</span></span>
   1. <span data-ttu-id="3a5f9-168">Откройте `https://localhost:3000/tab` и переехав на страницу.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-168">Open `https://localhost:3000/tab` and proceed to the page.</span></span>

1. <span data-ttu-id="3a5f9-169">Выберите **Добавить в команду или** **добавить** в чат и найти канал или чат, который можно использовать для тестирования из модуля в Teams.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-169">Select **Add to a team** or **Add to a chat** and locate a channel or chat you can use for testing from the modal in Teams.</span></span>
1. <span data-ttu-id="3a5f9-170">Выберите **Настройка вкладки**. Страница конфигурации отображается в модале.</span><span class="sxs-lookup"><span data-stu-id="3a5f9-170">Select **Set up a tab**. The configuration page displays in a modal.</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="Снимок экрана страницы конфигурации вкладок канала.":::

1. <span data-ttu-id="3a5f9-172">Выберите **Сохранить,** чтобы настроить вкладку. Появится следующая страница контента:</span><span class="sxs-lookup"><span data-stu-id="3a5f9-172">Select **Save** to configure the tab. The following content page appears:</span></span>

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="Снимок экрана вкладки канала со статическим представлением контента.":::

## <a name="see-also"></a><span data-ttu-id="3a5f9-174">См. также</span><span class="sxs-lookup"><span data-stu-id="3a5f9-174">See also</span></span>

* [<span data-ttu-id="3a5f9-175">Создание и запуск первого приложения Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-175">Build and run your first Microsoft Teams app</span></span>](../build-your-first-app/build-and-run.md) 
* [<span data-ttu-id="3a5f9-176">Клиентский SDK JavaScript для Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-176">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="3a5f9-177">Разработка вкладки для настольных и веб-страниц Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-177">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="3a5f9-178">Разработка приложения Microsoft Teams с помощью шаблонов пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="3a5f9-178">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="3a5f9-179">Вкладки на мобильных устройствах</span><span class="sxs-lookup"><span data-stu-id="3a5f9-179">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="3a5f9-180">Поддержка единого входного знака (SSO) для вкладок</span><span class="sxs-lookup"><span data-stu-id="3a5f9-180">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="3a5f9-181">Обзор API Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-181">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="3a5f9-182">Создание настраиваемой личной вкладки с Node.js и генератором Yeoman для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="3a5f9-182">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="3a5f9-183">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="3a5f9-183">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a5f9-184">Создание бота</span><span class="sxs-lookup"><span data-stu-id="3a5f9-184">Build a bot</span></span>](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a5f9-185">Создание расширения для сообщений</span><span class="sxs-lookup"><span data-stu-id="3a5f9-185">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)