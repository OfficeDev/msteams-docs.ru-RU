---
title: Начать работу - Создайте свой первый обзор приложения и предпосылки
author: girliemac
description: Узнайте, как начать работу с Microsoft Teams разработки приложений и настройки среды.
ms.author: timura
ms.date: 03/18/2021
ms.topic: quickstart
ms.openlocfilehash: dae942be9383ef1e0a931d238e6148651f334ef5
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565881"
---
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="6a466-103">Начать работу с Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="6a466-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="6a466-104">Создайте простое приложение, чтобы узнать основы Teams разработки приложений.</span><span class="sxs-lookup"><span data-stu-id="6a466-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="6a466-105">Как только вы видите "Здравствуйте, мир!", попробуйте любой из других начать статьи для получения дополнительной информации об общих инструментах, фундаментальных концепций и расширенных функций.</span><span class="sxs-lookup"><span data-stu-id="6a466-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="6a466-106">Чему вы научитесь</span><span class="sxs-lookup"><span data-stu-id="6a466-106">What you'll learn</span></span>

* <span data-ttu-id="6a466-107">Встать и работает быстро с Teams набор средств, Visual Studio Code расширение.</span><span class="sxs-lookup"><span data-stu-id="6a466-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="6a466-108">Настройте приложение с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="6a466-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="6a466-109">Ознакомиться с Teams и SDKs.</span><span class="sxs-lookup"><span data-stu-id="6a466-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="6a466-110">Рассмотрим важные Teams приложений, такие как аутентификация и разработка передового опыта.</span><span class="sxs-lookup"><span data-stu-id="6a466-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="6a466-111">Вы можете создать приложение Teams с помощью любой технологии по вашему выбору, например, командно-линейный интерфейс (CLI).</span><span class="sxs-lookup"><span data-stu-id="6a466-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="6a466-112">Но, эти статьи помогут вам начать работу со следующими рекомендуемых инструментов и технологий:</span><span class="sxs-lookup"><span data-stu-id="6a466-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="6a466-113">Teams набор средств, Visual Studio Code расширение</span><span class="sxs-lookup"><span data-stu-id="6a466-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="6a466-114">React.js для вкладок</span><span class="sxs-lookup"><span data-stu-id="6a466-114">React.js for tabs</span></span>
* <span data-ttu-id="6a466-115">Node.js для ботов и расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="6a466-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="6a466-116">Teams основы приложения</span><span class="sxs-lookup"><span data-stu-id="6a466-116">Teams app fundamentals</span></span>

<span data-ttu-id="6a466-117">Вы можете создавать пользовательские Teams приложения для себя, людей в вашей организации, или людей во всем мире.</span><span class="sxs-lookup"><span data-stu-id="6a466-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="6a466-118">Прежде чем приступить к работе, следует понять следующие фундаментальные понятия Teams разработке приложения:</span><span class="sxs-lookup"><span data-stu-id="6a466-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="6a466-119">Общие случаи использования приложений</span><span class="sxs-lookup"><span data-stu-id="6a466-119">Common app use cases</span></span>

<span data-ttu-id="6a466-120">Некоторые типичные сценарии, с Teams может помочь пользовательский пользователь:</span><span class="sxs-lookup"><span data-stu-id="6a466-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="6a466-121">Встраивание веб-контента, например веб-приложения или части веб-сайта, в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="6a466-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="6a466-122">Быстро посмотрите информацию в другой системе и добавив ее в Teams разговоре.</span><span class="sxs-lookup"><span data-stu-id="6a466-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="6a466-123">Триггер рабочих процессов и процессов непосредственно из того, что сказано в разговоре.</span><span class="sxs-lookup"><span data-stu-id="6a466-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="6a466-124">Возможности и инструменты приложения</span><span class="sxs-lookup"><span data-stu-id="6a466-124">App capabilities and tools</span></span>

<span data-ttu-id="6a466-125">Приложение состоит из одной или Teams и точек взаимодействия пользователей.</span><span class="sxs-lookup"><span data-stu-id="6a466-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="6a466-126">Ваш инструментарий разработки будет варьироваться в зависимости от возможностей, которые вы хотите.</span><span class="sxs-lookup"><span data-stu-id="6a466-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="6a466-127">**Возможности приложения**</span><span class="sxs-lookup"><span data-stu-id="6a466-127">**App capabilities**</span></span>| <span data-ttu-id="6a466-128">**Точки взаимодействия**</span><span class="sxs-lookup"><span data-stu-id="6a466-128">**Interaction points**</span></span> | <span data-ttu-id="6a466-129">**Рекомендуемые инструменты**</span><span class="sxs-lookup"><span data-stu-id="6a466-129">**Recommended tools**</span></span> | <span data-ttu-id="6a466-130">**Пакеты SDK**</span><span class="sxs-lookup"><span data-stu-id="6a466-130">**SDKs**</span></span> | <span data-ttu-id="6a466-131">**Технологические стеки**</span><span class="sxs-lookup"><span data-stu-id="6a466-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="6a466-132">Вкладки</span><span class="sxs-lookup"><span data-stu-id="6a466-132">Tabs</span></span> | <span data-ttu-id="6a466-133">Пространства, где пользователи могут взаимодействовать со встроенным веб-контентом в личных и общих контекстах.</span><span class="sxs-lookup"><span data-stu-id="6a466-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="6a466-134">VS Code с Teams набор средств расширением или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="6a466-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="6a466-135">Клиентский SDK JavaScript для Teams</span><span class="sxs-lookup"><span data-stu-id="6a466-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="6a466-136">Общие веб-технологии (HTML, CSS и JavaScript) или React.js</span><span class="sxs-lookup"><span data-stu-id="6a466-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="6a466-137">Боты</span><span class="sxs-lookup"><span data-stu-id="6a466-137">Bots</span></span> | <span data-ttu-id="6a466-138">Чат-боты, которые взаимодействуют с пользователями в личном и общем контексте.</span><span class="sxs-lookup"><span data-stu-id="6a466-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="6a466-139">VS Code с Teams набор средств расширением или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="6a466-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="6a466-140">Бот Рамочная SDK</span><span class="sxs-lookup"><span data-stu-id="6a466-140">Bot Framework SDK</span></span> | <span data-ttu-id="6a466-141">Node.js, СЗ или Пайтон</span><span class="sxs-lookup"><span data-stu-id="6a466-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="6a466-142">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="6a466-142">Messaging extensions</span></span> | <span data-ttu-id="6a466-143">Ярлыки для вставки содержимого приложения или действия на сообщении без навигации от разговора.</span><span class="sxs-lookup"><span data-stu-id="6a466-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="6a466-144">VS Code с Teams набор средств расширением или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="6a466-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="6a466-145">Бот Рамочная SDK</span><span class="sxs-lookup"><span data-stu-id="6a466-145">Bot Framework SDK</span></span> | <span data-ttu-id="6a466-146">Node.js, СЗ или Пайтон</span><span class="sxs-lookup"><span data-stu-id="6a466-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="6a466-147">Teams не хост вашего приложения</span><span class="sxs-lookup"><span data-stu-id="6a466-147">Teams doesn't host your app</span></span>

<span data-ttu-id="6a466-148">Когда пользователь устанавливает ваше приложение в Teams, он устанавливает только пакет приложений, содержащий файл конфигурации (также известный как манифест приложения) и значки вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="6a466-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="6a466-149">Логика и хранение данных приложения размещаются в других местах, таких как Веб-службы Azure или локальный хостинг во время разработки.</span><span class="sxs-lookup"><span data-stu-id="6a466-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="6a466-150">Teams доступ к этим ресурсам через HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6a466-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Иллюстрация, показывающая ваше приложение Teams, указывает на логику приложения на облачном сервере.":::

## <a name="next-step"></a><span data-ttu-id="6a466-152">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="6a466-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a466-153">Создание и запуск первого Teams приложения</span><span class="sxs-lookup"><span data-stu-id="6a466-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
