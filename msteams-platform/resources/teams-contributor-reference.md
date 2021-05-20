---
title: Вклад в Microsoft Teams документацию
description: шаги по созданию и публикации Teams документации
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
# <a name="contributing-to-microsoft-teams-documentation"></a>Вклад в Microsoft Teams документацию

[Teams документация](/microsoftteams/platform/overview) является частью библиотеки [технической документации Microsoft Docs.](https://docs.microsoft.com/) Содержимое организовано в группы, называемые docsets, каждая из которых представляет группу связанных документов, управляемых как единое целое. Статьи в том же docset имеют то же расширение пути URL *после документов <span></span> .microsoft.com*.  Например, `/docs.microsoft.com/microsoftteams/...` это начало пути файла Teams docset. Teams статьи написаны в [синтаксисе MarkDown](#markdown-reference) и размещены [на GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform).

## <a name="set-up-your-workspace"></a>Настройка рабочего пространства

> [!div class="checklist"]
>
> * Установка [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Установка [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Установите [пакет авторов документов](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) прямо с VS Code Marketplace.
<br>&emsp;&emsp; или

> [!div class="checklist"]
>
> * Установка изнутри VS Code:

   1. Выберите **значок расширений** на боковой стойке активности **или используйте команду View и> Extensions** (Ctrl-Shift-X) и ищите *пакет авторов документов* (Microsoft).
   1. Выберите **кнопку Установить.**
   1. Как только установка завершена, **кнопка Установки** будет переверха к **кнопке Управления** передач.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Просмотрите руководство по авторам документов Майкрософт

Руководство [для участников](/contribute) предлагает направление для создания, публикации и обновления технического контента на платформе Microsoft Docs.

## <a name="microsoft-writing-style-and-content-guides"></a>Руководство по написанию, стилю и контенту майкрософт

* **[Руководство по стилю письма корпорации Майкрософт](/style-guide/welcome)**. Рассмотрите возможность добавления этого онлайн-руководства в меню **избранного браузера.** Это комплексный ресурс для современного технического письма и отражает современный подход Корпорации Майкрософт к голосу и стилю.

* **[Написание содержимого разработчика](/style-guide/developer-content/)**. Teams контент ориентирован на аудиторию разработчиков с фундаментальным пониманием концепций и процессов программирования. Важно, чтобы вы предоставили четкую, технически точную информацию убедительным образом, сохраняя при этом тон и стиль корпорации Майкрософт.

* **[Написание пошагових инструкций.](/style-guide/procedures-instructions/writing-step-by-step-instructions)** Прикладной и интерактивный опыт является отличным способом для разработчиков, чтобы узнать о продуктах и технологиях Microsoft. Представление сложных или простых процедур в прогрессивном формате является естественным и удобным для пользователя.

## <a name="markdown-reference"></a>Ссылка markDown

 Страницы Microsoft Docs написаны в синтаксисе MarkDown и разобрана с [помощью движка Markdig.](https://github.com/lunet-io/markdig) *Пожалуйста,* [посмотрите Ссылку Docs Markdown](/contribute/markdown-reference) для конкретных тегов и конвенций форматирования.

## <a name="file-paths"></a>Пути файла

Настройка действительного пути файла для гиперссылок в документации может быть сложной задачей, особенно при использовании относительных путей и создании ссылок на другие документы.  Сборка не будет успешной на GitHub если путь файла неправильный или недействительный.

Для получения дополнительной информации о гиперссылки и пути файла, [см.](/contribute/how-to-write-links)

>[!IMPORTANT]
> Ссылаться на статью, которая *является частью* Teams платформы docset:<br>
> &emsp;&#x2714; использовать относительный путь без ведущего вперед черту.<br>
> &emsp;&#x2714; включите расширение файла Markdown.<br>
>Ex:  **родительский каталог/каталог/путь к article.md** -> `[Building an app for Microsoft Teams](../concepts/building-an-app.md)` <br><br>
> Ссылка на статью библиотеки Microsoft Docs, *которая не входит в* Teams платформы:<br>
> &emsp;&#x2714; использовать относительный путь, который начинается с перемотка вперед.<br>
> &emsp;&#x2714; не включает расширение файла. <br> Ex:  **/docset/адрес-файл-место** -> `[Use the Microsoft Graph API to work with Microsoft Teams](/graph/api/resources/teams-api-overview)`<br><br>
> Для ссылки на страницу за пределами библиотеки Microsoft Docs, например GitHub, используйте полный `https` путь файла.<br>

## <a name="code-samples-and-snippets"></a>Образцы кода и фрагменты

Образцы кода играют важную роль в оказании разработчикам помощи в успешном использовании API и SDKs. Хорошо представленные образцы кода могут сообщить, как все работает более четко, чем описательный текст и учебная информация в одиночку. Образцы кода должны быть точными, краткими, хорошо документированными и, самое главное, дружественными к читателю. Код, который легко читается, также легко понять, протестировать, отладить, поддерживать, изменять и расширять. Для получения дополнительной информации [узнайте, как включить код в документы.](/contribute/code-in-docs)

## <a name="see-also"></a>См. также

* [Документы стиль и голос быстрый старт](/contribute/style-quick-start)
* [Cutting Edge : Источник кода Читаемость Советы](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips).

> [!div class="nextstepaction"]
> [Получайте обновления Документов Майкрософт и последние объявления](/teamblog)
