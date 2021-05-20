---
title: Проверьте обзор приложения
description: Описывает процесс проверки пользовательского Teams в Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Настройка Microsoft 365 для Teams тестирования приложения
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565188"
---
# <a name="test-your-app"></a>Тестирование приложения

После интеграции приложения с Microsoft Teams, вы должны проверить свое приложение перед публикацией. Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что тестирование приложения на нескольких устройствах, которые пользователи могут использовать. Для тестирования приложения:

* Подготовь Microsoft 365 арендатора.
* Выберите рабочее пространство для тестирования и отладки приложения.
* Добавьте тестовые данные к Microsoft 365 арендатору.

## <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Перед началом тестирования приложения подготовьте Microsoft 365 и включите пользовательские Teams, позволяющие загружать приложение. Вы должны зарегистрироваться для Microsoft 365 разработчика и управлять настройками Teams для вашей организации. Настройте подписку разработчика и настройте ее через [подготовку Microsoft 365 арендатора.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Тестирование и отладка

Чтобы протестировать и отладить приложение, необходимо создать по крайней мере одно рабочее пространство. Вы можете выбрать настройку тестирования, например локального хоста или облачного хоста, чтобы протестировать и отладить приложение. Руководство по отладке Teams приложения предоставляется для загрузки и запуска приложения. Для получения дополнительной [информации можно выбрать настройку и запустить Microsoft Teams приложение.](~/concepts/build-and-test/debug.md)

Проверьте своего бота локально. Для получения дополнительной информации [см.](~/bots/how-to/debug/locally-with-an-ide.md) Вы также можете отладить ваш бот с [инспекцией среднего программного обеспечения и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивных инструментов.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Для просмотра журналов консолей, просмотра или изменения HTML, css и сетевых запросов во время выполнения добавьте точки разрыва в код JavaScript и выполните интерактивную отладку доступа к DevTools. Для получения дополнительной [информации, см. Доступ к DevTools для Teams вкладок](~/tabs/how-to/developer-tools.md). 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Добавление тестовых данных к Microsoft 365 арендатору

Добавьте тестовые данные Microsoft 365 тест-арендатора. Для получения дополнительной [информации, с Office 365 м.](~/concepts/build-and-test/test-data.md)

## <a name="see-also"></a>См. также

- [Отладить вкладку](~/tabs/how-to/developer-tools.md)
 
- [Отладить ботов](~/bots/how-to/debug/locally-with-an-ide.md)

- [Тестовые разрешения RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
