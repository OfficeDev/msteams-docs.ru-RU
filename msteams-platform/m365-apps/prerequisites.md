---
title: Настройка среды разработчиков для расширения Teams приложений в Microsoft 365
description: Вот необходимые условия для расширения Teams приложений в Microsoft 365
ms.date: 11/15/2021
ms.topic: how-to
ms.custom: m365apps
ms.openlocfilehash: 967e45bb59c431476ead902e1413ab743c566779
ms.sourcegitcommit: 239807b74aa222452559509d49c4f2808cd9c9ca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/09/2021
ms.locfileid: "61391348"
---
# <a name="set-up-your-dev-environment-for-extending-teams-apps-across-m365-preview"></a>Настройка среды разработчиков для расширения Teams в M365 (предварительный просмотр)

Среда разработки для расширения Teams по Microsoft 365 похожа на то, что используется для Microsoft Teams разработки. В этой статье обсуждаются конкретные конфигурации, необходимые для запуска предварительных сборки Microsoft Teams и Microsoft Office приложений для предварительного просмотра Teams приложений, работающих в Outlook и Office. Чтобы настроить среду разработки, необходимо:

> [!div class="checklist"]
> * [Получение клиента разработчика M365 (песочница) и возможность загрузки](#prepare-a-developer-tenant-for-testing)
> * [Регистрация клиента M365 в *Office 365 целевых выпусках*](#enroll-your-developer-tenant-for-office-365-targeted-releases)
> * [Настройка учетной записи для доступа к версиям предварительного просмотра Outlook и Office](#install-office-apps-in-your-test-environment)
> * [Переключиться на Developer Preview версию Teams](#switch-to-the-developer-preview-version-of-teams)
> * [*Необязательный*] [Установка Teams набор средств расширения для Visual Studio Code](#install-visual-studio-code-and-teams-toolkit-preview-extension)

## <a name="prepare-a-developer-tenant-for-testing"></a>Подготовка клиента-разработчика к тестированию

Если его еще нет, создайте [](/office/developer-program/microsoft-365-developer-program-get-started) клиент Microsoft 365 подписки разработчика или получите тестовый клиент через организацию.

После того, как у вас [](/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading) есть клиент, вам необходимо включить побок для клиента, во время регистрации в [Центр администрирования Microsoft 365](https://admin.microsoft.com) и навигации, чтобы показать все > Teams > Teams приложений > политики установки > **Global**.  Переустанавка **Upload настраиваемые приложения** и **сохранить**.

Если у вас есть существующий клиент, убедитесь, что побная загрузка включена путем входа в Teams и выбора **приложений.** Вы увидите параметр **Upload приложения,** если для клиента включена боковая загрузка.

:::image type="content" source="images/teams-sideloading-enabled.png" alt-text="Для клиента включена боковая загрузка, если вы видите возможность &quot;Upload настраиваемого приложения&quot; из Teams панели &quot;Приложения&quot;":::

## <a name="enroll-your-developer-tenant-for-office-365-targeted-releases"></a>Регистрация клиента разработчика для Office 365 целевых выпусков

> [!IMPORTANT]
> Обратитесь к последнему в [Microsoft Teams - Microsoft 365 блог](https://devblogs.microsoft.com/microsoft365dev/category/teams/) разработчика, чтобы проверить, outlook.com и office.com поддержку Teams приложений для тестовых клиентов.

Чтобы просмотреть Teams приложения, работающие в outlook.com или office.com, выберите в тестовом клиенте Office 365 [целевые выпуски.](/microsoft-365/admin/manage/release-options-in-office-365#targeted-release)

1. Войдите в Центр администрирования Microsoft 365 с помощью учетных данных для тест-клиента и перейдите на вкладку [Организационный](https://admin.microsoft.com/AdminPortal/Home?#/Settings/OrganizationProfile) профиль *(Параметры*  >  *параметров*  >>  организации)). Выберите **параметры выпуска** и выберите одно из целевых *предпочтений* выпуска:

  :::image type="content" source="images/m365-admin-center-targeted-releases.png" alt-text="Центр администрирования Microsoft 365 меню &quot;Параметры выпуска&quot; с выбранным параметром целевого выпуска":::

  Дополнительные сведения о Office 365 версиях см. в справке [Set up the Standard или Targeted release options](/microsoft-365/admin/manage/release-options-in-office-365) in *Центр администрирования Microsoft 365.*

1. Убедитесь, что клиент поддерживает Teams личные вкладки, работающие на office.com и outlook.com, подписавшись на тестовые учетные данные клиента. Если на боковой панели (точка входа для Teams личных вкладок) вы видите параметр ellipses **(...),** у клиента есть поддержка.

  :::image type="content" source="images/outlook-web-ellipses.png" alt-text="Эллипсы &quot;...&quot; точка входа в Teams вкладки приложений в outlook.com":::

1. Проверьте поддержку тестовых клиентов для расширений обмена сообщениями в outlook.com, проверяя параметр **More apps** в области Outlook составить сообщение.

> [!NOTE]
> Если вы выбрали целевые выпуски, но не видите эти параметры, вероятно, поддержка функций предварительного просмотра все еще находится в процессе выхода на клиент. Последние обновления см. в [Microsoft Teams блог разработчика.](https://devblogs.microsoft.com/microsoft365dev/category/teams/)

## <a name="install-office-apps-in-your-test-environment"></a>Установка Office приложений в тестовой среде

> [!IMPORTANT]
> Обратитесь к последнему Microsoft Teams [- Microsoft 365](https://devblogs.microsoft.com/microsoft365dev/category/teams/) блогу разработчика, чтобы проверить, Outlook для Windows для Teams расширений сообщений доступен для тестовых клиентов.

Вы можете просмотреть Teams приложения, работающие Outlook на Windows настольном компьютере с помощью недавней *сборки бета-канала.* Чтобы установить сборку Outlook бета-версии канала в тестовой [](/deployoffice/change-update-channels?WT.mc_id=M365-MVP-5002016) среде, вам, вероятно, потребуется изменить канал обновления Приложения Microsoft 365 для клиента тестирования.

Ниже ниже 10 действий по установке Office 365 *бета-каналов* в тестовой среде:

1. Войдите в тестовую среду с помощью учетной записи тест-клиента.
1. Скачайте [средство Office развертывания](https://www.microsoft.com/download/details.aspx?id=49117) и извлеките в локализованную папку.
1. Откройте *configuration-Office365-x86.xml* (или **x64.xml*, в зависимости от среды) в текстовом редакторе и обновите значение *Channel* до `BetaChannel` .
1. Из командного запроса с повышенными уровнями `setup.exe /configure configuration-Office365-x86.xml` запустите (или используйте файл **x64.xml,* в зависимости от настройки).
1. Откройте Outlook (клиент настольного компьютера) и установите учетную запись почты с помощью тестовых учетных данных клиента.
1. В Outlook откройте файл Office Учетную запись о Outlook , и подтвердите, что вы находитесь сейчас на бета-канале и что ваш номер сборки  >    >   **14416** или выше. 
1. Перегнать **кнопку Coming Soon** в углу окна Outlook клиента:

   :::image type="content" source="images/outlook-coming-soon.png" alt-text="Кнопка &quot;Скоро&quot; в Outlook настольном компьютере с перемежатой кнопкой &quot;On&quot;}":::

  > [!NOTE]
  > Может потребоваться закрыть Outlook и перезапустить компьютер для появления кнопки *Coming Soon.*

Вы можете убедиться, что клиент поддерживает Teams личные вкладки, работающие на Outlook для Windows настольного компьютера, подписавшись с учетными данными тестовых клиентов и нажав параметр ellipses **(...**) на боковой панели (точка входа для Teams личных вкладок).

:::image type="content" source="images/outlook-desktop-ellipses.png" alt-text="Эллипсы &quot;...&quot; точка входа в Teams приложений вкладки в Outlook для рабочего стола":::

Кроме того, можно проверить поддержку тестовых клиентов для расширений обмена сообщениями в Outlook для Windows настольного компьютера, проверяя параметр More **apps** в ленте Outlook сообщений.

> [!NOTE]
> Если вы выбрали выпуски бета-канала, но не видите эти параметры эллипсов, вероятно, поддержка функций предварительного просмотра все еще находится в процессе отката к вашему клиенту. Последние обновления см. в [Microsoft Teams блог разработчика.](https://devblogs.microsoft.com/microsoft365dev/category/teams/)

## <a name="switch-to-the-developer-preview-version-of-teams"></a>Переключиться на Developer Preview версию Teams

Убедитесь, что вы выбираете [*общедоступный Developer Preview*](../resources/dev-preview/developer-preview-intro.md) от Microsoft Teams клиента.

1. Во входящие Teams с учетной записью клиента в песочнице.
1. Из меню ellipsis **(...**) рядом с профилем пользователя выберите **параметр О** и выберите параметр **предварительного просмотра разработчика.**
1. После того как диалоговое окно появится, выберите переключатель для предварительного просмотра для Teams и убедитесь, что Developer Preview включена. 

:::image type="content" source="images/teams-dev-preview.png" alt-text="Из Teams эллипсов откройте параметр &quot;About&quot; и убедитесь, что Developer Preview 'проверяется&quot;":::

## <a name="install-visual-studio-code-and-teams-toolkit-preview-extension"></a>Установка Visual Studio Code и Teams набор средств предварительного просмотра

Необязательно, вы можете воспользоваться преимуществами [Visual Studio Code,](https://code.visualstudio.com/) чтобы расширить Teams приложения в Office и Outlook.

Расширение Teams набор средств [для Visual Studio Code](https://aka.ms/teams-toolkit) (или более поздней) предоставляет команды, которые могут помочь изменить существующий код Teams, чтобы быть совместимым с Outlook и `v2.10.0` Office. Продолжить, [чтобы Teams личную вкладку для Office и Outlook,](extend-m365-teams-personal-tab.md) чтобы узнать больше.

## <a name="next-steps"></a>Дальнейшие действия

- [Включение личной вкладки Teams в Office и Outlook](extend-m365-teams-personal-tab.md)
- [Включение расширения для сообщений Teams в Outlook](extend-m365-teams-message-extension.md)