---
title: DevTools для вкладок Microsoft Teams
description: Описание того, как добраться до DevTools при использовании клиента Microsoft Teams для настольных ПК
ms.topic: how-to
keywords: devtools debug mobile chrome desktop client developer tools
ms.openlocfilehash: 8f23a5d56faa00d40451d2bbeadde32f6a5d0f7f
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014581"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools для вкладок Microsoft Teams

Когда Teams работает в браузере, легко получить доступ к devTools браузера: F12 (в Windows) или Command-Option-I (в MacOS). DevTools предоставляет доступ к:

1. Просмотр журналов консоли.
1. Просмотр и изменение html-запросов, CSS и сетевых запросов во время работы.
1. Добавьте точки останова в код JavaScript и выполните интерактивную отладку.

Эта функция доступна только в классических клиентах и клиентах Android Developer Preview включена. Дополнительные [сведения см. в](~/resources/dev-preview/developer-preview-intro.md) Developer Preview.

## <a name="accessing-devtools-in-the-desktop"></a>Доступ к DevTools на рабочем столе

Несмотря на то что веб-версия Teams и классические версии команд практически не отличаются, существуют некоторые различия, особенно в отношении проверки подлинности. Иногда единственным способом выяснить, что происходит, является использование DevTools. Вот как получить к ним возможность из настольного клиента Teams. Чтобы использовать DevTools в настольном клиенте:

1. Убедитесь, что вы включили [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md)
1. Откройте вкладку, чтобы получить что-то для проверки с помощью DevTools.
1. Откройте DevTools
    * В Windows вы открываете DevTools с помощью значка Microsoft Teams в области рабочего стола:

  ![Щелкните правой кнопкой мыши, чтобы открыть DevTools](~/assets/images/dev-preview/devtools-right-click.png)

    * В MacOS щелкните значок Microsoft Teams на док-станции.

Вот как выглядит вкладка с открытым devTools и выбранным элементом:

![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)

## <a name="accessing-devtools-from-an-android-client"></a>Доступ к DevTools из клиента Android

Вы также можете включить DevTools из клиента Teams Android. Для этого:

1. Убедитесь, что вы включили [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md)
1. Подключение устройства к настольному компьютеру и настройка устройства с Android для [удаленной отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/)
1. В браузере Chrome откройте `chrome://inspect/#devices` .
1. Щелкните **"Проверить"** под вкладками, которые нужно отлажать, как по снимку экрана ниже.

![Android DevTools](~/assets/images/android-devtools.png)
