---
title: Создание секрета клиента
description: Описание создания секрета клиента
ms.topic: how-to
ms.localizationpriority: medium
keywords: вкладки проверки подлинности teams Microsoft Azure Active Directory (Azure AD) API Graph
ms.openlocfilehash: 77d1c4e43c9bdfb9d2cb9e3e97ee3a26b8b0fa01
ms.sourcegitcommit: c398dfdae9ed96f12e1401ac7c8d0228ff9c0a2b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2022
ms.locfileid: "66558851"
---
# <a name="create-client-secret"></a>Создание секрета клиента

Секрет клиента — это строка, которую приложение использует для подтверждения своей личности при запросе маркера.

1. Выберите **"Управление** > **сертификатами & секретами"**.

2. Выберите **+Новый секрет клиента**.

    :::image type="content" source="../../../assets/images/adaptive-cards/client-secret.png" alt-text="Страница секрета клиента":::

   **Появится страница "Добавление секрета** клиента".

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-secret.png" alt-text="Добавление страницы секрета клиента":::

3. Введите описание.
4. Выберите срок действия секрета.
5. Нажмите **Добавить**.

   В браузере отобразится сообщение об обновлении секрета клиента и его отображении на странице.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-secret-added.png" alt-text="Добавлен секрет клиента":::

6. Нажмите кнопку копирования рядом со **значением** секрета клиента.
7. Сохраните значение, скопированное для последующего использования.

   > [!NOTE]
   > Обязательно скопируйте значение секрета клиента сразу после его создания. Значение отображается только во время создания секрета клиента и не может быть просмотрено после этого.
