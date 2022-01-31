---
title: Настройка среды разработчиков для расширения Teams приложений в Microsoft 365
description: Вот необходимые условия для расширения Teams приложений в Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.openlocfilehash: e024b11f03c605144a5d1cac6904cdd0095ec15c
ms.sourcegitcommit: abe5ccd61ba3e8eddc1bec01752fd949a7ba0cc2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/31/2022
ms.locfileid: "62281702"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365"></a>Настройка среды разработчиков для расширения Teams приложений в M365

> [!NOTE]
> Приложение Extend teams Microsoft 365 в настоящее время доступно только в [предварительном просмотре общедоступных разработчиков](~/resources/dev-preview/developer-preview-intro.md).

Среда разработки для расширения Teams по Microsoft 365 похожа на Microsoft Teams разработки. В этой статье обсуждаются конкретные конфигурации, необходимые для запуска предварительных сборки Microsoft Teams и Microsoft Office приложений для предварительного просмотра Teams приложений, работающих в Outlook и Office.

Чтобы настроить среду разработки:

> [!div class="checklist"]
> * [Получите клиента разработчика M365 (песочница) и вьет побочный разгрузки](#prepare-a-developer-tenant-for-testing)
> * [Регистрация клиента M365 в *Office 365 целевых выпусках*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Настройка учетной записи для доступа к версиям предварительного просмотра Outlook и Office](#install-office-apps-in-your-test-environment)
> * [Переключиться на Developer Preview версию Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Необязательный*] [Установка Teams набор средств расширения для Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Подготовка клиента-разработчика к тестированию

Чтобы настроить среду разработки, Microsoft 365 клиент подписки на подписку разработчика. Если его еще нет, создайте клиент из песочницы или получите тестовый клиент через организацию.[](/office/developer-program/microsoft-365-developer-program-get-started)

После того, как у вас есть клиент, необходимо включить боковой загрузки для клиента, см. [включить sideloading](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading). Чтобы проверить, включена ли Teams загрузка, выберите **Приложения** и **Upload настраиваемый параметр** приложения.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Upload настраиваемый параметр приложения":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Регистрация клиента разработчика для Office 365 целевых выпусков

> [!IMPORTANT]
> Обратитесь к последним обновлениям Microsoft Teams [- Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) блог разработчика, чтобы проверить, доступна ли Outlook.com и Office.com для Teams приложений для тестовых клиентов.

Чтобы записать тестовый клиент для Office 365 целевых выпусков:

1. Во входе [Центр администрирования Microsoft 365](https://admin.microsoft.com) с учетными данными тестовых клиентов.
1. Перейдите **к** >  Параметры **Org Параметры** >  **Organization profile**.
1. Выберите **параметры выпуска**.
1. Выберите любое *целевое предпочтение выпуска* :
    1. **Целевой выпуск для всех**
    1. **Целевой выпуск для отдельных пользователей**

    :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Центр администрирования Microsoft 365 меню &quot;Параметры выпуска&quot; с выбранным параметром целевого выпуска":::
    
1. Нажмите кнопку **Сохранить**.

Дополнительные сведения о Office 365 версиях см. в справке [Настройка](/microsoft-365/admin/manage/release-options-in-office-365?view=o365-worldwide&preserve-view=true#targeted-release) стандартных или целевых *Центр администрирования Microsoft 365 выпусков*.

## <a name="install-office-apps-in-your-test-environment"></a>Установка Office приложений в тестовой среде

> [!IMPORTANT]
> Обратитесь к последним обновлениям Microsoft Teams [- Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/) блог разработчика, чтобы проверить, доступна ли Outlook для Windows поддержки Teams расширений обмена сообщениями для тестовых клиентов.

Вы можете просмотреть Teams приложения, работающие Outlook на Windows настольном компьютере с помощью недавней *сборки бета-канала*. Проверьте, необходимо ли изменить канал обновления [Приложения Microsoft 365](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) для тестового клиента для установки Office 365 сборки бета-канала.

Установка Office 365 приложений бета-канала в тестовой среде:

1. Вопишитесь в тестовую среду с учетными данными тестовых клиентов.
1. Скачайте [средство Office развертывания](https://www.microsoft.com/download/details.aspx?id=49117) и извлеките в локализованную папку.
1. Перейдите к локальной папке и *откройтеconfiguration-Office365-x86.xml* (или *x64.xml*, в зависимости от среды) в текстовом редакторе и обновите значение *Channel* до `BetaChannel`.
1. Откройте командную подсказку и перейдите к локальному пути папки.
1. Запустите `setup.exe /configure configuration-Office365-x86.xml` (или используйте файл **x64.xml* , в зависимости от настройки).
1. Откройте Outlook (клиент настольного компьютера) и установите учетную запись почты с помощью тестовых учетных данных клиента.
1. Open **File** >  **Office** **AccountAbout** >  Outlook.  
   Если число сборки **14416** или выше, а каналом является бета-канал *, вы* Microsoft 365 сборку бета-канала.
1. В правом верхнем углу включаем очки **Coming Soon** .
    
    :::image type="content" source="images/outlook-coming-soon.png" alt-text="Дополнительные приложения":::

> [!NOTE]
> Может потребоваться закрыть Outlook и перезапустить компьютер для появления кнопки *Coming Soon*.

Вы можете проверить поддержку тестовых клиентов для учетной записи клиента:

* Для Teams личных вкладок, работающих на office.com, outlook.com и Outlook для Windows настольного компьютера, впишитесь в тестовые учетные данные клиента и проверьте параметр ellipses (**...**) на нижней левой области.

    :::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Эллипсы" lightbox="images/outlook-desktop-ellipses.png":::

* Для расширений обмена сообщениями в outlook.com и Outlook для Windows проверьте параметр Дополнительные приложения в Outlook составить  ленту сообщений.

> [!NOTE]
> Если вы выбрали выпуски бета-канала, но не видите эти параметры эллипсов, вероятно, поддержка функций предварительного просмотра будет развертываться на клиента. Последние обновления см. в [Microsoft Teams блог разработчика](https://devblogs.microsoft.com/microsoft365dev/).

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Переключиться на Developer Preview версию Teams

Убедитесь, что вы переходите на [общедоступные Developer Preview](../resources/dev-preview/developer-preview-intro.md) из Microsoft Teams клиента.

1. Во входе Teams учетные данные клиента из песочницы.
1. В меню ellipsis (**...**) рядом с профилем пользователя выберите **предварительный** просмотр **AboutDeveloper** > . Появится диалоговое окно, выберите **Переключатель для предварительного просмотра разработчика**.
1. После перезапуска Teams перезапуска приложения перейдите в меню ellipsis (**...**) рядом с профилем пользователя и проверьте, выбран ли Developer Preview.

    :::image type="content" source="images/teams-dev-preview.png" alt-text="Общедоступная предварительная версия для разработчиков" lightbox="images/teams-dev-preview.png":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Установка Visual Studio Code и Teams набор средств предварительного просмотра

Необязательно, вы можете [использовать Visual Studio Code для](https://code.visualstudio.com/) расширения Teams приложений в Office и Outlook.

Расширение Teams набор средств [для Visual Studio Code](https://aka.ms/teams-toolkit) (`v2.10.0`или более поздней) предоставляет команды, которые могут помочь изменить существующий код Teams, чтобы быть совместимым с Outlook и Office. Дополнительные сведения см. в Teams личной вкладке для [Office и Outlook](extend-m365-teams-personal-tab.md).

## <a name="next-steps"></a>Дальнейшие действия

- [Включение личной вкладки Teams в Office и Outlook](extend-m365-teams-personal-tab.md)
- [Включение расширения для сообщений Teams в Outlook](extend-m365-teams-message-extension.md)