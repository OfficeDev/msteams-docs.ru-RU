---
title: Добавление вкладки Teams в SharePoint
author: laujan
description: Развертывание существующей вкладки Teams в SharePoint в качестве веб-части SharePoint Framework.
keywords: teams tabs sharepoint framework development
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: a2ea6c470f094a9d7b8617a210559e911f5f81c9
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058483"
---
# <a name="add-teams-tab-to-sharepoint"></a><span data-ttu-id="2b725-104">Добавление вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-104">Add Teams tab to SharePoint</span></span> 

<span data-ttu-id="2b725-105">Вы можете получить богатый опыт интеграции между Microsoft Teams и SharePoint, добавив вкладку Microsoft Teams в SharePoint в качестве веб-части SPFx.</span><span class="sxs-lookup"><span data-stu-id="2b725-105">You can get a rich integration experience between Microsoft Teams and SharePoint by adding a Microsoft Teams tab in SharePoint as an SPFx web part.</span></span> <span data-ttu-id="2b725-106">В этом документе вы можете узнать, как взять вкладку из примерного приложения Microsoft Teams и использовать ее в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-106">This document guides you on how you to take a tab from a Microsoft Teams sample app and use it in SharePoint.</span></span> 

## <a name="rich-integration-between-teams-and-sharepoint"></a><span data-ttu-id="2b725-107">Насыщенная интеграция между Teams и SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-107">Rich integration between Teams and SharePoint</span></span>

<span data-ttu-id="2b725-108">После ноябрьского выпуска Teams и SharePoint Framework v.1.7 у разработчиков есть две мощные возможности:</span><span class="sxs-lookup"><span data-stu-id="2b725-108">With the November release of Teams and SharePoint Framework v.1.7, developers have two powerful capabilities:</span></span>

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
                        <h3><span data-ttu-id="2b725-109">Командные вкладки в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-109">Teams Tabs in SharePoint</span></span></h3>
                        <p><span data-ttu-id="2b725-110">Создайте богатые возможности приложения в SharePoint, введя приложение Teams в Sharepoint (эта статья).</span><span class="sxs-lookup"><span data-stu-id="2b725-110">Create rich app experiences in SharePoint by bringing your Teams app into Sharepoint (this article).</span></span></p>
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
                        <h3><span data-ttu-id="2b725-111">SharePoint Framework в teams</span><span class="sxs-lookup"><span data-stu-id="2b725-111">SharePoint Framework in Teams</span></span></h3>
                        <p><span data-ttu-id="2b725-112">Принесите веб-части SharePoint в Teams и позвольте SharePoint управлять хостингом для вас.</span><span class="sxs-lookup"><span data-stu-id="2b725-112">Bring your SharePoint web parts to Teams and let SharePoint manage the hosting for you.</span></span></p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a><span data-ttu-id="2b725-113">Вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-113">Teams tabs in SharePoint</span></span>

<span data-ttu-id="2b725-114">С помощью SharePoint Framework v.1.7 вы можете использовать вкладки Teams в SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-114">With SharePoint Framework v.1.7, you can host your Teams tabs in SharePoint.</span></span> <span data-ttu-id="2b725-115">Так как вкладки, которые будут  храниться в SharePoint, получите аналогичную полную страницу, обнажая все функции вкладок Teams, сохраняя при этом контекст и знакомство сайта SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-115">As tabs hosted in SharePoint get a similar **full page** experience, exposing all the features of Teams tabs while retaining the context and familiarity of a SharePoint site.</span></span>

### <a name="sharepoint-framework-in-teams"></a><span data-ttu-id="2b725-116">SharePoint Framework в teams</span><span class="sxs-lookup"><span data-stu-id="2b725-116">SharePoint Framework in Teams</span></span>

<span data-ttu-id="2b725-117">Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework.</span><span class="sxs-lookup"><span data-stu-id="2b725-117">You can also implement your Microsoft Teams tabs using SharePoint Framework.</span></span> <span data-ttu-id="2b725-118">Веб-части SharePoint Framework находятся в SharePoint без необходимости для внешних служб, таких как Azure.</span><span class="sxs-lookup"><span data-stu-id="2b725-118">SharePoint Framework web parts are hosted within SharePoint without any need for external services, such as Azure.</span></span> <span data-ttu-id="2b725-119">Для разработчиков SharePoint это значительно упрощает процесс разработки вкладок Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-119">For SharePoint developers, this significantly simplifies the development process for Teams tabs.</span></span> <span data-ttu-id="2b725-120">Дополнительные сведения о SharePoint Framework в Teams см. в разделе Использование [SharePoint Framework в Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span><span class="sxs-lookup"><span data-stu-id="2b725-120">For more information on SharePoint Framework in Teams, see [how to use the SharePoint Framework in Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)</span></span>

## <a name="introduction"></a><span data-ttu-id="2b725-121">Введение</span><span class="sxs-lookup"><span data-stu-id="2b725-121">Introduction</span></span>

<span data-ttu-id="2b725-122">Вкладка, используемая здесь, уже находится в Azure, чтобы сосредоточиться на требуемой работе по интеграции.</span><span class="sxs-lookup"><span data-stu-id="2b725-122">The tab used here is already hosted on Azure, to focus on the required integration work.</span></span>

<span data-ttu-id="2b725-123">Используемая примерная приложение — приложение управления талантами.</span><span class="sxs-lookup"><span data-stu-id="2b725-123">The sample app that is being used is a Talent Management application.</span></span> <span data-ttu-id="2b725-124">Он управляет процессом найма кандидатов на открытые позиции в команде.</span><span class="sxs-lookup"><span data-stu-id="2b725-124">It manages the hiring process of candidates for open positions in a team.</span></span> <span data-ttu-id="2b725-125">Создайте пример приложения Teams и загрузите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-125">Build a sample Teams app and load it into Teams.</span></span> <span data-ttu-id="2b725-126">Не создавайте реальное приложение для управления талантами.</span><span class="sxs-lookup"><span data-stu-id="2b725-126">Do not create a real talent management application.</span></span>

### <a name="benefits-of-this-approach"></a><span data-ttu-id="2b725-127">Преимущества этого подхода</span><span class="sxs-lookup"><span data-stu-id="2b725-127">Benefits of this approach</span></span>

* <span data-ttu-id="2b725-128">Охватите пользователей SharePoint с помощью существующей вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-128">Reach SharePoint users with your existing Teams tab.</span></span>
* <span data-ttu-id="2b725-129">Загрузите манифест приложения непосредственно в каталог приложений SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-129">Upload your app manifest directly to your SharePoint app catalog.</span></span> <span data-ttu-id="2b725-130">[Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-130">[Teams application packages](~/concepts/build-and-test/apps-package.md) are now supported by SharePoint.</span></span>
* <span data-ttu-id="2b725-131">Пользователи настраивают вкладку на странице так же, как и любую другую веб-часть SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-131">The users configure the tab on a page just like any other SharePoint web part.</span></span>
* <span data-ttu-id="2b725-132">Ваша вкладка может получить доступ к [контексту,](~/tabs/how-to/access-teams-context.md) как это возможно, при работе внутри Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-132">Your tab can access its [context](~/tabs/how-to/access-teams-context.md) sameas it can, when running inside Teams.</span></span>

<span data-ttu-id="2b725-133">**Добавление вкладки Teams в SharePoint**</span><span class="sxs-lookup"><span data-stu-id="2b725-133">**To add Teams tab to SharePoint**</span></span>

<span data-ttu-id="2b725-134">Выполните следующие действия, чтобы добавить вкладку Teams в SharePoint:</span><span class="sxs-lookup"><span data-stu-id="2b725-134">Perform the following steps to add Teams tab to SharePoint:</span></span>

## <a name="1-test-the-sample-app"></a><span data-ttu-id="2b725-135">1. Проверка примера приложения</span><span class="sxs-lookup"><span data-stu-id="2b725-135">1. Test the sample app</span></span>

<span data-ttu-id="2b725-136">Скачайте [манифест примера приложения](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span><span class="sxs-lookup"><span data-stu-id="2b725-136">Download the [sample app manifest](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).</span></span>

1. <span data-ttu-id="2b725-137">Откройте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-137">Open Microsoft Teams.</span></span>
1. <span data-ttu-id="2b725-138">Выберите **значок Appstore** в нижней левой части боковой вкладки.</span><span class="sxs-lookup"><span data-stu-id="2b725-138">Select the **Appstore** icon at the lower left of side tab.</span></span>
1. <span data-ttu-id="2b725-139">Выберите **Отправка настраиваемого приложения** в левом нижнем ок.</span><span class="sxs-lookup"><span data-stu-id="2b725-139">Select **Upload a custom app** at the lower left.</span></span> <span data-ttu-id="2b725-140">На следующем изображении отображается соответствующий экран:</span><span class="sxs-lookup"><span data-stu-id="2b725-140">The following image displays the corresponding screen:</span></span>  

    ![загрузка настраиваемой приложения](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. <span data-ttu-id="2b725-142">Файл для отправки находится в папке **Downloads.**</span><span class="sxs-lookup"><span data-stu-id="2b725-142">The file to upload is located in your **Downloads** folder.</span></span> <span data-ttu-id="2b725-143">Он называется TalentMgmt-Azure.zip.</span><span class="sxs-lookup"><span data-stu-id="2b725-143">It is called TalentMgmt-Azure.zip.</span></span> <span data-ttu-id="2b725-144">На следующем изображении отображается соответствующий экран:</span><span class="sxs-lookup"><span data-stu-id="2b725-144">The following image displays the corresponding screen:</span></span>
 
    ![TalentMgmt в Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. <span data-ttu-id="2b725-146">Вы можете увидеть экран установки или согласия для приложения управления талантами.</span><span class="sxs-lookup"><span data-stu-id="2b725-146">You can see the install or consent screen for the talent management app.</span></span> <span data-ttu-id="2b725-147">Выберите команду, которая будет устанавливаться.</span><span class="sxs-lookup"><span data-stu-id="2b725-147">Select the team you want to install.</span></span> 
1. <span data-ttu-id="2b725-148">Выберите **установку** и начните экспериментировать с приложением.</span><span class="sxs-lookup"><span data-stu-id="2b725-148">Select the **Install** and start experimenting with the app.</span></span>

## <a name="2-use-teams-tab-in-sharepoint"></a><span data-ttu-id="2b725-149">2. Использование вкладки Teams в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-149">2. Use Teams tab in SharePoint</span></span>

1. <span data-ttu-id="2b725-150">Загрузите и разверните пакет приложений Teams в каталог приложений SharePoint, посетив `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` .</span><span class="sxs-lookup"><span data-stu-id="2b725-150">Upload and deploy your Teams app package to your SharePoint App Catalog by visiting `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span> <span data-ttu-id="2b725-151">Например, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span><span class="sxs-lookup"><span data-stu-id="2b725-151">For example, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.</span></span>

1. <span data-ttu-id="2b725-152">При запросе **вделайте это решение доступным для всех сайтов в организации.**</span><span class="sxs-lookup"><span data-stu-id="2b725-152">When prompted, enable **Make this solution available to all sites in the organization**.</span></span>
<span data-ttu-id="2b725-153">На следующем изображении отображается соответствующий экран:</span><span class="sxs-lookup"><span data-stu-id="2b725-153">The following image displays the corresponding screen:</span></span>

   ![Вкладки в представлении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. <span data-ttu-id="2b725-155">На своем сайте создайте новую страницу, выбрав кнопку передач в правом верхнем справа, а затем **выберите Добавить страницу**.</span><span class="sxs-lookup"><span data-stu-id="2b725-155">In your site, create a new page by selecting the gear button at the upper right and then  select **Add a page**.</span></span>
<span data-ttu-id="2b725-156">На следующем изображении отображается соответствующий экран:</span><span class="sxs-lookup"><span data-stu-id="2b725-156">The following image displays the corresponding screen:</span></span>

   ![Представление Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. <span data-ttu-id="2b725-158">Вы можете увидеть опыт авторинга страниц SharePoint.</span><span class="sxs-lookup"><span data-stu-id="2b725-158">You can see the SharePoint pages authoring experience.</span></span> <span data-ttu-id="2b725-159">Назови свою страницу **вкладками "Мои команды".**</span><span class="sxs-lookup"><span data-stu-id="2b725-159">Name your page as **My Teams Tab**.</span></span>

1. <span data-ttu-id="2b725-160">Откройте инструментарий веб-части, нажав кнопку, и выберите вкладку `+` Teams с именем **Hr Contoso.**</span><span class="sxs-lookup"><span data-stu-id="2b725-160">Open the web part toolbox by pressing the `+` button, and select your Teams Tab, named **Contoso HR**.</span></span> <span data-ttu-id="2b725-161">Веб-части сортироваться в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="2b725-161">Web parts are sorted alphabetically.</span></span> <span data-ttu-id="2b725-162">Если это длинный список, его можно найти с помощью панели поиска.</span><span class="sxs-lookup"><span data-stu-id="2b725-162">If it is a long list, you can use the search bar to find it.</span></span> <span data-ttu-id="2b725-163">Это создает веб-часть на холсте, содержаще вкладку Teams. На следующем изображении отображается представление вкладки:</span><span class="sxs-lookup"><span data-stu-id="2b725-163">This creates a web part in the canvas that contains your Teams tab. The following image displays the tab view:</span></span>

   ![Представление Tab](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. <span data-ttu-id="2b725-165">Нажмите **кнопку Публикация** после завершения редактирования.</span><span class="sxs-lookup"><span data-stu-id="2b725-165">Press the **Publish** button after you finish  editing.</span></span>

1. <span data-ttu-id="2b725-166">Выберите **страницу Добавить в навигацию,** чтобы иметь быструю ссылку на страницу в левой панели навигации.</span><span class="sxs-lookup"><span data-stu-id="2b725-166">Select **Add page to navigation** to have a quick reference to your page in the left navigation bar.</span></span> <span data-ttu-id="2b725-167">На следующем изображении отображается вкладка в Sharepoint:</span><span class="sxs-lookup"><span data-stu-id="2b725-167">The following image displays the tab in Sharepoint:</span></span> 

   ![Вкладка в изображении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a><span data-ttu-id="2b725-169">3. Изучение страниц приложений в SharePoint</span><span class="sxs-lookup"><span data-stu-id="2b725-169">3. Explore App Pages in SharePoint</span></span>

<span data-ttu-id="2b725-170">После публикации страницы вы можете изучить возможность превращения приложения Teams в более полное приложение [в SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages)</span><span class="sxs-lookup"><span data-stu-id="2b725-170">After your page is published, you can explore [turning your Teams app into a more complete experience inside SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages).</span></span> <span data-ttu-id="2b725-171">Это преобразует текущую страницу в страницу приложения, показывая нормальный макет страницы SharePoint с полным опытом страницы для вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="2b725-171">This converts the current page into an App Page, showing the normal SharePoint page layout with a full page experience for the Teams tab.</span></span> 

<span data-ttu-id="2b725-172">На следующем изображении отображается полное представление приложения Teams в Sharepoint: Изображение вкладок ![ в Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span><span class="sxs-lookup"><span data-stu-id="2b725-172">The following image displays the complete experience of Teams app in Sharepoint: ![Image of Tabs in Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="2b725-173">Пример кода</span><span class="sxs-lookup"><span data-stu-id="2b725-173">Code sample</span></span>
| <span data-ttu-id="2b725-174">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="2b725-174">**Sample name**</span></span> | <span data-ttu-id="2b725-175">**Описание**</span><span class="sxs-lookup"><span data-stu-id="2b725-175">**Description**</span></span> | <span data-ttu-id="2b725-176">**SPFx**</span><span class="sxs-lookup"><span data-stu-id="2b725-176">**SPFx**</span></span> |
|-----------------|-----------------|----------|
| <span data-ttu-id="2b725-177">Веб-часть SPFx</span><span class="sxs-lookup"><span data-stu-id="2b725-177">SPFx web part</span></span> | <span data-ttu-id="2b725-178">Образцы веб-части SPFx для вкладок, каналов и групп.</span><span class="sxs-lookup"><span data-stu-id="2b725-178">SPFx web part samples for tabs, channels, and groups.</span></span> | [<span data-ttu-id="2b725-179">View</span><span class="sxs-lookup"><span data-stu-id="2b725-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a><span data-ttu-id="2b725-180">См. также</span><span class="sxs-lookup"><span data-stu-id="2b725-180">See also</span></span>

- [<span data-ttu-id="2b725-181">Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал</span><span class="sxs-lookup"><span data-stu-id="2b725-181">Building Microsoft Teams tab using SharePoint Framework - Tutorial</span></span>](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

- [<span data-ttu-id="2b725-182">Использование страницы одной части приложения в SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="2b725-182">Using single part app pages in SharePoint Online</span></span>](/sharepoint/dev/spfx/web-parts/single-part-app-pages)

- [<span data-ttu-id="2b725-183">Интеграция веб-приложений</span><span class="sxs-lookup"><span data-stu-id="2b725-183">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
