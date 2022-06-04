---
title: Создание секрета клиента
description: Описание создания секрета клиента
ms.topic: how-to
ms.localizationpriority: medium
keywords: Вкладки проверки подлинности teams API Graph Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 79116a0da845cd143de695424a904cf5b5968a15
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888306"
---
# <a name="create-client-secret"></a>Создание секрета клиента

Секрет клиента — это строка, которую приложение использует для подтверждения своей личности при запросе маркера.

1. Выберите **"Управление** > **сертификатами & секретами"**.

2. Выберите **+Новый секрет клиента**.

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="Страница секрета клиента":::

   **Появится страница "Добавление секрета** клиента".

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="Добавление страницы секрета клиента" border="true":::

3. Введите описание.
4. Выберите срок действия секрета.
5. Нажмите **Добавить**.

   В браузере отобразится сообщение об обновлении секрета клиента и его отображении на странице.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="Добавлен секрет клиента":::

6. Нажмите кнопку копирования рядом со **значением** секрета клиента.
7. Сохраните значение, скопированное для последующего использования.

   > [!NOTE]
   > Обязательно скопируйте значение секрета клиента сразу после его создания. Значение отображается только во время создания секрета клиента и не может быть просмотрено после этого.
