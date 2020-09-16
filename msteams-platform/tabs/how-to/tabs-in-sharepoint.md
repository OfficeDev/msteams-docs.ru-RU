---
title: Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx
author: laujan
description: Сведения о том, как развернуть существующую вкладку Teams в SharePoint в качестве веб-части SharePoint Framework.
keywords: разработка SharePoint Framework для вкладок Teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2bdc7ab578be485eee33020b3b0c1a4099fd8ade
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818943"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="034de-104">Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx</span><span class="sxs-lookup"><span data-stu-id="034de-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

> [!IMPORTANT]
> <span data-ttu-id="034de-105">Эта функция в настоящее время находится на этапе тестирования и может быть изменена.</span><span class="sxs-lookup"><span data-stu-id="034de-105">This feature is currently in preview and is subject to change.</span></span> <span data-ttu-id="034de-106">Он не поддерживается для использования в рабочих средах.</span><span class="sxs-lookup"><span data-stu-id="034de-106">It is not supported for use in production environments.</span></span> <span data-ttu-id="034de-107">Отзывы и предложения по этой функции отправляйте с помощью [списка проблем в документации разработчиков SharePoint](https://github.com/SharePoint/sp-dev-docs/issues).</span><span class="sxs-lookup"><span data-stu-id="034de-107">Your feedback and input around this capability is welcome using the [SharePoint Dev Docs issue list](https://github.com/SharePoint/sp-dev-docs/issues).</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="034de-108">Расширенная интеграция между Teams и SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-108">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="034de-109">С помощью выпуска Teams и SharePoint Framework в ноябре.</span><span class="sxs-lookup"><span data-stu-id="034de-109">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="034de-110">1,7 у разработчиков есть два мощных возможности:</span><span class="sxs-lookup"><span data-stu-id="034de-110">1.7, developers have two powerful capabilities:</span></span>

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="034de-111">Вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-111">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="034de-112">Создайте полнофункциональные приложения в SharePoint, переведя приложение Teams в SharePoint (Эта статья).</span><span class="sxs-lookup"><span data-stu-id="034de-112">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3><span data-ttu-id="034de-113">SharePoint Framework в Teams</span><span class="sxs-lookup"><span data-stu-id="034de-113">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="034de-114">Перенесите веб-части SharePoint в Teams и позвольте SharePoint управлять размещением.</span><span class="sxs-lookup"><span data-stu-id="034de-114">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="034de-115">Вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-115">Teams tabs in SharePoint</span></span>

<span data-ttu-id="034de-116">В SharePoint Framework v. 1.7 мы теперь поддерживаем возможность разработчикам принимать свои вкладки Teams и размещать их в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="034de-116">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="034de-117">Как вкладки, размещенные в SharePoint, получают похожий вид "полная страница", предоставляя все функции вкладок Teams, сохраняя контекст и знакомство с сайтом SharePoint.</span><span class="sxs-lookup"><span data-stu-id="034de-117">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="034de-118">SharePoint Framework в Teams</span><span class="sxs-lookup"><span data-stu-id="034de-118">SharePoint Framework in Teams</span></span>

<span data-ttu-id="034de-119">Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="034de-119">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="034de-120">Для разработчиков SharePoint это значительно упрощает процесс разработки для вкладок Teams, так как веб-части SharePoint Framework размещаются в SharePoint без необходимости использования внешних служб, таких как Azure.</span><span class="sxs-lookup"><span data-stu-id="034de-120">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="034de-121">Узнайте больше об использовании SharePoint Framework в Teams.</span><span class="sxs-lookup"><span data-stu-id="034de-121">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="034de-122">Введение</span><span class="sxs-lookup"><span data-stu-id="034de-122">Introduction</span></span>

<span data-ttu-id="034de-123">В этих инструкциях объясняется, как можно взять вкладку из примера приложения Microsoft Teams и использовать его в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="034de-123">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="034de-124">Мы будем использовать вкладку, которая уже размещена в Azure, чтобы сосредоточиться на необходимой работе по интеграции.</span><span class="sxs-lookup"><span data-stu-id="034de-124">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="034de-125">Пример приложения, который мы используем, является приложением для управления.</span><span class="sxs-lookup"><span data-stu-id="034de-125">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="034de-126">Он управляет процессом найма кандидатов для открытых позиций в группе.</span><span class="sxs-lookup"><span data-stu-id="034de-126">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="034de-127">(Само приложение, хотя оно отлично, не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="034de-127">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="034de-128">Мы хотим сосредоточиться на создании приложения Teams и его загрузке в Teams, но не создавать приложение для управления реальными специалистами.</span><span class="sxs-lookup"><span data-stu-id="034de-128">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="034de-129">Преимущества этого подхода</span><span class="sxs-lookup"><span data-stu-id="034de-129">Benefits of this approach</span></span>

- <span data-ttu-id="034de-130">Доступ к пользователям SharePoint с помощью текущей вкладки групп</span><span class="sxs-lookup"><span data-stu-id="034de-130">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="034de-131">Отправьте манифест приложения непосредственно в каталог приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="034de-131">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="034de-132">[Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются в SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-132">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="034de-133">Конечные пользователи настраивают вкладку на странице, как и любые другие веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-133">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="034de-134">Вкладка может получать доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как и при работе в Teams</span><span class="sxs-lookup"><span data-stu-id="034de-134">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="034de-135">Шаг 1: Тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="034de-135">Step 1: Testing the sample app</span></span>

<span data-ttu-id="034de-136">Скачайте пример манифеста приложения [**отсюда**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="034de-136">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="034de-137">В Microsoft Teams щелкните значок магазин в левом нижнем углу, а затем "Отправить настраиваемое приложение" в нижнем левом углу.</span><span class="sxs-lookup"><span data-stu-id="034de-137">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="034de-138">Файл, который требуется отправить, будет размещен в папке "загрузки"; Он называется TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="034de-138">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="034de-139">Если все правильно, вы увидите экран Установка/согласие для приложения управления.</span><span class="sxs-lookup"><span data-stu-id="034de-139">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="034de-140">Выберите группу, в которую вы хотите установить, и нажмите кнопку установить.</span><span class="sxs-lookup"><span data-stu-id="034de-140">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="034de-141">Теперь вы можете поэкспериментировать с приложением.</span><span class="sxs-lookup"><span data-stu-id="034de-141">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="034de-142">Шаг 2: Использование вкладки "команды" в SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-142">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="034de-143">Отправьте и разверните пакет приложения Teams в каталоге приложений SharePoint, посетив `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` , например, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="034de-143">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="034de-144">При появлении соответствующего запроса включите параметр "сделать это решение доступным для всех сайтов в организации":</span><span class="sxs-lookup"><span data-stu-id="034de-144">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Вкладки в представлении SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="034de-146">На сайте создайте новую страницу, нажав кнопку шестеренки в верхнем правом углу, а затем "добавить страницу".</span><span class="sxs-lookup"><span data-stu-id="034de-146">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Представление SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="034de-148">Вы увидите процесс создания страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="034de-148">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="034de-149">Присвойте странице имя "Моя группа".</span><span class="sxs-lookup"><span data-stu-id="034de-149">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="034de-150">Откройте панель элементов веб-частей, нажав кнопку +, и выберите вкладку группы (с именем "Contoso HR").</span><span class="sxs-lookup"><span data-stu-id="034de-150">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="034de-151">Веб-части сортируются по алфавиту; Если это длинный список, его можно найти с помощью панели поиска.</span><span class="sxs-lookup"><span data-stu-id="034de-151">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="034de-152">При этом на холсте, содержащем вкладку Teams, будет создана веб-часть:</span><span class="sxs-lookup"><span data-stu-id="034de-152">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Режим вкладки](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="034de-154">После завершения редактирования нажмите кнопку "опубликовать".</span><span class="sxs-lookup"><span data-stu-id="034de-154">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="034de-155">Можно нажать кнопку "добавить страницу в навигацию", чтобы получить краткую ссылку на страницу в левой панели навигации:</span><span class="sxs-lookup"><span data-stu-id="034de-155">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Вкладка в изображении SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="034de-157">Шаг 3: изучение страниц приложения в SharePoint</span><span class="sxs-lookup"><span data-stu-id="034de-157">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="034de-158">После публикации страницы вы можете изучить [возможности приложения Teams в среде SharePoint полностью](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span><span class="sxs-lookup"><span data-stu-id="034de-158">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="034de-159">При этом текущая страница преобразуется в страницу приложения с обычным макетом страницы SharePoint с использованием полноэкранной среды для вкладки teams:</span><span class="sxs-lookup"><span data-stu-id="034de-159">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Изображение вкладок в SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a><span data-ttu-id="034de-161">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="034de-161">More information</span></span>

- [<span data-ttu-id="034de-162">Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал</span><span class="sxs-lookup"><span data-stu-id="034de-162">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="034de-163">Использование страницы одной части приложения в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="034de-163">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
