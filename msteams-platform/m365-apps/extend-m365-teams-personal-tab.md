---
title: Расширение приложения личной вкладки Teams в Microsoft 365
description: Расширение приложения личной вкладки Teams в Microsoft 365
ms.date: 05/24/2022
ms.topic: tutorial
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 7c7c53b7b269e5c406cb27c3faee8b818dc567a6
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668139"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Расширение личной вкладки Teams в Microsoft 365

Личные вкладки — это отличный способ расширить возможности Microsoft Teams. Используя личные вкладки, вы можете предоставить пользователю доступ к приложению прямо в Teams, при этом ему не понадобится выходить из интерфейса или снова входить в систему. В этой предварительной версии личные вкладки могут подсвечиваться в других приложениях Microsoft 365. В этом руководстве демонстрируется процесс использования существующей личной вкладки Teams и ее обновления для работы как в настольном, так и в веб-интерфейсе Outlook, а также в Office в Интернете (office.com).

Обновление личного приложения для запуска в Outlook и Office состоит из следующих действий:

> [!div class="checklist"]
>
> * Обновите манифест вашего приложения
> * Обновите ссылки на TeamsJS SDK
> * Измените заголовки политики безопасности контента.
> * Обновите регистрацию приложения Microsoft Azure Active Directory (Azure AD) для единого входа (SSO)
> * Загрузите неопубликованное обновленное приложение в Teams

В остальной части этого руководства показано, как просмотреть личную вкладку в других Microsoft 365 приложениях.

## <a name="prerequisites"></a>Предварительные условия

Для следования этому руководству вам понадобятся:

* Клиент изолированной программной среды Microsoft 365 Developer Program
* Клиент песочницы, зарегистрированный в *целевых выпусках Office 365*
* Компьютер с приложениями Office, установленными из приложений Microsoft 365 *бета-канал*.
* (Необязательно) Расширение [Teams Toolkit](https://aka.ms/teams-toolkit) для Microsoft Visual Studio Code, помогающее обновлять код.

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Подготовьте личную вкладку к обновлению

Если у вас есть личное приложение табуляции, скопируйте или ветвь рабочего проекта для тестирования и обновите идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (отличается от рабочего идентификатора приложения для тестирования).

Если вы хотите использовать пример кода для работы с этим руководством, выполните действия по настройке в примере списка дел, чтобы создать личное приложение табуляции с помощью расширения Teams Toolkit для Visual Studio Code, а затем вернитесь к этой статье, чтобы обновить его для Microsoft 365.[](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend)

Кроме того, вы можете использовать базовое приложение Sign-On *Hello World*, уже включенное Microsoft 365 в следующем кратком руководстве, а затем перейти к загрузке неопубликованного приложения [в Teams](#sideload-your-app-in-teams).

### <a name="quickstart"></a>Быстрый запуск

Чтобы начать [с личной](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365) вкладки, которая уже включена для запуска в Outlook и Office, используйте расширение Teams Toolkit для Visual Studio Code.

1. В Visual Studio Code откройте палитру команд (`Ctrl+Shift+P`), введите `Teams: Create a new Teams app`.
1. Выберите **личную вкладку с поддержкой единого входа**.

    :::image type="content" source="images/toolkit-tab-sample.png" alt-text="Образец списка дел (работает в Teams, Outlook и Office) в Teams Toolkit":::

1. Выберите расположение папки рабочей области на локальном компьютере.
1. Откройте палитру команд (`Ctrl+Shift+P`) `Teams: Provision in the cloud` и введите необходимые ресурсы приложения (план Служба приложений, учетную запись служба хранилища, приложение-функцию, управляемое удостоверение) в учетной записи Azure.
1. Откройте палитру команд (`Ctrl+Shift+P`) и введите `Teams: Deploy to the cloud`, чтобы развернуть образец кода на подготовленных ресурсах в Azure и запустить приложение.

Здесь вы можете сразу перейти к загрузке неопубликованного приложения в Teams просмотреть его в Outlook и Office.[](#sideload-your-app-in-teams) (Манифест приложения и вызовы API TeamsJS уже обновлены для Microsoft 365.)

## <a name="update-the-app-manifest"></a>Обновите манифест приложения

Вам потребуется использовать версию [](../resources/schema/manifest-schema.md) `1.13` схемы манифеста Teams разработчика, чтобы Teams личную вкладку для Outlook и Office.

Существует два варианта обновления манифеста приложения:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте палитру команд: `Ctrl+Shift+P`.
1. Запустите команду `Teams: Upgrade Teams manifest` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://developer.microsoft.com/json-schemas/teams/v1.13/MicrosoftTeams.schema.json",
    "manifestVersion" : "1.13"
}
```

---

Если вы использовали Teams Toolkit для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд (`Ctrl+Shift+P`) и найдите **Teams: Проверка файла манифеста**.

## <a name="update-sdk-references"></a>Обновление ссылок на SDK

Для запуска в Outlook и Office приложение должно ссылаться на пакет npm (или более `@microsoft/teams-js@2.0.0` поздней версии). Хотя код с более ранними версиями поддерживается в Outlook и Office, предупреждения об устаревании регистрируются, и поддержка более ранних версий TeamsJS в Outlook и Office в конечном итоге прекращается.

С помощью Teams Toolkit можно определить и автоматизировать необходимые изменения кода для обновления с версии 1.x TeamsJS до TeamsJS версии 2.0.0. Кроме того, те же действия можно выполнить вручную. Дополнительные [сведения см. Microsoft Teams клиентского пакета SDK для JavaScript](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20).

1. Откройте *палитру команд*: `Ctrl+Shift+P`.
1. Выполните команду `Teams: Upgrade Teams JS SDK and code references`.

По завершении файл *package.json* `@microsoft/teams-js@2.0.0` будет ссылаться (или выше), `*.js/.ts` `*.jsx/.tsx` а файлы и файлы будут обновлены с помощью:

> [!div class="checklist"]
> * Инструкции импорта для teams-js@2.0.0
> * [Вызовы функций, перечислений и интерфейсов](../tabs/how-to/using-teams-client-sdk.md#whats-new-in-teamsjs-version-20) для teams-js@2.0.0
> * `TODO` напоминания примечаний пометки областей, на которые могут повлиять изменения [контекстного](../tabs/how-to/using-teams-client-sdk.md#updates-to-the-context-interface) интерфейса
> * `TODO` напоминания примечаний [для преобразования функций обратного вызова в обещания](../tabs/how-to/using-teams-client-sdk.md#callbacks-converted-to-promises)

> [!IMPORTANT]
> Код внутри *.html* не поддерживается средствами обновления и требует внесения изменений вручную.

## <a name="configure-content-security-policy-headers"></a>Настройка заголовков Content Security Policy

Как и Microsoft Teams, приложения табуляции размещаются в элементах [iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe) в Office и Outlook веб-клиентах.

Если приложение использует заголовки политики безопасности [содержимого (CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)), убедитесь, что в заголовках CSP разрешены [](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) все следующие предки кадров:

|Ведущий сайт Microsoft 365| разрешение для фрейма-предка|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Azure AD для единого входа

[Azure Active Directory (AD) единый вход (SSO)](../tabs/how-to/authentication/auth-aad-sso.md) для личных вкладок работает в Office и Outlook так же, как в Teams. Однако вам потребуется добавить несколько идентификаторов клиентского приложения в Azure AD регистрации приложения вкладки на портале *Регистрация приложений клиента.*

1. Войдите на [портал Microsoft Azure](https://portal.azure.com) с помощью учетной записи арендатора песочницы.
1. Откройте колонку **регистрации приложений**.
1. Выберите имя приложения с личной вкладкой, чтобы открыть регистрацию приложения.
1. Выберите **Открыть API** (в разделе *Управление*).

    :::image type="content" source="images/azure-app-registration-clients.png" alt-text="Авторизуйте идентификаторы клиентов из колонки *Регистрации приложений* на портале Azure":::

1. В разделе **Авторизованные клиентские приложения** убедитесь, что добавлены все следующие `Client Id` значения:

    |Клиентское приложение Microsoft 365 | Идентификатор клиента |
    |--|--|
    |Классическое, мобильное приложение Teams |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
    |Веб-приложение Teams |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
    |Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
    |Классические приложения Office  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
    |Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
    |Outlook Web Access | 00000002-0000-0ff1-ce00-000000000000 |
    |Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Загрузка неопубликованного приложения в Teams

Последним шагом к запуску приложения в Office и Outlook является загрузка неопубликованного пакета приложения личной вкладки в Microsoft Teams.[](..//concepts/build-and-test/apps-package.md)

1. Упакуйте Teams приложения ([манифест](../resources/schema/manifest-schema.md) и [значки приложения](/microsoftteams/platform/resources/schema/manifest-schema#icons)) в ZIP-файл. Если вы использовали Teams Toolkit для создания приложения, это можно легко сделать с помощью параметра zip **Teams** пакета метаданных в меню развертывания Teams Toolkit.

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр ''Zip Teams metadata package'' в расширении Teams Toolkit для Visual Studio Code":::

1. Войдите в Teams с помощью учетной записи клиента песочницы и переключитесь в режим *предварительной версии для разработчиков*. Выберите меню с многоточием (**...**) в профиле пользователя, а затем **выберите "О** >  предварительной **версии для разработчиков"**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="В меню с многоточием Teams откройте «О программе» и выберите параметр «Предварительная версия для разработчиков»":::

1. Выберите **Приложения**, чтобы открыть область **Управление приложениями**. Затем выберите **Опубликовать приложение**.

    :::image type="content" source="images/teams-manage-your-apps.png" alt-text="Откройте панель «Управление приложениями» и выберите «Опубликовать приложение»":::

1. Выберите **параметр "Отправить пользовательское приложение** " и выберите пакет приложения.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="«Отправить настраиваемое приложение» в Teams":::

После загрузки неопубликованного Teams личная вкладка будет доступна в Outlook и Office. Не забудьте войти с помощью тех же учетных данных, которые использовались для входа Teams загрузку неопубликованного приложения.

Вы можете закрепить приложение для быстрого доступа или найти его во всплывающем меню с многоточием (**...**) среди последних приложений на боковой панели слева. Закрепите приложение в Teams не закрепляйте его как приложение в Office или Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Предварительный просмотр личной вкладки в других приложениях Microsoft 365.

Ниже описано, как просмотреть приложение, работающее в Office и Outlook, веб-приложениях и Windows классических клиентах.

> [!NOTE]
> Удаление приложения из Teams также удаляет его из каталогов "Дополнительные приложения" Outlook и  Office. Если вы используете пример приложения Teams Toolkit, указанный выше.

### <a name="outlook-on-windows"></a>Outlook для Windows

Чтобы просмотреть приложение, работающее в Outlook на рабочем столе Windows:

1. Запустите Outlook и войдите в систему, используя свою учетную запись разработчика.
1. На боковой панели выберите "  **Другие приложения"**. Заголовок неопубликованного приложения отображается среди установленных приложений.
1. Щелкните значок приложения, чтобы запустить его в Outlook.

    :::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели настольного клиента Outlook, чтобы просмотреть установленные личные вкладки":::.

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы просмотреть свое приложение в Outlook в Интернете:

1. Перейдите в [Outlook в Интернете](https://outlook.office.com) и войдите, используя свою учетную запись клиента разработчика.
1. Щелкните многоточие (**...**) на боковой панели. Заголовок неопубликованного приложения отображается среди установленных приложений.
1. Щелкните значок приложения, чтобы запустить и просмотреть приложение, работающее в Outlook в Интернете.

    :::image type="content" source="images/outlook-web-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели Outlook.com, чтобы просмотреть установленные личные вкладки":::

### <a name="office-on-windows"></a>Office для Windows

Чтобы просмотреть приложение, работающее в Office на рабочем столе Windows:

1. Запустите Office и войдите в систему, используя учетную запись разработчика.
1. Щелкните многоточие (**...**) на боковой панели. Заголовок неопубликованного приложения отображается среди установленных приложений.
1. Щелкните значок приложения, чтобы запустить его в Office.

    :::image type="content" source="images/office-desktop-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели клиента Office для настольных компьютеров, чтобы просмотреть установленные личные вкладки":::

### <a name="office-on-the-web"></a>Office в Интернете

Чтобы предварительно просмотреть приложение, работающее в Office в Интернете, выполните указанные ниже действия.

1. Войдите **в office.com** с помощью тестовых учетных данных клиента.
1. Щелкните **значок** "Приложения" на боковой панели. Заголовок неопубликованного приложения отображается среди установленных приложений.
1. Щелкните значок приложения, чтобы запустить его в Office в Интернете.

    :::image type="content" source="images/office-web-more-apps.png" alt-text="Щелкните параметр &quot;Другие приложения&quot; на боковой панели office.com, чтобы просмотреть установленные личные вкладки.":::

## <a name="troubleshooting"></a>Устранение неполадок

В настоящее время подмножество типов Teams и возможностей поддерживается в Outlook и Office клиентах. Эта поддержка со временем расширяется.

См. [Microsoft 365,](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook) чтобы проверить поддержку узлов для различных возможностей TeamsJS.

Общие сведения о поддержке Microsoft 365 и платформ для приложений Teams см. в Teams приложениях [Microsoft 365](overview.md).

Вы можете проверить поддержку `isSupported()` узла для данной возможности во время выполнения, вызвав функцию для этой возможности (пространство имен) и соответствующим образом скорректируйте поведение приложения. Это позволяет приложению включить пользовательский интерфейс и функциональные возможности на узлах, которые его поддерживают, и обеспечить корректный резервный интерфейс на узлах, которые этого не поддерживают. Дополнительные сведения см. в разделе ["Дифференцирование интерфейса приложения"](../tabs/how-to/using-teams-client-sdk.md#differentiate-your-app-experience).

Используйте [каналы сообщества разработчиков Microsoft Teams](/microsoftteams/platform/feedback), чтобы сообщать о проблемах и оставлять отзывы.

### <a name="debugging"></a>Отладка

В Teams Toolkit можно отладить (`F5`) приложение табуляции, работающее в Office и Outlook, а также Teams.

:::image type="content" source="images/toolkit-debug-targets.png" alt-text="Выберите один Teams, Outlook и Office отладки в Teams Toolkit":::

При первом запуске локальной отладки в Office или Outlook вам будет предложено войти в учетную запись Microsoft 365 клиента и установить самозаверяющий тестовый сертификат. Вам также будет предложено вручную установить Teams. Выберите **"Установить в Teams**", чтобы открыть окно браузера и вручную установить приложение. Затем щелкните **"Продолжить**", чтобы перейти к отладке приложения в Office/Outlook.

:::image type="content" source="images/toolkit-dialog-teams-install.png" alt-text="Диалоговое окно набора средств Teams установки":::

Оставьте отзыв и ведите отчет о любых проблемах с Teams Toolkit на [Microsoft Teams Framework (TeamsFx).](https://github.com/OfficeDev/TeamsFx/issues)

## <a name="next-step"></a>Следующий этап

Опубликуйте приложение, чтобы его можно было обнаруживать в Teams, в Outlook и в Office:

> [!div class="nextstepaction"]
> [Публикация приложений Teams для Outlook и Office](publish.md)

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **Node.js** |
|---------------|--------------|--------|
| Список дел | Редактируемый список дел с единым входом, созданным React и Функции Azure. Работает только в Teams (используйте этот пример приложения, чтобы опробовать процесс обновления, описанный в этом руководстве). | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend)  |
| Список дел (Microsoft 365) | Редактируемый список дел с единым входом, созданным React и Функции Azure. Работает в Teams, Outlook, Office. | [View](https://github.com/OfficeDev/TeamsFx-Samples/tree/ga/todo-list-with-Azure-backend-M365)|
| Редактор изображений (Microsoft 365) | Создание, изменение, открытие и сохранение изображений с помощью Microsoft API Graph. Работает в Teams, Outlook, Office. | [View](https://github.com/OfficeDev/m365-extensibility-image-editor) |
