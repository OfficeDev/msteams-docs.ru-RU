---
title: Начало работы — создание первого обзора приложения и необходимых условий
author: heath-hamilton
description: Узнайте, как начать разработку приложений Microsoft Teams и настроить среду.
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: quickstart
ms.openlocfilehash: 4288efdbfada5f1a51fa1d4aeccdd6cdf9c64382
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797899"
---
# <a name="build-your-first-microsoft-teams-app-overview"></a>Создание первого обзора приложения Microsoft Teams

На **уроках по началу** работы вы узнаете, как создавать базовые приложения Teams. В каждом руководстве поется о том, как создать простое, реальное приложение Teams, а также общие инструменты, основные понятия и более сложные функции.

## <a name="what-youll-learn"></a>Что вы узнаете

Вот представление о том, что вы узнаете после уроков.

> [!div class="checklist"]
  >
  > * Быстрое создание и запуск teams **набор средств:** Microsoft Teams набор средств for Visual Studio Code создает проект приложения и создает скафолдинг, чтобы у вас было запущено приложение за несколько минут.
  > * **Настройте приложение с помощью App Studio:** укажите возможности и службы, которые использует ваше приложение Teams.
  > * **Область аудитории приложения:** создайте приложение Teams для личного использования, совместной работы или и того, и другое.
> * Получите опыт работы со средствами Teams и **SDK:** настройте приложение с помощью клиентского SDK JavaScript для Teams. Например, измените цветовую схему приложения в соответствие с темой Teams. Кроме того, узнайте о распространенных средствах для создания ботов и управления их.
  > * **Разберите свое** приложение. Во время уроков вы найдете интересуя вас связанные темы (например, руководство по проверке подлинности и проектированию).

## <a name="teams-app-fundamentals"></a>Основы приложения Teams

Прежде чем приступить к учебникам, необходимо знать следующее о создании приложений для Teams.

### <a name="apps-can-have-multiple-capabilities-and-entry-points"></a>Приложения могут иметь несколько возможностей и точек входа

Приложение Teams состоит из одной или более возможностей [платформы](../concepts/capabilities-overview.md) (как люди используют приложение) и точек входа [(где](../concepts/extensibility-points.md) люди используют приложение).

### <a name="teams-doesnt-host-your-app"></a>Приложение не в Teams

Приложение Teams включает следующие важные элементы:

* Логика, хранилище данных и API-вызовы, которые могут быть в вашем приложении. Эти службы не находятся в Teams и должны быть доступны по протоколу HTTPS.
* Клиент Teams (веб-, настольный или мобильный), в котором пользователи используют ваше приложение.
* ИД приложения, который позволяет настроить приложение с помощью App Studio.

## <a name="get-prerequisites"></a>Получить необходимые условия

Убедитесь, что у вас есть учетная запись для создания приложений Teams и установите некоторые рекомендуемые средства разработки.

### <a name="set-up-your-development-account"></a>Настройка учетной записи разработки

Вам нужна учетная запись Teams, которая позволяет настраивать загрузку нео том же приложения. (Возможно, ваша учетная запись уже предоставила это.)

1. Если у вас есть учетная запись Teams, проверьте, можете ли вы загрузку неогрузки приложений в Teams:
    1. В клиенте Teams выберите **"Приложения".**
    1. Найди вариант **отправки настраиваемого приложения.**

    :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно отправить пользовательское приложение.":::

<!-- markdownlint-disable MD033 -->
<details>

<summary><b>Выберите здесь,</b> если не видите параметр загрузки неогрузки или у вас нет учетной записи Teams.</summary>

Вы можете получить бесплатную тестовую учетную запись Teams, которая позволяет загрузку неогрузки приложения, присоединившись к программе для разработчиков Microsoft 365. (Процесс регистрации занимает приблизительно две минуты.)

1. Перейдите в [программу для разработчиков Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)
1. Выберите **"Присоединиться сейчас"** и следуйте инструкциям на экране.
1. When you get to the welcome screen, select **Set up E5 subscription**.
1. Настройка учетной записи администратора. После завершения вы увидите экран, похожий на этот.
:::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации в программе для разработчиков Microsoft 365.":::
1. Войдите в Teams с помощью только что настроенной учетной записи администратора.
1. Проверьте, есть ли у вас параметр **отправки настраиваемого** приложения.

</details>

> [!Note]
> Если вы по-прежнему не можете загружать неогружаемые приложения, включите настраиваемые приложения Teams и включите отправку [пользовательских приложений.](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant#enable-custom-teams-apps-and-turn-on-custom-app-uploading)

### <a name="install-your-development-tools"></a>Установка средств разработки

Вы можете создавать приложения Teams с помощью предпочитаемых инструментов, но эти уроки показывают, как быстро начать работу с microsoft Teams набор средств для Visual Studio Code.

Teams отображает содержимое приложения только через ПОДКЛЮЧЕНИЯ HTTPS. Для локальной отлаки определенных типов приложений, таких как бот, вы узнаете, как использовать [ngrok](../concepts/build-and-test/debug.md#locally-hosted) для настроить безопасный туннель между Teams и вашим приложением. (Приложения Production Teams находятся в облаке.)

1. Установите [Node.js](https://nodejs.org/en/).
1. Установите [ngrok,](https://ngrok.com/download) если вы планируете создать бота или расширение для обмена сообщениями.
1. Установите последнюю версию [Visual Studio Code.](https://code.visualstudio.com/download) (Более ранние версии могут не работать с набором средств.)
1. В Visual Studio code выберите **"Расширения"** в левой панели действий и установите :::image type="icon" source="../assets/icons/vs-code-extensions.png"::: microsoft Teams **набор средств.**

    :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, на которой по Visual Studio Code можно установить расширение Microsoft Teams набор средств.":::

## <a name="about-the-tutorials"></a>Об учебниках

Вы можете начать с любого из уроков по **началу** работы с Teams. Если вы не знаете, куда перейти в первую очередь, следуйте нашему начинающему удобному пути и создайте "Hello, World!" app.

:::image type="content" source="../assets/images/build-your-first-app/skill-tree-overview.png" alt-text="Дерево навыков, в котором показаны учебные пути для уроков &quot;начало работы&quot; Teams." border="false":::

## <a name="next-step"></a>Следующий шаг

После того как вы настроите свою учетную запись и среду, вы сможете приступить к построению.

### <a name="beginner-friendly-tutorial"></a>Обучающие курсы для начинающих

> [!div class="nextstepaction"]
> [Создание приложения "Hello, World!"](../build-your-first-app/build-and-run.md)

### <a name="other-tutorials"></a>Другие учебники

> [!div class="nextstepaction"]
> [Создание бота](../build-your-first-app/build-bot.md)
> [!div class="nextstepaction"]
> [Создание расширения для сообщений](../build-your-first-app/build-messaging-extension.md)
