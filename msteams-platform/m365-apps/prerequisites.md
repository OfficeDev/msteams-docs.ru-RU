---
title: Настройка среды разработки для расширения Teams приложений в Microsoft 365
description: Ниже приведены предварительные требования для расширения Teams приложений в Microsoft 365
ms.date: 02/11/2022
ms.openlocfilehash: 094da29fdb871ef4af091e32e123e2d644b7445f
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104072"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Настройка среды разработки для расширения Teams приложений в Microsoft 365

> [!NOTE]
> Расширение приложения Teams Microsoft 365 в настоящее время доступно только в [общедоступной предварительной версии разработчика](~/resources/dev-preview/developer-preview-intro.md).

Среда разработки для расширения Teams в Microsoft 365 аналогична Microsoft Teams разработки. В этой статье рассматриваются конкретные конфигурации, необходимые для запуска предварительных сборок приложений Microsoft Teams и Microsoft Office для предварительного просмотра Teams приложений, работающих в Outlook и Office.

Чтобы настроить среду разработки:

> [!div class="checklist"]
>
> * [Получение Microsoft 365 разработчика (песочница) и включение загрузки неопубликованных приложений](#prepare-a-developer-tenant-for-testing)
> * [Регистрация клиента Microsoft 365 в *Office 365 целевых выпусках*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Настройка учетной записи для доступа к предварительным версиям Outlook и Office](#install-office-apps-in-your-test-environment)
> * [Переключитесь на предварительную версию Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Необязательно*] [Установка Teams набор средств для Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Подготовка клиента разработчика к тестированию

Для настройки среды разработки Microsoft 365 клиент песочницы подписки разработчика. Если у вас его еще нет, создайте клиент [песочницы](/office/developer-program/microsoft-365-developer-program-get-started) или получите тестовый клиент в организации.

После того как у вас есть клиент, необходимо включить загрузку неопубликованных приложений для клиента. Дополнительные сведения см. в разделе ["Включение загрузки неопубликованных приложений"](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Чтобы проверить, включена ли загрузка неопубликованных приложений, войдите в Teams, выберите "Приложения", **а Upload параметр пользовательского** приложения.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload настраиваемого приложения":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Регистрация клиента разработчика для Office 365 целевых выпусков

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями на сайте [Microsoft Teams — Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли поддержка Outlook.com и Office.com для приложений Teams тестового клиента.

Чтобы зарегистрировать тестовый клиент для Office 365 целевых выпусков:

1. Войдите [в Центр администрирования Microsoft 365](https://admin.microsoft.com) с помощью учетных данных тестового клиента.
1. Перейдите **Параметры** >  **Org Параметры** >  **Organization profile**.
1. Выберите **параметры выпуска**.
1. Выберите любой *целевой выпуск* :
    1. **Целевой выпуск для всех**
    1. **Целевой выпуск для выбранных пользователей**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Центр администрирования Microsoft 365 меню &quot;Параметры выпуска&quot; с выбранным параметром &quot;Целевой выпуск&quot;":::

1. Выберите **Сохранить**.

Дополнительные сведения о вариантах Office 365 см. в разделе "[](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release)Настройка стандартных или целевых выпусков" Центр администрирования Microsoft 365 *справке*.

## <a name="install-office-apps-in-your-test-environment"></a>Установка Office приложений в тестовой среде

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями в Microsoft Teams [— Microsoft 365 Developer Blog](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли поддержка Outlook для Windows классических приложений для расширений сообщений Teams для тестового клиента.

Вы можете просмотреть Teams приложения, работающие Outlook на Windows настольном компьютере, с помощью последней сборки *бета-канала*. Проверьте, нужно ли изменить канал [обновления Приложения Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) для тестового клиента, чтобы установить Office 365 бета-канала.

Чтобы установить Office 365 бета-канала в тестовой среде, с помощью следующих параметров:

1. Войдите в тестовую среду, используя учетные данные тестового клиента.
1. Скачайте [Office развертывания и](https://www.microsoft.com/download/details.aspx?id=49117) извлеките его в локальную папку.
1. Перейдите в локальную папку и откройте *configuration-Office365-x86.xml(или***x64.xml* в зависимости от среды) в текстовом редакторе и обновите значение *канала*`BetaChannel`.
1. Откройте командную строку и перейдите по пути к локальной папке.
1. Выполните `setup.exe /configure configuration-Office365-x86.xml` (или используйте **x64.xml* в зависимости от настройки).
1. Откройте Outlook (настольный клиент) и настроите учетную запись электронной почты, используя учетные данные тестового клиента.
1. Открыть **файл Office** >  **AccountAbout** >  Outlook.  
   Если номер сборки **— 14416** или более поздней версии, а канал — beta *Channel*, вы используете Microsoft 365 бета-версии канала.
1. В правом верхнем углу включите переключатель **"** Ожидается в ближайшее время".

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Переключатель &quot;Ожидается в ближайшее время&quot; в Outlook":::

> [!NOTE]
> Может потребоваться закрыть Outlook и перезапустить компьютер, чтобы отобразить кнопку *"* Ожидается в ближайшее время".

Вы можете проверить поддержку тестового клиента для учетной записи клиента:

* Для Teams личных вкладок, работающих на office.com, outlook.com и Outlook для Windows desktop, войдите с использованием учетных данных тестового клиента и проверьте наличие многоточия (**...**) на левой боковой панели Office или Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Кнопка с многоточием (...) на левой боковой панели Outlook":::

* Для расширений сообщений в outlook.com и Outlook для Windows проверьте параметр "Дополнительные приложения" в нижней  части Outlook области создания сообщений.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="Параметр &quot;Другие приложения&quot; в области Outlook создания сообщения":::

> [!NOTE]
> Если вы согласились на использование бета-каналов, но не видите эти варианты многоточия, скорее всего, поддержка функций предварительной версии будет развернута в клиенте. Последние обновления см. в Microsoft Teams [блога разработчика](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Переключитесь на предварительную версию Teams

Убедитесь, что вы переключились на [общедоступную](../resources/dev-preview/developer-preview-intro.md) предварительную версию разработчика из Microsoft Teams клиента.

1. Войдите в Teams учетные данные клиента песочницы.
1. В меню с многоточием (**...**) рядом с профилем пользователя выберите **предварительный** просмотр **AboutDeveloper** > . Появится диалоговое окно и выберите **"Переключиться на предварительную версию разработчика"**.
1. После перезапуска Teams перезапустите приложение, перейдите в меню с многоточием (**...**) рядом с профилем пользователя и проверьте, выбрана ли предварительная **версия для** разработчиков.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Параметр общедоступной предварительной версии для разработчиков в Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Установка Visual Studio Code и Teams набор средств preview

При необходимости можно [использовать Visual Studio Code для](https://code.visualstudio.com/) расширения Teams приложений в Office и Outlook.

Расширение Teams набор средств [для Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`или более поздней версии) предоставляет команды, которые могут помочь изменить существующий код Teams для совместимости с Outlook и Office. Дополнительные сведения см. в разделе [Teams личных вкладок для Office и Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Включение личной вкладки Teams в Office и Outlook](extend-m365-teams-personal-tab.md)
* [Включение расширения Teams сообщений для Outlook](extend-m365-teams-message-extension.md)
