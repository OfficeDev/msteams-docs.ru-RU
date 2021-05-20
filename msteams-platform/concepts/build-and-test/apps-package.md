---
title: Пакет приложения
description: Узнайте, как упаковать Microsoft Teams приложение для тестирования, загрузки и публикации в магазине.
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 219e2d5341707ed51b7e0a3a8077f93df9eac640
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565216"
---
# <a name="create-a-microsoft-teams-app-package"></a>Создание пакета Microsoft Teams приложений

Вам нужен пакет приложений, однако вы планируете распространять свои Microsoft Teams приложения. Действительный пакет является файлом, который содержит следующее:

* **Манифест приложения**: Описывает, как настроено ваше приложение, включая его возможности, необходимые ресурсы и другие важные атрибуты.
* **Значки приложений**: Каждый пакет требует значка цвета и контура для вашего приложения.

## <a name="app-manifest"></a>Манифест приложения

Файл манифеста приложения должен быть на верхнем уровне пакета с `manifest.json` именем. 

При публикации в Teams, убедитесь, что ваш манифест ссылки на последнюю [схему](~/resources/schema/manifest-schema.md).

## <a name="app-icons"></a>Значки приложений

Пакет приложений должен включать две версии значка приложения PNG: цвет и наброски версии.

> [!Note]
> Если в вашем приложении есть бот или расширение обмена сообщениями, ваши значки также будут включены в Microsoft Azure Bot Service.

Чтобы ваше приложение Teams обзор магазина, эти значки должны соответствовать следующим требованиям к размеру.

### <a name="color-icon"></a>Значок цвета

Цветовая версия значка отображается в большинстве сценариев Teams должна быть 192x192 пикселей. Символ значка (96x96 пикселей) может быть любого цвета, но он должен сидеть на твердом или полностью прозрачном квадратном фоне.

Teams автоматически обуборляет значок, чтобы отображать квадрат с закругленными углами в нескольких сценариях и шестиугольной формой в сценариях ботов. Чтобы обрезать символ, не теряя деталей, включите 48 пикселей обивки вокруг вашего символа.

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams цвет и руководство по дизайну." border="false":::

### <a name="outline-icon"></a>Значок контура

Значок контура отображается в двух сценариях:

* Когда приложение используется и «поднимается» на бар приложения на левой стороне Teams.
* Когда пользователь прижимает расширение обмена сообщениями вашего приложения.

Значок должен быть 32x32 пикселей. Он может быть белым с прозрачным фоном или прозрачным с белым фоном (никакие другие цвета не допускаются). Значок контура не должен иметь дополнительной обивки вокруг символа.

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams наброски руководства по проектированию иконок." border="false":::

### <a name="best-practices"></a>Рекомендации

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="Иллюстрация, показывающая, как проектировать значки приложений." border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a>У: Следуйте точным рекомендациям значок контура

Значения RGB белого, используемого в вашей иконке, должны быть красными: 255, зелеными: 255, синими: 255. Все остальные части значка контура должны быть полностью прозрачными, а альфа-канал установлен на 0.

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="Иллюстрация, показывающая, как не проектировать значки приложений." border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a>Не: Урожай в круглой или округлой квадратной форме

Значок цвета, представленный в пакете приложения, должен быть квадратным. Не обгоните углы иконы. Teams автоматически регулирует радиус угла.

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a>Не: Копировать другие бренды

Ваши значки не должны имитировать любые защищенные авторским правом продукты, которые вы не владеете. Например, дизайн, похожий на продукт или бренд корпорации Майкрософт.

### <a name="examples"></a>Примеры

Вот как значки приложений отображаются в различных Teams и контекстах.

#### <a name="personal-app"></a>Личное приложение

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит в личном приложении." border="false":::

#### <a name="bot-channel"></a>Бот (канал)

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="Пример, показывающий, как значок приложения выглядит на боте внутри канала." border="false":::

#### <a name="messaging-extension"></a>Расширение для обмена сообщениями

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<альт текстовых>" border="false":::

## <a name="next-step"></a>Следующий шаг

Выберите способ распространения приложения:

> [!div class="nextstepaction"]
> [Загрузка приложения в Teams](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [Опубликовать приложение на сайте org](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [Публикация приложения в магазине](~/concepts/deploy-and-publish/appsource/publish.md)
