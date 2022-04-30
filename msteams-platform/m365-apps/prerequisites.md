---
title: Настройте среду разработки для расширения приложений Teams в Microsoft 365.
description: Вот необходимые условия для расширения приложений Teams в Microsoft 365
ms.date: 02/11/2022
ms.localizationpriority: high
ms.openlocfilehash: 483ae6982dd51a16573655ed14dc93577642ba4b
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111502"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Настройте среду разработки для расширения приложений Teams в Microsoft 365.

> [!NOTE]
> Расширение приложения Teams в Microsoft 365 сейчас доступно только в [общедоступной предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-intro.md).

Среда разработки для расширения приложений Teams в Microsoft 365 аналогична среде разработки Microsoft Teams. В этой статье обсуждаются определенные конфигурации, необходимые для запуска предварительных сборок приложений Microsoft Teams и Microsoft Office для предварительного просмотра приложений Teams, работающих в Outlook и Office.

Чтобы настроить среду разработки:

> [!div class="checklist"]
>
> * [Получите клиент Microsoft 365 Developer (Sandbox) и разрешите загрузку неопубликованных приложений](#prepare-a-developer-tenant-for-testing)
> * [Зарегистрируйте клиент Microsoft 365 в *Целевых выпусках Office 365.*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Настройте учетную запись для доступа к предварительным версиям Outlook и Office.](#install-office-apps-in-your-test-environment)
> * [Переключитесь на предварительную версию Teams для разработчиков](#switch-to-the-developer-preview-version-of-teams)
> * [*Необязательно*] [Установите расширение Teams Toolkit для Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Подготовьте клиент разработчика к тестированию

Для настройки среды разработки вам потребуется клиент песочницы с подпиской на Microsoft 365. Если у вас его еще нет, создайте [клиент песочницы](/office/developer-program/microsoft-365-developer-program-get-started) или получите тестовый клиент через свою организацию.

Если у вас есть клиент, вам необходимо включить загрузку неопубликованных приложений для него, см. [Разрешение загрузки неопубликованных приложений](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Чтобы проверить, разрешена ли загрузка неопубликованных приложений, войте в Teams, выберите **Приложения**, а затем найдите **Параметр загрузки пользовательского приложения**.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Параметр загрузки пользовательского приложения":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Зарегистрируйте клиент разработчика для целевых выпусков Office 365.

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями в [Блоге разработчиков Microsoft 365 — Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли поддержка Outlook.com и Office.com для приложений Teams для вашего тестового клиента.

Чтобы зарегистрировать тестовый клиент для целевых выпусков Office 365:

1. Войдите в [Центр администрирования Microsoft 365](https://admin.microsoft.com), используя учетные данные тестового клиента.
1. Перейдите в **Параметры** > **Параметры организации** > **Профиль организации**.
1. Выберите **Параметры выпуска**.
1. Выберите любую настройку *Нацеленного выпуска*:
    1. **Целевой выпуск для всех**
    1. **Целевой выпуск для выбранных пользователей**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Меню &quot;Параметры выпуска&quot; центра администрирования Microsoft 365 с выбранным параметром &quot;Целевой выпуск&quot;":::

1. Нажмите кнопку **Сохранить**.

Подробнее о вариантах выпуска Office 365 см. в [Настройка параметров стандартного или целевого выпуска](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) в разделе *справки Центра администрирования Microsoft 365.*.

## <a name="install-office-apps-in-your-test-environment"></a>Установите приложения Office в тестовой среде.

> [!IMPORTANT]
> Ознакомьтесь с последними обновлениями в [Блогеразработчиков Microsoft 365 — Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/), чтобы проверить, доступна ли для вашего тестового клиента поддержка Outlook для рабочего стола Windows для расширений сообщений Teams.

Вы можете просмотреть приложения Teams, работающие в Outlook на рабочем столе Windows, с помощью последней сборки *Бета-канал*. Проверьте, нужно ли [Изменить канал обновления приложений Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) для вашего тестового клиента, чтобы установить сборку бета-канала Office 365.

Чтобы установить приложения Office 365 Бета-канал в тестовой среде:

1. Войдите в свою тестовую среду, используя свои учетные данные тестового клиента.
1. Загрузите [Средство развертывания Office](https://www.microsoft.com/download/details.aspx?id=49117) и извлеките его в локальную папку.
1. Перейдите к локальной папке и откройте *configuration-Office365-x86.xml* (или **x64.xml*, в зависимости от вашей среды) в текстовом редакторе и обновите значение *Канал* до `BetaChannel`.
1. Откройте командную строку и перейдите к пути к локальной папке.
1. Запустите `setup.exe /configure configuration-Office365-x86.xml` (или используйте файл **x64.xml* в зависимости от настроек).
1. Откройте Outlook (клиент для настольных компьютеров) и настройте учетную запись электронной почты, используя учетные данные тестового клиента.
1. Открыть **Файл** > **Учетная запись Office** > **Об Outlook**.  
   Если номер сборки **14416** или выше, а канал *Бета-канал*, вы используете версию сборки Microsoft 365 Бета-канал.
1. В правом верхнем углу включите переключатель **Ожидается в ближайшее время**.

    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Параметр переключателя &quot;Ожидается в ближайшее время&quot; в Outlook":::

> [!NOTE]
> Возможно, вам придется закрыть Outlook и перезагрузить компьютер, чтобы появилась кнопка *Ожидается в ближайшее время*.

Вы можете проверить поддержку тестового клиента для своей учетной записи клиента:

* Для личных вкладок Teams, работающих на office.com, outlook.com и Outlook для рабочего стола Windows, войдите в систему с учетными данными тестового клиента и проверьте наличие многоточия (**...**) на левой боковой панели Office или Outlook.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Многоточия ('...') на левой боковой панели Outlook":::

* Для расширений сообщений в Outlook.com и Outlook для Windows установите флажок **Дополнительные приложения** в нижней части области создания сообщений Outlook.

    :::image type="content" source="images/outlook-web-compose-more-apps.png" alt-text="&quot;Дополнительные приложения&quot; в области создания сообщений Outlook":::

> [!NOTE]
> Если вы выбрали выпуски бета-канала, но не видите эти параметры с многоточием, вероятно, поддержка функции предварительного просмотра находится в процессе развертывания для вашего клиента. О последних обновлениях можно узнать в [ Блоге разработчиков Microsoft Teams](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Переключитесь на предварительную версию Teams для разработчиков.

Убедитесь, что вы переключились на [Общедоступную предварительную версию для разработчиков](../resources/dev-preview/developer-preview-intro.md) из клиента Microsoft Teams.

1. Войдите в Teams, используя учетные данные клиента песочницы.
1. В меню с многоточием (**...**) рядом с вашим профилем пользователя выберите **О** > **предварительной версии для разработчиков**. Появится диалоговое окно, выберите **Переключиться на предварительную версию для разработчиков**.
1. После перезапуска приложения Teams перейдите в меню с многоточием (**...**) рядом с вашим профилем пользователя и проверьте, выбрана ли **Предварительная версия для разработчиков**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Общедоступная предварительная версия для разработчиков в Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Установите расширение Visual Studio Code и Teams Toolkit Preview.

При желании вы можете использовать [Visual Studio Code](https://code.visualstudio.com/) для расширения приложений Teams в Office и Outlook.

Расширение [Teams Toolkit для Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`или более поздней версии) предоставляет команды, которые могут помочь изменить существующий код Teams, чтобы он был совместим с Outlook и Office. Подробнее в разделе [Разрешение личной вкладки Teams для Office и Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Дальнейшие действия

* [Включение личной вкладки Teams в Office и Outlook](extend-m365-teams-personal-tab.md)
* [Включение расширения для сообщений Teams в Outlook](extend-m365-teams-message-extension.md)
