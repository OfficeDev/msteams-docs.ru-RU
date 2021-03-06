---
title: Поддерживаемый форматирование текста в беседах
description: Описывает поддержку форматирования текста в беседах с ботами
keywords: боты беседы сообщений
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

Вы можете настроить необязательный свойство для управления тем, как отрисовка текстового контента [`TextFormat`](/bot-framework/dotnet/bot-builder-dotnet-create-messages#customizing-a-message) сообщения.

Microsoft Teams поддерживает следующие параметры форматирования:

| Значение TextFormat | Описание |
| --- | --- |
| простая | Текст следует рассматривать как необработанные тексты, при этом форматирование не применяется вообще. |
| Markdown | Текст следует рассматривать как форматирование Markdown и отрисовку на канале по мере необходимости; см. [форматирование текстового контента](#formatting-text-content) для поддерживаемых стилей. |
| xml | Текст простой XML-разметки; см. [форматирование текстового контента](#formatting-text-content) для поддерживаемых стилей. |

## <a name="formatting-text-content"></a>Форматирование текстового контента

Microsoft Teams поддерживает подмножество тегов форматирования Markdown и XML (HTML).

В настоящее время применяются следующие ограничения:

* Текстовые сообщения не поддерживают форматирование таблиц

Сведения о форматирования в картах см. в Teams [Справка по карточкам.](~/task-modules-and-cards/cards/cards-reference.md)

### <a name="cross-platform-support"></a>Поддержка на разных платформах

Чтобы гарантировать, что форматирование работает на всех платформах, поддерживаемых Microsoft Teams, следует помнить, что некоторые стили в настоящее время поддерживаются не на всех платформах.

| Style                     | Текстовые сообщения | Карточки (только XML) |
|---------------------------|--------------------|------------------|
| bold                      | ✔                  | ✖                |
| italic                    | ✔                  | ✔                |
| загон (уровни 1 &ndash; 3) | ✖                  | ✔                |
| strikethrough             | ✖                  | ✔                |
| горизонтальное правило           | ✖                  | ✖                |
| необученный список            | ✖                  | ✔                |
| упорядоченный список              | ✖                  | ✔                |
| предформатированный текст         | ✔                  | ✔                |
| blockquote                | ✔                  | ✔                |
| гиперссылка                 | ✔                  | ✔                |
| ссылка на изображение                | ✔                  | ✖                |

### <a name="support-by-individual-platform"></a>Поддержка по отдельной платформе

Поддержка форматирования текста зависит от типа сообщения и платформы.

#### <a name="text-only-messages"></a>Текстовые сообщения

| Style                     | Desktop | iOS | Android |
|---------------------------|---------|-----|---------|
| bold                      | ✔       | ✔   | ✔       |
| italic                    | ✔       | ✔   | ✔       |
| загон (уровни 1 &ndash; 3) | ✖       | ✖   | ✖       |
| strikethrough             | ✔       | ✔   | ✖       |
| горизонтальное правило           | ✖       | ✖   | ✖       |
| необученный список            | ✔       | ✖   | ✖       |
| упорядоченный список              | ✔       | ✖   | ✖       |
| предформатированный текст         | ✔       | ✔   | ✔       |
| blockquote                | ✔       | ✔   | ✔       |
| гиперссылка                 | ✔       | ✔   | ✔       |
| ссылка на изображение                | ✔       | ✔   | ✔       |

### <a name="examples-of-text-formatting"></a>Примеры форматирования текста

| Style | Пример | Markdown | XML (HTML) |
| --- | --- | --- | --- |
| bold | **text** | `**text**` | `<strong>text</strong>` |
| italic | *text* | `*text*` | `<em>text</em>` |
| загон (уровни 1 &ndash; 3) | **Text** | `### Text` | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `~~text~~` | `<strike>text</strike>` |
| необученный список | <ul><li>текст</li><li>текст</li></ul> | `* text`<br>`* text` | `<ul><li>text</li><li>text</li></ul>` |
| упорядоченный список | <ol><li>текст</li><li>текст</li></ol> | `1. text`<br>`2. text` | `<ol><li>text</li><li>text</li></ol>` |
| предформатированный текст | `text` | `` `text` `` | `<pre>text</pre>` |
| blockquote | <blockquote>текст</blockquote> | `>text` | `<blockquote>text</blockquote>` |
| гиперссылка | [Bing](https://www.bing.com/) | `[Bing](https://www.bing.com/)` | `<a href="https://www.bing.com/">Bing</a>` |
| ссылка на изображение | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `![Duck on a rock](http://aka.ms/Fo983c)` | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |
