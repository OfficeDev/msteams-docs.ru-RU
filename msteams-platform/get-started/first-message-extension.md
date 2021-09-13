---
title: Начало работы — создание первого расширения для сообщений
author: adrianhall
description: Создайте расширение для сообщений для Microsoft Teams с помощью набора средств Teams.
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: 52352d23533b80c9df5422f87e58d318987b6e95
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59157328"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>Создание и запуск первого расширения для сообщений для Microsoft Teams

В этом руководстве вы узнаете, как создать команду поиска для поиска внешних данных и вставить результаты в сообщение.  

Существует два типа **расширений для сообщений** Teams.

- [Команды поиска](../messaging-extensions/how-to/search-commands/define-search-command.md) позволяют выполнять поиск во внешних системах и вставлять результаты поиска в сообщение в виде карточки.
- [Команды действий](../messaging-extensions/how-to/action-commands/define-action-command.md) позволяют предоставлять пользователям модальное всплывающее окно для сбора или отображения информации, а затем обрабатывать их действия и отправлять информацию обратно в Teams.

## <a name="before-you-begin"></a>Перед началом работы

Убедитесь, что среда разработки настроена путем установки необходимых условий.

> [!div class="nextstepaction"]
> [Установка необходимых компонентов](prerequisites.md)

## <a name="create-your-project"></a>Создание проекта

Используйте набор средств Teams для создания своего первого проекта.

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. Откройте Visual Studio Code.
1. Выберите значок Teams на боковой панели, чтобы открыть Teams набор средств.

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Значок Teams на боковой панели Visual Studio Code":::.

1. Выберите **Создать проект**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Расположение ссылки &quot;Создать проект&quot; на боковой панели набора средств Teams":::.

1. Выберите **Создать приложение Teams**.

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="Запуск мастера для создания проекта":::

1. В разделе **Выбор возможностей выберите** расширение **сообщений,** разблокировать **вкладку и** выбрать **ОК.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="Снимок экрана: добавление возможностей в новое приложение.":::

1. В разделе **Регистрация ботов** выберите **Создать новую регистрацию бота.**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="Выбор создания новой регистрации бота":::

   > [!NOTE]
   > Расширения для сообщений используют боты для диалога между пользователем и кодом.

1. В разделе **Язык программирования** выберите **JavaScript**.

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="Снимок экрана: выбор языка.":::

1. Выберите папку рабочей области.  В папке рабочей области будет создана папка для создаваемого проекта.

1. Введите подходящее имя для приложения, например `helloworld`.  Имя приложения должно состоять только из букв и цифр.  Чтобы продолжить, нажмите клавишу **ВВОД**.

   Создание приложения Teams займет несколько секунд.

# <a name="command-line"></a>[Командная строка](#tab/cli)

Используйте для создания первого проекта интерфейс командной строки `teamsfx`.  Начните с папки, в которой будет создана папка проекта.

``` bash
teamsfx new
```

Интерфейс командной строки выдаст несколько вопросов, ответы на которые используются для создания проекта.  Каждый вопрос сопровождается подсказкой о том, как на него отвечать (например, использовать клавиши со стрелками для выбора варианта).  Ответив на вопрос, подтвердите свой выбор, нажав клавишу **ВВОД**.

1. Выберите **Создать приложение Teams**.
1. Выберите **вкладку Расширение сообщений** **и** выселку.
1. Выберите **Создать новую регистрацию бота**.
1. Выберите **JavaScript** в качестве языка.
1. Нажмите клавишу **ВВОД**, чтобы выбрать папку рабочей области по умолчанию.
1. Введите подходящее имя для приложения, например `helloworld`.  Имя приложения должно состоять только из букв и цифр.

   После ответа на все вопросы создается проект.

---

## <a name="take-a-tour-of-the-source-code"></a>Знакомство с исходным кодом

Если вы хотите пропустить этот раздел, вы можете [запустить приложение локально](#run-your-app-locally).

Расширение для сообщений использует [Bot Framework](https://docs.botframework.com), чтобы дать пользователю возможность взаимодействовать со службой посредством общения.  После генерации кода проект будет выглядеть следующим образом:

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="Макет файла проекта бота.":::

Код бота хранится в каталоге `bot`.  `bot/messageExtensionBot.js` — это главная точка входа для расширения для сообщений.

> [!Tip]
> Перед интеграцией своего первого бота в Teams ознакомьтесь с ботами за пределами Teams.  Дополнительные сведения о ботах см. в руководстве [Служба Azure Bot](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true).

## <a name="run-your-app-locally"></a>Локальный запуск приложения

Набор средств Teams позволяет размещать приложение локально.  Для этого:

- Приложение Azure Active Directory регистрируется в клиенте M365.
- Манифест приложения отправляется на портал разработчика для Teams.
- API запускается локально с помощью Azure Functions Core Tools для поддержки приложения.
- [ngrok](https://ngrok.io) устанавливается и используется для обеспечения туннеля между Teams и расширением для сообщений.

Чтобы создать и запустить приложение локально, выполните следующие действия.

1. С Visual Studio Code нажмите **клавишу F5,** чтобы запустить приложение в режиме отлаживания.

   > При первом запуске приложения произойдет загрузка всех зависимостей и сборка приложения.  По завершении сборки автоматически откроется окно браузера.  Для завершения может потребоваться от 3 до 5 минут.

1. В браузере будет выполнена загрузка Teams, и вам будет предложено войти. При появлении запроса на открытие Microsoft Teams выберите "Отменить", чтобы остаться в браузере. Войдите с помощью своей учетной записи M365.

1. Выберите **Добавить,** чтобы добавить приложение в свою учетную запись.

   После загрузки приложения вы будете доставлены непосредственно в диалоговое окно поиска:

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="Принцип работы расширения для сообщений на основе поиска":::

   Введите текст в поле поиска и выберите один из вариантов.  В поле ввода будет добавлена адаптивная карточка.

<!-- markdownlint-disable MD033 -->
<details>
<summary>Узнайте, что происходит при локальном запуске приложения в отладчике.</summary>

При нажатии **клавиши F5** Teams набор средств:

1. Регистрирует приложение с помощью Azure Active Directory.
1. Регистрирует приложение для "боковой загрузки" в Microsoft Teams.
1. Запускает локализованную работу backend приложения с помощью основных средств [Azure Function.](/azure/azure-functions/functions-run-local?#start)
1. Запускает туннель ngrok, чтобы Teams взаимодействовать с приложением.
1. Начинается Microsoft Teams с командой Teams для загрузки приложения.

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>Узнайте, как устранить распространенные проблемы при локальном запуске приложения.</summary>

Чтобы запустить приложение в Teams, у вас должна быть учетная запись разработчика Microsoft 365, позволяющая устанавливать неопубликованные приложения. Дополнительные сведения о создании учетной записи см. в разделе [Необходимые компоненты](prerequisites.md#enable-sideloading).

> [!TIP]
> Перед установкой неопубликованного приложения проверьте наличие проблем с помощью [средства проверки приложений](https://dev.teams.microsoft.com/appvalidation.html), которое входит в набор средств. Исправьте ошибки, чтобы успешно установить неопубликованное приложение.
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>Узнайте, что происходит после развертывания приложения в Azure</summary>

До развертывания приложение работает локально:

1. Серверная часть работает с использованием _Azure Functions Core Tools_.
1. Конечная точка HTTP приложения, в которую Microsoft Teams загружает приложение, работает локально.

Развертывание включает подготовку ресурсов для активной подписки Azure и развертывание (загрузку) внутреннего и внешнего кода приложения в Azure. Серверная часть использует различные службы Azure, включая службу приложений Azure и службу Azure Bot.

</details>

## <a name="add-a-configuration-page-to-your-messaging-extension"></a>Добавление страницы конфигурации в расширение обмена сообщениями

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a>Пример кода

В Teams в примере проектов по GitHub показано, как создавать расширения обмена сообщениями, включающие страницу конфигурации и проверку подлинности службы [ботов.](https://github.com/microsoft/BotBuilder-Samples#teams-samples) В примерах также показано, как создавать расширения сообщений, которые принимают запросы на поиск и возвращают результаты после того, как пользователь вписался.

| **Название примера** | **Описание** | **.NET** | **Node.js** | **Python** |
|-----------------|-----------------|-------------|--------------|--------|
| Строитель ботов | Создание расширений обмена сообщениями. | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [View]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a>Дополнительный пример кода

> [!div class="nextstepaction"]
> [Просмотр дополнительных примеров bot Framework в GitHub](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a>См. также

* [Обзор учебников](code-samples.md) 
* [Создание приложения с React](first-app-react.md)
* [Создание приложения с помощью Blazor](first-app-blazor.md)
* [Создание приложения с SPFx](first-app-spfx.md)
* [Создание приложения с помощью C# или .NET](get-started-dotnet-app-studio.md)
* [Создайте приложение с помощью Node.js](get-started-nodejs-app-studio.md)
* [Создание приложения с помощью генератора Yeoman](get-started-yeoman.md)
* [Создание бота беседы](first-app-bot.md)
* [Примеры кода](https://github.com/OfficeDev/Microsoft-Teams-Samples)