---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании настольного клиента Microsoft Teams
ms.topic: how-to
keywords: devtools отладка мобильных средств разработки настольных компьютеров chrome для настольных компьютеров
ms.openlocfilehash: 7bd9403a74fd33619a2f8ac1b4b3a4c74a21175d
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654393"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools для вкладок Microsoft Teams

Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 на Windows или Command-Option-I на MacOS. DevTools предоставляет вам доступ к:

1. Просмотр журналов консоли.
1. Просмотр или изменение HTML-запросов, CSS и сетевых запросов во время работы.
1. Добавьте breakpoints в код JavaScript и выполните интерактивную отладку.

> [!NOTE]
> Эта функция доступна только для клиентов на настольных компьютерах и Android **после** Developer Preview включена. Дополнительные сведения см. в [обзоре Как включить предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)

## <a name="access-devtools-in-the-desktop"></a>Доступ к DevTools на рабочем столе

Несмотря на то, что веб-версия и десктопная версия Teams практически одинаковы, существуют некоторые различия в проверке подлинности. Иногда единственный способ выяснить, что происходит, это использовать DevTools. Чтобы использовать DevTools в настольном клиенте, необходимо:

1. Убедитесь, что вы [включили предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)
1. Откройте вкладку, чтобы вам было что проверить с помощью DevTools.
1. Откройте DevTools одним из следующих способов:
    * **Windows.** Выберите значок Teams в настольном лотке.
    * **macOS.** Выберите значок Teams в доке.
 
   На следующем изображении показано, как DevTools проверяет элемент в диалоговом окантовке конфигурации вкладок:

   ![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="access-devtools-from-an-android-client"></a>Доступ к DevTools от клиента Android

Вы также можете включить DevTools из клиента Teams Android. Чтобы включить DevTools, необходимо:

1. Включить [предварительный просмотр разработчика.](~/resources/dev-preview/developer-preview-intro.md)
1. Подключите устройство к настольному компьютеру и установите устройство Android для [удаленного отладки.](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. В браузере Chrome откройте `chrome://inspect/#devices` .
1. Выберите  инспектировать в вкладке, необходимой для отладки, как на следующем изображении:

   ![Android DevTools](~/assets/images/android-devtools.png)
