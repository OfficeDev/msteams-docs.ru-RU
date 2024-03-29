---
title: Публикация приложений Teams с помощью набора средств Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете, как публиковать приложения Teams с помощью набора средств Teams и публиковать их в отдельной области или в неопубликованных разрешениях.
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d6333afb6d62fc832310c165c30970254998e91e
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833158"
---
# <a name="publish-teams-apps-using-teams-toolkit"></a>Публикация приложений Teams с помощью набора средств Teams

После создания приложения вы можете распространять его в различных объемах, таких как отдельные лица, группы, организации или все остальные. Распределение зависит от нескольких факторов, таких как потребности, бизнес- и технические требования, а также от вашей цели для приложения. Для распространения в другом объеме может потребоваться другой процесс проверки. Как правило, чем больше объем, тем больше проверок должно пройти приложение на предмет безопасности и соответствия требованиям.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish-flow.png" alt-text="Поток публикации":::

В этом разделе вы узнаете следующее:

* [Публикация в отдельной области или разрешение на загрузку неопубликованного приложения](#publish-to-individual-scope-or-sideload-permission)
* [Публикация в организации](#publish-to-your-organization)
* [Публикация в магазине Microsoft Teams](#publish-to-microsoft-teams-store)

## <a name="prerequisites"></a>Предварительные условия

* Создайте [пакет приложения](~/concepts/build-and-test/apps-package.md) и [проверьте его](https://dev.teams.microsoft.com/appvalidation.html) на наличие ошибок.
* [Включите загрузку пользовательских приложений](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) в Teams.
* Убедитесь, что приложение работает и доступно через HTTPS.
* Убедитесь, что вы выполнили ряд рекомендаций при публикации приложения в магазине Microsoft Teams для публикации приложения.

## <a name="publish-to-individual-scope-or-sideload-permission"></a>Публикация в отдельной области или разрешение на загрузку неопубликованного приложения

Вы можете добавить пользовательское приложение в Teams, отправив [пакет приложения](../concepts/build-and-test/apps-package.md) в файл *.zip непосредственно команде или в личном контексте. Добавление пользовательского приложения путем отправки пакета приложения называется загрузкой неопубликованных приложений. Он позволяет тестировать приложение во время отправки в Teams. Вы можете создавать и тестировать приложение в следующих сценариях:

* Тестируйте и отлаживайте приложение локально.
* Создайте приложение для себя, например, для автоматизации рабочего процесса.
* Создайте приложение для небольшой группы пользователей, например для вашей рабочей группы.

Вы можете создать приложение только для внутреннего использования и поделиться им со своей командой, не отправляя его в каталог приложений Teams в магазине приложений Teams. Дополнительные сведения см [. в разделе Отправка приложения в Teams](../concepts/deploy-and-publish/apps-upload.md).

### <a name="to-build-your-app-to-zip-app-package-file"></a>Создание приложения в zip-файле пакета приложения

Сначала необходимо выполнить команду `Provision in the cloud` перед сборкой пакета приложения. Следующие шаги помогут вам создать пакет приложения.

* Выберите **Пакет метаданных Zip Teams** в разделе **РАЗВЕРТЫВАНИЕ**.<br>
    Созданный пакет приложения будет расположен в `{your project folder}/build/appPackage/appPackage.{env}.zip`.

### <a name="to-upload-app-package"></a>Отправка пакета приложения

Выполните следующие действия, чтобы отправить пакет приложения:

1. В клиенте Teams выберите **Приложения** > **Управление приложениями** > **, отправив приложение**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/publish1.png" alt-text="Публикация приложения":::

   Откроется окно **отправки приложения**.

2. Выберите **Отправить пользовательское приложение**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/upload.png" alt-text="отправка приложения":::

   Теперь приложение загружается неопубликованно в клиент Teams, и его можно добавить и просмотреть.

## <a name="publish-to-your-organization"></a>Публикация в организации

Когда приложение будет готово для использования в рабочей среде, вы можете отправить его с помощью API отправки приложений Teams, вызываемого из API Graph. API отправки приложений Teams — это интегрированная среда разработки (IDE), например Microsoft Visual Studio Code, установленная с набором средств Teams. Следующие действия помогут вам опубликовать приложение в вашей организации.

* [Публикация из набора средств Teams](#publish-from-teams-toolkit)
* [Утверждение в центре Администратор](#approve-on-admin-center)

### <a name="publish-from-teams-toolkit"></a>Публикация из набора средств Teams

Следующие действия помогут вам опубликовать приложение из набора средств Teams.

1. Вы можете опубликовать приложение Teams одним из следующих способов:
     * Выберите **Опубликовать в Teams** в разделе **РАЗВЕРТЫВАНИЕ** в виде дерева набора средств Teams.
     * Введите триггер **Teams: публикация в Teams** из палитры команд.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-publish.png" alt-text="Выберите Опубликовать.":::

1. Выберите **Установить для своей организации**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/installforyourorganization.png" alt-text="Установить для вашей организации":::

   Теперь приложение успешно опубликовано на портале администрирования, и вы увидите следующее уведомление:

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/confirm-publish.png" alt-text="Подтверждение публикации":::

Теперь приложение доступно в Центре администрирования Microsoft Teams **,** где вы и администратор можете просмотреть и утвердить его.

> [!NOTE]
> Приложение еще не опубликовано в магазине приложений вашей организации. Этот шаг отправляет приложение в центр администрирования Microsoft Teams, где вы можете утвердить его для публикации в магазине приложений вашей организации.

### <a name="approve-on-admin-center"></a>Утверждение в центре Администратор

Набор средств Teams для Visual Studio Code создан на основе API отправки приложений Teams и позволяет автоматизировать процесс отправки и утверждения для пользовательских приложений в Teams.

  > [!NOTE]
  > Убедитесь, что у вас есть проект приложения Teams в коде VS. Как администратор, **Управление приложениями** в центре администрирования [Microsoft Teams](https://admin.teams.microsoft.com/policies/manage-apps) — это место, где вы можете просматривать и управлять всеми приложениями Teams для вашей организации. В Центре администрирования можно выполнить следующие действия:
  >
  > * См. сведения о состоянии и свойствах приложений на уровне организации.
  > * Утверждение или отправка новых пользовательских приложений в магазин приложений вашей организации.
  > * Блокировать или разрешать приложения на уровне организации.
  > * Добавление приложений в Teams.
  > * Приобретение служб для сторонних приложений.
  > * Просмотр разрешений, запрашиваемых приложениями.
  > * Предоставление согласия администратора приложениям.
  > * [Управление параметрами приложений для всей организации](https://admin.teams.microsoft.com/policies/manage-apps).

Следующие действия помогут вам утвердить в центре Администратор.

1. Выберите **Перейти на портал администрирования**.

1. :::image type="icon" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Showall.PNG"::: Щелкните значок > **приложение** >  Teams **Управление приложениями**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manage-apps.png" alt-text="Выберите Управление приложениями":::

   Вы можете просмотреть все приложения Teams для вашей организации.

   Виджет ''Ожидает утверждения'' в верхней части страницы позволяет узнать, когда пользовательское приложение отправлено на утверждение. В таблице только что отправленное приложение автоматически публикует состояние отправленных и заблокированных приложений. Чтобы найти приложение, можно отсортировать столбец состояния публикации в порядке убывания.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/admin-approval-for-teams-app-1.png" alt-text="утверждение":::

1. Выберите имя приложения, чтобы перейти на страницу сведений о приложении. На вкладке **О программе** можно просмотреть сведения о приложении, включая описание, состояние и идентификатор приложения.

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/about-submitted-app-1.png" alt-text="отправленное приложение":::

1. Выберите раскрывающийся список состояние и измените значение **с "Отправлено"** на **"Опубликовать**".

   После публикации приложения статус публикации изменится на ''Опубликовано'', а статус автоматически изменится на ''Разрешено''.

   Дополнительные сведения см. в статье [Публикация в организации](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json).

## <a name="publish-to-microsoft-teams-store"></a>Публикация в магазине Microsoft Teams

Вы можете распространять приложение в магазине непосредственно в Microsoft Teams и связываться с миллионами пользователей по всему миру. Если ваше приложение также доступно в магазине, вы можете мгновенно охватить потенциальных клиентов. Приложения, опубликованные в магазине Teams, также автоматически отображаются в Microsoft AppSource, который является официальной торговой площадкой для приложений и решений Microsoft 365.

Дополнительные сведения см. [в статье Публикация приложения в магазине Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md#publish-your-app-to-the-microsoft-teams-store).

## <a name="see-also"></a>См. также

* [Распространение приложения Microsoft Teams](../concepts/deploy-and-publish/apps-publish-overview.md)
* [Создание пакета приложения в Teams](../concepts/build-and-test/apps-package.md)
* [Подготовка клиента Microsoft 365](../concepts/build-and-test/prepare-your-o365-tenant.md)
* [Опубликуйте свое приложение в Магазине Microsoft Teams](../concepts/deploy-and-publish/appsource/publish.md)
* [Отправка приложения в Microsoft Teams](../concepts/deploy-and-publish/apps-upload.md)
* [Управление приложением Teams в Центре администрирования Microsoft Teams](/MicrosoftTeams/manage-apps?toc=%2Fmicrosoftteams%2Fplatform%2Ftoc.json&bc=%2Fmicrosoftteams%2Fplatform%2Fbreadcrumb%2Ftoc.json)
