---
title: Участие в Microsoft Teams документации
description: действия по созданию и публикации Teams документации
author: laujan
ms.author: lajanuar
localization_priority: Normal
ms.topic: contributor-guide
ms.openlocfilehash: 52253bb096857e2cb883295c8ae6b58518506d9a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566231"
---
# <a name="contributing-to-microsoft-teams-documentation"></a>Участие в Microsoft Teams документации

[Teams документация](/microsoftteams/platform/overview) входит в библиотеку технической документации [Microsoft Docs.](https://docs.microsoft.com/) Содержимое организовано в группы под названием docsets, каждая из которых представляет группу связанных документов, управляемых как единое целое. Статьи в том же docset имеют одно и то же расширение пути URL-адреса после *<span></span> документы .microsoft.com*.  Например, `/docs.microsoft.com/microsoftteams/...` это начало пути Teams docset. Teams статьи написаны в [синтаксис MarkDown](#markdown-reference) и помещались [в GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Настройка рабочего пространства

> [!div class="checklist"]
>
> * Установка [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Установка [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Установите [пакет авторов docs](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) непосредственно из VS Code Marketplace.
<br>&emsp;&emsp; или

> [!div class="checklist"]
>
> * Установка из VS Code:

   1. Выберите **значок** Расширения на боковой панели действий или используйте команду **View => Extensions** (Ctrl+Shift+X) и поиск пакета авторов *docs* (Microsoft).
   1. Выберите **кнопку Установка.**
   1. После завершения установки кнопка **Install** изменится на кнопку **Управление** передачей.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Просмотрите руководство по вкладчикам Microsoft Docs

Руководство [по созданию,](/contribute) публикации и обновлению технического контента на платформе Microsoft Docs предоставляет руководство по созданию, публикации и обновлению технического контента.

## <a name="microsoft-writing-style-and-content-guides"></a>Руководство по написанию, стилю и контенту Корпорации Майкрософт

* **[Руководство по стилю записи Microsoft](/style-guide/welcome)**. Рассмотрите возможность добавления этого руководства по Интернету в меню **Избранное браузера.** Это комплексный ресурс для современной технической записи и отражает современный подход Корпорации Майкрософт к голосу и стилю.

* **[Написание контента разработчика](/style-guide/developer-content/)**. Teams контент предназначен для аудитории разработчика с фундаментальным пониманием концепций и процессов программирования. Важно предоставить четкие и технически точные сведения, сохраняя при этом тон и стиль Корпорации Майкрософт.

* **[Написание пошагових инструкций.](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Прикладные и интерактивные функции — это отличный способ для разработчиков узнать о продуктах и технологиях Майкрософт. Представлять сложные или простые процедуры в прогрессивном формате естественно и удобно.

## <a name="markdown-reference"></a>Ссылка MarkDown

 Страницы Microsoft Docs написаны в синтаксис MarkDown и разбором с помощью [двигателя Markdig.](https://github.com/lunet-io/markdig) См. *ссылку* [docs Markdown](/contribute/markdown-reference) для определенных тегов и соглашений форматирования.

## <a name="file-paths"></a>Пути файлов

Настройка допустимого пути для гиперссылки в документации может быть сложной задачей, особенно при использовании относительных путей и создании ссылок на другие документы.  Сборка не будет успешной в GitHub, если путь файла неправильный или недействительный.

Дополнительные сведения о гиперссылках и пути к файлам см. в документе [Использование ссылок.](/contribute/how-to-write-links)

>[!IMPORTANT]
> Чтобы со ссылкой на статью, которая *является частью* Teams платформы docset:<br>
> &emsp;&#x2714; используйте относительный путь без ведущей косой черты.<br>
> &emsp;&#x2714; включаем расширение файла Markdown.<br>
>Ex:  **parent directory/directory/path-to-article.md** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Ссылки на статью библиотеки  Microsoft Docs, которая не входит в Teams платформы:<br>
> &emsp;&#x2714; используйте относительный путь, который начинается с косой черты.<br>
> &emsp;&#x2714; не включайте расширение файла. <br> Ex:  **/docset/address-to-file-location** —> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Чтобы ссылаться на страницу за пределами библиотеки Microsoft Docs, например GitHub, используйте полный `https` путь файла.<br>

## <a name="code-samples-and-snippets"></a>Примеры кода и фрагменты

Примеры кода играют важную роль в том, чтобы помочь разработчикам успешно использовать API и SDKs. Хорошо представленные примеры кода могут сообщать о том, как все работает более четко, чем только описательный текст и инструкции. Образцы кода должны быть точными, краткими, хорошо документированными и, самое главное, удобными для чтения. Простой для чтения код также легко понять, протестировать, отлагировать, поддерживать, изменять и расширять. Дополнительные сведения см. [в дополнительных сведениях о том, как включить код в документы.](/contribute/code-in-docs)

## <a name="see-also"></a>См. также

* [Быстрый запуск стиля и голосового голоса в docs](/contribute/style-quick-start)
* [Передний край: читаемость исходных кодов Советы](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Получения обновлений Microsoft Docs и последних объявлений](/teamblog)
