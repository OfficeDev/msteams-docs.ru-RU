---
title: Создание расширения для сообщений с помощью App Studio
author: clearab
description: Узнайте, как создать расширение обмена сообщениями Microsoft Teams с помощью App Studio.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 25086d959004046e8227de46b31d840c0b3fd228
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51697248"
---
# <a name="create-a-messaging-extension-using-app-studio"></a><span data-ttu-id="d854e-103">Создание расширения для сообщений с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="d854e-103">Create a messaging extension using App Studio</span></span>

> [!TIP]
> <span data-ttu-id="d854e-104">Ищете более быстрый способ начать работу?</span><span class="sxs-lookup"><span data-stu-id="d854e-104">Looking for a faster way to get started?</span></span> <span data-ttu-id="d854e-105">Создание расширения [обмена сообщениями с](../build-your-first-app/build-messaging-extension.md) помощью microsoft Teams набор средств.</span><span class="sxs-lookup"><span data-stu-id="d854e-105">Create a [messaging extension](../build-your-first-app/build-messaging-extension.md) using the Microsoft Teams Toolkit.</span></span>

<span data-ttu-id="d854e-106">На высоком уровне необходимо выполнить следующие действия для создания расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d854e-106">At a high level, you'll need to complete the following steps to create a messaging extension.</span></span>

1. <span data-ttu-id="d854e-107">Подготовка среды разработки</span><span class="sxs-lookup"><span data-stu-id="d854e-107">Prepare your development environment</span></span>
2. <span data-ttu-id="d854e-108">Создание и развертывание веб-службы (при разработке используйте туннельную службу, например ngrok, чтобы запустить ее локально)</span><span class="sxs-lookup"><span data-stu-id="d854e-108">Create and deploy your web service (while developing use a tunneling service like ngrok to run it locally)</span></span>
3. <span data-ttu-id="d854e-109">Регистрация веб-службы в Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d854e-109">Register your web service with the Bot Framework</span></span>
4. <span data-ttu-id="d854e-110">Создание пакета приложений</span><span class="sxs-lookup"><span data-stu-id="d854e-110">Create your app package</span></span>
5. <span data-ttu-id="d854e-111">Отправка пакета в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d854e-111">Upload your package to Microsoft Teams</span></span>

<span data-ttu-id="d854e-112">Создание веб-службы, создание пакета приложений и регистрация веб-службы с помощью Bot Framework можно сделать в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="d854e-112">Creating your web service, creating your app package, and registering your web service with the Bot Framework can be done in any order.</span></span> <span data-ttu-id="d854e-113">Так как эти три части настолько переплетены, независимо от того, какой порядок вы их делаете, вам потребуется вернуться, чтобы обновить другие.</span><span class="sxs-lookup"><span data-stu-id="d854e-113">Because those three pieces are so intertwined, no matter which order you do them in you'll need return to update the others.</span></span> <span data-ttu-id="d854e-114">Для регистрации требуется конечная точка обмена сообщениями из развернутой веб-службы, а веб-службе необходим код и пароль, созданные в вашей регистрации.</span><span class="sxs-lookup"><span data-stu-id="d854e-114">Your registration needs the messaging endpoint from your deployed web service, and your web service needs the Id and password created from your registration.</span></span> <span data-ttu-id="d854e-115">Манифест приложения также должен быть id для подключения Teams к веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d854e-115">Your app manifest also needs that Id to connect Teams to your web service.</span></span>

<span data-ttu-id="d854e-116">При создании расширения обмена сообщениями вы будете регулярно передвигаться между изменением манифеста приложения и развертыванием кода в веб-службе.</span><span class="sxs-lookup"><span data-stu-id="d854e-116">As you're building your messaging extension, you'll regularly be moving between changing your app manifest, and deploying code to your web service.</span></span> <span data-ttu-id="d854e-117">При работе с манифестом приложения имейте в виду, что вы можете либо вручную управлять JSON-файлом, либо вносить изменения через App Studio.</span><span class="sxs-lookup"><span data-stu-id="d854e-117">When working with the app manifest, keep in mind that you can either manually manipulate the JSON file, or make changes through App Studio.</span></span> <span data-ttu-id="d854e-118">В любом случае при внесении изменений в манифест необходимо повторно развернуть (загрузить) приложение в Teams, но при развертывании изменений в веб-службе это не требуется.</span><span class="sxs-lookup"><span data-stu-id="d854e-118">Either way, you'll need to re-deploy (upload) your app in Teams when you make a change to the manifest, but there's no need to do so when you deploy changes to your web service.</span></span>

[!include[prepare environment](~/includes/prepare-environment.md)]

## <a name="create-your-web-service"></a><span data-ttu-id="d854e-119">Создание веб-службы</span><span class="sxs-lookup"><span data-stu-id="d854e-119">Create your web service</span></span>

<span data-ttu-id="d854e-120">Сердцем расширения обмена сообщениями является веб-служба.</span><span class="sxs-lookup"><span data-stu-id="d854e-120">The heart of your messaging extension is your web service.</span></span> <span data-ttu-id="d854e-121">Он определяет один маршрут, как `/api/messages` правило, для получения всех запросов.</span><span class="sxs-lookup"><span data-stu-id="d854e-121">It will define a single route, typically `/api/messages`, to receive all requests on.</span></span> <span data-ttu-id="d854e-122">Если вы начинаете работу с нуля, у вас есть несколько вариантов на выбор.</span><span class="sxs-lookup"><span data-stu-id="d854e-122">If you're getting started from scratch, you have a few options to choose from.</span></span>

* <span data-ttu-id="d854e-123">Используйте один из наших [учебников quickstarts,](#learn-more) который поможет вам создать веб-службу.</span><span class="sxs-lookup"><span data-stu-id="d854e-123">Use one of our [quickstarts](#learn-more) tutorials that will guide you through the creation of your web service.</span></span>
* <span data-ttu-id="d854e-124">Выберите один из примеров расширения обмена сообщениями, доступный в репозитории [образца Bot Framework,](https://github.com/Microsoft/BotBuilder-Samples) чтобы начать с него.</span><span class="sxs-lookup"><span data-stu-id="d854e-124">Choose one of the messaging extension samples available in the [Bot Framework sample repository](https://github.com/Microsoft/BotBuilder-Samples) to start from.</span></span>
* <span data-ttu-id="d854e-125">Если вы используете JavaScript, используйте генератор [Yeoman](https://github.com/OfficeDev/generator-teams) для Microsoft Teams для подмены приложения Teams, включая веб-службу.</span><span class="sxs-lookup"><span data-stu-id="d854e-125">If you're using JavaScript, use the [Yeoman generator for Microsoft Teams](https://github.com/OfficeDev/generator-teams) to scaffold your Teams app, including your web service.</span></span>
* <span data-ttu-id="d854e-126">Создайте веб-службу с нуля.</span><span class="sxs-lookup"><span data-stu-id="d854e-126">Create your web service from scratch.</span></span> <span data-ttu-id="d854e-127">Вы можете добавить пакет SDK Bot Framework для своего языка или работать непосредственно с полезными данными JSON.</span><span class="sxs-lookup"><span data-stu-id="d854e-127">You can choose to add the Bot Framework SDK for your language, or you can work directly with the JSON payloads.</span></span>

## <a name="register-your-web-service-with-the-bot-framework"></a><span data-ttu-id="d854e-128">Регистрация веб-службы в Bot Framework</span><span class="sxs-lookup"><span data-stu-id="d854e-128">Register your web service with the Bot Framework</span></span>

<span data-ttu-id="d854e-129">Расширения обмена сообщениями пользуются схемой обмена сообщениями Bot Framework и протоколом безопасной связи; если у вас еще нет его, вам потребуется зарегистрировать веб-службу в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d854e-129">Messaging extensions take advantage of the Bot Framework's messaging schema and secure communication protocol; if you don't already have one you'll need to register your web service on the Bot Framework.</span></span> <span data-ttu-id="d854e-130">Id Приложения Майкрософт (мы назначим это как бот-Ид изнутри Teams, чтобы идентифицировать его из другого app Id, с помощью который вы можете работать) и конечная точка обмена сообщениями, с помощью реестра ботов, будет использоваться в расширении обмена сообщениями для получения запросов и реагирования на них.</span><span class="sxs-lookup"><span data-stu-id="d854e-130">The Microsoft App Id (we'll refer to this as your Bot Id from inside of Teams, to identify it from other App Id's you might be working with) and the messaging endpoint your register with the Bot Framework will be used in your messaging extension to receive and respond to requests.</span></span> <span data-ttu-id="d854e-131">Если вы используете существующую регистрацию, убедитесь, что вы [включаете канал Microsoft Teams.](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="d854e-131">If you're using an existing registration, make sure you [enable the Microsoft Teams channel](/azure/bot-service/bot-service-manage-channels.md?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="d854e-132">Если вы выполните один из quickstarts или начнете с одного из доступных образцов, вы будете руководствоваться регистрацией веб-службы.</span><span class="sxs-lookup"><span data-stu-id="d854e-132">If you follow one of the quickstarts or start from one of the available samples you'll be guided through registering your web service.</span></span> <span data-ttu-id="d854e-133">Если вы хотите вручную зарегистрировать свою службу, у вас есть три варианта для этого.</span><span class="sxs-lookup"><span data-stu-id="d854e-133">If you want to manually register your service you have three options to do so.</span></span> <span data-ttu-id="d854e-134">Если вы решите зарегистрироваться без использования подписки Azure, вы не сможете воспользоваться упрощенным потоком проверки подлинности OAuth, предоставляемым Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d854e-134">If you choose to register without using an Azure subscription you will not be able to take advantage of the simplified OAuth authentication flow provided by the Bot Framework.</span></span> <span data-ttu-id="d854e-135">После создания вы сможете перенести регистрацию в Azure.</span><span class="sxs-lookup"><span data-stu-id="d854e-135">You will be able to migrate your registration to Azure after creation.</span></span>

* <span data-ttu-id="d854e-136">Если у вас есть подписка Azure (или вы хотите создать новую), вы можете зарегистрировать веб-службу вручную с помощью портала Azure.</span><span class="sxs-lookup"><span data-stu-id="d854e-136">If you have an Azure subscription (or want to create a new one), you can register your web service manually using the Azure Portal.</span></span> <span data-ttu-id="d854e-137">Создайте ресурс "Регистрация каналов ботов".</span><span class="sxs-lookup"><span data-stu-id="d854e-137">Create a "Bot Channels Registration" resource.</span></span> <span data-ttu-id="d854e-138">Вы можете выбрать уровень бесплатных цен, так как сообщения из Microsoft Teams не учитываются в общем допустимом уровне сообщений в месяц.</span><span class="sxs-lookup"><span data-stu-id="d854e-138">You can choose the free pricing tier, as messages from Microsoft Teams do not count towards your total allowable messages per month.</span></span>
* <span data-ttu-id="d854e-139">Если вы не хотите использовать подписку Azure, вы можете использовать устаревший портал [регистрации.](https://dev.botframework.com/bots/new)</span><span class="sxs-lookup"><span data-stu-id="d854e-139">If you do not wish to use an Azure subscription, you can use the [legacy registration portal](https://dev.botframework.com/bots/new).</span></span>
* <span data-ttu-id="d854e-140">App Studio также может помочь вам зарегистрировать веб-службу (бот).</span><span class="sxs-lookup"><span data-stu-id="d854e-140">App Studio can also help you register your web service (bot).</span></span> <span data-ttu-id="d854e-141">Веб-службы, зарегистрированные через App Studio, не регистрируются в Azure.</span><span class="sxs-lookup"><span data-stu-id="d854e-141">Web services registered through App Studio are not registered in Azure.</span></span> <span data-ttu-id="d854e-142">Вы можете использовать [устаревший портал для](https://dev.botframework.com/bots) просмотра, управления и переноса регистраций.</span><span class="sxs-lookup"><span data-stu-id="d854e-142">You can use the [legacy portal](https://dev.botframework.com/bots) to view, manage, and migrate your registrations.</span></span>

## <a name="create-your-app-manifest"></a><span data-ttu-id="d854e-143">Создание манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="d854e-143">Create your app manifest</span></span>

<span data-ttu-id="d854e-144">Вы можете использовать App Studio для создания манифеста приложения или создать его вручную.</span><span class="sxs-lookup"><span data-stu-id="d854e-144">You can either use App Studio to help you create your app manifest, or create it manually.</span></span>

### <a name="create-your-app-manifest-using-app-studio"></a><span data-ttu-id="d854e-145">Создание манифеста приложения с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="d854e-145">Create your app manifest using App Studio</span></span>

<span data-ttu-id="d854e-146">Приложение App Studio можно использовать в клиенте Microsoft Teams для создания манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="d854e-146">You can use the App Studio app from within the Microsoft Teams client to help create your app manifest.</span></span>

1. <span data-ttu-id="d854e-147">В клиенте Teams откройте App Studio из меню переполнения **...** на панели навигации слева.</span><span class="sxs-lookup"><span data-stu-id="d854e-147">In the Teams client, open App Studio from the **...** overflow menu on the left navigation rail.</span></span> <span data-ttu-id="d854e-148">Если он еще не установлен, это можно сделать, ища его.</span><span class="sxs-lookup"><span data-stu-id="d854e-148">If it isn't already installed, you can do so by searching for it.</span></span>
2. <span data-ttu-id="d854e-149">На **вкладке Редактор** Манифест выберите **Создание** нового приложения (или если вы добавляете расширение обмена сообщениями в существующее приложение, вы можете импортировать пакет приложения)</span><span class="sxs-lookup"><span data-stu-id="d854e-149">On the **Manifest editor** tab select **Create a new app** (or if you're adding a messaging extension to an existing app, you can import your app package)</span></span>
3. <span data-ttu-id="d854e-150">Добавьте сведения о приложении (см. [определение схемы манифеста](~/resources/schema/manifest-schema.md) с полным описанием каждого поля).</span><span class="sxs-lookup"><span data-stu-id="d854e-150">Add your app details (see [manifest schema definition](~/resources/schema/manifest-schema.md) for full descriptions of each field).</span></span>
4. <span data-ttu-id="d854e-151">На **вкладке Расширения обмена сообщениями нажмите** кнопку **Настройка.**</span><span class="sxs-lookup"><span data-stu-id="d854e-151">On the **Messaging extensions** tab click the **Setup** button.</span></span>
5. <span data-ttu-id="d854e-152">Вы можете создать новую веб-службу (бот) для расширения обмена сообщениями для использования, или если вы уже зарегистрировали один выбор или добавить его здесь.</span><span class="sxs-lookup"><span data-stu-id="d854e-152">You can either create a new web service (bot) for your messaging extension to use, or if you've already registered one select/add it here.</span></span>
6. <span data-ttu-id="d854e-153">При необходимости обновите адрес конечной точки бота, чтобы он указывал на вашего бота.</span><span class="sxs-lookup"><span data-stu-id="d854e-153">If necessary, update your bot endpoint address to point to your bot.</span></span> <span data-ttu-id="d854e-154">Он должен выглядеть примерно следующим образом: `https://someplace.com/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="d854e-154">It should look something like `https://someplace.com/api/messages`.</span></span>
7. <span data-ttu-id="d854e-155">Кнопка **Добавить** в разделе **Команда** поможет вам добавить команды в расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d854e-155">The **Add** button in the **Command** section will guide you through adding commands to your messaging extension.</span></span> <span data-ttu-id="d854e-156">Дополнительные [ссылки на](#learn-more) дополнительные сведения о добавлении команд см. в разделе Дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="d854e-156">See the [Learn more](#learn-more) section for links to more information on adding commands.</span></span> <span data-ttu-id="d854e-157">Помните, что для расширения обмена сообщениями можно определить до 10 команд.</span><span class="sxs-lookup"><span data-stu-id="d854e-157">Remember you can define up to 10 commands for your messaging extension.</span></span>
8. <span data-ttu-id="d854e-158">Раздел **Обработчики** сообщений позволяет добавить домен, на который будут запускаться ваши сообщения.</span><span class="sxs-lookup"><span data-stu-id="d854e-158">The **Message Handlers** section allows you to add a domain that your messaging will trigger on.</span></span> <span data-ttu-id="d854e-159">Дополнительные [сведения см. в ссылке unfurling.](~/messaging-extensions/how-to/link-unfurling.md)</span><span class="sxs-lookup"><span data-stu-id="d854e-159">See [link unfurling](~/messaging-extensions/how-to/link-unfurling.md) for more information.</span></span>

<span data-ttu-id="d854e-160">На **вкладке Готово =>** тест и  распространение можно скачать пакет приложения (который включает манифест  приложения, а также значки приложения) или установить пакет.</span><span class="sxs-lookup"><span data-stu-id="d854e-160">From the **Finish => Test and distribute** tab you can **Download** your app package (which includes your app manifest as well as your app icons), or **Install** the package.</span></span>

### <a name="create-your-app-manifest-manually"></a><span data-ttu-id="d854e-161">Создание манифеста приложения вручную</span><span class="sxs-lookup"><span data-stu-id="d854e-161">Create your app manifest manually</span></span>

<span data-ttu-id="d854e-162">Как и в ботах и [](~/resources/schema/manifest-schema.md#composeextensions) вкладок, вы обновляете манифест приложения для приложения, чтобы включить свойства расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d854e-162">As with bots and tabs, you update the [app manifest](~/resources/schema/manifest-schema.md#composeextensions) of your app to include the messaging extension properties.</span></span> <span data-ttu-id="d854e-163">Эти свойства регулируют, как отображается и ведет себя расширение обмена сообщениями в клиенте Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d854e-163">These properties govern how your messaging extension appears and behaves in the Microsoft Teams client.</span></span> <span data-ttu-id="d854e-164">Расширения обмена сообщениями поддерживаются начиная с v1.0 манифеста.</span><span class="sxs-lookup"><span data-stu-id="d854e-164">Messaging extensions are supported beginning with v1.0 of the manifest.</span></span>

#### <a name="declare-your-messaging-extension"></a><span data-ttu-id="d854e-165">Объявление расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="d854e-165">Declare your messaging extension</span></span>

<span data-ttu-id="d854e-166">Чтобы добавить расширение обмена сообщениями, включите новую структуру JSON верхнего уровня в манифест приложения с `composeExtensions` свойством.</span><span class="sxs-lookup"><span data-stu-id="d854e-166">To add a messaging extension, include a new top-level JSON structure in your app manifest with the `composeExtensions` property.</span></span> <span data-ttu-id="d854e-167">Для приложения создается одно расширение обмена сообщениями с до 10 командами.</span><span class="sxs-lookup"><span data-stu-id="d854e-167">You create a single messaging extension for your app, with up to 10 commands.</span></span>

> [!NOTE]
> <span data-ttu-id="d854e-168">Манифест относится к расширениям обмена сообщениями как `composeExtensions` .</span><span class="sxs-lookup"><span data-stu-id="d854e-168">The manifest refers to messaging extensions as `composeExtensions`.</span></span> <span data-ttu-id="d854e-169">Это необходимо для поддержания обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="d854e-169">This is to maintain backward compatibility.</span></span>

<span data-ttu-id="d854e-170">Определение расширения — это объект, который имеет следующую структуру:</span><span class="sxs-lookup"><span data-stu-id="d854e-170">The extension definition is an object that has the following structure:</span></span>

| <span data-ttu-id="d854e-171">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="d854e-171">Property name</span></span> | <span data-ttu-id="d854e-172">Назначение</span><span class="sxs-lookup"><span data-stu-id="d854e-172">Purpose</span></span> | <span data-ttu-id="d854e-173">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="d854e-173">Required?</span></span> |
|---|---|---|
| `botId` | <span data-ttu-id="d854e-174">Уникальный идентификатор приложения Майкрософт для бота, зарегистрированный в Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="d854e-174">The unique Microsoft app ID for the bot as registered with the Bot Framework.</span></span> <span data-ttu-id="d854e-175">Обычно это должно быть то же самое, что и для общего приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="d854e-175">This should typically be the same as the ID for your overall Teams app.</span></span> | <span data-ttu-id="d854e-176">Да</span><span class="sxs-lookup"><span data-stu-id="d854e-176">Yes</span></span> |
| `canUpdateConfiguration` | <span data-ttu-id="d854e-177">Включает элемент **меню "Параметры".**</span><span class="sxs-lookup"><span data-stu-id="d854e-177">Enables **Settings** menu item.</span></span> | <span data-ttu-id="d854e-178">Нет</span><span class="sxs-lookup"><span data-stu-id="d854e-178">No</span></span> |
| `commands` | <span data-ttu-id="d854e-179">Массив команд, поддерживаемых этим расширением обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d854e-179">Array of commands that this messaging extension supports.</span></span> <span data-ttu-id="d854e-180">Вы ограничены 10 командами.</span><span class="sxs-lookup"><span data-stu-id="d854e-180">You are limited to 10 commands.</span></span> | <span data-ttu-id="d854e-181">Да</span><span class="sxs-lookup"><span data-stu-id="d854e-181">Yes</span></span> |

#### <a name="define-your-commands"></a><span data-ttu-id="d854e-182">Определение команд</span><span class="sxs-lookup"><span data-stu-id="d854e-182">Define your commands</span></span>

<span data-ttu-id="d854e-183">Расширение обмена сообщениями должно объявлять одну или несколько команд, определяющих, где пользователи могут запускать расширение обмена сообщениями, и тип взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="d854e-183">Your messaging extension should declare one or more commands, which define where your users can trigger your messaging extension, and the type of interaction.</span></span> <span data-ttu-id="d854e-184">Дополнительные [сведения о](#learn-more) командах расширения обмена сообщениями см. в дополнительных сведениях.</span><span class="sxs-lookup"><span data-stu-id="d854e-184">See [learn more](#learn-more) for more information on messaging extension commands.</span></span>

#### <a name="simple-manifest-example"></a><span data-ttu-id="d854e-185">Пример простого манифеста</span><span class="sxs-lookup"><span data-stu-id="d854e-185">Simple manifest example</span></span>

<span data-ttu-id="d854e-186">Ниже приводится простой объект расширения обмена сообщениями в манифесте приложения с командой поиска.</span><span class="sxs-lookup"><span data-stu-id="d854e-186">The following example is a simple messaging extension object in the app manifest with a search command.</span></span> <span data-ttu-id="d854e-187">Это не весь файл манифеста приложения, а только часть, относящаяся к расширениям для обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="d854e-187">This is not the entire app manifest file, just the part specific to messaging extensions.</span></span> <span data-ttu-id="d854e-188">Полный [пример см. в](~/resources/schema/manifest-schema.md) схеме манифеста приложения.</span><span class="sxs-lookup"><span data-stu-id="d854e-188">See [app manifest schema](~/resources/schema/manifest-schema.md) for a complete example.</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "abcd1234-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "searchCmd",
        "description": "Search you ToDo's",
        "title": "Search",
        "initialRun": true,
        "parameters": [
          {
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }
        ]
      }
    ]
  }
]
...
```

#### <a name="complete-app-manifest-example"></a><span data-ttu-id="d854e-189">Полный пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="d854e-189">Complete app manifest example</span></span>

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

## <a name="add-your-invoke-message-handlers"></a><span data-ttu-id="d854e-190">Добавление обработчиков сообщений вызова</span><span class="sxs-lookup"><span data-stu-id="d854e-190">Add your invoke message handlers</span></span>

<span data-ttu-id="d854e-191">Когда пользователи запускают расширение обмена сообщениями, вам потребуется обрабатывать начальное сообщение вызова, собирать некоторые сведения от пользователя, а затем обрабатывать эти сведения и соответствующим образом реагировать.</span><span class="sxs-lookup"><span data-stu-id="d854e-191">When your users trigger your messaging extension you'll need to handle the initial invoke message, collect some information from the user, then process that information and respond appropriately.</span></span> <span data-ttu-id="d854e-192">Для этого сначала необходимо решить, какие команды необходимо добавить в расширение обмена сообщениями, [](~/messaging-extensions/how-to/action-commands/define-action-command.md) а также добавить команды действий или добавить команды [поиска.](~/messaging-extensions/how-to/search-commands/define-search-command.md)</span><span class="sxs-lookup"><span data-stu-id="d854e-192">To do that, you'll first need to decide what kind of commands you want to add to your messaging extension and either [add an action commands](~/messaging-extensions/how-to/action-commands/define-action-command.md) or [add a search commands](~/messaging-extensions/how-to/search-commands/define-search-command.md).</span></span>

## <a name="messaging-extensions-in-teams-meetings"></a><span data-ttu-id="d854e-193">Расширения обмена сообщениями в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="d854e-193">Messaging extensions in Teams meetings</span></span>

> [!NOTE]
> <span data-ttu-id="d854e-194">Если в реестре на собрании или групповом чате есть федераторы, Teams подавляет доступ к расширениям обмена сообщениями для всех пользователей, включая организатора.</span><span class="sxs-lookup"><span data-stu-id="d854e-194">If a meeting or group chat has federated users in the roster, Teams suppresses access to messaging extensions for all users, including the organizer.</span></span>

<span data-ttu-id="d854e-195">После начала собрания участники Teams могут напрямую взаимодействовать с расширением обмена сообщениями во время прямого вызова.</span><span class="sxs-lookup"><span data-stu-id="d854e-195">Once a meeting begins, Teams participants can interact directly with your messaging extension during a live call.</span></span> <span data-ttu-id="d854e-196">При создании расширения обмена сообщениями на собрании рассмотрим следующее:</span><span class="sxs-lookup"><span data-stu-id="d854e-196">Consider the following when building your in-meeting messaging extension:</span></span>

1. <span data-ttu-id="d854e-197">**Location**.</span><span class="sxs-lookup"><span data-stu-id="d854e-197">**Location**.</span></span> <span data-ttu-id="d854e-198">Расширение обмена сообщениями можно вызвать из области составить сообщение, командного окна или @mentioned в чате собрания.</span><span class="sxs-lookup"><span data-stu-id="d854e-198">Your messaging extension can be invoked from the compose message area, the command box, or @mentioned in the meeting chat.</span></span>

1. <span data-ttu-id="d854e-199">**Метаданные**.</span><span class="sxs-lookup"><span data-stu-id="d854e-199">**Metadata**.</span></span> <span data-ttu-id="d854e-200">При вызове расширения обмена сообщениями он может идентифицировать пользователя и клиента от `userId` и `tenantId` .</span><span class="sxs-lookup"><span data-stu-id="d854e-200">When your messaging extension is invoked it can identify the user and tenant from `userId` and `tenantId`.</span></span> <span data-ttu-id="d854e-201">`meetingId` может быть частью объекта `channelData`.</span><span class="sxs-lookup"><span data-stu-id="d854e-201">The `meetingId` can be found as part of the `channelData` object.</span></span> <span data-ttu-id="d854e-202">Приложение может использовать запрос API и для получения `userId` `meetingId`  ролей `GetParticipant` пользователя.</span><span class="sxs-lookup"><span data-stu-id="d854e-202">Your app can use the `userId` and `meetingId`  for the `GetParticipant` API request to retrieve user roles.</span></span>

1. <span data-ttu-id="d854e-203">**Тип команды**.</span><span class="sxs-lookup"><span data-stu-id="d854e-203">**Command type**.</span></span> <span data-ttu-id="d854e-204">Если в расширении сообщения [используются команды,](../messaging-extensions/what-are-messaging-extensions.md#action-commands)основанные на действиях, оно должно выполнять проверку подлинности вкладки с одним [входом.](../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="d854e-204">If your message extension uses [action-based commands](../messaging-extensions/what-are-messaging-extensions.md#action-commands), it should follow tabs [single sign-on](../tabs/how-to/authentication/auth-aad-sso.md) authentication.</span></span>

1. <span data-ttu-id="d854e-205">**Пользовательский опыт**.</span><span class="sxs-lookup"><span data-stu-id="d854e-205">**User experience**.</span></span> <span data-ttu-id="d854e-206">Расширение обмена сообщениями должно выглядеть и вести себя так же, как и вне собрания.</span><span class="sxs-lookup"><span data-stu-id="d854e-206">You messaging extension should look and behave the same as it would outside a meeting.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d854e-207">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d854e-207">Next steps</span></span>

* [<span data-ttu-id="d854e-208">Создание команд действий</span><span class="sxs-lookup"><span data-stu-id="d854e-208">Create action commands</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="d854e-209">Создание команд поиска</span><span class="sxs-lookup"><span data-stu-id="d854e-209">Create search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [<span data-ttu-id="d854e-210">Развертывание ссылки</span><span class="sxs-lookup"><span data-stu-id="d854e-210">Link unfurling</span></span>](~/messaging-extensions/how-to/link-unfurling.md)

## <a name="learn-more"></a><span data-ttu-id="d854e-211">Подробнее</span><span class="sxs-lookup"><span data-stu-id="d854e-211">Learn more</span></span>

<span data-ttu-id="d854e-212">Попробуйте его в quickstart:</span><span class="sxs-lookup"><span data-stu-id="d854e-212">Try it out in a quickstart:</span></span>

* <span data-ttu-id="d854e-213">Quickstarts для C #</span><span class="sxs-lookup"><span data-stu-id="d854e-213">Quickstarts for C#</span></span>
  * [<span data-ttu-id="d854e-214">Расширение обмена сообщениями с командами на основе действий</span><span class="sxs-lookup"><span data-stu-id="d854e-214">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="d854e-215">Расширение обмена сообщениями с командами на основе поиска</span><span class="sxs-lookup"><span data-stu-id="d854e-215">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="d854e-216">Quickstarts для JavaScript</span><span class="sxs-lookup"><span data-stu-id="d854e-216">Quickstarts for JavaScript</span></span>
  * [<span data-ttu-id="d854e-217">Расширение обмена сообщениями с командами на основе действий</span><span class="sxs-lookup"><span data-stu-id="d854e-217">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="d854e-218">Расширение обмена сообщениями с командами на основе поиска</span><span class="sxs-lookup"><span data-stu-id="d854e-218">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

<span data-ttu-id="d854e-219">Узнайте больше о концепциях разработки Teams:</span><span class="sxs-lookup"><span data-stu-id="d854e-219">Learn more about Teams development concepts:</span></span>

* [<span data-ttu-id="d854e-220">Понимание возможностей приложений Teams</span><span class="sxs-lookup"><span data-stu-id="d854e-220">Understand Teams app capabilities</span></span>](../concepts/capabilities-overview.md)
* [<span data-ttu-id="d854e-221">Что такое расширения для сообщений?</span><span class="sxs-lookup"><span data-stu-id="d854e-221">What are messaging extensions?</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
