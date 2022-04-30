---
title: Протестируйте обзор приложения
description: Описывает процесс тестирования и отладки пользовательского приложения Teams в Microsoft 365.
ms.topic: how-to
ms.localizationpriority: high
keywords: Настройка отправки тестового приложения клиента Microsoft 365 Teams
ms.openlocfilehash: 98c00ece54e1654570556bac122e6760b283b73f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111530"
---
# <a name="test-your-app"></a>Тестирование приложения

После интеграции приложения с Microsoft Teams необходимо протестировать его перед публикацией. Конечная цель — привлечь как можно больше пользователей для приложения, поэтому обязательно протестируйте приложение на разных пользовательских устройствах. Для тестирования приложения:

* Подготовьте клиент Microsoft 365.
* Выберите рабочую область для тестирования и отладки приложения.
* Добавьте тестовые данные в клиент Microsoft 365.

## <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Прежде чем приступить к тестированию приложения, подготовьте тестовый клиент Microsoft 365 и включите пользовательское приложение Teams, позволяющее загружать приложение. Необходимо зарегистрироваться в программе для разработчиков Microsoft 365 и управлять параметрами Teams для организации. Настройте подписку разработчика, [подготовив клиент Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md).

## <a name="test-and-debug"></a>Тестирование и отладка

Для тестирования и отладки приложения необходимо создать хотя бы одну рабочую область. Вы можете выбрать тестовую настройку, например локальный хост или облачный хост, для тестирования и отладки приложения. Руководство по отладке приложения Teams предоставляется для загрузки и запуска приложения. Дополнительные сведения см. в разделе [Выбор настройки и запуск приложения Microsoft Teams](~/concepts/build-and-test/debug.md).

Протестируйте бот локально. Подробнее см. в разделе [Отладка вашего бота локально с помощью IDE](~/bots/how-to/debug/locally-with-an-ide.md). Вы также можете отлаживать бот с [помощью промежуточного программного обеспечения для проверки](/azure/bot-service/bot-service-debug-inspection-middleware?view=azure-bot-service-4.0&tabs=csharp&preserve-view=true) и [адаптивных инструментов](/azure/bot-service/bot-service-debug-adaptive-tools?view=azure-bot-service-4.0&preserve-view=true).

Для просмотра журналов консоли, просмотра или изменения html, css и сетевых запросов во время выполнения, добавления точек останова в код JavaScript и выполнения интерактивной отладки используйте DevTools. Дополнительные сведения см. в разделе [Доступ к вкладкам DevTools для Teams](~/tabs/how-to/developer-tools.md).

## <a name="add-test-data-to-your-microsoft-365-tenant"></a>Добавьте тестовые данные в клиент Microsoft 365.

Добавьте тестовые данные в тестовый клиент Microsoft 365. Дополнительные сведения см. в разделе [Добавление тестовых данных в тестовый клиент Office 365](~/concepts/build-and-test/test-data.md) и выполните все предварительные условия, прежде чем начать загрузку тестовых данных.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Подготовка клиента Microsoft 365](~/concepts/build-and-test/prepare-your-o365-tenant.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Отладка вкладки](~/tabs/how-to/developer-tools.md)
* [Отладка ботов](~/bots/how-to/debug/locally-with-an-ide.md)
* [Тестирование разрешений RSC](~/graph-api/rsc/test-resource-specific-consent.md)
