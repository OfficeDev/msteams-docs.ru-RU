---
title: Поддерживаемое форматирование текста в разговорах
description: Описывает поддержку форматирования текста в разговорах ботов
keywords: боты разговоры сообщений
ms.topic: how-to
localization_priority: Normal
ms.date: 03/29/2018
ms.openlocfilehash: dfb91e18a2ad895ae5b48c905046a22449304fc6
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566749"
---
# <a name="formatting-bot-messages"></a>Форматирование сообщений бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Вы можете установить дополнительное [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) свойство для управления тем, как отображается текстовое содержимое вашего сообщения.

Microsoft Teams поддерживает следующие варианты форматирования:

| Значение TextFormat | Описание |
| --- | --- |
| равнина | Текст следует рассматривать как необработанный текст без применения форматирования. |
| Markdown | Текст следует рассматривать как форматирование Markdown и по мере необходимости оказывать на канале; увидеть [содержимое текста форматирования для](#formatting-text-content) поддерживаемых стилей. |
| xml | Текст прост XML разметки; увидеть [содержимое текста форматирования для](#formatting-text-content) поддерживаемых стилей. |

## <a name="formatting-text-content"></a>Форматирование текстового контента

Microsoft Teams поддерживает подмножество тегов форматирования Markdown и XML (HTML).

В настоящее время применяются следующие ограничения:

* Текстовые сообщения не поддерживают форматирование таблицы

Для получения информации о форматировании в карты, [Teams карты Справка](~/task-modules-and-cards/cards/cards-reference.md).

### <a name="cross-platform-support"></a>Кросс-платформенный поддержка

Чтобы убедиться, что форматирование работает на всех платформах, поддерживаемых Microsoft Teams, имейте в виду, что некоторые стили в настоящее время поддерживаются не на всех платформах.

| Style                     | Текстовые сообщения | Карты (только XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| заголовок (уровни 1 &ndash; 3) | ✖                  | ✔                |
| ударная попере             | ✖                  | ✔                |
| горизонтальное правило           | ✖                  | ✖                |
| неупорядочеченный список            | ✖                  | ✔                |
| упорядоченный список              | ✖                  | ✔                |
| преформатированный текст         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| гиперссылка                 | ✔                  | ✔                |
| ссылка на изображение                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Поддержка по индивидуальной платформе

Поддержка форматирования текста варьируется в зависимости от типа сообщения и платформы.

#### <a name="text-only-messages"></a>Текстовые сообщения

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| заголовок (уровни 1 &ndash; 3) | ✖       | ✖   | ✖       |
| ударная попере             | ✔       | ✔   | ✖       |
| горизонтальное правило           | ✖       | ✖   | ✖       |
| неупорядочеченный список            | ✔       | ✖   | ✖       |
| упорядоченный список              | ✔       | ✖   | ✖       |
| преформатированный текст         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| гиперссылка                 | ✔       | ✔   | ✔       |
| ссылка на изображение                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Примеры форматирования текста

| Style | Пример | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| заголовок (уровни 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| ударная попере | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| неупорядочеченный список | <ul><li>текст</li><li>текст</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| преформатированный текст | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
