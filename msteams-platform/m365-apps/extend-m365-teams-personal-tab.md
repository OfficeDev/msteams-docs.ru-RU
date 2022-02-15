---
title: Расширение личного приложения Teams вкладок в Microsoft 365
description: Расширение личного приложения Teams вкладок в Microsoft 365
ms.date: 11/15/2021
ms.topic: tutorial
ms.custom: Microsoft 365 apps
ms.localizationpriority: medium
ms.openlocfilehash: 9c6c88835dc24c64f93605d09ac15da5409add0f
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821418"
---
# <a name="extend-a-teams-personal-tab-across-microsoft-365"></a>Расширение личной вкладки Teams в Microsoft 365

> [!NOTE]
> *Расширение личной вкладки Teams во всех* Microsoft 365 доступно только в [предварительном просмотре общедоступных разработчиков](../resources/dev-preview/developer-preview-intro.md). Возможности, включенные в предварительную версию, могут быть неполными. Они также могут быть изменены перед общедоступным выпуском. Они предназначены только для целей тестирования и изучения. Их нельзя использовать в производственных приложениях.

Личные вкладки предоставляют отличный способ улучшить Microsoft Teams. С помощью личных вкладок вы можете предоставить пользователю доступ к приложению прямо в Teams, без необходимости повторного доступа пользователя к интерфейсу или входу. С помощью этого предварительного просмотра личные вкладки могут заживеть в других Microsoft 365 приложениях. В этом руководстве демонстрируется процесс принятия существующей личной вкладки Teams и ее обновления для запуска как в Outlook, так и в веб-опытом, а также Office в Интернете (office.com).

Обновление личного приложения для запуска в Outlook и Office Home включает следующие действия:

> [!div class="checklist"]
> * Обновление манифеста приложения
> * Обновление ссылок teamsJS SDK 
> * Изменение заглавных заглавок политики безопасности контента
> * Обновление Microsoft Azure Active Directory приложения (Azure AD) для единого знака (SSO)

Тестирование приложения потребует следующих действий:

> [!div class="checklist"]
> * Регистрация клиента Microsoft 365 в *Office 365 целевых выпусках*
> * Настройка учетной записи для доступа к предварительным версиям Outlook и Office приложений
> * Перенагрузите обновленное приложение в Teams

После этих действий приложение должно отображаться в предварительных версиях Outlook и Office приложениях.

## <a name="prerequisites"></a>Предварительные условия

Чтобы завершить этот учебник, вам потребуется:

* Клиент Microsoft 365 программы разработчиков
* Клиент песочницы, зарегистрированный *в Office 365 целевых выпусках*
* Машина с Office приложениями, установленными с Приложения Microsoft 365 *бета-канала*
* (Необязательный) [Teams набор средств](https://aka.ms/teams-toolkit) для Microsoft Visual Studio кода, чтобы помочь обновить код

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)

## <a name="prepare-your-personal-tab-for-the-upgrade"></a>Подготовка личной вкладки для обновления

Если у вас есть существующее приложение для личной вкладки, сделайте копию или филиал производственного проекта для тестирования и обновления идентификатора приложения в манифесте приложения, чтобы использовать новый идентификатор (в отличие от идентификатора производственного приложения).

Если вы хотите использовать пример кода для завершения этого руководства, выполните действия по настройке в примере списка [Todo](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend) Для создания личного приложения вкладки с помощью расширения Teams набор средств для Visual Studio Code. Или можно начать с того же образца списка Todo, обновленного для [TeamsJS SDK v2 Preview](https://github.com/OfficeDev/TeamsFx-Samples/tree/main/todo-list-with-Azure-backend-M365), и перейти к просмотру [личной вкладки в других Microsoft 365 опытом](#preview-your-personal-tab-in-other-microsoft-365-experiences). Обновленный пример также доступен в Teams набор средств: *developmentView* >  *samplesTodo* >  **List (Работает в Teams, Outlook и Office)**.

:::image type="content" source="images/toolkit-todo-sample.png" alt-text="Пример списка todo (Работает в Teams, Outlook и Office) в Teams набор средств":::


## <a name="update-the-app-manifest"></a>Обновление манифеста приложения

Чтобы включить [](/microsoftteams/platform/resources/schema/manifest-schema-dev-preview) `Microsoft 365 DevPreview` личную вкладку Teams в Office и Outlook, необходимо использовать схему предварительного просмотра Teams разработчика и версию манифеста.

Вы можете использовать Teams набор средств для обновления манифеста приложения или применять изменения вручную:

# <a name="teams-toolkit"></a>[Набор средств Teams](#tab/manifest-teams-toolkit)

1. Откройте *палитру Команд*: `Ctrl+Shift+P`
1. Запустите команду `Teams: Upgrade Teams manifest to support Outlook and Office apps` и выберите файл манифеста приложения. Изменения будут внесены на месте.

# <a name="manual-steps"></a>[Действия вручную](#tab/manifest-manual)

Откройте манифест Teams приложения и обновите `$schema` следующие `manifestVersion` значения:

```json
{
    "$schema" : "https://raw.githubusercontent.com/OfficeDev/microsoft-teams-app-schema/preview/DevPreview/MicrosoftTeams.schema.json",
    "manifestVersion" : "m365DevPreview"
}
```
---

Если вы Teams набор средств для создания личного приложения, вы также можете использовать его для проверки изменений в файле манифеста и выявления ошибок. Откройте палитру `Ctrl+Shift+P` команд и **Teams:** проверьте файл манифеста или выберите параметр из меню развертывания Teams набор средств (найдите значок Teams слева от Visual Studio Code).

:::image type="content" source="images/toolkit-validate-manifest-file.png" alt-text="Teams набор средств параметр &quot;Проверка файла манифеста&quot; в меню &quot;Развертывание&quot;":::

## <a name="update-sdk-references"></a>Обновление ссылок на SDK

Чтобы запустить Outlook и Office, вашему приложению необходимо будет зависеть от пакета npm `@microsoft/teams-js@2.0.0-beta.1` (или более *поздней бета-версии*). Хотя код с downlevel версиями поддерживается в Outlook и Office, предупреждения об амортизации будут зарегистрированы, и поддержка downlevel `@microsoft/teams-js` `@microsoft/teams-js` версий в Outlook и Office в конечном итоге прекратится.

Вы можете использовать Teams набор средств`@microsoft/teams-js`, чтобы автоматизировать некоторые изменения кода, чтобы принять следующую версию, но если вы хотите сделать шаги вручную, см. в Microsoft Teams [JavaScript клиента SDK Preview](using-teams-client-sdk-preview.md) для подробных сведений.

1. Откройте *палитру Команд*: `Ctrl+Shift+P`
1. Запуск команды `Teams: Upgrade Teams JS SDK references to support Outlook and Office apps`

По завершении утилита `package.json` обновит файл с зависимостью TeamsJS SDK Preview (`@microsoft/teams-js@2.0.0-beta.1` или более поздней версии `*.js/.ts` `*.jsx/.tsx` ), а ваши файлы и файлы будут обновлены с помощью:

> [!div class="checklist"]
> * `package.json` ссылки на предварительный просмотр TeamsJS SDK
> * Отчеты об импорте для предварительного просмотра командных команд SDK
> * [Вызовы функции, enum и интерфейса](using-teams-client-sdk-preview.md#apis-organized-into-capabilities) для предварительного просмотра TeamsJS SDK
> * `TODO`напоминания о комментариях для просмотра областей, на которые могут повлиять изменения [интерфейса Context](using-teams-client-sdk-preview.md#updates-to-the-context-interface)
> * `TODO` напоминания комментариев для обеспечения преобразования функций [обещаний](using-teams-client-sdk-preview.md#callbacks-converted-to-promises) из функций стилей вызова прошли хорошо на каждом сайте вызова найденного средства

> [!IMPORTANT]
> Код внутри *.html* не поддерживается инструментом обновления и требует ручных изменений.

> [!NOTE]
> Если вы хотите вручную обновить код, Microsoft Teams [javaScript клиент SDK Preview](using-teams-client-sdk-preview.md), чтобы узнать о необходимых изменениях.

## <a name="configure-content-security-policy-headers"></a>Настройка заглавных заглавок политики безопасности контента

[Как и в Microsoft Teams](/microsoftteams/platform/tabs/what-are-tabs), приложения вкладок находятся внутри ([элементы iframe](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/iframe)) в Office и Outlook веб-клиентах.

Если ваше приложение использует заглавные материалы политики безопасности контента [(CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy)), убедитесь, что вы разрешаете всем следующим [](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Security-Policy/frame-ancestors) предкам кадра в своих загонах CSP:

|Microsoft 365 хост| разрешение фрейм-предка|
|--|--|
| Teams | `teams.microsoft.com` |
| Office | `*.office.com` |
| Outlook | `outlook.office.com`, `outlook.office365.com` |

## <a name="update-azure-ad-app-registration-for-sso"></a>Обновление регистрации приложения Azure AD для SSO

Azure Active Directory для личных вкладок работает так же, как в Office и Outlook, как и в [Teams](/microsoftteams/platform/tabs/how-to/authentication/auth-aad-sso) году, однако вам потребуется добавить несколько идентификаторов клиентских приложений в регистрацию приложения Azure AD приложения вкладки на портале регистрации приложений клиента.

1. Во входе [на Microsoft Azure портал](https://portal.azure.com) с учетной записью клиента в песочнице.
1. Откройте **лезвие регистрации приложений** .
1. Выберите имя личного приложения вкладки, чтобы открыть регистрацию приложения. 
1. Выберите  **Expose aPI** (в *статье Управление*).

:::image type="content" source="images/azure-app-registration-clients.png" alt-text="Авторизировать клиентские ИД из лезвия *App registrations* на портале Azure":::

В разделе **Авторизованные клиентские приложения** убедитесь, `Client Id` что добавлены все следующие значения:

|Microsoft 365 клиентского приложения | Идентификатор клиента |
|--|--|
|Teams, мобильный |1fec8e78-bce4-4aaf-ab1b-5451cc387264 |
|Teams веб |5e3ce6c0-2b1f-4285-8d4b-75ee78787346 |
|Office.com  |4345a7b9-9a63-4910-a426-35363201d503|
|Office.com  |4765445b-32c6-49b0-83e6-1d93765276ca|
|Office рабочего стола  | 0ec893e0-5785-4de6-99da-4ed124e5296c |
|Классическое приложение Outlook | d3590ed6-52b3-4102-aeff-aad2292ab01c |
|Outlook Web Access | 00000002-0000-0ff1-ce00-00000000000000 |
|Outlook Web Access | bc59ab01-8403-45c6-8796-ac3ef710b3e3 |

## <a name="sideload-your-app-in-teams"></a>Загрузка неопубликованного приложения в Teams

Последний шаг — загрузка обновленной личной вкладки [(пакета](/microsoftteams/platform/concepts/build-and-test/apps-package) приложений) в Microsoft Teams. После завершения работы приложение будет доступно для Office и Outlook, а также Teams.

1. Пакет Teams приложения (манифест [и значки](/microsoftteams/platform/resources/schema/manifest-schema#icons) приложения) в почтовый файл. Если вы Teams набор средств для создания приложения, вы можете легко сделать это с помощью параметра пакета метаданных Zip **Teams** в меню развертывания Teams набор средств  `Ctrl+Shift+P` или в командной палитре Visual Studio Code:

    :::image type="content" source="images/toolkit-zip-teams-metadata-package.png" alt-text="Параметр &quot;Пакет Teams метаданных&quot; в Teams набор средств для Visual Studio Code":::

1. Войдите Teams учетную запись клиента в песочнице и убедитесь, что вы находитесь в Developer Preview. Вы можете убедиться, что вы на предварительном просмотре в клиенте Teams, нажав на меню ellipsis (**...**) в профиле пользователя и открывая около,  чтобы проверить, что параметр  предварительного просмотра разработчика переглушают.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Из Teams эллипсов откройте параметр &quot;About&quot; и убедитесь, что Developer Preview 'проверяется&quot;":::

1. Откройте области *Приложений* и **нажмите кнопку Upload настраиваемом** приложении, а затем **Upload для меня или моих команд**.

    :::image type="content" source="images/teams-upload-custom-app.png" alt-text="Кнопка Upload настраиваемом приложении в области Teams &quot;Приложения&quot;":::

1. Выберите пакет приложения и нажмите кнопку *Открыть*.

После загрузки Teams, ваша личная вкладка будет доступна в Outlook и Office. Не забудьте войти с помощью тех же учетных данных, что и для загрузки приложения в Teams.

Вы можете прикрепить приложение для быстрого доступа или найти приложение в вылете эллипсов (**...**) среди последних приложений в боковой панели слева.

> [!NOTE]
> Закрепление приложения в Teams не прикрепит его в качестве приложения в Office.com или Outlook.

## <a name="preview-your-personal-tab-in-other-microsoft-365-experiences"></a>Просмотр личной вкладки в других Microsoft 365 опытом

При обновлении личной вкладки Teams и ее боковой загрузке в Teams она также будет работать в Outlook и веб-клиентах и Office в Интернете (office.com). Вот как просмотреть его из этих Microsoft 365 опытом.

### <a name="outlook"></a>Outlook

Чтобы просмотреть приложение, Outlook на Windows, запустите Outlook и вопишитесь с помощью учетной записи клиента разработчика. Нажмите на эллипсы (**...**) на боковой панели. В установленных приложениях появится заголовок приложения с боковой загрузкой.

:::image type="content" source="images/outlook-desktop-more-apps.png" alt-text="Щелкните параметр ellipses ('More apps') на боковой панели Office настольного компьютера, чтобы увидеть установленные личные вкладки":::

Щелкните значок приложения, чтобы запустить приложение в Outlook.

### <a name="outlook-on-the-web"></a>Outlook в Интернете

Чтобы просмотреть приложение в Outlook в Интернете, посетите https://outlook.office.com и вопишитесь с помощью учетной записи клиента разработчика. Нажмите на эллипсы (**...**) на боковой панели. В установленных приложениях появится заголовок приложения с боковой загрузкой.

:::image type="content" source="images/outlook-web-more-apps.png" alt-text="Щелкните параметр ellipses ('More apps') на боковой панели outlook.com, чтобы увидеть установленные личные вкладки":::

Щелкните значок приложения для запуска и предварительного просмотра приложения, запущенного в Outlook в Интернете.

### <a name="office-on-the-web"></a>Office в Интернете

> [!IMPORTANT]
> Обратитесь к последним обновлениям Microsoft Teams [- Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) блог разработчика, чтобы проверить, доступна ли Office.com для Teams личных приложений для тестовых клиентов.

Для предварительного просмотра приложения, запущенного Office в Интернете, войдите в office.com с помощью тестовых учетных данных клиента. Нажмите на эллипсы (**...**) на боковой панели. В установленных приложениях появится заголовок приложения с боковой загрузкой.

Щелкните значок приложения, чтобы запустить приложение в Office Home.

## <a name="next-steps"></a>Дальнейшие действия

Outlook и Office с включенной поддержкой личных вкладок находятся в предварительном просмотре и не поддерживаются для использования в производстве. Вот как распределить личное приложение вкладки для предварительного просмотра аудиторий для целей тестирования.

### <a name="single-tenant-distribution"></a>Распределение с одним клиентом

Outlook и Office личные вкладки с поддержкой Office могут быть распространены среди аудитории предварительного просмотра в клиенте тестовых (или производственных) одним из трех способов:

#### <a name="teams-client"></a>Teams клиента

Из меню *Apps* выберите *Управление приложениями* > **.** Для этого требуется утверждение от ИТ-администратора.

#### <a name="microsoft-teams-admin-center"></a>Microsoft Teams Центр администрирования

Как администратор Teams, вы можете загрузить и предварительно установить пакет приложений для клиента вашей организации из https://admin.teams.microsoft.com/. Подробные Upload в центре [администрирования Microsoft Teams пользовательских](/MicrosoftTeams/upload-custom-apps) приложений.

#### <a name="microsoft-admin-center"></a>Центр администрирования Майкрософт

В качестве глобального администратора вы можете загрузить и предварительно установить пакет приложений из https://admin.microsoft.com/. Дополнительные сведения см. в Приложения Microsoft 365 и развертывании Приложения Microsoft 365 партнеров на [портале интегрированных](/microsoft-365/admin/manage/test-and-deploy-microsoft-365-apps) приложений.

### <a name="multi-tenant-distribution"></a>Распределение с несколькими арендаторами

Распространение в Microsoft AppSource не поддерживается во время предварительного предварительного просмотра Outlook и Office с Teams вкладками.
