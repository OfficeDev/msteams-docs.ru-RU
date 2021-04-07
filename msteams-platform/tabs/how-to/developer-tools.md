---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании настольного клиента Microsoft Teams
ms.topic: how-to
keywords: devtools отладка мобильных средств разработки настольных компьютеров chrome для настольных компьютеров
ms.openlocfilehash: 1bf7d246136a24316309ae144ac9552c5fd4f57d
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596275"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools для вкладок Microsoft Teams

Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 (на Windows) или Command-Option-I (на MacOS). DevTools предоставляет вам доступ к:

1. Просмотр журналов консоли.
1. Просмотр и изменение html-запросов, css и сетевых запросов во время работы.
1. Добавьте точки брейк-пойнтов в код JavaScript и выполните интерактивную отладку.

Функция доступна только в настольных и android-клиентах после Developer Preview включена. Дополнительные [сведения см.](~/resources/dev-preview/developer-preview-intro.md) в Developer Preview.

## <a name="accessing-devtools-in-the-desktop"></a>Доступ к DevTools на рабочем столе

Несмотря на то, что веб-версия Teams и десктопная версия команд практически одинаковы, существуют некоторые различия, особенно в отношении проверки подлинности. Иногда единственный способ выяснить, что происходит, это использовать DevTools. Вот как добраться до них с настольного клиента Teams. Использование DevTools в настольном клиенте:

1. Убедитесь, что вы включили [предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md)
1. Откройте вкладку, чтобы вам было что проверить с помощью DevTools.
1. Откройте DevTools одним из следующих способов:
    * **Windows.** Выберите значок Teams в настольном лотке.
    * **macOS.** Выберите значок Teams в доке.

На следующем скриншоте показано, как DevTools проверяет элемент в диалоговом окантовке конфигурации вкладок:

![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Доступ к DevTools от клиента Android

Вы также можете включить DevTools из клиента Teams Android.

1. Убедитесь, что вы включили [предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md)
1. Подключение устройства к настольному компьютеру и настройка устройства Android для [удаленного отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. В браузере Chrome откройте `chrome://inspect/#devices` .
1. Нажмите **кнопку** проверки ниже вкладки, которая необходимо отлажать, как на скриншоте ниже.

![Android DevTools](~/assets/images/android-devtools.png)
