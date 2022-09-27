---
title: Улучшение документации Teams
description: Инструкции по созданию и публикации документации Teams
author: surbhigupta
ms.author: lajanuar
ms.localizationpriority: medium
ms.topic: contributor-guide
ms.openlocfilehash: 4a0c522b5e9d4bcf99ee884de41b1d75846b004a
ms.sourcegitcommit: 377a4b712b50a211851aeecc1029414939945390
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/27/2022
ms.locfileid: "68044667"
---
# <a name="contribute-to-teams-documentation"></a>Улучшение документации Teams

Документация по Teams является частью **библиотеки технической документации Microsoft Learn** . Содержимое организовано в группы, называемые docsets, каждый из которых представляет группу родственных документов, управляемых как одна сущность. Статьи в том же наборе docset имеют то же расширение URL-пути после `learn.microsoft.com`. Например, `/learn.microsoft.com/microsoftteams/...` это начало файлового пути к docset Teams. Статьи о Teams написаны на синтаксисе Markdown и размещаются на GitHub.

## <a name="set-up-your-workspace"></a>Настройка рабочей области

> [!div class="checklist"]
>
> * Установите [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).
> * Установите [Microsoft Visual Studio (](https://code.visualstudio.com/)VS Code).
> * Install [Docs Authoring Pack](https://marketplace.visualstudio.com/items?itemName=docsmsft.docs-authoring-pack) directly from the VS Code Marketplace.
<br>&emsp;&emsp;Или
> [!div class="checklist"]
>
> * Установите в VS Code:

   1. Щелкните  значок расширений на боковой панели действий или воспользуйтесь командой **View => Extensions** или CTRL+SHIFT+X и выполните поиск пакета разработки **документации**.
   1. Нажмите кнопку **Установить**.
   1. После установки кнопка **Установить** изменяется на кнопку **Управление** в виде шестеренки.

## <a name="review-the-microsoft-docs-contributor-guide"></a>Просмотрите руководство Документация Майкрософт участника

Руководство для участников содержит инструкции по созданию, публикации и обновлению технического содержимого на **платформе Microsoft Learn** .

## <a name="microsoft-writing-style-and-content-guides"></a>Руководства Корпорации Майкрософт по написанию, стилю и содержимому 

* **[Руководство по стилю письма Майкрософт](/style-guide/welcome)**. Руководство по стилю письма (Майкрософт) — это комплексный ресурс для технических писателей, отражающий современный подход корпорации Майкрософт к голосу и стилю. Для удобства добавьте это интерактивное руководство в меню **Избранное** браузера.

* **[Написание содержимого для разработчиков](/style-guide/developer-content/)**. Содержимое, специфичное для Teams, предназначено для аудитории разработчиков, обладающих глубоким пониманием основных концепций программирования и процессов. Важно предоставить четкие и технически точные сведения, сохраняя тон и стиль корпорации Майкрософт.

* **[Написание пошаговых инструкций](/style-guide/procedures-instructions/writing-step-by-step-instructions)**. Прикладное и интерактивное взаимодействие пользователей — отличный способ для разработчиков узнать о продуктах и технологиях Майкрософт. Представлять сложные или простые процедуры в прогрессивном формате естественно и понятно пользователям.

## <a name="markdown-reference"></a>Справочник по MarkDown

**Страницы Microsoft Learn** написаны в **синтаксисе MarkDown** и анализируются с помощью [модуля Markdig](https://github.com/lunet-io/markdig) . Дополнительные сведения о конкретных тегах и соглашениях о форматировании см. в [справочнике по Docs Markdown](/contribute/markdown-reference).

## <a name="file-paths"></a>Пути к файлу

При использовании относительных путей и создании ссылок на другие документы важно задать допустимый путь к файлу для гиперссылок в документации. Сборка выполняется на GitHub только в том случае, если путь к файлу правильный и допустимый.

Дополнительные сведения о гиперссылках и путях к файлам см. в разделе [использование ссылок в документации](/contribute/how-to-write-links).

> [!IMPORTANT]
> Чтобы сослаться на статью, которая является **частью** платформы Teams:<br>
> &emsp;&#x2714; Используйте относительный путь без косой черты в начале.<br>
> &emsp;&#x2714; Включите расширение файла Markdown.<br>
>Например, **родительский_каталог/каталог/путь_к_статье.md** — > [создание приложения для Microsoft Teams](../concepts/building-an-app.md) <br><br>
> Чтобы сослаться на статью Microsoft Learn, которая не **является частью** набора документации по платформе Teams, сделайте следующее:<br>
> &emsp;&#x2714; используйте относительный путь, который начинается с косой черты.<br>
> &emsp;&#x2714; Do not include the file extension. <br>
> Например: **/docset/адрес_местонахождения_файла** —> [Работа с Microsoft Teams при помощи API Microsoft Graph](/graph/api/resources/teams-api-overview)<br><br>
> Чтобы ссылаться на страницу за пределами Microsoft Learn, например GitHub, используйте полный `https` путь к файлу.<br>

## <a name="code-samples-and-snippets"></a>Примеры кода и фрагменты кода

Примеры кода играют важную роль для эффективного использования API и пакетов SDK. Хорошо представленные примеры кода могут объяснить механизм работы лучше, чем только описательный текст и инструктивная информация. Примеры кода должны быть точными, краткими, хорошо документированными и понятными для чтения. Код, который легко прочитать, должен быть простым для понимания, тестирования, отладки, обслуживания, изменения и расширения. Дополнительные сведения см. [в разделе о том, как включить код в статью](/contribute/code-in-docs).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Получение обновлений Microsoft Learn и последних объявлений](/teamblog)

## <a name="see-also"></a>См. также

* [Microsoft Learn](/)
* [Руководство для участников документации Microsoft Learn](/contribute)
* [Краткое руководство по стилю и голосовой связи Microsoft Learn](/contribute/style-quick-start)
* [Передний край: советы по удобочитаемости исходного кода](/archive/msdn-magazine/2014/october/cutting-edge-source-code-readability-tips)
* [Документация Teams](/microsoftteams/platform/overview)
* [GitHub](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform)
