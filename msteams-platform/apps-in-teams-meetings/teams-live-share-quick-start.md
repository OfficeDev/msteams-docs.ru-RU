---
title: Краткое руководство по Live Share
description: В этом модуле вы узнаете, как быстро опробовать пример Dice Roller
ms.topic: concept
ms.localizationpriority: high
ms.author: stevenic
ms.openlocfilehash: 98150265f0c5876e726710cacc873db2ac23e9ee
ms.sourcegitcommit: c7fbb789b9654e9b8238700460b7ae5b2a58f216
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2022
ms.locfileid: "66484588"
---
---

# <a name="quick-start-guide"></a>Краткое руководство по началу работы

Начните работу с SDK Live Share с использованием примера Dice Roller, который разработан на основе [краткой инструкции по Fluid Framework](https://fluidframework.com/docs/start/quick-start/) и предназначен для быстрого запуска примера [Dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller) на основе пакета SDK Live Share в узле localhost компьютера.

:::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Пример DiceRoller":::

> [!NOTE]
> В этом руководстве даны пошаговые инструкции для локального использования Live Share в браузере. Чтобы узнать больше об использовании пакета SDK для собраний Teams, ознакомьтесь с нашим [руководством для разработки игры в покер по гибкой методике](../sbs-teams-live-share.yml).

## <a name="set-up-your-development-environment"></a>Настройка среды разработки

Чтобы начать работу, установите следующие компоненты.

* [Node.js](https://nodejs.org/en/download). Пакет SDK Live Share поддерживает Node.js LTS начиная с версии 12.17.
* [Новейшая версия Visual Studio Code](https://code.visualstudio.com/).
* [Git](https://git-scm.com/downloads)

## <a name="build-and-run-the-dice-roller-app"></a>Сборка и запуск приложения Dice Roller

1. Перейдите к примеру приложения [Dice Roller](https://github.com/microsoft/live-share-sdk/tree/main/samples/01.dice-roller).

1. Клонируйте репозиторий [Live Share SDK](https://github.com/microsoft/live-share-sdk) для тестирования примера приложения:

    ```bash
    $ git clone https://github.com/microsoft/live-share-sdk.git
    ```

1. Выполните следующую команду, чтобы перейти в папку примера приложения Dice Roller:

   ```bash
    $ cd live-share-sdk\samples\01.dice-roller
   ```

1. Выполните следующую команду, чтобы установить пакет зависимостей:

    ```bash
    $ npm install
    ```

1. Выполните указанную ниже команду, чтобы запустить клиент и локальный сервер:

   ```bash
   $ npm start
   ```
  
     Откроется новая вкладка браузера, где откроется URL-адрес `http://localhost:8080` и приложение Dice Roller.

1. Скопируйте полный URL-адрес в браузере, включая идентификатор, и вставьте URL-адрес в новом окне или другом браузере.

   Откроется второй клиент для приложения Dice Roller.

1. Откройте оба окна и нажмите кнопку **Бросок игральных костей** в одном из окон. Состояние брошенных игральных костей изменяется в обоих клиентах.

    :::image type="content" source="../assets/images/teams-live-share/dice-roller.png" alt-text="Приложение Dice Roller с несколькими вкладками":::
  
   **Поздравляем**, вы научились собирать и запускать приложения с помощью Live Share SDK.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Руководство по примеру Dice Roller](teams-live-share-tutorial.md)

## <a name="see-also"></a>См. также

* [Репозиторий GitHub](https://github.com/microsoft/live-share-sdk)
* [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
* [Справочная документация по пакету SDK мультимедиа Live Share](/javascript/api/@microsoft/live-share-media/)
* [Возможности Live Share](teams-live-share-capabilities.md)
* [Вопросы и ответы по Live Share](teams-live-share-faq.md)
* [Приложения Teams на собраниях](teams-apps-in-meetings.md)
