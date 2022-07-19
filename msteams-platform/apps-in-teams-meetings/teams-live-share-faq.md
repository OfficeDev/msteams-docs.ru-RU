---
title: Вопросы и ответы о Live Share
author: surbhigupta
description: В этом модуле вы узнаете больше о часто задаваемых вопросах Live Share.
ms.topic: overview
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 04/07/2022
ms.openlocfilehash: d29318397e388faca93695040914493ecae369a5
ms.sourcegitcommit: 79d525c0be309200e930cdd942bc2c753d0b718c
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/19/2022
ms.locfileid: "66841872"
---
---

# <a name="live-share-sdk-faq"></a>Вопросы и ответы по Live Share SDK

Найдите ответы на распространенные вопросы при использовании Live Share.<br>

<br>

<details>

<summary><b>Могу ли я использовать собственную службу Azure Fluid Relay?</b></summary>

Да. При создании `TeamsFluidClient`класса можно определить собственный`AzureConnectionConfig`. Live Share связывает создаваемые вами контейнеры с собраниями, но вам потребуется создать собственную `ITokenProvider` Azure, чтобы подписывать токены для ваших контейнеров и региональных требований. Дополнительные сведения см. в [документации по Azure Fluid Relay](/azure/azure-fluid-relay/).

<br>

</details>

<details>

<summary><b>Как долго доступны данные, хранящиеся в размещенной службе Live Share?</b></summary>

Любые данные, отправленные или сохраненные через контейнеры Fluid, созданные службой Azure Fluid Relay Live Share, доступны в течение 24 часов. Если вы хотите, чтобы данные сохранялись дольше 24 часов, вы можете заменить нашу размещенную службу Azure Fluid Relay собственной. Кроме того, вы можете использовать своего поставщика хранилища параллельно с размещенной службой Live Share.

<br>

</details>

<details>

<summary><b>Какие типы собраний поддерживает Live Share?</b></summary>

Сейчас поддерживаются только запланированные собрания, и все участники должны быть в календаре собраний. Такие типы собраний, как индивидуальные вызовы, групповые вызовы и собрания сейчас, не поддерживаются.

<br>

</details>

<details>

<summary><b>Будет ли мультимедийный пакет Live Share работать с содержимым DRM?</b></summary>

Нет. Сейчас Teams не поддерживает зашифрованные носители для приложений с вкладками.

<br>

</details>

<details>
<summary><b>Сколько человек может присутствовать на сеансе Live Share?</b></summary>

Сейчас Live Share поддерживает не более 100 участников за сеанс.

<br>

</details>

## <a name="have-more-questions-or-feedback"></a>У вас есть дополнительные вопросы или отзывы?

Вы можете отправлять вопросы и запросы функций в репозиторий SDK для [Live Share SDK](https://github.com/microsoft/live-share-sdk). Используйте тег `live-share` и `microsoft-teams` для публикации практических вопросов об SDK на [Stack Overflow](https://stackoverflow.com/questions/tagged/live-share+microsoft-teams).

## <a name="see-also"></a>См. также

- [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
- [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Справочные документы по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
- [Приложения Teams на собраниях](teams-apps-in-meetings.md)
