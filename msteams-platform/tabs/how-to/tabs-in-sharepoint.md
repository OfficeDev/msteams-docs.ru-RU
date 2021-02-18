---
title: Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx
author: laujan
description: Развертывание существующей вкладки Teams в SharePoint в качестве веб-части SharePoint Framework.
keywords: Разработка sharepoint Framework для вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270793"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a><span data-ttu-id="496f6-104">Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx</span><span class="sxs-lookup"><span data-stu-id="496f6-104">Adding a Microsoft Teams tab in SharePoint as an SPFx web part</span></span>

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="496f6-105">Интеграция Teams и SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-105">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="496f6-106">В ноябрьских выпусках Teams и SharePoint Framework v.</span><span class="sxs-lookup"><span data-stu-id="496f6-106">With the November release of Teams and SharePoint Framework v.</span></span> <span data-ttu-id="496f6-107">1.7 У разработчиков есть две мощные возможности:</span><span class="sxs-lookup"><span data-stu-id="496f6-107">1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="496f6-108">Вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-108">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="496f6-109">Создайте богатые возможности приложений в SharePoint, введя приложение Teams в Sharepoint (эта статья).</span><span class="sxs-lookup"><span data-stu-id="496f6-109">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="496f6-110">SharePoint Framework в Teams</span><span class="sxs-lookup"><span data-stu-id="496f6-110">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="496f6-111">Перенесите веб-части SharePoint в Teams и позвольте SharePoint управлять размещением.</span><span class="sxs-lookup"><span data-stu-id="496f6-111">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="496f6-112">Вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-112">Teams tabs in SharePoint</span></span>

<span data-ttu-id="496f6-113">В SharePoint Framework v.1.7 мы поддерживаем возможность разработчиков использовать свои вкладки Teams и проводить их в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="496f6-113">With SharePoint Framework v.1.7, we’re now supporting the ability for developers to take their Teams tabs and host it in SharePoint.</span></span> <span data-ttu-id="496f6-114">По мере того как вкладки, вкладки, которые были в SharePoint, получают аналогичную "полную страницу", выдавая все функции вкладок Teams, сохраняя контекст и знакомство с сайтом SharePoint.</span><span class="sxs-lookup"><span data-stu-id="496f6-114">As Tabs hosted in SharePoint get a similar "full page" experience, exposing the all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="496f6-115">SharePoint Framework в Teams</span><span class="sxs-lookup"><span data-stu-id="496f6-115">SharePoint Framework in Teams</span></span>

<span data-ttu-id="496f6-116">Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="496f6-116">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="496f6-117">Для разработчиков SharePoint это значительно упрощает процесс разработки вкладок Teams, так как веб-части SharePoint Framework находятся в SharePoint без необходимости в внешних службах, таких как Azure.</span><span class="sxs-lookup"><span data-stu-id="496f6-117">For SharePoint developers, this significantly simplifies the development process for Teams tabs because SharePoint Framework web parts are hosted within SharePoint without any need for external services such as Azure.</span></span> [<span data-ttu-id="496f6-118">Узнайте больше об использовании SharePoint Framework в Teams.</span><span class="sxs-lookup"><span data-stu-id="496f6-118">Learn more about using the SharePoint Framework in Teams.</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a><span data-ttu-id="496f6-119">Введение</span><span class="sxs-lookup"><span data-stu-id="496f6-119">Introduction</span></span>

<span data-ttu-id="496f6-120">В этих инструкциях объясняется, как можно получить вкладку из примера приложения Microsoft Teams и использовать ее в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="496f6-120">These instructions will explain how you can take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> <span data-ttu-id="496f6-121">Мы будем использовать вкладку, которая уже есть в Azure, чтобы сосредоточиться на необходимых процессах интеграции.</span><span class="sxs-lookup"><span data-stu-id="496f6-121">We will be using a tab that's already hosted on Azure in order to focus on the required integration work.</span></span>

<span data-ttu-id="496f6-122">Пример приложения, который мы используем, — это приложение управления одаренно.</span><span class="sxs-lookup"><span data-stu-id="496f6-122">The sample app we're using is a Talent Management application.</span></span> <span data-ttu-id="496f6-123">Он управляет процессом найма кандидатов на открытые позиции в команде.</span><span class="sxs-lookup"><span data-stu-id="496f6-123">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="496f6-124">(Само приложение, несмотря на то, что оно выглядит хорошо, на самом деле ничего не делают.</span><span class="sxs-lookup"><span data-stu-id="496f6-124">(The app itself, while it looks nice, doesn't actually do anything.</span></span> <span data-ttu-id="496f6-125">Мы хотим сосредоточиться на создании приложения Teams и его загрузке в Teams, а не на создании реального приложения для управления одаренными менеджерами.)</span><span class="sxs-lookup"><span data-stu-id="496f6-125">We want to focus on building a Teams app and loading it into Teams, not create a real talent management application.)</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="496f6-126">Преимущества этого подхода</span><span class="sxs-lookup"><span data-stu-id="496f6-126">Benefits of this approach</span></span>

- <span data-ttu-id="496f6-127">Доступ к пользователям SharePoint с помощью существующей вкладки Teams</span><span class="sxs-lookup"><span data-stu-id="496f6-127">Reach SharePoint users with your existing Teams tab</span></span>
- <span data-ttu-id="496f6-128">Загрузите манифест приложения непосредственно в каталог приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="496f6-128">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="496f6-129">[Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются в SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-129">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint</span></span>
- <span data-ttu-id="496f6-130">Конечные пользователи настраивают вкладку на странице так же, как и любые другие веб-части SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-130">End users configure the tab on a page just like any other SharePoint web part</span></span>
- <span data-ttu-id="496f6-131">Ваша вкладка может получить доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как и при запуске в Teams</span><span class="sxs-lookup"><span data-stu-id="496f6-131">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) just as it can when running inside Teams</span></span>

## <a name="step-1-testing-the-sample-app"></a><span data-ttu-id="496f6-132">Шаг 1. Тестирование примера приложения</span><span class="sxs-lookup"><span data-stu-id="496f6-132">Step 1: Testing the sample app</span></span>

<span data-ttu-id="496f6-133">Скачайте пример манифеста [**приложения**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)здесь.</span><span class="sxs-lookup"><span data-stu-id="496f6-133">Download the sample app manifest from [**here**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

<span data-ttu-id="496f6-134">В Microsoft Teams щелкните значок Магазина в левом нижнем конце, а затем "Отправить пользовательское приложение" в левом нижнем.</span><span class="sxs-lookup"><span data-stu-id="496f6-134">In Microsoft Teams, click on the Store icon at the lower left and then "Upload a custom app" at the lower left.</span></span> <span data-ttu-id="496f6-135">Отложенный файл будет расположен в папке "Загрузки"; он называется TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="496f6-135">The file to upload will be located in your Downloads folder; it's called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="496f6-136">Если все пройдет хорошо, вы увидите экран установки и согласия для приложения управления одарением.</span><span class="sxs-lookup"><span data-stu-id="496f6-136">If all goes well, you'll see the install/consent screen for the talent management app.</span></span> <span data-ttu-id="496f6-137">Выберите команду, в который вы хотите установить, и нажмите кнопку "Установить".</span><span class="sxs-lookup"><span data-stu-id="496f6-137">Choose the team you want to install to and click the Install button.</span></span> <span data-ttu-id="496f6-138">Теперь вы можете поэкспериментировать с приложением.</span><span class="sxs-lookup"><span data-stu-id="496f6-138">You're now free to experiment with the app.</span></span>

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a><span data-ttu-id="496f6-139">Шаг 2. Использование вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-139">Step 2: Using the Teams tab in SharePoint</span></span>

<span data-ttu-id="496f6-140">Загрузите и развернете пакет приложения Teams в каталоге приложений SharePoint, посетив, `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` например.</span><span class="sxs-lookup"><span data-stu-id="496f6-140">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, e.g. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

<span data-ttu-id="496f6-141">При запросе в включить "Сделать это решение доступным для всех сайтов в организации":</span><span class="sxs-lookup"><span data-stu-id="496f6-141">When prompted, enable "Make this solution available to all sites in the organization":</span></span>

![Вкладки в представлении SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

<span data-ttu-id="496f6-143">Создайте новую страницу на своем сайте, нажав кнопку шестеренки в правом верхнем правом верхнем направлении и нажав кнопку "Добавить страницу":</span><span class="sxs-lookup"><span data-stu-id="496f6-143">In your site, create a new page by clicking in the gear button at the upper right and then "Add a page":</span></span>

![Представление SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

<span data-ttu-id="496f6-145">Вы увидите, как будет делиться страницами SharePoint.</span><span class="sxs-lookup"><span data-stu-id="496f6-145">You'll see the SharePoint Pages authoring experience.</span></span> <span data-ttu-id="496f6-146">Назовите страницу "Моя вкладка Teams".</span><span class="sxs-lookup"><span data-stu-id="496f6-146">Name your page "My Teams Tab".</span></span>

<span data-ttu-id="496f6-147">Откройте панели инструментов веб-части, нажав кнопку +, и выберите вкладку Teams (с именем "Contoso HR").</span><span class="sxs-lookup"><span data-stu-id="496f6-147">Open the web part toolbox by pressing the + button, and select your Teams Tab (named "Contoso HR").</span></span> <span data-ttu-id="496f6-148">Веб-части сортироваться в алфавитном порядке; Если это длинный список, вы можете найти его с помощью панели поиска.</span><span class="sxs-lookup"><span data-stu-id="496f6-148">Web parts are sorted alphabetically; if it's a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="496f6-149">В результате на холсте будет создаваться веб-часть, содержаная вкладку Teams:</span><span class="sxs-lookup"><span data-stu-id="496f6-149">This will create a web part in the canvas that contains your Teams tab:</span></span>

![Представление "Вкладка"](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

<span data-ttu-id="496f6-151">После завершения редактирования нажмите кнопку "Опубликовать".</span><span class="sxs-lookup"><span data-stu-id="496f6-151">Press the "Publish" button when you are finished editing.</span></span>

<span data-ttu-id="496f6-152">Может потребоваться нажать кнопку "Добавить страницу в навигацию", чтобы получить быструю ссылку на страницу в левой панели навигации:</span><span class="sxs-lookup"><span data-stu-id="496f6-152">You may want to click "Add page to navigation" to have a quick reference to your page in the left navigation bar:</span></span>

![Вкладка в изображении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="496f6-154">Шаг 3. Изучение страниц приложений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="496f6-154">Step 3: Explore App Pages in SharePoint</span></span>

<span data-ttu-id="496f6-155">После публикации страницы вы можете изучить, как сделать приложение Teams более полным [в SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="496f6-155">Once your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="496f6-156">При этом текущая страница преобразуется в страницу приложения, где показан обычный макет страницы SharePoint с полно страницей для вкладки Teams:</span><span class="sxs-lookup"><span data-stu-id="496f6-156">This converts the current page into an App Page, showing the normal SharePoint page layout with a full-page experience for the Teams tab:</span></span>

![Изображение вкладок в Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a><span data-ttu-id="496f6-158">Пример кода</span><span class="sxs-lookup"><span data-stu-id="496f6-158">Code sample</span></span>
| <span data-ttu-id="496f6-159">**Имя примера**</span><span class="sxs-lookup"><span data-stu-id="496f6-159">**Sample name**</span></span> | <span data-ttu-id="496f6-160">**Описание**</span><span class="sxs-lookup"><span data-stu-id="496f6-160">**Description**</span></span> | <span data-ttu-id="496f6-161">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="496f6-161">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="496f6-162">Веб-часть SPFx</span><span class="sxs-lookup"><span data-stu-id="496f6-162">SPFx web part</span></span> | <span data-ttu-id="496f6-163">Примеры веб-части SPFx для вкладок, каналов и групп.</span><span class="sxs-lookup"><span data-stu-id="496f6-163">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="496f6-164">View</span><span class="sxs-lookup"><span data-stu-id="496f6-164">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a><span data-ttu-id="496f6-165">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="496f6-165">More information</span></span>

- [<span data-ttu-id="496f6-166">Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал</span><span class="sxs-lookup"><span data-stu-id="496f6-166">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [<span data-ttu-id="496f6-167">Использование страницы одной части приложения в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="496f6-167">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
