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
# <a name="contribute-to-teams-documentation"></a>Внести вклад в Teams документации

Teams документация входит в библиотеку технической документации **Microsoft Docs.** Содержимое организовано в группы под названием docsets, каждая из которых представляет группу связанных документов, управляемых как единое целое. Статьи в том же docset имеют одно и то же расширение пути **URL-адреса** после docs.microsoft.com . Например, `/docs.microsoft.com/microsoftteams/...` это начало пути Teams docset. Teams статьи написаны в синтаксис Markdown и помещались на GitHub.

## <a name="set-up-your-workspace"></a>Настройка рабочего пространства

> [!div class="checklist"]
>
> * Установка [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Установка [Visual Studio Code](https://code.visualstudio.com/) (VS Code).
> * Установите [пакет авторов docs](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) непосредственно из VS Code Marketplace.
<br>&emsp;&emsp; или

> [!div class="checklist"]
>
> * Установка в VS Code:

   1. Выберите **значок** Расширения на боковой панели действий или используйте команду **View => Extensions** или Ctrl+Shift+X и поиск пакета авторов **Microsoft Docs**.
   1. Нажмите кнопку **Установить**.
   1. После установки установите **кнопку** **Управление** передачей.

## <a name="review-the-microsoft-docs-contributors-guide"></a>Просмотрите руководство по вкладчикам Microsoft Docs

Руководство по созданию, публикации и обновлению технического контента на платформе Microsoft Docs содержит руководство по созданию, публикации **и обновлению технического** контента. 

## <a name="microsoft-writing-style-and-content-guides"></a>Руководство по написанию, стилю и контенту Корпорации Майкрософт

* **[Руководство по стилю](/style-guide/welcome)** записи Майкрософт. Руководство по стилю записи Майкрософт является всеобъемлющим ресурсом для технической записи и отражает современный подход Корпорации Майкрософт к голосу и стилю. Для легкой ссылки добавьте это руководство в меню Избранное **браузера.**

* **[Написание](/style-guide/developer-content/)** контента Teams предназначено для аудитории разработчика с фундаментальным пониманием концепций и процессов программирования. Важно предоставить четкие и технически точные сведения, сохраняя при этом тон и стиль Корпорации Майкрософт.

* **[Пошаговая](/style-guide/procedures-instructions/writing-step-by-step-instructions)** написание инструкций. Прикладное и интерактивное обучение — отличный способ для разработчиков узнать о продуктах и технологиях Майкрософт. Представляем сложные или простые процедуры в прогрессивном формате естественно и удобно для пользователей.

## <a name="markdown-reference"></a>Ссылка MarkDown

**Страницы Microsoft Docs** написаны в **синтаксис MarkDown** и разбором с помощью [двигателя Markdig.](https://github.com/lunet-io/markdig) Дополнительные сведения о конкретных тегах и конвенциях форматирования см. в справке [Docs Markdown.](/contribute/markdown-reference)

## <a name="file-paths"></a>Пути файлов

При использовании относительных путей и создании ссылок на другие документы важно установить допустимый путь к файлам для гиперссылок в документации. Сборка успешно GitHub только в том случае, если путь файла правильный или допустимый.
 
Дополнительные сведения о гиперссылках и пути к файлам см. в [документе об использовании ссылок.](/contribute/how-to-write-links)

> [!IMPORTANT]
> Чтобы со ссылкой на статью, которая **является частью** Teams платформы docset:<br>
> &emsp;&#x2714; используйте относительный путь без ведущей косой черты.<br>
> &emsp;&#x2714; включаем расширение файла Markdown.<br>
>Ex: **родительский каталог/каталог/путь** к article.md —> создание [приложения для Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Ссылки на статью библиотеки  Microsoft Docs, которая не входит в Teams платформы:<br>
> &emsp;&#x2714; используйте относительный путь, который начинается с косой черты.<br>
> &emsp;&#x2714; не включай расширение файла. <br> Ex: **/docset/address-to-file-location** —> [Используйте API](/graph/api/resources/teams-api-overview) microsoft Graph для работы с Microsoft Teams<br><br>
> Чтобы ссылаться на страницу за пределами библиотеки Microsoft Docs, например GitHub, используйте полный `https` путь файла.<br>

## <a name="code-samples-and-snippets"></a>Примеры кода и фрагменты

Образцы кода играют важную роль для эффективного использования API и SDKs. Хорошо представленные примеры кода могут сообщить, как все работает более четко, чем описательный текст и учебные сведения только. Образцы кода должны быть точными, краткими, хорошо документированными и удобными для чтения. Простой для чтения код должен быть понятным, тестировать, отлагировать, поддерживать, изменять и расширять. Дополнительные сведения см. [в дополнительных сведениях о том, как включить код в документы.](/contribute/code-in-docs)

## <a name="see-also"></a>См. также

* [Документы Майкрософт](/)
* [руководство по вкладчикам](/contribute)
* [Быстрый запуск стиля и голосового голоса в docs](/contribute/style-quick-start)
* [Передний край: читаемость исходных кодов Советы](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Teams документации](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)


## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Получения обновлений Microsoft Docs и последних объявлений](/teamblog)
