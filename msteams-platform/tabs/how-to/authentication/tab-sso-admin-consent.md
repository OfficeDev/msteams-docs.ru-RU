---
title: Настройка согласия администратора
description: Описание настройки согласия администратора
ms.topic: how-to
ms.localizationpriority: medium
keywords: Вкладки проверки подлинности teams API Graph Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: dd954ef1ede05b6025b12512dfcee03044223642
ms.sourcegitcommit: e16b51a49756e0fe4eaf239898e28d3021f552da
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2022
ms.locfileid: "65888311"
---
# <a name="configure-admin-consent"></a>Настройка согласия администратора

Вы можете определить область приложения для предоставленного API и определить, могут ли пользователи дать согласие на эту область в каталогах, где включено согласие пользователя. Вы можете разрешить только администраторам предоставлять согласие на разрешения с более высоким уровнем привилегий.

## <a name="to-expose-an-api"></a>Предоставление API

1. На **панели** >  слева выберите "Управление **предоставлением API**".

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-api-menu.png" alt-text="Предоставление параметра меню API." border="false":::

    **Появится страница "Предоставление API**".

1. Выберите **"Задать** ", чтобы создать универсальный код ресурса (URI) идентификатора приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/expose-an-api.png" alt-text="Задание URI идентификатора приложения" border="false":::

    Появится раздел для настройки URI идентификатора приложения.

1. Введите URI идентификатора приложения и нажмите кнопку " **Сохранить"**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/set-app-id-uri.png" alt-text="URI кода надстройки" border="true":::

    В браузере отображается сообщение об обновлении URI идентификатора приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-msg.png" alt-text="Сообщение URI идентификатора приложения" border="false":::

    URI идентификатора приложения отображается на странице.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/app-id-uri-added.png" alt-text="Обновлен URI идентификатора приложения" border="false":::

## <a name="to-configure-api-scope"></a>Настройка области API

1. Выберите **"+ Добавить область** " в областях **, определенных в этом разделе API** .

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/select-scope.png" alt-text="Выбор области" border="true":::

    **Появится страница "Добавление области**".

1. Введите сведения о приложении для области приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-scope.png" alt-text="Добавление сведений об области" border="true":::

    1. Введите имя области. Это поле является обязательным.
    1. Выберите **администраторов и пользователей,** чтобы настроить пользователей, которые могут дать согласие на использование учетных данных для входа пользователя. По умолчанию используется только **администратор.**
    1. Введите **отображаемое имя согласия администратора**. Это поле является обязательным.
    1. Введите описание согласия администратора. Это поле является обязательным.
    1. Введите **отображаемое имя согласия пользователя**.
    1. Введите описание согласия пользователя.
    1. Выберите параметр **"Включено** " для состояния.
    1. Нажмите **Добавить область**.

    В браузере отображается сообщение о добавлении области.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added-msg.png" alt-text="Сообщение о добавлении области" border="false":::

    URI идентификатора приложения отображается на странице.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/scope-added.png" alt-text="Область добавлена и отображена" border="false":::

## <a name="to-configure-authorized-client-application"></a>Настройка авторизованного клиентского приложения

1. Перейдите на **страницу "Предоставление API** " **в раздел** авторизованного клиентского приложения и выберите **"+ Добавить клиентское приложение"**.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/auth-client-apps.png" alt-text="Авторизованные клиентские приложения" border="true":::

    **Появится страница "Добавление клиентского** приложения".

1. Введите сведения о добавлении клиентского приложения. В этом разделе вы добавите два клиентских приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/add-client-app.png" alt-text="Добавление клиентского приложения" border="true":::

    1. **Введите 1fec8e78-bce4-4aaf-ab1b-5451cc387264 в** качестве идентификатора клиента для мобильного или настольного приложения Teams.
    1. Выберите идентификатор приложения, созданный для приложения, для **авторизованных областей**.
    1. Нажмите кнопку **Добавить приложение**.

    В браузере отобразится сообщение о добавлении клиентского приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Добавлено сообщение о добавлении клиентского приложения" border="false":::

    Идентификаторы клиентского приложения отображаются на странице.

1. Повторите предыдущий шаг, чтобы добавить клиентское приложение для веб-приложения Teams.

    1. **Введите 5e3ce6c0-2b1f-4285-8d4b-75ee78787346** в качестве идентификатора клиента для веб-приложения.
    1. Выберите идентификатор приложения, созданный для приложения, для **авторизованных областей**.
    1. Нажмите кнопку **Добавить приложение**.

    В браузере отобразится сообщение о добавлении клиентского приложения.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/update-app-auth-msg.png" alt-text="Добавлено сообщение о добавлении клиентского приложения для веб-приложения" border="false":::

    Идентификаторы клиентского приложения отображаются на странице.

    :::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/client-app-added.png" alt-text="Добавлено и отображено клиентское приложение" border="true":::
