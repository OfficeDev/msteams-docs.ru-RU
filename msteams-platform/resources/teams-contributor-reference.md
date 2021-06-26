---
title: Внести вклад в Teams документации
description: действия по созданию и публикации Teams документации
author: surbhigupta
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a567b0462397780650d6173df9dae1b340a06f97
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140518"
---
# <a name="contribute-to-teams-documentation"></a><span data-ttu-id="b50f0-103">Внести вклад в Teams документации</span><span class="sxs-lookup"><span data-stu-id="b50f0-103">Contribute to Teams documentation</span></span>

<span data-ttu-id="b50f0-104">Teams документация входит в библиотеку технической документации **Microsoft Docs.**</span><span class="sxs-lookup"><span data-stu-id="b50f0-104">Teams documentation is part of the **Microsoft Docs** technical documentation library.</span></span> <span data-ttu-id="b50f0-105">Содержимое организовано в группы под названием docsets, каждая из которых представляет группу связанных документов, управляемых как единое целое.</span><span class="sxs-lookup"><span data-stu-id="b50f0-105">The content is organized into groups called docsets, each representing a group of related documents managed as a single entity.</span></span> <span data-ttu-id="b50f0-106">Статьи в том же docset имеют одно и то же расширение пути **URL-адреса** после docs.microsoft.com .</span><span class="sxs-lookup"><span data-stu-id="b50f0-106">Articles in the same docset have the same URL path extension after **docs.microsoft.com**.</span></span> <span data-ttu-id="b50f0-107">Например, `/docs.microsoft.com/microsoftteams/...` это начало пути Teams docset.</span><span class="sxs-lookup"><span data-stu-id="b50f0-107">For example, `/docs.microsoft.com/microsoftteams/...` is the beginning of the Teams docset file path.</span></span> <span data-ttu-id="b50f0-108">Teams статьи написаны в синтаксис Markdown и помещались на GitHub.</span><span class="sxs-lookup"><span data-stu-id="b50f0-108">Teams articles are written in Markdown syntax and hosted on GitHub.</span></span>

## <a name="set-up-your-workspace"></a><span data-ttu-id="b50f0-109">Настройка рабочего пространства</span><span class="sxs-lookup"><span data-stu-id="b50f0-109">Set up your workspace</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b50f0-110">Установка [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span><span class="sxs-lookup"><span data-stu-id="b50f0-110">Install [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).</span></span>
> * <span data-ttu-id="b50f0-111">Установка [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span><span class="sxs-lookup"><span data-stu-id="b50f0-111">Install [Visual Studio Code](https://code.visualstudio.com/) (VS Code).</span></span>
> * <span data-ttu-id="b50f0-112">Установите [пакет авторов docs](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) непосредственно из VS Code Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b50f0-112">Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.</span></span>
<br><span data-ttu-id="b50f0-113">&emsp;&emsp; или</span><span class="sxs-lookup"><span data-stu-id="b50f0-113">&emsp;&emsp; or</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b50f0-114">Установка в VS Code:</span><span class="sxs-lookup"><span data-stu-id="b50f0-114">Install within VS Code:</span></span>

   1. <span data-ttu-id="b50f0-115">Выберите **значок** Расширения на боковой панели действий или используйте команду **View => Extensions** или Ctrl+Shift+X и поиск пакета авторов **Microsoft Docs**.</span><span class="sxs-lookup"><span data-stu-id="b50f0-115">Select the **Extensions icon** on the side activity bar or use the **View => Extensions** command or Ctrl+Shift+X and, search for **Microsoft Docs Authoring Pack**.</span></span>
   1. <span data-ttu-id="b50f0-116">Нажмите кнопку **Установить**.</span><span class="sxs-lookup"><span data-stu-id="b50f0-116">Select **Install**.</span></span>
   1. <span data-ttu-id="b50f0-117">После установки установите **кнопку** **Управление** передачей.</span><span class="sxs-lookup"><span data-stu-id="b50f0-117">After installation, the **Install** changes to the **Manage** gear button.</span></span>

## <a name="review-the-microsoft-docs-contributors-guide"></a><span data-ttu-id="b50f0-118">Просмотрите руководство по вкладчикам Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="b50f0-118">Review the Microsoft Docs Contributors Guide</span></span>

<span data-ttu-id="b50f0-119">Руководство по созданию, публикации и обновлению технического контента на платформе Microsoft Docs содержит руководство по созданию, публикации **и обновлению технического** контента.</span><span class="sxs-lookup"><span data-stu-id="b50f0-119">The contributors guide provides direction to create, publish, and update technical content on the **Microsoft Docs** platform.</span></span> 

## <a name="microsoft-writing-style-and-content-guides"></a><span data-ttu-id="b50f0-120">Руководство по написанию, стилю и контенту Корпорации Майкрософт</span><span class="sxs-lookup"><span data-stu-id="b50f0-120">Microsoft Writing, Style, and Content Guides</span></span>

* <span data-ttu-id="b50f0-121">**[Руководство по стилю](/style-guide/welcome)** записи Майкрософт. Руководство по стилю записи Майкрософт является всеобъемлющим ресурсом для технической записи и отражает современный подход Корпорации Майкрософт к голосу и стилю.</span><span class="sxs-lookup"><span data-stu-id="b50f0-121">**[Microsoft Writing Style Guide](/style-guide/welcome)**: Microsoft Writing Style Guide is a comprehensive resource for technical writing and reflects Microsoft's modern approach to voice and style.</span></span> <span data-ttu-id="b50f0-122">Для легкой ссылки добавьте это руководство в меню Избранное **браузера.**</span><span class="sxs-lookup"><span data-stu-id="b50f0-122">For easy reference, add this online guide to your browser's **Favorites** menu.</span></span>

* <span data-ttu-id="b50f0-123">**[Написание](/style-guide/developer-content/)** контента Teams предназначено для аудитории разработчика с фундаментальным пониманием концепций и процессов программирования.</span><span class="sxs-lookup"><span data-stu-id="b50f0-123">**[Writing developer content](/style-guide/developer-content/)**: Teams specific content is aimed at a developer audience with a fundamental understanding of programming concepts and processes.</span></span> <span data-ttu-id="b50f0-124">Важно предоставить четкие и технически точные сведения, сохраняя при этом тон и стиль Корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b50f0-124">It is important that you must provide clear, technically accurate information in a compelling manner while maintaining Microsoft's tone and style.</span></span>

* <span data-ttu-id="b50f0-125">**[Пошаговая](/style-guide/procedures-instructions/writing-step-by-step-instructions)** написание инструкций. Прикладное и интерактивное обучение — отличный способ для разработчиков узнать о продуктах и технологиях Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="b50f0-125">**[Writing step-by-step instructions](/style-guide/procedures-instructions/writing-step-by-step-instructions)**: Applied and interactive experiences are a great way for developers to learn about Microsoft products and technologies.</span></span> <span data-ttu-id="b50f0-126">Представляем сложные или простые процедуры в прогрессивном формате естественно и удобно для пользователей.</span><span class="sxs-lookup"><span data-stu-id="b50f0-126">Presenting complex or simple procedures in a progressive format is natural and user friendly.</span></span>

## <a name="markdown-reference"></a><span data-ttu-id="b50f0-127">Ссылка MarkDown</span><span class="sxs-lookup"><span data-stu-id="b50f0-127">MarkDown reference</span></span>

<span data-ttu-id="b50f0-128">**Страницы Microsoft Docs** написаны в **синтаксис MarkDown** и разбором с помощью [двигателя Markdig.](https://github.com/lunet-io/markdig)</span><span class="sxs-lookup"><span data-stu-id="b50f0-128">**Microsoft Docs** pages are written in **MarkDown** syntax and parsed through a [Markdig](https://github.com/lunet-io/markdig) engine.</span></span> <span data-ttu-id="b50f0-129">Дополнительные сведения о конкретных тегах и конвенциях форматирования см. в справке [Docs Markdown.](/contribute/markdown-reference)</span><span class="sxs-lookup"><span data-stu-id="b50f0-129">For more information on specific tags and formatting conventions, see [Docs Markdown reference](/contribute/markdown-reference).</span></span>

## <a name="file-paths"></a><span data-ttu-id="b50f0-130">Пути файлов</span><span class="sxs-lookup"><span data-stu-id="b50f0-130">File Paths</span></span>

<span data-ttu-id="b50f0-131">При использовании относительных путей и создании ссылок на другие документы важно установить допустимый путь к файлам для гиперссылок в документации.</span><span class="sxs-lookup"><span data-stu-id="b50f0-131">When using relative paths and creating links to other docsets, it is important to set a valid file path for hyperlinks in your documentation.</span></span> <span data-ttu-id="b50f0-132">Сборка успешно GitHub только в том случае, если путь файла правильный или допустимый.</span><span class="sxs-lookup"><span data-stu-id="b50f0-132">Your build succeeds on GitHub only if the file path is correct or valid.</span></span>
 
<span data-ttu-id="b50f0-133">Дополнительные сведения о гиперссылках и пути к файлам см. в [документе об использовании ссылок.](/contribute/how-to-write-links)</span><span class="sxs-lookup"><span data-stu-id="b50f0-133">For more information on hyperlinks and file paths, see [use links in documentation](/contribute/how-to-write-links).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b50f0-134">Чтобы со ссылкой на статью, которая **является частью** Teams платформы docset:</span><span class="sxs-lookup"><span data-stu-id="b50f0-134">To reference an article that is **part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="b50f0-135">&emsp;&#x2714; используйте относительный путь без ведущей косой черты.</span><span class="sxs-lookup"><span data-stu-id="b50f0-135">&emsp;&#x2714; Use a relative path without a leading forward slash.</span></span><br>
> <span data-ttu-id="b50f0-136">&emsp;&#x2714; включаем расширение файла Markdown.</span><span class="sxs-lookup"><span data-stu-id="b50f0-136">&emsp;&#x2714; Include the Markdown file extension.</span></span><br>
><span data-ttu-id="b50f0-137">Ex: **родительский каталог/каталог/путь** к article.md —> создание [приложения для Microsoft Teams](../concepts/building-an-app.md)</span><span class="sxs-lookup"><span data-stu-id="b50f0-137">Ex:  **parent directory/directory/path-to-article.md** —> [Building an app for Microsoft Teams](../concepts/building-an-app.md)</span></span> <br><br>
> <span data-ttu-id="b50f0-138">Ссылки на статью библиотеки  Microsoft Docs, которая не входит в Teams платформы:</span><span class="sxs-lookup"><span data-stu-id="b50f0-138">To reference a Microsoft Docs library article that **is not part of** the Teams platform docset:</span></span><br>
> <span data-ttu-id="b50f0-139">&emsp;&#x2714; используйте относительный путь, который начинается с косой черты.</span><span class="sxs-lookup"><span data-stu-id="b50f0-139">&emsp;&#x2714; Use a relative path that begins with a forward slash.</span></span><br>
> <span data-ttu-id="b50f0-140">&emsp;&#x2714; не включай расширение файла.</span><span class="sxs-lookup"><span data-stu-id="b50f0-140">&emsp;&#x2714; Do not include the file extension.</span></span> <br> <span data-ttu-id="b50f0-141">Ex: **/docset/address-to-file-location** —> [Используйте API](/graph/api/resources/teams-api-overview) microsoft Graph для работы с Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="b50f0-141">Ex:  **/docset/address-to-file-location** —> [Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)</span></span><br><br>
> <span data-ttu-id="b50f0-142">Чтобы ссылаться на страницу за пределами библиотеки Microsoft Docs, например GitHub, используйте полный `https` путь файла.</span><span class="sxs-lookup"><span data-stu-id="b50f0-142">To reference a page outside of the Microsoft Docs library, such as GitHub, use the full `https` file path.</span></span><br>

## <a name="code-samples-and-snippets"></a><span data-ttu-id="b50f0-143">Примеры кода и фрагменты</span><span class="sxs-lookup"><span data-stu-id="b50f0-143">Code Samples and Snippets</span></span>

<span data-ttu-id="b50f0-144">Образцы кода играют важную роль для эффективного использования API и SDKs.</span><span class="sxs-lookup"><span data-stu-id="b50f0-144">Code samples play an important role to use APIs and SDKs effectively.</span></span> <span data-ttu-id="b50f0-145">Хорошо представленные примеры кода могут сообщить, как все работает более четко, чем описательный текст и учебные сведения только.</span><span class="sxs-lookup"><span data-stu-id="b50f0-145">Well presented code samples can communicate how things work more clearly than descriptive text and instructional information alone.</span></span> <span data-ttu-id="b50f0-146">Образцы кода должны быть точными, краткими, хорошо документированными и удобными для чтения.</span><span class="sxs-lookup"><span data-stu-id="b50f0-146">Your code samples must be accurate, concise, well documented, and reader friendly.</span></span> <span data-ttu-id="b50f0-147">Простой для чтения код должен быть понятным, тестировать, отлагировать, поддерживать, изменять и расширять.</span><span class="sxs-lookup"><span data-stu-id="b50f0-147">Code that is easy to read must be easy to understand, test, debug, maintain, modify, and extend.</span></span> <span data-ttu-id="b50f0-148">Дополнительные сведения см. [в дополнительных сведениях о том, как включить код в документы.](/contribute/code-in-docs)</span><span class="sxs-lookup"><span data-stu-id="b50f0-148">For more information, see [how to include code in docs](/contribute/code-in-docs).</span></span>

## <a name="see-also"></a><span data-ttu-id="b50f0-149">См. также</span><span class="sxs-lookup"><span data-stu-id="b50f0-149">See also</span></span>

* [<span data-ttu-id="b50f0-150">Документы Майкрософт</span><span class="sxs-lookup"><span data-stu-id="b50f0-150">Microsoft Docs</span></span>](/)
* [<span data-ttu-id="b50f0-151">руководство по вкладчикам</span><span class="sxs-lookup"><span data-stu-id="b50f0-151">contributors guide</span></span>](/contribute)
* [<span data-ttu-id="b50f0-152">Быстрый запуск стиля и голосового голоса в docs</span><span class="sxs-lookup"><span data-stu-id="b50f0-152">Docs style and voice quick start</span></span>](/contribute/style-quick-start)
* [<span data-ttu-id="b50f0-153">Передний край: читаемость исходных кодов Советы</span><span class="sxs-lookup"><span data-stu-id="b50f0-153">Cutting Edge : Source Code Readability Tips</span></span>](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [<span data-ttu-id="b50f0-154">Teams документации</span><span class="sxs-lookup"><span data-stu-id="b50f0-154">Teams documentation</span></span>](/microsoftteams/platform/overview)
* [<span data-ttu-id="b50f0-155">GitHub</span><span class="sxs-lookup"><span data-stu-id="b50f0-155">GitHub</span></span>](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a><span data-ttu-id="b50f0-156">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="b50f0-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b50f0-157">Получения обновлений Microsoft Docs и последних объявлений</span><span class="sxs-lookup"><span data-stu-id="b50f0-157">Get Microsoft Docs updates and the latest announcements</span></span>](/teamblog)
