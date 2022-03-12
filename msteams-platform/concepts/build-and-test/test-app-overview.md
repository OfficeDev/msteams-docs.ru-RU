---
title: Проверка обзора приложения
description: Описывает процесс тестирования и отлаговки Teams настраиваемого приложения в Microsoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: Настройка Microsoft 365 клиента Teams загрузки тестового приложения
ms.openlocfilehash: 7831d245fd48b9eb5c6dd4761a84a1fee3d9cfef
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453882"
---
# <a name="test-your-app"></a>Тестирование приложения

После интеграции приложения с Microsoft Teams необходимо протестировать его перед публикацией. Конечная цель состоит в том, чтобы получить как можно больше пользователей для вашего приложения, поэтому убедитесь, что приложение тестировать на нескольких устройствах, которые пользователи могут использовать. Для тестирования приложения:

* Подготовка Microsoft 365 клиента.
* Выберите рабочее пространство для тестирования и отлаговки приложения.
* Добавьте тестовые данные в Microsoft 365 клиента.

## <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Прежде чем приступить к тестированию приложения, Microsoft 365 тестовый клиент и включить настраиваемые Teams приложение позволяет загружать приложение. Необходимо зарегистрироваться для Microsoft 365 и управлять настройками Teams организации. Настройте подписку разработчика и настройте ее путем [подготовки Microsoft 365 клиента](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Тестирование и отладка

Чтобы протестировать и отлагировать приложение, необходимо создать хотя бы одно рабочее пространство. Вы можете выбрать тестовую установку, например локальный хост или облачный хост для тестирования и отлаговки приложения. Рекомендации по отлажению Teams приложения для загрузки и запуска приложения. Дополнительные сведения см. в дополнительных сведениях о настройках и [запуске Microsoft Teams приложения](~/concepts/build-and-test/debug.md).

Протестировать бот локально. Дополнительные сведения см. [в примере отламывка бота локально с помощью IDE](~/bots/how-to/debug/locally-with-an-ide.md). Кроме того, вы можете отстраить бота с помощью [средств](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) проверки и [адаптивного программного обеспечения](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).

Чтобы просмотреть журналы консоли, просмотреть или изменить запросы html, css и сетевые запросы во время выполнения, добавьте точки разрывов в код JavaScript и выполните интерактивный отладки доступа к DevTools. Дополнительные сведения см. [в вкладки Access the DevTools для Teams.](~/tabs/how-to/developer-tools.md)

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Добавление тестовых данных в Microsoft 365 клиента

Добавьте тестовые данные в Microsoft 365 тестовый клиент. Дополнительные сведения см. в дополнительных сведениях о добавлении [тестовых](~/concepts/build-and-test/test-data.md) данных в Office 365 тестовый клиент и выполните все необходимые условия перед отправкой тестовых данных.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>См. также

* [Отламывка вкладки](~/tabs/how-to/developer-tools.md)
* [Отламывка ботов](~/bots/how-to/debug/locally-with-an-ide.md)
* [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)
