---
title: Поддерживаемое форматирование текста в беседах
description: Описывается поддержка форматирования текста в botовых беседах
keywords: Обмен сообщениями Боты
ms.date: 03/29/2018
ms.openlocfilehash: cc6cba697a1f6907bfb13b94740e7bf9e92596da
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675198"
---
# <a name="formatting-bot-messages"></a>Форматирование сообщений Bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Можно задать необязательное [`TextFormat`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) свойство, чтобы управлять отображением текстового контента сообщения.

Microsoft Teams поддерживает следующие параметры форматирования:

| Значение TextFormat | Описание |
| --- | --- |
| содержимое | Текст должен рассматриваться как необработанный текст без форматирования. |
| Markdown | Текст должен рассматриваться как форматирование Markdown и отрисовывается в канале по мере необходимости; Дополнительные сведения о [форматировании текстовых контентов](#formatting-text-content) для поддерживаемых стилей |
| язык | Текст представляет собой простую разметку XML; Дополнительные сведения о [форматировании текстовых контентов](#formatting-text-content) для поддерживаемых стилей |

## <a name="formatting-text-content"></a>Форматирование текстового содержимого

Microsoft Teams поддерживает подмножество тегов форматирования Markdown и XML (HTML).

В настоящее время применяются следующие ограничения:

* Текстовые сообщения не поддерживают форматирование таблиц

Сведения о форматировании карточек можно найти в статье [Справочник по карточкам Teams](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Поддержка нескольких платформ

Чтобы ваше форматирование применялось на всех платформах, поддерживаемых Microsoft Teams, обратите внимание на то, что некоторые стили в настоящее время не поддерживаются на всех платформах.

| Стиль                     | Текстовые сообщения | Cards (только XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| Верхний колонтитул (уровни&ndash;1 3) | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| Горизонтальная линейка           | ✖                  | ✖                |
| неупорядоченный список            | ✖                  | ✔                |
| упорядоченный список              | ✖                  | ✔                |
| предварительно отформатированный текст         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| гиперссылка                 | ✔                  | ✔                |
| Ссылка на изображение                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Поддержка отдельными платформами

Поддержка форматирования текста зависит от типа сообщения и платформы.

#### <a name="text-only-messages"></a>Текстовые сообщения

| Стиль                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| Верхний колонтитул (уровни&ndash;1 3) | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| Горизонтальная линейка           | ✖       | ✖   | ✖       |
| неупорядоченный список            | ✔       | ✖   | ✖       |
| упорядоченный список              | ✔       | ✖   | ✖       |
| предварительно отформатированный текст         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| гиперссылка                 | ✔       | ✔   | ✔       |
| Ссылка на изображение                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Примеры форматирования текста

| Стиль | Пример | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| Верхний колонтитул (уровни&ndash;1 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| неупорядоченный список | <ul><li>текст</li><li>текст</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| предварительно отформатированный текст | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| Ссылка на изображение | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
