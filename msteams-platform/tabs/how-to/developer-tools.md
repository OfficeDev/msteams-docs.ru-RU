---
title: DevTools для вкладок Microsoft Teams
description: В этом модуле вы узнаете, как получить доступ к средствам разработки при использовании настольного клиента Microsoft Teams и отладке
ms.localizationpriority: medium
ms.topic: how-to
ms.openlocfilehash: a0d5e3ea15fd796c2c426f1cf1457171f0abe7b2
ms.sourcegitcommit: 024be23411bc0f2573d19f48f9266021f9b76f0d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/31/2022
ms.locfileid: "67488273"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools для вкладок Microsoft Teams

Когда Teams работает в браузере, можно легко получить доступ к средствам разработчика браузера: F12 в Windows или Command-Option-I в MacOS. DevTools предоставляет вам доступ к:

1. Просмотр журналов консоли.
1. Просмотр или изменение HTML, CSS и сетевых запросов во время выполнения.
1. Добавляйте точки останова в код JavaScript и выполняйте интерактивную отладку.

> [!NOTE]
> Эта функция доступна только для настольных компьютеров и клиентов Android после включения **предварительной версии для разработчиков**. Подробнее об этом см.:[Как включить предварительный просмотр для разработчиков](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Доступ к DevTools на рабочем столе

Хотя веб-версия и настольная версия Teams почти одинаковы, существуют некоторые различия в отношении проверки подлинности. Иногда единственный способ выяснить, что происходит, — использовать DevTools. Чтобы использовать DevTools в настольном клиенте, необходимо:

1. Убедитесь, что вы включили [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md).
1. Откройте вкладку, чтобы вам было что проверить с помощью DevTools.
1. Откройте DevTools одним из следующих способов:
    * В Windows DevTools открывается с помощью значка Microsoft Teams на панели задач рабочего стола.

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * В MacOS выберите значок Microsoft Teams в Dock.

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

В следующем примере показано, как DevTools открывает и проверяет диалоговое окно конфигурации вкладки:

   [![Вкладка и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Доступ к DevTools с устройства Android

Вы также можете включить DevTools из клиента Teams для Android. Чтобы включить DevTools, необходимо:

1. Включить [предварительную версию для разработчиков](~/resources/dev-preview/developer-preview-intro.md).
1. Подключите свое устройство к настольному компьютеру и настройте устройство Android для [удаленной отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).
1. В браузере Chrome откройте `chrome://inspect/#devices`.
1. Выберите **Проверить** на вкладке, которую вы хотите отладить, как на следующем изображении:

   ![DevTools для Android ](~/assets/images/android-devtools.png)

## <a name="see-also"></a>См. также

[Очистка кэша клиента Teams](/microsoftteams/troubleshoot/teams-administration/clear-teams-cache)
