---
title: Проверка обзора приложения
description: Описывает процесс тестирования настраиваемого Teams в Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Настройка Microsoft 365 клиента Teams загрузки тестового приложения
ms.openlocfilehash: 2c9f23a5c6ae286ff4b7d911f370bd45b854a647
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565188"
---
# <a name="test-your-app"></a>Тестирование приложения

После интеграции приложения с Microsoft Teams необходимо протестировать приложение перед его публикацией. Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что приложение тестировать на нескольких устройствах, которые пользователи могут использовать. Для тестирования приложения:

* Подготовка Microsoft 365 клиента.
* Выберите рабочее пространство для тестирования и отлаговки приложения.
* Добавьте тестовые данные в Microsoft 365 клиента.

## <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Прежде чем приступить к тестированию приложения, Microsoft 365 тестовый клиент и включить настраиваемые Teams, которые позволяют загружать приложение. Необходимо зарегистрироваться для Microsoft 365 разработчика и управлять Teams параметров для вашей организации. Настройте подписку разработчика и настройте ее путем [подготовки Microsoft 365 клиента.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Тестирование и отладка

Чтобы протестировать и отлагировать приложение, необходимо создать хотя бы одно рабочее пространство. Вы можете выбрать тестовую установку, например локальный хост или облачный хост для тестирования и отлаговки приложения. Рекомендации по отлажению Teams приложения для загрузки и запуска приложения. Дополнительные сведения см. [в дополнительных сведениях о](~/concepts/build-and-test/debug.md)настройках и запуске Microsoft Teams приложения.

Протестировать бот локально. Дополнительные сведения см. [в примере отламывка](~/bots/how-to/debug/locally-with-an-ide.md)бота локально с помощью IDE. Вы также можете отстраить бота с помощью [среднего поверки и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивного средства проверки.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Чтобы просмотреть журналы консоли, просмотреть или изменить запросы html, css и сетевые запросы во время выполнения, добавьте точки разрывов в код JavaScript и выполните интерактивный отладки доступа к DevTools. Дополнительные сведения см. [в вкладки Access the DevTools для Teams.](~/tabs/how-to/developer-tools.md) 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Добавление тестовых данных в Microsoft 365 клиента

Добавьте тестовые данные в Microsoft 365 тестовый клиент. Дополнительные сведения см. в дополнительных сведениях о добавлении [тестовых](~/concepts/build-and-test/test-data.md)данных в Office 365 тестовый клиент и выполните все необходимые условия перед отправкой тестовых данных.

## <a name="see-also"></a>См. также

- [Отламывка вкладки](~/tabs/how-to/developer-tools.md)
 
- [Отламывка ботов](~/bots/how-to/debug/locally-with-an-ide.md)

- [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
