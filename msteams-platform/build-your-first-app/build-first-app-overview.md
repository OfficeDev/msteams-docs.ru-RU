---
title: Начало работы — создание первого обзора приложения и необходимых условий
author: girliemac
description: Узнайте, как начать работу с Microsoft Teams разработки приложений и настроить среду.
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
# <a name="get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="8907d-103">Начало работы с разработкой Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="8907d-103">Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="8907d-104">Создайте простое приложение, чтобы узнать основы разработки Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="8907d-104">Build a simple app to learn the basics of Teams app development.</span></span> <span data-ttu-id="8907d-105">После того как вы увидите "Hello, World!", попробуйте другие статьи для начала работы, чтобы получить дополнительные сведения об общих средствах, фундаментальных концепциях и расширенных функций.</span><span class="sxs-lookup"><span data-stu-id="8907d-105">Once you see "Hello, World!", try any of the other get started articles for more information on common tools, fundamental concepts, and advanced features.</span></span>



## <a name="what-youll-learn"></a><span data-ttu-id="8907d-106">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="8907d-106">What you'll learn</span></span>

* <span data-ttu-id="8907d-107">Встать и быстро работать с помощью Teams набор средств, Visual Studio Code расширения.</span><span class="sxs-lookup"><span data-stu-id="8907d-107">Get up and running quickly with the Teams Toolkit, a Visual Studio Code extension.</span></span> 
* <span data-ttu-id="8907d-108">Настройка приложения с помощью App Studio.</span><span class="sxs-lookup"><span data-stu-id="8907d-108">Configure your app with App Studio.</span></span>
* <span data-ttu-id="8907d-109">Ознакомьтесь с Teams разработчиками и SDKs.</span><span class="sxs-lookup"><span data-stu-id="8907d-109">Get familiar with Teams developer tools and SDKs.</span></span>
* <span data-ttu-id="8907d-110">Рассмотрим важные Teams приложения, такие как проверка подлинности и разработка.</span><span class="sxs-lookup"><span data-stu-id="8907d-110">Consider important Teams app concepts, such as authentication and design best practices.</span></span>

<span data-ttu-id="8907d-111">Вы можете создать приложение Teams с помощью любой технологии по вашему выбору, например интерфейс командной строки (CLI).</span><span class="sxs-lookup"><span data-stu-id="8907d-111">You can build a Teams app using any technology of your choice, for example, command-line interface (CLI).</span></span> <span data-ttu-id="8907d-112">Но эти статьи помогают начать работу со следующими рекомендуемыми средствами и технологиями:</span><span class="sxs-lookup"><span data-stu-id="8907d-112">But, these articles help you get started with the following recommended tools and technologies:</span></span>

* <span data-ttu-id="8907d-113">Teams набор средств, расширение Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="8907d-113">Teams Toolkit, a Visual Studio Code extension</span></span>
* <span data-ttu-id="8907d-114">React.js для вкладок</span><span class="sxs-lookup"><span data-stu-id="8907d-114">React.js for tabs</span></span>
* <span data-ttu-id="8907d-115">Node.js для ботов и расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8907d-115">Node.js for bots and messaging extensions</span></span>


## <a name="teams-app-fundamentals"></a><span data-ttu-id="8907d-116">Teams приложений</span><span class="sxs-lookup"><span data-stu-id="8907d-116">Teams app fundamentals</span></span>

<span data-ttu-id="8907d-117">Вы можете создавать настраиваемые Teams приложения для себя, людей в вашей организации или людей по всему миру.</span><span class="sxs-lookup"><span data-stu-id="8907d-117">You can build custom Teams apps for yourself, people in your org, or people all over the world.</span></span> <span data-ttu-id="8907d-118">Перед началом работы необходимо понять следующие основные понятия о разработке Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="8907d-118">Before you begin, you should understand the following fundamental concepts about Teams app development:</span></span>

### <a name="common-app-use-cases"></a><span data-ttu-id="8907d-119">Распространенные случаи использования приложения</span><span class="sxs-lookup"><span data-stu-id="8907d-119">Common app use cases</span></span>

<span data-ttu-id="8907d-120">Некоторые типичные сценарии, с Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="8907d-120">Some typical scenarios that a custom Teams app can help with are:</span></span>

* <span data-ttu-id="8907d-121">Встраить веб-контент, например веб-приложение или часть веб-сайта, в Teams клиента.</span><span class="sxs-lookup"><span data-stu-id="8907d-121">Embed web-based content, such as a web app or part of a website, in the Teams client.</span></span>
* <span data-ttu-id="8907d-122">Быстро посмотрите информацию в другой системе и добавьте ее в Teams беседу.</span><span class="sxs-lookup"><span data-stu-id="8907d-122">Look up information quickly in another system and adding it to a Teams conversation.</span></span>
* <span data-ttu-id="8907d-123">Запуск рабочего процесса и процессов непосредственно из того, что говорится в беседе.</span><span class="sxs-lookup"><span data-stu-id="8907d-123">Trigger workflows and processes directly from what's said in a conversation.</span></span>

### <a name="app-capabilities-and-tools"></a><span data-ttu-id="8907d-124">Возможности и средства приложения</span><span class="sxs-lookup"><span data-stu-id="8907d-124">App capabilities and tools</span></span>

<span data-ttu-id="8907d-125">Приложение состоит из одного или более Teams возможностей и точек взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="8907d-125">An app is made up of one or more Teams capabilities and user interaction points.</span></span> <span data-ttu-id="8907d-126">Ваш инструментарий разработки будет отличаться в зависимости от необходимых возможностей.</span><span class="sxs-lookup"><span data-stu-id="8907d-126">Your development toolset will vary depending on the capabilities you want.</span></span>

| <span data-ttu-id="8907d-127">**Возможности приложения**</span><span class="sxs-lookup"><span data-stu-id="8907d-127">**App capabilities**</span></span>| <span data-ttu-id="8907d-128">**Точки взаимодействия**</span><span class="sxs-lookup"><span data-stu-id="8907d-128">**Interaction points**</span></span> | <span data-ttu-id="8907d-129">**Рекомендуемые средства**</span><span class="sxs-lookup"><span data-stu-id="8907d-129">**Recommended tools**</span></span> | <span data-ttu-id="8907d-130">**Пакеты SDK**</span><span class="sxs-lookup"><span data-stu-id="8907d-130">**SDKs**</span></span> | <span data-ttu-id="8907d-131">**Стеки технологий**</span><span class="sxs-lookup"><span data-stu-id="8907d-131">**Technology stacks**</span></span> |
|--------|--------|--------|--------|--------|
| <span data-ttu-id="8907d-132">Вкладки</span><span class="sxs-lookup"><span data-stu-id="8907d-132">Tabs</span></span> | <span data-ttu-id="8907d-133">Пространства, в которых пользователи могут взаимодействовать со встроенным веб-контентом в личных и общих контекстах.</span><span class="sxs-lookup"><span data-stu-id="8907d-133">Spaces where users can interact with embedded web content in personal and shared contexts.</span></span> | <span data-ttu-id="8907d-134">VS Code с расширением Teams набор средств или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="8907d-134">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="8907d-135">Клиентский SDK JavaScript для Teams</span><span class="sxs-lookup"><span data-stu-id="8907d-135">Teams JavaScript client SDK</span></span> | <span data-ttu-id="8907d-136">Общие веб-технологии (HTML, CSS и JavaScript) или React.js</span><span class="sxs-lookup"><span data-stu-id="8907d-136">General web technologies (HTML, CSS, and JavaScript) or React.js</span></span> |
| <span data-ttu-id="8907d-137">Боты</span><span class="sxs-lookup"><span data-stu-id="8907d-137">Bots</span></span> | <span data-ttu-id="8907d-138">Чат-боты, взаимодействующие с пользователями в личных и общих контекстах.</span><span class="sxs-lookup"><span data-stu-id="8907d-138">Chatbots that interact with users in personal and shared contexts.</span></span> | <span data-ttu-id="8907d-139">VS Code с расширением Teams набор средств или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="8907d-139">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="8907d-140">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="8907d-140">Bot Framework SDK</span></span> | <span data-ttu-id="8907d-141">Node.js, C# или Python</span><span class="sxs-lookup"><span data-stu-id="8907d-141">Node.js, C#, or Python</span></span> | 
| <span data-ttu-id="8907d-142">Расширения для система обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="8907d-142">Messaging extensions</span></span> | <span data-ttu-id="8907d-143">Ярлыки для вставки контента приложения или действия в сообщении, не переходя от беседы.</span><span class="sxs-lookup"><span data-stu-id="8907d-143">Shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span> | <span data-ttu-id="8907d-144">VS Code с расширением Teams набор средств или генератором Yeoman</span><span class="sxs-lookup"><span data-stu-id="8907d-144">VS Code with Teams Toolkit extension or Yeoman Generator</span></span> | <span data-ttu-id="8907d-145">Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="8907d-145">Bot Framework SDK</span></span> | <span data-ttu-id="8907d-146">Node.js, C# или Python</span><span class="sxs-lookup"><span data-stu-id="8907d-146">Node.js, C#, or Python</span></span> |

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="8907d-147">Teams не является хост-приложением</span><span class="sxs-lookup"><span data-stu-id="8907d-147">Teams doesn't host your app</span></span>

<span data-ttu-id="8907d-148">Когда пользователь устанавливает приложение в Teams, он устанавливает только пакет приложений, содержащий файл конфигурации (также известный как манифест приложения) и значки приложения.</span><span class="sxs-lookup"><span data-stu-id="8907d-148">When a user installs your app in Teams, they only install an app package that contains a configuration file (also known as an app manifest) and your app’s icons.</span></span> <span data-ttu-id="8907d-149">Логика и хранение данных вашего приложения находятся в другом месте, например в Azure Web Services или localhost во время разработки.</span><span class="sxs-lookup"><span data-stu-id="8907d-149">Your app’s logic and data storage are hosted elsewhere, such as Azure Web Services or localhost during development.</span></span> <span data-ttu-id="8907d-150">Teams доступ к этим ресурсам с помощью HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8907d-150">Teams accesses these resources via HTTPS.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-in-cloud.png" alt-text="Иллюстрация, показывающая ваше Teams, показывает логику приложения на облачном сервере.":::

## <a name="next-step"></a><span data-ttu-id="8907d-152">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="8907d-152">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8907d-153">Создание и запуск первого Teams приложения</span><span class="sxs-lookup"><span data-stu-id="8907d-153">Build and run your first Teams app</span></span>](../build-your-first-app/build-and-run.md)
