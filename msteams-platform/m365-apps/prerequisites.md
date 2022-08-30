---
title: Настройте среду разработки для расширения приложений Teams в Microsoft 365.
description: В этой статье вы узнаете о предварительных условиях, необходимых для запуска ознакомительных версий сборок для расширения ваших приложений Teams в Microsoft 365.
ms.date: 05/24/2022
ms.custom: m365apps
ms.topic: conceptual
ms.localizationpriority: high
ms.openlocfilehash: 965c9d8b7b05141aa6add18bba51512bd9e0a213
ms.sourcegitcommit: b13361f342c76d637321df21d2ef900471bf0eef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2022
ms.locfileid: "67457293"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-microsoft-365"></a>Настройте среду разработки для расширения приложений Teams в Microsoft 365.

Среда разработки для расширения приложений Teams в Microsoft 365 аналогична среде разработки Microsoft Teams. В этой статье обсуждаются определенные конфигурации, необходимые для запуска предварительных сборок приложений Microsoft Teams и Microsoft Office для предварительного просмотра приложений Teams, работающих в Outlook и Office.

Чтобы настроить среду разработки:

> [!div class="checklist"]
>
> * [Получите клиент Microsoft 365 Developer (Sandbox) и разрешите загрузку неопубликованных приложений](#prepare-a-developer-tenant-for-testing)
> * [Зарегистрируйте клиент Microsoft 365 в *Целевых выпусках Office 365.*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Установка сборок бета-канала Приложений Microsoft 365 в тестовой среде](#install-office-apps-in-your-test-environment)
> * [Переключитесь на предварительную версию Teams для разработчиков](#switch-to-the-developer-preview-version-of-teams)
> * [*Необязательно*] [Установите расширение Teams Toolkit для Microsoft Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Подготовьте клиент разработчика к тестированию

Для настройки среды разработки вам потребуется клиент песочницы с подпиской на Microsoft 365. Если у вас его еще нет, создайте [клиент песочницы](/office/developer-program/microsoft-365-developer-program-get-started) или получите тестовый клиент через свою организацию.

Вам также потребуется включить загрузку неопубликованных приложений для вашего клиента:

 1. Войдите в [Центр администрирования Teams,](https://admin.teams.microsoft.com/dashboard) используя учетные данные тестового клиента.

 1. Перейдите к **приложениям Teams Для** > **управления приложениями**.

 1. В правом верхнем углу выберите **параметры приложения для всей организации**.

 1. В разделе "Пользовательские приложения" включите переключатель **"** Взаимодействие с пользовательским приложением" и сохраните его.

    :::image type="content" source="images/teams-admin-enable-sideloading.png" alt-text="Снимок экрана— пример, в котором включена загрузка неопубликованных приложений из Центра Администратор Teams":::

 1. Помимо параметров приложения для всей организации, пользовательские параметры политики приложений также позволяют пользователям отправлять пользовательские приложения в Teams. Дополнительные сведения см. [в статье об управлении настраиваемыми политиками и параметрами приложений](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).

 1. В Центре администрирования Teams перейдите к политикам установки приложений **Teams** > **, а** затем выберите глобальную **(по умолчанию для всей организации) политику**.

 1. Включите **отправку пользовательских приложений** и нажмите кнопку **"Сохранить"**.

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Зарегистрируйте клиент разработчика для целевых выпусков Office 365.

> [!IMPORTANT]
> Может потребоваться до пяти дней после создания [клиента песочницы разработчика Microsoft 365](/office/developer-program/microsoft-365-developer-program-get-started) и регистрации в [целевых выпусках Office 365](#enroll-your-developer-tenant-for-office-365-targeted-releases), чтобы загруженные неопубликованные приложения Teams отобразились в Outlook и Office.

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

Вы можете просмотреть приложения Teams, работающие в Outlook на рабочем столе Windows, с помощью последней сборки *Бета-канал*. Проверьте, нужно ли [Изменить канал обновления приложений Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) для вашего тестового клиента, чтобы установить сборку бета-канала Office 365.

Чтобы установить приложения Office 365 Бета-канал в тестовой среде:

1. Войдите в свою тестовую среду, используя свои учетные данные тестового клиента.
1. Загрузите [Средство развертывания Office](https://www.microsoft.com/download/details.aspx?id=49117) и извлеките его в локальную папку.
1. Перейдите к локальной папке и откройте *configuration-Office365-x86.xml* (или **x64.xml*, в зависимости от вашей среды) в текстовом редакторе и обновите значение *Канал* до `BetaChannel`.
1. Откройте командную строку и перейдите к пути к локальной папке.
1. Запустите `setup.exe /configure configuration-Office365-x86.xml` (или используйте файл **x64.xml* в зависимости от настроек).
1. Откройте Outlook (клиент для настольных компьютеров) и настройте учетную запись электронной почты, используя учетные данные тестового клиента.
1. Откройте **Файл** > **Учетная запись Office** > **О программе Outlook**, чтобы убедиться, что вы используете сборку Microsoft 365 *Бета-канал* для Outlook.

    :::image type="content" source="images/outlook-about-beta-channel.png" alt-text="Перейдите в раздел &quot;О программе Outlook&quot; из учетной записи Office, чтобы убедиться, что вы используете сборку бета-канала.":::

1. Убедитесь, что установлено *Microsoft Edge WebView2 Runtime*. Откройте Windows **Start** >  **Приложения и функции** и выполните поиск **веб-представления**:

    :::image type="content" source="images/windows-addremove-webview2.png" alt-text="Найдите 'веб-представление' в разделе &quot;Приложения и функции&quot; в &quot;Параметрах&quot; Windows":::

    Если этот элемент отсутствует в списке, установите [Microsoft Edge WebView2](https://developer.microsoft.com/microsoft-edge/webview2/) в тестовую среду.

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Переключитесь на предварительную версию Teams для разработчиков.

Убедитесь, что вы переключились на [Общедоступную предварительную версию для разработчиков](../resources/dev-preview/developer-preview-intro.md) из клиента Microsoft Teams.

1. Войдите в Teams, используя учетные данные клиента песочницы.
1. В меню с многоточием (**...**) рядом с вашим профилем пользователя выберите **О** > **предварительной версии для разработчиков**. Появится диалоговое окно, выберите **Переключиться на предварительную версию для разработчиков**.
1. После перезапуска приложения Teams перейдите в меню с многоточием (**...**) рядом с вашим профилем пользователя и проверьте, выбрана ли **Предварительная версия для разработчиков**.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Общедоступная предварительная версия для разработчиков в Teams":::

## <a name="install-visual-studio-code-and-teams-toolkit-extension"></a>Установите Visual Studio Code и расширение Teams Toolkit

При желании вы можете использовать [Visual Studio Code](https://code.visualstudio.com/) для расширения приложений Teams в Office и Outlook.

Расширение [Teams Toolkit для Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`или более поздней версии) предоставляет команды, которые могут помочь изменить существующий код Teams, чтобы он был совместим с Outlook и Office. Дополнительные сведения см. в разделе [Включение личной вкладки Teams для Office и Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-step"></a>Следующий этап

Создайте или обновите приложение Teams для работы в Microsoft 365:

> [!div class="nextstepaction"]
> [Включение личной вкладки Teams в Office и Outlook](extend-m365-teams-personal-tab.md)
> [!div class="nextstepaction"]
> [Включение расширения для сообщений Teams в Outlook](extend-m365-teams-message-extension.md)
