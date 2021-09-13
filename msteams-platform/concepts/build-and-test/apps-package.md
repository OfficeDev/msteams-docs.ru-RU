---
title: Пакет приложения
description: Узнайте, как упаковировать Microsoft Teams для тестирования, загрузки и публикации в магазине.
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: bcffc581ab832dfa51d0b772f466b92dea731ccf
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157487"
---
# <a name="create-a-microsoft-teams-app-package"></a>Создание пакета Microsoft Teams приложения

Вам нужен пакет приложений, однако вы планируете распространять Microsoft Teams приложение. Допустимый пакет — это файл ZIP, содержащий следующие сведения:

* **Манифест приложения.** Описывается настройка приложения, включая его возможности, необходимые ресурсы и другие важные атрибуты.
* **Значки** приложения. Для каждого пакета требуется значок цвета и контура для приложения.

## <a name="app-manifest"></a>Манифест приложения

Файл манифеста приложения должен быть на верхнем уровне пакета с `manifest.json` именем. 

При публикации в Teams убедитесь, что манифест ссылается на последнюю [схему.](~/resources/schema/manifest-schema.md)

## <a name="app-icons"></a>Значки приложений

Пакет приложения должен включать две PNG-версии значка приложения: цветную и очертания.

> [!Note]
> Если у приложения есть расширение бота или обмена сообщениями, значки также будут включены в Microsoft Azure службы ботов.

Чтобы приложение прошло проверку Teams магазина, эти значки должны соответствовать следующим требованиям к размеру.

### <a name="color-icon"></a>Значок цвета

Цветная версия значка отображается в большинстве Teams и должна быть 192x192 пикселей. Символ значка (96x96 пикселей) может быть любого цвета, но он должен сидеть на сплошном или полностью прозрачном квадратном фоне.

Teams автоматически обнажает значок для отображения квадрата с закругленными углами в нескольких сценариях и шестиугольной формы в сценариях ботов. Чтобы обрезать символ без потери деталей, включите 48 пикселей обивки вокруг символа.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams значок цвета и руководство по дизайну." border="false":::

### <a name="outline-icon"></a>Значок Outline

Значок плана отображает в двух сценариях:

* Когда приложение используется и "подъехалось" на панели приложения слева от Teams.
* Когда пользователь пин-коды расширения обмена сообщениями вашего приложения.

Значок должен быть 32x32 пикселей. Он может быть белым с прозрачным фоном или прозрачным с белым фоном (другие цвета не допускаются). Значок outline не должен иметь дополнительных обивок вокруг символа.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams руководство по проектированию значков." border="false":::

### <a name="best-practices"></a>Рекомендации

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, как создать значки приложения." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>Do: Следуйте указаниям по точным значкам плана

Значения RGB белого цвета, используемые в значке, должны быть красными: 255, Зеленым: 255, Синим: 255. Все остальные части значка контура должны быть полностью прозрачными, а альфа-каналу установлено 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, как не проектировать значки приложения." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>Не: Обрезать в круговой или округлой квадратной форме

Значок цвета, представленный в пакете приложения, должен быть квадратным. Не закругляйте углы значка. Teams автоматически регулирует радиус угла.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>Не: скопируйте другие бренды

Значки не должны имитировать какие-либо продукты, защищенные авторским правом, которые не принадлежат вам. Например, дизайн, аналогичный продукту или бренду Майкрософт.

### <a name="examples"></a>Примеры

Вот как значки приложений отображаются в разных Teams и контекстах.

#### <a name="personal-app"></a>Личное приложение

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, показывающий внешний вид значка приложения в личном приложении." border="false":::

#### <a name="bot-channel"></a>Бот (канал)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a>Расширение для обмена сообщениями

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<alt text>" border="false":::

## <a name="next-step"></a>Следующий этап

Выберите, как вы планируете распространять приложение:

> [!div class="nextstepaction"]
> [Sideload ваше приложение в Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Публикация приложения в вашей организации](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Публикация приложения в магазине](~/concepts/deploy-and-publish/appsource/publish.md)
