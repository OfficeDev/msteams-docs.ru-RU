---
title: Предварительные требования для создания приложения Teams с помощью Visual Studio Code
author: zyxiaoyuer
description: В этом модуле вы узнаете о предварительных требованиях, необходимых для инструментов и пакета SDK
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 412b7bfedb6ba39f1d38f42aac56cc793ea385b1
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617280"
---
# <a name="prerequisites-for-creating-your-teams-app"></a>Предварительные требования для создания приложения Teams

Прежде чем приступить к созданию приложения Teams, убедитесь, что выполнены следующие предварительные требования:

* [Основные требования для создания приложения Teams](#basic-requirements-to-build-your-teams-app)
* [Подготовка учетных записей для создания приложения Teams](#accounts-to-build-your-teams-app)
* [Разрешение на загрузку неопубликованных приложений](#sideloading-permission)

## <a name="basic-requirements-to-build-your-teams-app"></a>Основные требования для создания приложения Teams

Перед началом сборки приложения Teams убедитесь, что выполнены следующие требования:

| &nbsp; | Основные требования | Для использования| Для типа среды|
   | --- | --- | --- |
   | **Required** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | Набор средств Teams| Расширение Microsoft Visual Studio Code, которое создает шаблон проекта для вашего приложения. Используйте последнюю версию. | JavaScript и SPFx|
   | &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | Совместная работа со всеми пользователями, с которыми вы работаете, с помощью приложений для чата, собраний,  звонка — все в одном месте.| JavaScript и SPFx|
   | &nbsp; | [Node.js](https://nodejs.org/en/download/) | Серверной среды выполнения JavaScript. Используйте последнюю версию версии 16 LTS.| JavaScript и SPFx|
   | &nbsp; |[Диспетчер пакетов узлов (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx) | Установка пакетов и управление ими для использования в Node.js и ASP.NET Core приложениях.| JavaScript и SPFx|
   | &nbsp; | [Microsoft&nbsp; Edge](https://www.microsoft.com/edge) (рекомендуется) или [Google Chrome](https://www.google.com/chrome/) | Браузера со средствами разработчика. | JavaScript и SPFx|
   | &nbsp; | [Visual Studio Code](https://code.visualstudio.com/download); | Сред сборки JavaScript, TypeScript или SharePoint Framework (SPFx). Используйте версию 1.55 или более позднюю. | JavaScript и SPFx|
   | **Необязательное** | &nbsp; | &nbsp; | &nbsp; |
   | &nbsp; | [Средства Azure для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack) [и Azure CLI](/cli/azure/install-azure-cli) | Доступ к сохраненным данным или развертывание облачной серверной части для приложения Teams в Azure. | JavaScript|
   | &nbsp; | [React средств разработчика для Chrome](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi) [или React средств разработчика для Microsoft&nbsp;Edge](https://microsoftedge.microsoft.com/addons/detail/react-developer-tools/gpphkfbcpidddadnkolkpfckpihlkkil) | Расширение DevTools браузера для библиотеки JavaScript React с открытым кодом. | JavaScript|
   | &nbsp; | [Песочница Microsoft Graph](https://developer.microsoft.com/graph/graph-explorer) | Средство на основе браузера, которое позволяет выполнять запросы из данных Microsoft Graph. | JavaScript и SPFx|
   | &nbsp; | [Портал разработчика Teams](https://dev.teams.microsoft.com/) | Веб-портала для настройки, управления и распространения приложений Teams, в том числе в вашей организации или магазине Teams.| JavaScript и SPFx|

   > [!NOTE]
   >
   > * Документ тестируются с помощью Набора средств Teams версии 4.0.0 и Nodejs версии 16.
   > * Закладки обозревателя Microsoft Graph, чтобы узнать о службах Microsoft Graph. Это средство на основе браузера позволяет запрашивать и получать доступ к Microsoft Graph за пределами приложения.

## <a name="accounts-to-build-your-teams-app"></a>Учетные записи для создания приложения Teams

Прежде чем приступить к созданию приложения Teams, убедитесь, что у вас есть следующие учетные записи:

| Учетные записи | Для использования| Для типа среды|
| --- | --- |
|[Учетная запись Microsoft 365 с действующей подпиской](#microsoft-365-developer-program)|Учетная запись разработчика Teams при разработке приложения.| JavaScript и SPFx|
|[Учетная запись Azure](accounts.md#azure-account-to-host-backend-resources)|Серверные ресурсы в Azure.| JavaScript и SPFx|
|[Учетная запись администратора сайта семейства SharePoint](#sharepoint-collection-site-administrator-account) |Развертывание для размещения.| SPFx|

### <a name="microsoft-365-developer-program"></a>Программа для разработчиков Microsoft 365

Чтобы создать учетную запись Microsoft 365, зарегистрируйтесь для получения подписки программы для разработчиков Microsoft 365. Подписка бесплатна в течение 90 дней и продолжает обновляться до тех пор, пока вы используете ее для разработки.

Если у вас есть подписка на Visual Studio Enterprise или Professional, она включает бесплатную [подписку для разработчиков](https://aka.ms/MyVisualStudioBenefits) Microsoft 365. Она активна до тех пор, пока активна подписка на Visual Studio. Дополнительные сведения см. в статье [Подписка для разработчиков Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).

Вы можете зарегистрироваться в программе для разработчиков с помощью одного из следующих типов учетных записей.

* **Учетная запись Майкрософт для личного использования**

  :::row:::

    :::column span="3":::

       Учетная запись обеспечивает доступ к продуктам и облачным службам Майкрософт, таким как Outlook, Messenger, OneDrive, MSN, Xbox Live и Microsoft 365. 

       Для создания учетной записи Майкрософт, с помощью которой возможен доступ к потребительским облачным службам Майкрософт или Azure, можно зарегистрировать почтовый ящик Outlook.com.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/personal-account-icon.png" alt-text="личная учетная запись.":::
   :::column-end:::

  :::row-end:::

* **Рабочая учетная запись Майкрософт для бизнеса**

  :::row:::

    :::column span="3":::

       Учетная запись предоставляет доступ ко всем облачным службам Майкрософт малого, среднего и корпоративного уровня. К службам относятся Azure, Microsoft Intune или Microsoft 365. 

       Когда вы регистрируетесь в качестве организации в одной из этих служб, в Azure AD автоматически подготавливается облачный каталог для представления вашей организации.

    :::column-end:::
    :::column span="1":::
             :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/work-account-icon.png" alt-text="рабочую учетную запись.":::
    :::column-end:::

  :::row-end:::

#### <a name="create-a-free-microsoft-365-developer-account"></a>Создание бесплатной учетной записи разработчика Microsoft 365

Чтобы создать бесплатную учетную запись разработчика Microsoft 365, присоединитесь к программе для разработчиков Microsoft 365 и выполните следующую учетную запись:

1. Перейдите в [программу для разработчиков Microsoft 365](https://developer.microsoft.com/microsoft-365/dev-program).
1. Выберите **Присоединиться сейчас**.
1. Настройте свою учетную запись администратора.

   После завершения подписки вы увидите следующее изображение.

    :::image type="content" source="../assets/images/teams-toolkit-v2/m365-account.png" alt-text="Учетная запись M365":::

### <a name="azure-account"></a>Учетная запись Azure

Вам потребуется учетная запись Azure для размещения приложения Teams или внутренних ресурсов для приложения Teams с помощью набора средств Teams в Visual Studio Code. Вам потребуется подписка Azure в следующих сценариях:

* Если у вас уже есть приложение в другом поставщике облачных служб, отличном от Azure, и вы хотите интегрировать приложение на платформе Teams, у вас должна быть подписка Azure.
* Вы можете выбрать подписку Azure для размещения серверных ресурсов с помощью другого поставщика облачных служб или на собственных серверах, если они доступны из общедоступного домена.

> [!NOTE]
> Перед началом [работы необходимо создать бесплатную](https://azure.microsoft.com/free/) учетную запись.

### <a name="sharepoint-collection-site-administrator-account"></a>Учетная запись администратора сайта семейства SharePoint

При создании приложения Teams с помощью среды SPFx вам потребуется учетная запись администратора сайта семейства SharePoint при развертывании для размещения. Если вы используете клиент программы разработчика Microsoft 365, вы можете использовать учетную запись администратора, созданную в это время.

## <a name="sideloading-permission"></a>Разрешение на загрузку неопубликованных приложений

После создания приложения необходимо загрузить это приложение в Teams, не распространяя его. Этот процесс называется загрузкой без публикации. Войдите в учетную запись Microsoft 365, чтобы просмотреть этот параметр.

Вы можете проверить, включено ли разрешение на загрузку без публикации, с помощью Visual Studio Code или клиента Teams.

<br>
<details>
<summary><b>Проверка разрешения на загрузку без публикации с помощью Visual Studio Code</b></summary>

1. Откройте **Visual Studio Code**.
1. Щелкните значок Набора средств :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: Teams на панели инструментов Teams Toolkit.

   > [!NOTE]
   > Если вы не видите этот параметр, см. статью "Установка [набора средств Teams](install-Teams-Toolkit.md) для установки расширения Набора средств Teams" в Visual Studio Code.
1. Выберите **вход в M365 в** **разделе "Учетные** записи" и войдите в учетную запись Microsoft 365.

    :::image type="content" source="../assets/images/teams-toolkit-v2/accounts.png" alt-text="сведения об учетных записях":::

1. Проверьте, есть ли пункт **Разрешение загрузки без публикации**, как показано на следующем изображении:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sideloading.png" alt-text="Разрешение загрузки без публикации":::

</details>
<br>
<details>
<summary><b>Проверка разрешения на загрузку без публикации с помощью клиента Teams</b></summary>

1. В клиенте Teams выберите " **Приложения"**.
1. Выберите **"Управление приложением"**.
1. Выберите **"Отправить приложение"**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-app.png" alt-text="Публикация приложения":::

4. Проверьте, есть ли пункт **Отправка пользовательского приложения**, как показано на следующем изображении:

    :::image type="content" source="../assets/images/teams-toolkit-v2/upload-custom-app1.png" alt-text="Отправка пользовательского приложения":::.

</details>

### <a name="enable-sideloading-using-admin-center"></a>Включение загрузки неопубликованных приложений с помощью Центра администрирования

Если вы не можете просмотреть параметр "Отправить пользовательское приложение", это означает **,** что у вас нет необходимых разрешений для загрузки неопубликованных приложений.

* Администратор клиента включает для клиента или для организации параметр загрузки без публикации в центре администрирования Teams.
* Если вы не являетесь администратором клиента, вам нужно связаться с администратором клиента, чтобы включить загрузку без публикации.

Если у вас есть права администратора, выполните следующие действия, чтобы отправить пользовательское приложение с помощью Центра администрирования:

  1. Войдите в [Центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) со своими учетными данными администратора.

  1. Щелкните значок :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: > **Teams**.

       :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center.png" alt-text="Microsoft 365 Admin центре":::

     > [!Note]
     > Может потребоваться **до 24 часов** для появления пункта **Teams**. Можно [отправить пользовательское приложение в среду Teams](/microsoftteams/upload-custom-apps) для тестирования и проверки.

  1. Войдите в Центр администрирования Microsoft Teams с учетными данными администратора.
  1. Щелкните значок :::image type="icon" source="../assets/images/teams-toolkit-v2/showall icon.PNG"::: > **приложений** >  Teams **.**

     :::image type="content" source="../assets/images/teams-toolkit-v2/m365-admin-center1.png" alt-text="Microsoft 365 Admin center1":::

  1. Выбор **глобального (по умолчанию для всей организации)**

     :::image type="content" source="../assets/images/teams-toolkit-v2/select-manage-policies.png" alt-text="Выбор &quot;Управление политиками&quot;":::

  1. Установите переключатель **Отправка пользовательских приложений** в положение **Включено**.

     :::image type="content" source="../assets/images/teams-toolkit-v2/Upload-custom-apps.png" alt-text="Отправка пользовательских приложений":::

  5. Нажмите кнопку **Сохранить**.

     > [!Note]
     > Для включения возможности загрузки без публикации может потребоваться до 24 часов. В течение этого времени для тестирования приложения можно использовать возможность **отправки для своего клиента**. Чтобы отправить пакет приложения в формате .zip, см. раздел [Отправка пользовательских приложений](/microsoftteams/teams-app-setup-policies).

     Убедитесь, что теперь у вас есть разрешение на загрузку неопубликованных приложений, выполнив действия, описанные в процедуре проверки разрешения на загрузку неопубликованных приложений с помощью Visual Studio Code [или клиента Teams.](#sideloading-permission)

</details>

## <a name="see-also"></a>См. также

* [Управление пользовательскими политиками и параметрами приложений в Teams](/microsoftteams/teams-custom-app-policies-and-settings)
* [Управление политиками настройки приложений в Teams](/microsoftteams/teams-app-setup-policies)
* [Отправка пользовательских приложений](/microsoftteams/teams-app-setup-policies)
* [Подготовка облачных ресурсов с помощью Набора средств Teams](provision.md)
* [Развертывание приложения Teams в облаке](deploy.md)
