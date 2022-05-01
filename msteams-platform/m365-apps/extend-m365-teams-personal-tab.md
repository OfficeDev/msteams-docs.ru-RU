---
title: Расширение приложения личной вкладки Teams в Microsoft 365
description: Расширение приложения личной вкладки Teams в Microsoft 365
ms.date: 02/11/2022
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: high
ms.openlocfilehash: 873a6fa6207d122581e18cef0ae922ffca87762f
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111523"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Расширение личной вкладки Teams в Microsoft 365

> [!NOTE]
> *Расширение личной вкладки Teams в Microsoft 365* сейчас доступно только в [общедоступной предварительной версии для разработчиков](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

Личные вкладки — это отличный способ расширить возможности Microsoft Teams. Используя личные вкладки, вы можете предоставить пользователю доступ к приложению прямо в Teams, при этом ему не понадобится выходить из интерфейса или снова входить в систему. В этой предварительной версии личные вкладки могут подсвечиваться в других приложениях Microsoft 365. В этом руководстве демонстрируется процесс использования существующей личной вкладки Teams и ее обновления для работы как в настольном, так и в веб-интерфейсе Outlook, а также в Office в Интернете (office.com).

Обновление личного приложения для работы в Outlook и Office Home включает следующие шаги:

> [!div class="checklist"]
>
> * Обновите манифест вашего приложения
> * Обновите ссылки на TeamsJS SDK
> * Измените заголовки политики безопасности контента.
> * Обновите регистрацию приложения Microsoft Azure Active Directory (Azure AD) для единого входа (SSO)

Для тестирования приложения сделайте следующее:

> [!div class="checklist"]
>
> * Зарегистрируйте своего клиента Microsoft 365 в *целевых выпусках Office 365*.
> * Настройте учетную запись для доступа к предварительным версиям приложений Outlook и Office.
> * Загрузите неопубликованное обновленное приложение в Teams

После этого ваше приложение должно появиться в предварительных версиях приложений Outlook и Office.

## <a name="prerequisites"></a>Предварительные условия

Для следования этому руководству вам понадобятся:

* Клиент изолированной программной среды Microsoft 365 Developer Program
* Клиент песочницы, зарегистрированный в *целевых выпусках Office 365*
* Компьютер с приложениями Office, установленными из приложений Microsoft 365 *бета-канал*.
* (Необязательно) Расширение [Teams Toolkit](https://aka.ms/teams-toolkit) для Microsoft Visual Studio Code, помогающее обновлять код.

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Подготовьте личную вкладку к обновлению

Если у вас есть приложение с личной вкладкой, сделайте копию или ветку рабочего проекта для тестирования и обновите идентификатор приложения в манифесте приложения, чтобы использовать новый идентификатор (отличный от идентификатора рабочего приложения).

Если вы хотите использовать образец кода для выполнения этого руководства, выполните действия по настройке в разделе [Начало работы с образцом списка задач](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend), чтобы создать приложение с личной вкладкой с помощью расширения Teams Toolkit для Visual Studio Code. Или вы можете начать с того же [образца списка задач, обновленного для TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365), и перейти к [предварительному просмотру личной вкладки в других возможностях Microsoft 365](#preview-your-personal-tab-in-other-microsoft-365-experiences). Обновленный пример также доступен в расширении Teams Toolkit: *Разработка* > *Посмотреть образцы* > **Список дел (работает в Teams, Outlook и Office)**.

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Образец списка дел (работает в Teams, Outlook и Office) в Teams Toolkit":::

## <a name="update-the-app-manifest"></a>Обновите манифест приложения

Вам потребуется использовать схему манифеста [Предварительной версии для разработчиков Teams](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) и версию манифеста `Microsoft 365 DevPreview`, чтобы ваша личная вкладка Teams работала в Office и Outlook.

Вы можете использовать Teams Toolkit для обновления манифеста приложения или применить изменения вручную:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Запустите команду `Teams: Upgrade Teams manifest to support Outlook and Office apps` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Выполнение вручную](#tab/manifest-manual)

Откройте манифест приложения Teams и обновите `$schema` и `manifestVersion` со следующими значениями:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```

---

Если вы использовали Teams Toolkit для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру команд `Ctrl+Shift+P` и найдите **Teams: проверьте файл манифеста** или выберите параметр в меню ''Развертывание'' набора инструментов Teams (найдите значок Teams в левой части кода Visual Studio).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Параметр Teams Toolkit &quot;Проверить файл манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="update-sdk-references"></a>Обновление ссылок на SDK

Для работы в Outlook и Office ваше приложение должно зависеть от пакета npm `@microsoft/teams-js@2.0.0-beta.1` (или более поздней *бета-версии*). Хотя код с более ранними версиями `@microsoft/teams-js` поддерживается в Outlook и Office, предупреждения об устаревании будут регистрироваться, а поддержка более ранних версий `@microsoft/teams-js` в Outlook и Office со временем прекратится.

Вы можете использовать Teams Toolkit, чтобы автоматизировать некоторые изменения кода для перехода на следующую версию `@microsoft/teams-js`, но если вы хотите выполнить эти шаги вручную, см. подробности в статье [Предварительная версия пакета SDK для клиента Microsoft Teams JavaScript](using-teams-client-sdk-preview.md).

1. Откройте *Палитру команд*: `Ctrl+Shift+P`
1. Выполните команду `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

По завершении утилита обновит ваш файл `package.json` с помощью зависимости TeamsJS SDK Preview (`@microsoft/teams-js@2.0.0-beta.1` или более поздней версии), а файлы `*.js/.ts` и `*.jsx/.tsx` будут обновлены с помощью:

> [!div class="checklist"]
>
> * `package.json` ссылки на TeamsJS SDK Preview
> * Операторы импорта для TeamsJS SDK Preview
> * [Вызовы функций, Enum и интерфейса](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) для TeamsJS SDK Preview
> * `TODO` комментарий с напоминанием о необходимости просмотра областей, на которые могут повлиять изменения интерфейса [Контекста](using-teams-client-sdk-preview.md#updates-to-the-context-interface)
> * `TODO` напоминания о комментариях для обеспечения преобразования [ в функции promise из функций в стиле обратного вызова ](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) прошли успешно на каждом сайте вызова, найденном инструментом

> [!IMPORTANT]
> Код в файлах *.html* не поддерживается инструментами обновления и требует внесения изменений вручную.

> [!NOTE]
> Если вы хотите вручную обновить свой код, ознакомьтесь с [предварительной версией пакета SDK для клиента Microsoft Teams JavaScript](using-teams-client-sdk-preview.md), чтобы узнать о необходимых изменениях.

## <a name="configure-content-security-policy-headers"></a>Настройка заголовков Content Security Policy

[Как и в Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), приложения вкладок размещаются внутри ([элементов iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) в веб-клиентах Office и Outlook.

Если ваше приложение использует заголовки [Content Security Policy](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy) (CSP), убедитесь, что вы разрешаете все следующие [фреймы-предки](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) в заголовках CSP:

|Ведущий сайт Microsoft 365| разрешение для фрейма-предка|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com`, `outlook-sdf.office.com`, `outlook-sdf.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Azure AD для единого входа

Единый вход в Azure Active Directory (SSO) для личных вкладок работает в Office и Outlook так же, [как и в Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso), однако вам потребуется добавить несколько идентификаторов клиентских приложений в регистрацию приложения Azure AD для вкладки в клиенте. Портал *регистрации приложений*.

1. Войдите на [портал Microsoft Azure](https://portal.azure.com) с помощью учетной записи арендатора песочницы.
1. Откройте колонку **регистрации приложений**.
1. Выберите имя приложения с личной вкладкой, чтобы открыть регистрацию приложения.
1. Выберите **Открыть API** (в разделе *Управление*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Авторизуйте идентификаторы клиентов из колонки *Регистрации приложений* на портале Azure":::

В разделе **Авторизованные клиентские приложения** убедитесь, что добавлены все следующие `Client Id` значения:

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

Последний шаг — загрузить обновленную личную вкладку ([пакет приложения](/microsoftteams/platform/concepts/build-and-test/apps-package)) в Microsoft Teams. После завершения ваше приложение будет доступно для запуска в Office и Outlook, а также в Teams.

1. Упакуйте приложение Teams (манифест и [значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложений) в ZIP-файл. Если вы использовали Teams Toolkit для создания своего приложения, вы можете легко сделать это с помощью параметра **пакета метаданных Zip Teams** в меню *Развертывание* Teams Toolkit или в палитре команд `Ctrl+Shift+P` Visual Studio Code:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр ''Zip Teams metadata package'' в расширении Teams Toolkit для Visual Studio Code":::

1. Войдите в Teams с помощью учетной записи клиента песочницы и убедитесь, что вы находитесь в общедоступной предварительной версии для разработчиков. Вы можете убедиться, что вы находитесь в режиме предварительного просмотра в клиенте Teams, щелкнув меню с многоточием (**...**) в своем профиле пользователя и открыв **О программе**, чтобы убедиться, что параметр *Предварительная версия для разработчиков* включен.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="В меню с многоточием Teams откройте ''О программе'' и убедитесь, что установлен флажок ''Предварительная версия для разработчиков''.":::

1. Откройте панель *Приложения* и щелкните **Загрузить пользовательское приложение**, а затем **Загрузить для меня или моей группы**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка ''Отправить пользовательское приложение'' на панели ''Приложения'' Teams":::

1. Выберите пакет приложения и нажмите *Открыть*.

После загрузки неопубликованного приложения через Teams личная вкладка будет доступна в Outlook и Office. Обязательно войдите в систему с теми же учетными данными, которые вы использовали для загрузки неопубликованного приложения в Teams.

Вы можете закрепить приложение для быстрого доступа или найти его во всплывающем меню с многоточием (**...**) среди последних приложений на боковой панели слева.

> [!NOTE]
> Закрепление приложения в Teams не закрепит его в качестве приложения в Office.com или Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Предварительный просмотр личной вкладки в других приложениях Microsoft 365.

Когда вы обновляете личную вкладку Teams и загружаете ее в Teams, она работает в Outlook для Windows, в Интернете, Office для Windows и в Интернете (office.com). Вот как просмотреть его из этих возможностей Microsoft 365.

### <a name="outlook-on-windows"></a>Outlook для Windows

Чтобы просмотреть приложение, работающее в Outlook на рабочем столе Windows:

1. Запустите Outlook и войдите в систему, используя свою учетную запись разработчика.
1. Щелкните многоточие (**...**) на боковой панели. Название вашего неопубликованного приложения появится среди ваших установленных приложений.
1. Щелкните значок приложения, чтобы запустить его в Outlook.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели настольного клиента Outlook, чтобы просмотреть установленные личные вкладки":::.

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы просмотреть свое приложение в Outlook в Интернете:

1. Перейдите в [Outlook в Интернете](https://outlook.office.com) и войдите, используя свою учетную запись клиента разработчика.
1. Щелкните многоточие (**...**) на боковой панели. Название вашего неопубликованного приложения появится среди ваших установленных приложений.
1. Щелкните значок своего приложения, чтобы запустить и просмотреть приложение, работающее в Outlook в Интернете.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели Outlook.com, чтобы просмотреть установленные личные вкладки":::

### <a name="office-on-windows"></a>Office для Windows

Чтобы просмотреть приложение, работающее в Office на рабочем столе Windows:

1. Запустите Office и войдите в систему, используя учетную запись разработчика.
1. Щелкните многоточие (**...**) на боковой панели. Название вашего неопубликованного приложения появится среди ваших установленных приложений.
1. Щелкните значок приложения, чтобы запустить его в Office.

:::image type="content" source="images/office-desktop-more-apps.png" alt-text="Щелкните многоточие (''Дополнительные приложения'') на боковой панели клиента Office для настольных компьютеров, чтобы просмотреть установленные личные вкладки":::

### <a name="office-on-the-web"></a>Office в Интернете

Чтобы предварительно просмотреть приложение, работающее в Office в Интернете, выполните указанные ниже действия.

1. Войдите на сайт office.com с тестовыми учетными данными арендатора.
1. Щелкните многоточие (**...**) на боковой панели. Название вашего неопубликованного приложения появится среди ваших установленных приложений.
1. Щелкните значок своего приложения, чтобы запустить его в Office в Интернете.

:::image type="content" source="images/office-web-more-apps.png" alt-text="Нажмите многоточие (''Дополнительные приложения'') на боковой панели office.com, чтобы просмотреть установленные личные вкладки.":::

## <a name="next-steps"></a>Дальнейшие действия

Личные вкладки с поддержкой Outlook и Office находятся в предварительной версии и не поддерживаются для использования в рабочей среде. Вот как распространить приложение личной вкладки для предварительного просмотра аудиторий в целях тестирования.

### <a name="single-tenant-distribution"></a>Распространение с одним клиентом

Персональные вкладки с поддержкой Outlook и Office можно распространять среди аудитории предварительного просмотра в тестовом (или рабочем) клиенте одним из трех способов:

#### <a name="teams-client"></a>Клиент Teams

В меню *Приложения* выберите *Управление приложениями* > **Отправить приложение в организацию**. Для этого требуется одобрение ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Центр администрирования Microsoft Teams

Как администратор Teams, вы можете отправить и предварительно установить пакет приложения для клиента организации из [Администратора Teams](https://admin.teams.microsoft.com/). Подробнее в статье [Загрузка пользовательских приложений в центре администрирования Microsoft Teams.](/MicrosoftTeams/upload-custom-apps)

#### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

Как глобальный администратор, вы можете загрузить и предварительно установить пакет приложения из [Администратора Майкрософт](https://admin.microsoft.com/). Подробнее в разделе [Тестирование и развертывание приложений Microsoft 365 партнерами на портале интегрированных приложений](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps).

### <a name="multitenant-distribution"></a>Мультиклиентское распределение

Распространение в Microsoft AppSource не поддерживается во время этой ранней предварительной версии личных вкладок Teams с поддержкой Outlook и Office для разработчиков.
