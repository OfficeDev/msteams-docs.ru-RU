---
title: Манифест приложения Teams в наборе средств Teams для Visual Studio
author: surbhigupta
description: В этом модуле вы узнаете, как изменять, просматривать и настраивать манифест приложения Teams в другой среде для Visual Studio.
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: c391df383c97638d3c8ff5944afab75db2400580
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291655"
---
# <a name="edit-teams-app-manifest-using-visual-studio"></a>Изменение манифеста приложения Teams с помощью Visual Studio

Набор средств Teams в Visual Studio загружает манифест `manifest.template.json` `state.{env}.json` `config.{env}.json` с конфигурациями из и во время подготовки и подготовки зависимостей приложения. Вы также можете создать приложение Microsoft Teams на [портале разработчика](https://dev.teams.microsoft.com/apps) с манифестом.

После формирования шаблонов в файле `templates/appPackage` шаблона манифеста в папке `manifest.template.json` используется общий доступ между локальной и удаленной средой.

В шаблоне манифеста выберите **Project** > **Teams Toolkit Open****Manifest File (Открыть файл манифеста Project Teams Toolkit** > ).

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Открытие файла манифеста":::

### <a name="customize-app-manifest-in-teams-toolkit"></a>Настройка манифеста приложения в Наборе средств Teams

Существует два типа заполнителей `manifest.template.json`в:

- `{{state.xx}}` — это предварительно определенный заполнитель, значение которого разрешается набором средств Teams, определенным в `state.{env}.json`. Не рекомендуется изменять значения в `state.{env}.json`.
- `{{config.manifest.xx}}` — это настраиваемый заполнитель, значение которого разрешается из `config.{env}.json`.

Настраиваемый параметр можно добавить, выполнив следующие действия:

- Добавление заполнителя в шаблоне `manifest.template.json` : `{{config.manifest.xx}}`..
- Добавление значения конфигурации в `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### <a name="preview-app-manifest-in-teams-toolkit"></a>Предварительный просмотр манифеста приложения в Наборе средств Teams

Просмотреть значения в манифесте приложения можно двумя способами:

- При наведении указателя мыши на заполнитель отображаются `manifest.template.json`значения для среды  разработки  и локальной среды.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Наведите указатель мыши на заполнитель":::

- Вы также можете навести указатель `manifest.template.json`мыши на ключ рядом с каждым заполнителем, чтобы увидеть одинаковые значения  для среды разработки и локальной среды.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Наведите указатель мыши на ключ рядом с заполнителем":::

   > [!NOTE]
   > Если среда не была подготовлена или зависимости приложений Teams не были подготовлены, это означает, что значения для заполнителя не были созданы. Следуйте указаниям внутри наведения, чтобы создать соответствующие значения.

### <a name="preview-manifest-file"></a>Файл манифеста предварительной версии

Вы можете просмотреть файл манифеста, выполнив следующие действия.

- Выберите **меню "Набор средств Project** > **Teams**" и активирует подготовку зависимостей **приложений Teams** или подготовку в облаке, которые создают конфигурацию для локального или удаленного приложения Teams.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Файл манифеста предварительной версии":::

- Чтобы просмотреть манифест с реальным содержимым, Набор средств Teams создает файлы манифеста предварительного просмотра, щелкнув правой кнопкой мыши **файл manifest.template.json** в папке **appPackage** . Выберите **файл манифеста предварительной версии** > **для локального или** **azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Контекстное меню предварительного просмотра":::

Существует два других способа предварительного просмотра файла манифеста:

- Выберите **zip-пакет приложения Project** > **Teams Toolkit** > **,** а затем выберите **"Локальный"** или **"Для Azure"**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Zip-пакет приложения":::

- Вы также можете просмотреть тот же список меню, которые находятся в project > Teams Toolkit, если щелкнуть правой кнопкой мыши имя проекта и выбрать **Набор средств Teams** **в Обозреватель решений**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Список меню Teams Toolkit из обозревателя решений":::

    > [!NOTE]
    >В этом сценарии имя проекта **— MyTeamsApp1**.

### <a name="sync-local-changes-to-developer-portal"></a>Синхронизация локальных изменений с порталом разработчика

Локальные изменения можно синхронизировать с порталом разработчика после предварительного просмотра файла манифеста. Выберите манифест **обновления набора средств** >  **Project** >  Teams на **портале разработчика Teams** или контекстное меню Обозреватель решений.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Обновление манифеста на портале разработчика Teams":::

> [!NOTE]
> Изменения обновлены на портале разработчика Teams. Если на портале разработчика есть обновления вручную, их можно перезаписать. В **диалоговом** окне "Предупреждение" можно выбрать "**Перезаписать", "Обновить" или "****Отмена"**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Предупреждение об обновлении":::

## <a name="see-also"></a>См. также

- [Подготовка облачных ресурсов с помощью Visual Studio](provision-cloud-resources.md)
- [Развертывание приложения Teams в облаке с помощью Visual Studio](deploy-teams-app.md)
