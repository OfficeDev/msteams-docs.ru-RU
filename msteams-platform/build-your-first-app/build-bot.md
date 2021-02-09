---
title: Начало работы — создание бота
author: heath-hamilton
description: Быстро создайте бот Microsoft Teams с помощью microsoft Teams набор средств.
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 3e07c148e1b03431dc419a4e3679abac0229ff72
ms.sourcegitcommit: e08f309f62db2cf0f505f2aadfe728e5b46c17a5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/08/2021
ms.locfileid: "50140470"
---
# <a name="build-a-bot-for-microsoft-teams"></a>Создание бота для Microsoft Teams

В этом руководстве  вы создадим базовое бот-приложение. Бот действует как посредник между пользователями Teams и веб-службой. Люди могут общаться с ботом, чтобы быстро получить информацию или инициировать рабочий процесс и задачи, выполняемые вашей службой.

## <a name="your-assignment"></a>Назначение

На рабочем месте создано приложение Teams, использующее [вкладки](../build-your-first-app/build-personal-tab.md) для получения важных контактных данных. Например, у коллег есть быстрый доступ к номеру телефона службы поддержки. Но что делать, если бы люди могли обращаться в службу поддержки с помощью чат-робота? Ваш начальник просит вас узнать, как быстро вы можете получить базовый бот для бесед в Teams.

## <a name="what-youll-learn"></a>Что вы узнаете

> [!div class="checklist"]
>
> * Создание проекта приложения и бота с помощью microsoft Teams набор средств для Visual Studio Code
> * Определение некоторых конфигураций приложений и скаолдинг, релевантный для ботов
> * Локальное приложение
> * Настройка бота для Teams
> * Загрузка неогрузки и тестирование бота в Teams

## <a name="before-you-begin"></a>Прежде чем начать

Если вы еще не знаете и не установили необходимые условия для [разработки Teams.](build-first-app-overview.md#get-prerequisites)

## <a name="1-create-your-app-project"></a>1. Создайте проект приложения

Microsoft Teams набор средств поможет вам настроить следующие компоненты для вашего приложения:

* **Конфигурации приложений и скафолдинг,** релевантные для ботов
* **Бот,** автоматически зарегистрированный в службе ботов Microsoft Azure

> [!TIP]
> Если вы еще не создавали проект приложения Teams, возможно, вам будет полезно следовать этим инструкциям, чтобы подробнее объяснить проекты. [](../build-your-first-app/build-and-run.md)

1. В Visual Studio кода выберите **Microsoft Teams** в левой панели действий и выберите :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: **"Создать новое приложение Teams".**
1. При запросе во sign in with your Microsoft 365 development account.
1. On the **Add capabilities** screen, select **Bot** then **Next**.
1. Введите имя приложения Teams. (Это имя приложения по умолчанию, а также имя каталога проекта приложения на локальном компьютере.)
1. Go to **Configure bot** and select **Create a new Bot** then Create Bot **Registration**. В случае успеха новый бот будет иметь **зарегистрированный** статус.
1. Выберите **"Готово"** в нижней части экрана и выберите расположение для создания проекта.

## <a name="2-identify-relevant-app-project-components"></a>2. Определение соответствующих компонентов проекта приложения

Большая часть конфигураций и скафаолдинга приложений автоматически заданная при создании проекта с помощью командной набор средств. Рассмотрим основные компоненты для создания бота.

### <a name="app-configurations"></a>Конфигурации приложений

Чтобы просмотреть или обновить конфигурации бота, выберите **App Studio** в наборе средств и перейдите к **ботам.**

### <a name="app-scaffolding"></a>Скафаолдинг приложений

Скафолдинг приложения предоставляет файл, расположенный в корневом каталоге проекта, для обработки того, как бот обрабатывает действия в Teams (например, как бот реагирует на определенные сообщения, такие как `botActivityHandler.js` "Hello").

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. Настройка безопасного туннеля для приложения

Для тестирования разберем ваше приложение на локальном веб-сервере (порт 3978).

1. Если вы еще не сделали этого, установите [ngrok.](https://ngrok.com/download)
1. В терминале запустите `ngrok http -host-header=rewrite 3978` .
1. Скопируйте URL-адрес HTTPS в выходных данных (например, ),так как `https://468b9ab725e9.ngrok.io` Teams требует подключения HTTPS.

С помощью этого URL-адреса Teams (для которого требуются подключения ПО HTTPS) будет иметь туннель, в котором размещено приложение (через порт `localhost` 3978).

## <a name="4-configure-your-bot"></a>4. Настройте бота

Чтобы использовать бота в Teams, необходимо зарегистрировать его в службе ботов Azure. Это делается автоматически при настройках приложения с помощью командной набор средств.

Вам по-прежнему необходимо указать адрес конечной точки для получения и обработки пользовательских сообщений (то есть запросов), отправленных боту. Как правило, URL-адрес `https://HOST_URL/api/messages` выглядит. Это можно быстро настроить в наборе средств.

1. В Visual Studio code выберите **Microsoft Teams** в левой панели действий и :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: выберите команду **"Открыть Microsoft Teams набор средств.**
1. Перейдите **в > регистрации** существующих ботов и выберите бота, созданного во время установки.
1. В поле **адреса конечной точки бота** введите URL-адрес ngrok (например, url-адрес), в котором размещен бот, и `https://468b9ab725e9.ngrok.io` введите `/api/messages` его.<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="Иллюстрация, показывающая, где можно настроить URL-адрес конечной точки бота в набор средств.":::

Бот сможет отвечать на сообщения в Teams.

## <a name="5-build-and-run-your-app"></a>5. Сборка и запуск приложения

Вы настроили URL-адрес для своего бота и настроили его для обработки сообщений. Пора приумножите свое приложение к работе.

1. В терминале перейдите в корневой каталог проекта приложения и запустите `npm install` его.
1. Запустите `npm start` .

В случае успеха вы увидите следующее сообщение, указывающее, что ваш бот прослушивает действия на вашем `localhost` компьютере:

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. Загрузка нео sideload бота в Teams

С помощью бота вы можете установить его в Teams.

> [!TIP]
> Если вы еще не выгружали неогруженные приложения Teams и не могли с ним работать, следуйте [этим инструкциям.](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)

1. В Visual Studio Code нажмите клавишу **F5,** чтобы запустить веб-клиент Teams.
1. В диалоговом окте "Установка приложения" выберите **"Добавить для меня".** (You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)

## <a name="7-test-your-bot"></a>7. Тестирование бота

Теперь для интересной части: скажите "Hello" вашему боту.

1. В поле составить `Hello` сообщение.

Бот отвечает следующим сообщением:

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="Снимок экрана: пользователь говорит &quot;Hello&quot; боту Teams и получает ответ.":::

## <a name="well-done"></a>Прекрасно

Поздравляем! У вас есть базовый бот Teams, который может взаимодействовать с пользователями по одному или в параметрах группы (каналах и чатах).

## <a name="troubleshooting"></a>Устранение неполадок

Следующие сведения могут помочь, если у вас были проблемы с выполнением этого руководства.

### <a name="bot-isnt-connected-to-teams"></a>Бот не подключен к Teams

Если вы установили приложение, но бот не работает, убедитесь, что бот подключен к каналу Teams службы ботов [Azure. ](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)

Важно понимать, что это не то же самое, что канал в Teams. В этом случае служба ботов Azure подключает бота к Teams или другому поддерживаемом [приложению Майкрософт](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)или стороннему приложению для связи.

## <a name="learn-more"></a>Подробнее

* [Узнайте, что еще могут делать боты Teams с одним из наших примеров](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [Основы беседы для ботов](../bots/how-to/conversations/conversation-basics.md)
* Следуйте [нашим рекомендациям по проектированию](../bots/design/bots.md) и создавайте [шаблоны](../concepts/design/design-teams-app-ui-templates.md) пользовательского интерфейса, готовые к выпуску, чтобы у вас было простое впечатление.
* [Проверка подлинности ботов в Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [Создание бота без наборов средств](../resources/bot-v3/bots-create.md)
