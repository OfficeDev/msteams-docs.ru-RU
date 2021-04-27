---
title: Участие в документации Microsoft Teams
description: действия по созданию и публикации документации Teams
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: a6742b8b994cc3752df923db75a3d7d77cbebd83
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019673"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Участие в документации Microsoft Teams

[Документация teams](/microsoftteams/platform/overview) входит в библиотеку технической документации [Microsoft Docs.](https://docs.microsoft.com/) Содержимое организовано в группы под названием docsets, каждая из которых представляет группу связанных документов, управляемых как единое целое. Статьи в том же docset имеют одно и то же расширение пути URL-адреса после *<span></span> документы .microsoft.com*.  Например,  `/docs.microsoft.com/microsoftteams/...`   это начало пути файлов teams docset. Статьи Teams написаны в [синтаксис MarkDown](#markdown-reference) и помещались в [GitHub.](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)

## <a name="set-up-your-workspace"></a>Настройка рабочего пространства

> [!div class="checklist"]
>
> * Установка [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Установка [Visual Studio кода](https://code.visualstudio.com/) (VS Code).
> * Установка [пакета авторов docs непосредственно](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) с рынка кода VS
<br>&emsp;&emsp; или

> [!div class="checklist"]
>
> * Установка из кода VS:

   1. Выберите **значок** Расширения на боковой панели действий или используйте команду **View => Extensions** (Ctrl+Shift+X) и поиск пакета авторов *docs* (Microsoft).
   1. Выберите **кнопку Установка.**
   1. После завершения установки кнопка **Install** изменится на кнопку **Управление** передачей.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Просмотрите руководство по вкладчикам Microsoft Docs

Руководство [по созданию,](/contribute) публикации и обновлению технического контента на платформе Microsoft Docs предоставляет руководство по созданию, публикации и обновлению технического контента. *См. также,* [стиль docs и быстрое начало голоса](/contribute/style-quick-start) .

## <a name="microsoft-writing-style-and-content-guides"></a>Руководство по написанию, стилю и контенту Корпорации Майкрософт

* **[Руководство по стилю записи Microsoft](/style-guide/welcome)**. Рассмотрите возможность добавления этого руководства по Интернету в меню **Избранное браузера.** Это комплексный ресурс для современной технической записи и отражает современный подход Корпорации Майкрософт к голосу и стилю.

* **[Написание контента разработчика](/style-guide/developer-content/)**. Контент для групп предназначен для аудитории разработчика с фундаментальным пониманием концепций и процессов программирования. Важно предоставить четкие и технически точные сведения, сохраняя при этом тон и стиль Корпорации Майкрософт.

* **[Написание пошагових инструкций.](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Прикладные и интерактивные функции — это отличный способ для разработчиков узнать о продуктах и технологиях Майкрософт. Представлять сложные или простые процедуры в прогрессивном формате естественно и удобно.

## <a name="markdown-reference"></a>Ссылка MarkDown

 Страницы Microsoft Docs написаны в синтаксис MarkDown и разбором с помощью [двигателя Markdig.](https://github.com/lunet-io/markdig) См. *ссылку* [docs Markdown](/contribute/markdown-reference) для определенных тегов и соглашений форматирования.

## <a name="file-paths"></a>Пути файлов

Настройка допустимого пути для гиперссылки в документации может быть сложной задачей, особенно при использовании относительных путей и создании ссылок на другие документы.  Сборка не будет успешной в GitHub, если путь файла неправильный или недействительный.

Дополнительные сведения о гиперссылках  и пути к файлам см. в документе [Использование ссылок.](/contribute/how-to-write-links)

>[!IMPORTANT]
> Ссылку на статью, *которая входит в docset* платформы Teams:<br>
> &emsp;&#x2714; используйте относительный путь без ведущей косой черты.<br>
> &emsp;&#x2714; включаем расширение файла Markdown.<br>
>Ex:  **parent directory/directory/path-to-article.md** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Ссылки на статью библиотеки Microsoft Docs, которая не *входит* в docset платформы Teams:<br>
> &emsp;&#x2714; используйте относительный путь, который начинается с косой черты.<br>
> &emsp;&#x2714; не включайте расширение файла. <br> Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Чтобы ссылаться на страницу за пределами библиотеки Microsoft Docs, например GitHub, используйте полный `https` путь к файлу.<br>

## <a name="code-samples-and-snippets"></a>Примеры кода и фрагменты

Примеры кода играют важную роль в том, чтобы помочь разработчикам успешно использовать API и SDKs. Хорошо представленные примеры кода могут сообщать о том, как все работает более четко, чем только описательный текст и инструкции. Образцы кода должны быть точными, краткими, хорошо документированными и, самое главное, удобными для чтения. Простой для чтения код также легко понять, протестировать, отлагировать, поддерживать, изменять и расширять. *Узнайте,* [как включить код в документы.](/contribute/code-in-docs) Советы по читаемости *см. также* [в раздел Cutting Edge : Советы по читаемости исходных кодов.](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)

> [!div class="nextstepaction"]
> [Получения обновлений Microsoft Docs и последних объявлений](/teamblog)
