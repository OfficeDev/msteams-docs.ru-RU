---
title: Создание списка магазина для приложения
description: Описывает, как создать список магазинов для Microsoft Teams приложения.
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 270936ca967c17caaa8a56f85057b20ca3d6a409
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101431"
---
# <a name="create-a-store-listing-for-your-microsoft-teams-app"></a><span data-ttu-id="21bb2-103">Создание списка магазина для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="21bb2-103">Create a store listing for your Microsoft Teams app</span></span>

<span data-ttu-id="21bb2-104">Сведения, которые вы [](https://partner.microsoft.com) передаете в Центр партнеров&#8212;включая ваше имя, описания, значки и изображения,&#8212;становятся Microsoft Teams магазина и списка Microsoft AppSource для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-104">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Microsoft Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="21bb2-105">Список магазинов может быть первым впечатлением от вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-105">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="21bb2-106">Увеличение установок с помощью списка, который эффективно передает преимущества, функциональные возможности и бренд вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-106">Increase your installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

## <a name="specify-a-short-name"></a><span data-ttu-id="21bb2-107">Укажите короткое имя</span><span class="sxs-lookup"><span data-stu-id="21bb2-107">Specify a short name</span></span>

<span data-ttu-id="21bb2-108">Имя вашего приложения (в частности, его короткое [*имя)*](~/resources/schema/manifest-schema.md#name)играет решающую роль в том, как пользователи обнаруживают его в магазине.</span><span class="sxs-lookup"><span data-stu-id="21bb2-108">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

<span data-ttu-id="21bb2-109">В следующем примере выделяется, где короткое имя приложения отображается в списке магазина.</span><span class="sxs-lookup"><span data-stu-id="21bb2-109">The following example highlights where an app's short name displays in a store listing.</span></span>

:::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="Пример экрана показывает, где короткое имя приложения отображается в списке магазина.":::

### <a name="best-practices-for-names"></a><span data-ttu-id="21bb2-111">Лучшие практики для имен</span><span class="sxs-lookup"><span data-stu-id="21bb2-111">Best practices for names</span></span>

<span data-ttu-id="21bb2-112">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-112">**Do:**</span></span>

* <span data-ttu-id="21bb2-113">Выберите простое запоминающееся имя, которое подсказает, что делает ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="21bb2-113">Choose a simple, memorable name that hints at what your app does.</span></span>
* <span data-ttu-id="21bb2-114">Будьте отличительными.</span><span class="sxs-lookup"><span data-stu-id="21bb2-114">Be distinctive.</span></span>
* <span data-ttu-id="21bb2-115">Избегайте опечаток и грамматических ошибок.</span><span class="sxs-lookup"><span data-stu-id="21bb2-115">Avoid typos and grammatical errors.</span></span>

<span data-ttu-id="21bb2-116">**Не рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-116">**Don't:**</span></span>

* <span data-ttu-id="21bb2-117">Используйте ненормативную или пренебожную лексику.</span><span class="sxs-lookup"><span data-stu-id="21bb2-117">Use profane or derogatory terms.</span></span>
* <span data-ttu-id="21bb2-118">Используйте расово или культурно нечувствительный язык.</span><span class="sxs-lookup"><span data-stu-id="21bb2-118">Use racially or culturally insensitive language.</span></span>
* <span data-ttu-id="21bb2-119">Используйте общие термины или имена, аналогичные существующим приложениям.</span><span class="sxs-lookup"><span data-stu-id="21bb2-119">Use generic terms or names similar to existing apps.</span></span>
* <span data-ttu-id="21bb2-120">Включай Teams, "Microsoft", существующие и предстоящие имена продуктов Майкрософт или "приложение" в имя.</span><span class="sxs-lookup"><span data-stu-id="21bb2-120">Include "Teams", "Microsoft", existing/upcoming Microsoft product names, or  "app" in the name.</span></span>

> [!NOTE]
> <span data-ttu-id="21bb2-121">Если ваше приложение является частью официального партнерства с Microsoft, имя приложения должно быть первым (например, *Connector Salesforce для Microsoft Teams).*</span><span class="sxs-lookup"><span data-stu-id="21bb2-121">If your app is part of an official partnership with Microsoft, the name of your app must come first (for example, *Salesforce Connector for Microsoft Teams*).</span></span>

## <a name="write-descriptions"></a><span data-ttu-id="21bb2-122">Написание описаний</span><span class="sxs-lookup"><span data-stu-id="21bb2-122">Write descriptions</span></span>

<span data-ttu-id="21bb2-123">Вам нужно краткое и длинное описание приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-123">You need a short and long description of your app.</span></span>

### <a name="short-description"></a><span data-ttu-id="21bb2-124">Краткое описание</span><span class="sxs-lookup"><span data-stu-id="21bb2-124">Short description</span></span>

<span data-ttu-id="21bb2-125">Краткий сводка приложения, которая должна быть оригинальной, привлекательной и направленной для целевой аудитории.</span><span class="sxs-lookup"><span data-stu-id="21bb2-125">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="21bb2-126">В идеале сохраняем краткое описание в одном предложении.</span><span class="sxs-lookup"><span data-stu-id="21bb2-126">Ideally, keep the short description to one sentence.</span></span>

<span data-ttu-id="21bb2-127">В следующем примере выделяется, где краткое описание приложения отображается в списке магазина:</span><span class="sxs-lookup"><span data-stu-id="21bb2-127">The following example highlights where an app's short description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Пример экрана показывает, где краткое описание приложения отображается в списке магазина.":::

#### <a name="best-practices-for-short-descriptions"></a><span data-ttu-id="21bb2-129">Лучшие практики для коротких описаний</span><span class="sxs-lookup"><span data-stu-id="21bb2-129">Best practices for short descriptions</span></span>

<span data-ttu-id="21bb2-130">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-130">**Do:**</span></span>

* <span data-ttu-id="21bb2-131">Сначала разместите наиболее важные сведения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-131">Put the most important information first.</span></span>
* <span data-ttu-id="21bb2-132">Включай ключевые слова, которые клиенты, скорее всего, будут искать.</span><span class="sxs-lookup"><span data-stu-id="21bb2-132">Include keywords that customers are likely to search for.</span></span>

<span data-ttu-id="21bb2-133">**Не рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-133">**Don't:**</span></span>

* <span data-ttu-id="21bb2-134">Повторите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-134">Repeat your app name.</span></span>
* <span data-ttu-id="21bb2-135">Использование жаргона или специализированной терминологии.</span><span class="sxs-lookup"><span data-stu-id="21bb2-135">Rely on jargon or specialized terminology.</span></span> <span data-ttu-id="21bb2-136">(Вы не можете предположить, что пользователи знают, что искать.)</span><span class="sxs-lookup"><span data-stu-id="21bb2-136">(You can't assume users know what to look for.)</span></span>

### <a name="long-description"></a><span data-ttu-id="21bb2-137">Подробное описание</span><span class="sxs-lookup"><span data-stu-id="21bb2-137">Long description</span></span>

<span data-ttu-id="21bb2-138">Длинное описание может предоставить привлекательный повествование, которое выделяет основные функции приложения, проблемы, которые оно решает, и его целевую аудиторию.</span><span class="sxs-lookup"><span data-stu-id="21bb2-138">The long description can provide an engaging narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="21bb2-139">Хотя это описание может быть до 4000 символов, большинство пользователей будут читать только между 300-500 слов.</span><span class="sxs-lookup"><span data-stu-id="21bb2-139">While this description can be as long as 4000 characters, most users will only read between 300-500 words.</span></span>

<span data-ttu-id="21bb2-140">В следующем примере выделяется, где длинное описание приложения отображается в списке магазина:</span><span class="sxs-lookup"><span data-stu-id="21bb2-140">The following example highlights where an app's long description displays in a store listing:</span></span>

:::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="Пример экрана показывает, где длинное описание приложения отображается в списке магазина.":::

#### <a name="usage-examples"></a><span data-ttu-id="21bb2-142">Примеры использования</span><span class="sxs-lookup"><span data-stu-id="21bb2-142">Usage examples</span></span>

<span data-ttu-id="21bb2-143">Следующие фразы являются примерами того, что разрешено при написании длинных описаний:</span><span class="sxs-lookup"><span data-stu-id="21bb2-143">The following phrases are examples of what's allowed when writing long descriptions:</span></span>

* <span data-ttu-id="21bb2-144">"<имя приложения *>* с Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-144">"<*Your app name*> works with Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-145">"... тип <*для>* для Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-145">"... a <*type of app*> for Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-146">"<*имя* приложения> интегрируется с Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-146">"<*Your app name*> integrates with Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-147">"... интегрирована с Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-147">"... integrated with Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-148">"... для пользователей, работающих с Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-148">"... for users working with Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-149">"... для <*задачи>* в Microsoft Teams"</span><span class="sxs-lookup"><span data-stu-id="21bb2-149">"... for <*specific task*> within Microsoft Teams"</span></span>
* <span data-ttu-id="21bb2-150">"... построено на ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-150">"... built on ..."</span></span>
* <span data-ttu-id="21bb2-151">"... работает на ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-151">"... runs on ..."</span></span>
* <span data-ttu-id="21bb2-152">"... включено ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-152">"... enabled by ..."</span></span>
* <span data-ttu-id="21bb2-153">"... разработано для ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-153">"... developed for ..."</span></span>
* <span data-ttu-id="21bb2-154">"... предназначен для ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-154">"... designed for ..."</span></span>

#### <a name="best-practices-for-long-descriptions"></a><span data-ttu-id="21bb2-155">Лучшие практики для длинных описаний</span><span class="sxs-lookup"><span data-stu-id="21bb2-155">Best practices for long descriptions</span></span>

<span data-ttu-id="21bb2-156">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-156">**Do:**</span></span>

* <span data-ttu-id="21bb2-157">Используйте [Markdown для](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) формата описания.</span><span class="sxs-lookup"><span data-stu-id="21bb2-157">Use [Markdown](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) to format your description.</span></span>
* <span data-ttu-id="21bb2-158">Список функций с точками пули, поэтому проще сканировать описание.</span><span class="sxs-lookup"><span data-stu-id="21bb2-158">List features with bullet points so it's easier to scan the description.</span></span>
* <span data-ttu-id="21bb2-159">Используйте активный голос и поговорите с пользователями напрямую (например, *Вы можете ...*).</span><span class="sxs-lookup"><span data-stu-id="21bb2-159">Use active voice and speak to users directly (for example, *You can ...*).</span></span>
* <span data-ttu-id="21bb2-160">Включаем ссылку справка или поддержка.</span><span class="sxs-lookup"><span data-stu-id="21bb2-160">Include a help or support link.</span></span>
* <span data-ttu-id="21bb2-161">Определите, если это применимо: ограничения, настройка сведений, зависимостей учетных записей и обновления выпуска.</span><span class="sxs-lookup"><span data-stu-id="21bb2-161">Identify the following if applicable: limitations, set up information, account dependencies, and release updates.</span></span>

<span data-ttu-id="21bb2-162">**Не рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-162">**Don't:**</span></span>

* <span data-ttu-id="21bb2-163">Более 500 слов.</span><span class="sxs-lookup"><span data-stu-id="21bb2-163">Exceed 500 words.</span></span>
* <span data-ttu-id="21bb2-164">Включай слишком много ключевых слов.</span><span class="sxs-lookup"><span data-stu-id="21bb2-164">Include too many keywords.</span></span> <span data-ttu-id="21bb2-165">(Это отвлекает и не поможет людям найти ваше приложение.)</span><span class="sxs-lookup"><span data-stu-id="21bb2-165">(It's distracting and won't help people find your app.)</span></span>
* <span data-ttu-id="21bb2-166">Используйте следующий язык, если приложение не прошло официальный процесс сертификации:</span><span class="sxs-lookup"><span data-stu-id="21bb2-166">Use the following language unless the app has gone through an official certification process:</span></span>
  * <span data-ttu-id="21bb2-167">"... сертифицировано для ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-167">"... certified for ..."</span></span>
  * <span data-ttu-id="21bb2-168">" ... питание от ..."</span><span class="sxs-lookup"><span data-stu-id="21bb2-168">" ... powered by ..."</span></span>

### <a name="best-practices-for-all-descriptions"></a><span data-ttu-id="21bb2-169">Лучшие практики для всех описаний</span><span class="sxs-lookup"><span data-stu-id="21bb2-169">Best practices for all descriptions</span></span>

<span data-ttu-id="21bb2-170">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-170">**Do:**</span></span>

* <span data-ttu-id="21bb2-171">Ссылки на имена продуктов Майкрософт только при необходимости.</span><span class="sxs-lookup"><span data-stu-id="21bb2-171">Reference Microsoft product names only when necessary.</span></span> <span data-ttu-id="21bb2-172">Дополнительные сведения о руководстве см. в [руководстве по товарным знакам и брендам Майкрософт.](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)</span><span class="sxs-lookup"><span data-stu-id="21bb2-172">For more information on the guidelines, see [Microsoft Trademark and Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).</span></span>
* <span data-ttu-id="21bb2-173">Если вам нужно ссылаться **на Teams,** напишите первую ссылку как **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="21bb2-173">If you need to reference **Teams**, write the first reference as **Microsoft Teams**.</span></span> <span data-ttu-id="21bb2-174">Последующие ссылки можно сократить до **Teams.**</span><span class="sxs-lookup"><span data-stu-id="21bb2-174">Subsequent references can be shortened to **Teams**.</span></span>
* <span data-ttu-id="21bb2-175">Обратитесь **Microsoft 365** вместо **Office 365**.</span><span class="sxs-lookup"><span data-stu-id="21bb2-175">Refer to **Microsoft 365** instead of **Office 365**.</span></span>
* <span data-ttu-id="21bb2-176">Избегайте опечаток и грамматических ошибок.</span><span class="sxs-lookup"><span data-stu-id="21bb2-176">Avoid typos and grammatical errors.</span></span>
* <span data-ttu-id="21bb2-177">Избегайте ненужных капитализаций (например, **пользователи,** а не **пользователи).**</span><span class="sxs-lookup"><span data-stu-id="21bb2-177">Avoid unnecessary capitalizations (for example, **Users** instead of **users**).</span></span>
* <span data-ttu-id="21bb2-178">Избегайте аббревиатур.</span><span class="sxs-lookup"><span data-stu-id="21bb2-178">Avoid acronyms.</span></span>

<span data-ttu-id="21bb2-179">**Не рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-179">**Don't:**</span></span>

* <span data-ttu-id="21bb2-180">Сокращение Microsoft в качестве **MS или** **MSFT**.</span><span class="sxs-lookup"><span data-stu-id="21bb2-180">Abbreviate Microsoft as **MS** or **MSFT**.</span></span>
* <span data-ttu-id="21bb2-181">Указать, что приложение — это предложение от Корпорации Майкрософт, в том числе с помощью слоганы или taglines Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="21bb2-181">Indicate the app is an offering from Microsoft, including using Microsoft slogans or taglines.</span></span>
* <span data-ttu-id="21bb2-182">Используйте имена брендов, защищенные авторским правом, которые не принадлежат вам.</span><span class="sxs-lookup"><span data-stu-id="21bb2-182">Use copyrighted brand names you don't own.</span></span>

## <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="21bb2-183">Соблюдайте рекомендации по проектированию значков</span><span class="sxs-lookup"><span data-stu-id="21bb2-183">Adhere to icon design guidelines</span></span>

<span data-ttu-id="21bb2-184">Значки являются одним из основных элементов, которые пользователи видят при просмотре магазина.</span><span class="sxs-lookup"><span data-stu-id="21bb2-184">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="21bb2-185">Значки должны сообщать о цели бренда вашего приложения, а также о Teams требованиях.</span><span class="sxs-lookup"><span data-stu-id="21bb2-185">Your icons should communicate your app's brand purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="21bb2-186">Дополнительные сведения см. в [специальном руководстве по разработке значков Teams приложений.](~/concepts/build-and-test/apps-package.md#app-icons)</span><span class="sxs-lookup"><span data-stu-id="21bb2-186">For more information, see [specific guidance on designing Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

## <a name="capture-screenshots"></a><span data-ttu-id="21bb2-187">Захват скриншотов</span><span class="sxs-lookup"><span data-stu-id="21bb2-187">Capture screenshots</span></span>

<span data-ttu-id="21bb2-188">Скриншоты предоставляют видную визуальную предварительную версию приложения в дополнение к имени, значку и описаниям приложения.</span><span class="sxs-lookup"><span data-stu-id="21bb2-188">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

### <a name="requirements-for-screenshots"></a><span data-ttu-id="21bb2-189">Требования к скриншотам</span><span class="sxs-lookup"><span data-stu-id="21bb2-189">Requirements for screenshots</span></span>

* <span data-ttu-id="21bb2-190">До пяти скриншотов в списке.</span><span class="sxs-lookup"><span data-stu-id="21bb2-190">Up to five screenshots per listing.</span></span>
* <span data-ttu-id="21bb2-191">Поддерживаемые типы файлов включают PNG, JPEG и GIF.</span><span class="sxs-lookup"><span data-stu-id="21bb2-191">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="21bb2-192">Размеры должны быть 1366x768 пикселей.</span><span class="sxs-lookup"><span data-stu-id="21bb2-192">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="21bb2-193">Максимальный размер 1024 КБ.</span><span class="sxs-lookup"><span data-stu-id="21bb2-193">Maximum size of 1,024 KB.</span></span>

### <a name="best-practices-for-screenshots"></a><span data-ttu-id="21bb2-194">Лучшие практики для скриншотов</span><span class="sxs-lookup"><span data-stu-id="21bb2-194">Best practices for screenshots</span></span>

<span data-ttu-id="21bb2-195">**Рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-195">**Do:**</span></span>

* <span data-ttu-id="21bb2-196">Сосредоточься на возможностях приложения (например, на том, как люди могут общаться с вашим ботом).</span><span class="sxs-lookup"><span data-stu-id="21bb2-196">Focus on your app's capabilities (for example, how people can communicate with your bot).</span></span>
* <span data-ttu-id="21bb2-197">Включите содержимое, которое точно представляет ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="21bb2-197">Include content that accurately represents your app.</span></span>
* <span data-ttu-id="21bb2-198">Используйте текст разумно.</span><span class="sxs-lookup"><span data-stu-id="21bb2-198">Use text judiciously.</span></span>
* Скриншоты кадра с цветом, который отражает ваш бренд и включает маркетинговый контент, аналогичный следующему примеру [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (требования к размеру применяются к всему изображению, а не только к скриншоту): пример экрана сторонних приложений   :::image type="content" source="../../../../assets/images/freshdesk.png" alt-text="Freshdesk":::

<span data-ttu-id="21bb2-200">**Не рекомендуется:**</span><span class="sxs-lookup"><span data-stu-id="21bb2-200">**Don't:**</span></span>

* <span data-ttu-id="21bb2-201">Показ определенных устройств, например телефонов или ноутбуков.</span><span class="sxs-lookup"><span data-stu-id="21bb2-201">Show specific devices, such as phones or laptops.</span></span>
* <span data-ttu-id="21bb2-202">Отображение хрома или пользовательского интерфейса, не в приложении.</span><span class="sxs-lookup"><span data-stu-id="21bb2-202">Display chrome or UI that isn't in your app.</span></span>
* <span data-ttu-id="21bb2-203">Захват любого пользовательского Teams браузера на скриншотах.</span><span class="sxs-lookup"><span data-stu-id="21bb2-203">Capture any Teams or browser UI in your screenshots.</span></span>
* <span data-ttu-id="21bb2-204">Включите макеты, неточно отражающие фактический пользовательский интерфейс приложения, например отображение приложения в браузере вместо вкладки Teams.</span><span class="sxs-lookup"><span data-stu-id="21bb2-204">Include mockups that inaccurately reflect your app's actual UI, such as showing your app in  a browser instead of a Teams tab.</span></span>

<span data-ttu-id="21bb2-205">Дополнительные практические действия см. в [иллюстрации craft effective images for Microsoft app stores.](/office/dev/store/craft-effective-appsource-store-images)</span><span class="sxs-lookup"><span data-stu-id="21bb2-205">For more best practices, see [craft effective images for Microsoft app stores](/office/dev/store/craft-effective-appsource-store-images).</span></span>

## <a name="create-a-video"></a><span data-ttu-id="21bb2-206">Создание видео</span><span class="sxs-lookup"><span data-stu-id="21bb2-206">Create a video</span></span>

<span data-ttu-id="21bb2-207">Видео может быть наиболее эффективным способом общения, почему люди должны использовать ваше приложение.</span><span class="sxs-lookup"><span data-stu-id="21bb2-207">A video can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="21bb2-208">В видео необходимо ответить на следующие вопросы:</span><span class="sxs-lookup"><span data-stu-id="21bb2-208">You should address the following questions in a video:</span></span>

* <span data-ttu-id="21bb2-209">Кто для вашего приложения?</span><span class="sxs-lookup"><span data-stu-id="21bb2-209">Who is your app for?</span></span>
* <span data-ttu-id="21bb2-210">Какие проблемы может решить приложение?</span><span class="sxs-lookup"><span data-stu-id="21bb2-210">What problems can your app solve?</span></span>
* <span data-ttu-id="21bb2-211">Как работает ваше приложение?</span><span class="sxs-lookup"><span data-stu-id="21bb2-211">How does your app work?</span></span>
* <span data-ttu-id="21bb2-212">Какие еще преимущества вы получаете от использования приложения?</span><span class="sxs-lookup"><span data-stu-id="21bb2-212">What other benefits do you get from using your app?</span></span>

<span data-ttu-id="21bb2-213">Если вы включаете видео, оно отображается перед снимками экрана в списке.</span><span class="sxs-lookup"><span data-stu-id="21bb2-213">If you include a video, it appears before your screenshots in the listing.</span></span>

### <a name="best-practices-for-videos"></a><span data-ttu-id="21bb2-214">Лучшие практики для видео</span><span class="sxs-lookup"><span data-stu-id="21bb2-214">Best practices for videos</span></span>

* <span data-ttu-id="21bb2-215">Сохраняйте видео в течение 30-90 секунд.</span><span class="sxs-lookup"><span data-stu-id="21bb2-215">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="21bb2-216">Стремиться к качеству.</span><span class="sxs-lookup"><span data-stu-id="21bb2-216">Aim for quality.</span></span> <span data-ttu-id="21bb2-217">В списке пользователи увидят ваше видео перед снимками экрана.</span><span class="sxs-lookup"><span data-stu-id="21bb2-217">In a listing, users will see your video before screenshots.</span></span>

## <a name="localize-your-store-listing"></a><span data-ttu-id="21bb2-218">Локализовать список магазина</span><span class="sxs-lookup"><span data-stu-id="21bb2-218">Localize your store listing</span></span>

<span data-ttu-id="21bb2-219">Центр партнеров поддерживает [локализованные списки магазинов.](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)</span><span class="sxs-lookup"><span data-stu-id="21bb2-219">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="21bb2-220">Дополнительные сведения см. [в том, как локализовать список Teams приложения.](../../../../concepts/build-and-test/apps-localization.md)</span><span class="sxs-lookup"><span data-stu-id="21bb2-220">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="21bb2-221">См. также</span><span class="sxs-lookup"><span data-stu-id="21bb2-221">See also</span></span>

* [<span data-ttu-id="21bb2-222">Создание эффективных Microsoft 365 магазинов</span><span class="sxs-lookup"><span data-stu-id="21bb2-222">Create effective Microsoft 365 Stores listings</span></span>](/office/dev/store/create-effective-office-store-listings)
* <span data-ttu-id="21bb2-223">Teams руководства по разработке приложений для [копирования, контента и](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) [выражения бренда](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span><span class="sxs-lookup"><span data-stu-id="21bb2-223">Teams app design guidelines for [copy and content](~/concepts/design/design-teams-app-fundamentals.md#copy-and-content) and [brand expression](~/concepts/design/design-teams-app-fundamentals.md#brand-expression)</span></span>
* [<span data-ttu-id="21bb2-224">Рекомендации по товарным знакам и брендам Майкрософт</span><span class="sxs-lookup"><span data-stu-id="21bb2-224">Microsoft Trademark and Brand Guidelines</span></span>](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)

## <a name="next-step"></a><span data-ttu-id="21bb2-225">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="21bb2-225">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="21bb2-226">Подготовка отправки в магазин</span><span class="sxs-lookup"><span data-stu-id="21bb2-226">Prepare your store submission</span></span>](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
