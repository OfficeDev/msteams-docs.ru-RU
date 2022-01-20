---
title: Упаковка приложения
description: Узнайте, как упаковать приложение Microsoft Teams для тестирования, отправки и публикации в магазине.
ms.localizationpriority: high
ms.topic: conceptual
ms.openlocfilehash: 002da681a464770a31fa6963e96fdff54701b35f
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059681"
---
# <a name="create-a-microsoft-teams-app-package"></a>Создание манифеста приложения в Microsoft Teams

Вам нужен пакет приложения, но вы планируете распространять приложение Microsoft Teams. Допустимый пакет — это ZIP-файл, содержащий следующее:

* **Манифест приложения**. В манифесте описывается настройка приложения, включая его возможности, необходимые ресурсы и другие важные атрибуты.
* **Значки приложения**. Для каждого пакета приложения требуется цветной и контурный значок.

## <a name="app-manifest"></a>Манифест приложения

Файл манифеста приложения должен находится на верхнем уровне пакета с именем `manifest.json`. 

При публикации в магазине Teams убедитесь, что манифест ссылается на последнюю версию [схемы](~/resources/schema/manifest-schema.md).

## <a name="app-icons"></a>Значки приложений

Пакет приложения должен содержать две версии значка приложения в формате PNG: цветную и контурную версию.

> [!Note]
> Если у вашего приложения есть бот или расширение для обмена сообщениями, значки также будут включены в регистрацию службы Azure Bot.

Чтобы ваше приложение прошло проверку магазина Teams, эти значки должны соответствовать следующим требованиям к размеру.

### <a name="color-icon"></a>Цветной значок

Цветная версия значка отображается в большинстве ситуаций в Teams и должна иметь размер 192x192 пиксела. Символ значка (96x96 пикселов) может быть любого цвета, но он должен быть размещен на сплошном или полностью прозрачном квадратном фоне.

Teams автоматически обрезает значок и отображает квадрат с закругленными углами в нескольких сценариях и шестиугольную фигуру в сценариях с ботом. Чтобы обрезать символ без потери деталей, включите заполнение на 48 пикселей вокруг символа.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Руководство по цветному значку и дизайну в Teams." border="false":::

### <a name="outline-icon"></a>Контурный значок

Контурный значок отображается в двух сценариях.

* Когда приложение используется и когда оно находится в панели приложений в левой части Teams.
* Когда пользователь закрепляет расширение для сообщений вашего приложения.

Значок должен иметь размер 32x32 пикселя. Он может быть белым с прозрачным фоном или прозрачным с белым фоном (другие цвета не разрешаются). Вокруг контура не должно быть дополнительного заполнения.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Руководство по дизайну контурного значка в Teams." border="false":::

### <a name="best-practices"></a>Лучшие методики

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, каким должен быть дизайн значка приложения." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Следует точно выполнять инструкции для контурного значка

Значения RGB белого цвета, используемого в значке, должны быть следующими: красный — 255, зеленый — 255, синий — 255. Все остальные части значка контура должны быть полностью прозрачными, а альфа-канал должен иметь значение 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, каким не должен быть дизайн значка приложения." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>Не следует обрезать до круглой фигуры или квадратной фигуры со скругленными углами

Цветной значок, отправленный в пакете приложения, должен быть квадратным. Не следует закруглять углы значка. Teams автоматически настраивает радиус скругления угла.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>Не следует копировать другие бренды

Ваши значки не должны имитировать продукты, защищенные авторским правом, которым вы не владеете. Например, дизайн, похожий на продукт или торговую марку Майкрософт.

### <a name="examples"></a>Примеры

Вот как значки приложений отображаются в различных функциях и контекстах Teams.

#### <a name="personal-app"></a>Личное приложение

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример отображения значка в личном приложении." border="false":::

#### <a name="bot-channel"></a>Бот (канал)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример отображения значка на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a>Расширение для обмена сообщениями

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<замещающий текст>" border="false":::

## <a name="next-step"></a>Следующий этап

Выберите, как вы планируете распространять приложение:

> [!div class="nextstepaction"]
> [Загрузка неопубликованного приложения в Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Публикация приложения в организации](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Публикация приложения в магазине](~/concepts/deploy-and-publish/appsource/publish.md)

## <a name="see-also"></a>См. также

[Управление приложениями Microsoft Teams с помощью портала разработчика](~/concepts/build-and-test/teams-developer-portal.md)