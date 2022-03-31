---
title: DevTools для вкладок Microsoft Teams
description: Описывает, как добраться до DevTools при использовании Microsoft Teams настольного клиента и отладки
ms.localizationpriority: medium
ms.topic: how-to
keywords: devtools отладка мобильных хром настольных средств разработчика настольных компьютеров вкладка
ms.openlocfilehash: bec7b94b1db2492de9eaaa38ff62c0783c972f6e
ms.sourcegitcommit: d9daad3d5818d5774911b96fdc7bde45b04c9908
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/29/2022
ms.locfileid: "64511222"
---
# <a name="devtools-for-microsoft-teams-tabs"></a>DevTools для вкладок Microsoft Teams

Когда Teams в браузере, легко получить доступ к devTools браузера: F12 на Windows или Command-Option-I на MacOS. DevTools предоставляет вам доступ к:

1. Просмотр журналов консоли.
1. Просмотр или изменение HTML-запросов, CSS и сетевых запросов во время работы.
1. Добавьте breakpoints в код JavaScript и выполните интерактивную отладку.

> [!NOTE]
> Эта функция доступна только для клиентов на настольных компьютерах и Android после **Developer Preview включена** . Дополнительные сведения см. в [Разделы справки включить предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md).

## <a name="access-devtools-on-the-desktop"></a>Доступ к DevTools на рабочем столе

Несмотря на то, что веб-версия и Teams практически одинаковы, существуют некоторые различия в проверке подлинности. Иногда единственный способ выяснить, что происходит, это использовать DevTools. Чтобы использовать DevTools в настольном клиенте, необходимо:

1. Убедитесь, что вы [включили предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md).
1. Откройте вкладку, чтобы вам было что проверить с помощью DevTools.
1. Откройте DevTools одним из следующих способов:
    * На Windows вы открываете DevTools через значок Microsoft Teams в настольном лотке.

      :::image type="content" source="../../assets/images/dev-preview/devtools-right-click.png" alt-text="developer-tool-windows":::

    * На MacOS выберите значок Microsoft Teams в доке.

      :::image type="content" source="../../assets/images/dev-preview/mac-os-developer-tools.PNG" alt-text="mac-os-dev-tools":::

В следующем примере показано, как DevTools открывают и проверяют диалоговое окно конфигурации вкладок:

   [![Tab и DevTools](~/assets/images/dev-preview/tab-and-devtools.png)](~/assets/images/dev-preview/tab-and-devtools.png#lightbox)

## <a name="access-devtools-from-an-android-device"></a>Доступ к DevTools с android-устройства

Вы также можете включить DevTools из Teams Android клиента. Чтобы включить DevTools, необходимо:

1. Включить [предварительный просмотр разработчика](~/resources/dev-preview/developer-preview-intro.md).
1. Подключение устройство на настольный компьютер и установите устройство Android для [удаленной отладки](https://developers.google.com/web/tools/chrome-devtools/remote-debugging/).
1. В браузере Chrome откройте `chrome://inspect/#devices`.
1. Выберите **инспектировать** в вкладке, необходимой для отладки, как на следующем изображении:

   ![Android DevTools](~/assets/images/android-devtools.png)
