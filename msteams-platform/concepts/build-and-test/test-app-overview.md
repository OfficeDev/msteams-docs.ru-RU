---
title: Проверка обзора приложения
description: Описывает процесс тестирования настраиваемого приложения Teams в Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: Настройка microsoft 365 tenant Teams для загрузки тестового приложения
ms.openlocfilehash: 8815e73c054cb75782660ef4afb3ae583b4f40fa
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019939"
---
# <a name="test-your-app"></a>Тестирование приложения

После интеграции приложения с Microsoft Teams необходимо протестировать приложение перед его публикацией. Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что приложение тестировать на нескольких устройствах, которые пользователи могут использовать. Для тестирования приложения:

* Подготовка клиента Microsoft 365
* Выберите рабочее пространство для тестирования и отлаговки приложения
* Добавление тестовых данных в клиента Microsoft 365

## <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Прежде чем приступить к тестированию приложения, подготовьте тестовый клиент Microsoft 365 и впустите настраиваемые приложения Teams, позволяющие загружать приложение. Необходимо зарегистрироваться в программе разработчика Microsoft 365 и управлять настройками Teams для вашей организации. Настройте подписку на разработчика и настройте ее с [помощью подготовки клиента Microsoft 365.](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="test-and-debug"></a>Тестирование и отладка

Чтобы протестировать и отлагировать приложение, необходимо создать хотя бы одно рабочее пространство. Вы можете выбрать тестовую установку, например локальный хост или облачный хост для тестирования и отлаговки приложения. Рекомендации по отлажению приложения Teams предоставляются для загрузки и запуска приложения. Дополнительные сведения см. в дополнительных сведениях о настройках и запуске приложения [Microsoft Teams.](~/concepts/build-and-test/debug.md)

Протестировать бот локально. Дополнительные сведения см. [в примере отламывка](~/bots/how-to/debug/locally-with-an-ide.md)бота локально с помощью IDE. Вы также можете отстраить бота с помощью [среднего поверки и](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) [адаптивного средства проверки.](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true) 

Чтобы просмотреть журналы консоли, просмотреть или изменить запросы html, css и сетевые запросы во время выполнения, добавьте точки разрывов в код JavaScript и выполните интерактивный отладки доступа к DevTools. Дополнительные сведения см. в [вкладке Access the DevTools for Teams.](~/tabs/how-to/developer-tools.md) 

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Добавление тестовых данных в клиента Microsoft 365

Добавьте тестовые данные в тестовый клиент Microsoft 365. Дополнительные сведения см. в дополнительных сведениях о добавлении тестовых данных в тестовый клиент [Office 365](~/concepts/build-and-test/test-data.md)и выполните все необходимые условия перед отправкой тестовых данных.

## <a name="see-also"></a>См. также

> [!div class="nextstepaction"]
> [Отламывка вкладки](~/tabs/how-to/developer-tools.md)
 
> [!div class="nextstepaction"]
> [Отламывка ботов](~/bots/how-to/debug/locally-with-an-ide.md)

> [!div class="nextstepaction"]
> [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)
