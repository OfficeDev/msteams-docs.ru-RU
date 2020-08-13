---
title: Создание первого приложения Teams
author: heath-hamilton
description: Руководство по созданию реального приложения Microsoft Teams
ms.openlocfilehash: 4915dde4ef5a852f4fc5d1e4c83e3349db2eaf6b
ms.sourcegitcommit: 80bf79a952bb14cbc38c0bd1e3cf8a346158e28e
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/13/2020
ms.locfileid: "46655676"
---
# <a name="learn-how-to-build-your-first-teams-app"></a><span data-ttu-id="f79ce-103">Узнайте, как создать первое приложение Teams</span><span class="sxs-lookup"><span data-stu-id="f79ce-103">Learn how to build your first Teams app</span></span>

<span data-ttu-id="f79ce-104">В статье **Создание первого приложения**вы узнаете, как создать базовое приложение Teams с помощью учебников.</span><span class="sxs-lookup"><span data-stu-id="f79ce-104">In **Build your first app**, you learn how to create a basic Teams app through tutorials.</span></span> <span data-ttu-id="f79ce-105">В занятиях строится друг от друга, пошаговые инструкции по созданию простого приложения Teams в среде.</span><span class="sxs-lookup"><span data-stu-id="f79ce-105">The lessons build on each other, walking you through each step of creating a simple, real-world Teams app.</span></span> <span data-ttu-id="f79ce-106">Мы представим общие инструменты, основные понятия и полезную ссылку.</span><span class="sxs-lookup"><span data-stu-id="f79ce-106">We introduce you to common tools, fundamental concepts, and useful links along the way.</span></span>

<span data-ttu-id="f79ce-107">Начнем с создания и запуска "Hello, World!".</span><span class="sxs-lookup"><span data-stu-id="f79ce-107">You'll start with creating and running a "Hello, World!"</span></span> <span data-ttu-id="f79ce-108">Вкладка "приложение".</span><span class="sxs-lookup"><span data-stu-id="f79ce-108">tab app.</span></span> <span data-ttu-id="f79ce-109">Затем вы создадите простой пользовательский интерфейс и узнаете, как получить нужный контекст с помощью пакета SDK для Microsoft Teams JavaScript.</span><span class="sxs-lookup"><span data-stu-id="f79ce-109">You'll then create some simple UI and learn how to get useful context with the Microsoft Teams Javascript SDK.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="f79ce-110">Что вы узнаете</span><span class="sxs-lookup"><span data-stu-id="f79ce-110">What you'll learn</span></span>

> [!div class="checklist"]
  >
  > - <span data-ttu-id="f79ce-111">**Быстрый запуск и работа с набором инструментов Teams**: набор инструментов Microsoft Teams для Visual Studio Code создает проект приложения и формирование шаблонов, чтобы приложение могло работать в минутах.</span><span class="sxs-lookup"><span data-stu-id="f79ce-111">**Get up and running quickly with the Teams Toolkit**: The Microsoft Teams Toolkit for Visual Studio Code takes care of creating your app project and scaffolding so you can have a running app in minutes.</span></span>
  > - <span data-ttu-id="f79ce-112">**Определите приложение с манифестом**: манифест представляет собой план, в котором указываются возможности и службы, которые использует приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="f79ce-112">**Define your app with the manifest**: The manifest is a blueprint where you specify the capabilities and services your Teams app uses.</span></span>
  > - <span data-ttu-id="f79ce-113">**Область действия аудитории**: вы можете создать приложение Teams для личного использования или совместной работы.</span><span class="sxs-lookup"><span data-stu-id="f79ce-113">**Scope your audience**: You can build a Teams app for personal use or collaboration.</span></span> <span data-ttu-id="f79ce-114">В учебниках вы узнаете, как создать вкладку для отдельных пользователей или группу людей в канале или чате.</span><span class="sxs-lookup"><span data-stu-id="f79ce-114">In the tutorials, you'll learn how build a tab for individual users or a group of people in a channel or chat.</span></span>
  > - <span data-ttu-id="f79ce-115">**Использование SDK Teams для получения контекста**: Узнайте, как использовать пакет SDK Microsoft Teams SDK для изменения темы или настройки интерфейса настройки</span><span class="sxs-lookup"><span data-stu-id="f79ce-115">**Utilize Teams SDK to get context**: Learn how to use the Microsoft Teams JavaScript SDK to perform theme change or set up configuration experience</span></span>  
  > - <span data-ttu-id="f79ce-116">**Разверните приложение на своем приложении**: в учебниках мы будем ссылаться на связанные темы (некоторые из них включают рекомендации по проверке подлинности и проектированию).</span><span class="sxs-lookup"><span data-stu-id="f79ce-116">**Expand on your app**: Throughout the tutorials, we link to related topics you're probably interested in (some of which include authentication and design guidelines).</span></span>

## <a name="teams-app-fundamentals"></a><span data-ttu-id="f79ce-117">Основные сведения о приложениях Teams</span><span class="sxs-lookup"><span data-stu-id="f79ce-117">Teams app fundamentals</span></span>

<span data-ttu-id="f79ce-118">Прежде чем приступать к работе с руководствами, необходимо знать следующее о создании приложений для Teams.</span><span class="sxs-lookup"><span data-stu-id="f79ce-118">Before you begin the tutorials, you should know the following about building apps for Teams.</span></span>

### <a name="apps-can-have-multiple-capabilities"></a><span data-ttu-id="f79ce-119">Приложения могут иметь несколько возможностей</span><span class="sxs-lookup"><span data-stu-id="f79ce-119">Apps can have multiple capabilities</span></span>

<span data-ttu-id="f79ce-120">Приложения Teams состоят из одной или нескольких [функций платформы](../capabilities-overview.md), в том [числе вкладок](../doc-links/what-are-tabs.md), [Боты](../doc-links/what-are-bots.md ), [расширений обмена сообщениями](../doc-links/what-are-messaging-extensions.md), а также [веб-перехватчиков и соединителей](../doc-links/what-are-webhooks-and-connectors.md).</span><span class="sxs-lookup"><span data-stu-id="f79ce-120">Teams apps are made up of one or more [platform capabilities](../capabilities-overview.md), including [tabs](../doc-links/what-are-tabs.md), [bots](../doc-links/what-are-bots.md ), [messaging extensions](../doc-links/what-are-messaging-extensions.md), and [webhooks and connectors](../doc-links/what-are-webhooks-and-connectors.md).</span></span> <span data-ttu-id="f79ce-121">Приложения Teams также содержат много [соглашений и элементов пользовательского интерфейса](../doc-links/teams-ui-conventions.md), таких как карточки, модули задач и глубокая компоновка, которые можно использовать для создания наилучшего взаимодействия с пользователем.</span><span class="sxs-lookup"><span data-stu-id="f79ce-121">Teams apps also have many [UI conventions and elements](../doc-links/teams-ui-conventions.md), such as cards, task modules, and deep linking, you can use to build the best possible user experience.</span></span>

<span data-ttu-id="f79ce-122">В этом учебном пособии вы создадите только вкладки, но можете добавить в свое приложение Bot или другую возможность.</span><span class="sxs-lookup"><span data-stu-id="f79ce-122">For these tutorials, you'll build only tabs but can add a bot or other capability to your app as you like.</span></span>

### <a name="teams-doesnt-host-your-app"></a><span data-ttu-id="f79ce-123">В Teams не размещается ваше приложение</span><span class="sxs-lookup"><span data-stu-id="f79ce-123">Teams doesn't host your app</span></span>  

<span data-ttu-id="f79ce-124">Приложение Teams состоит из трех основных частей:</span><span class="sxs-lookup"><span data-stu-id="f79ce-124">A Teams app consists of three major pieces:</span></span>

1. <span data-ttu-id="f79ce-125">Клиент Microsoft Teams (на веб-сайте, на настольном компьютере или мобильном устройстве), в котором пользователи взаимодействуют с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="f79ce-125">The Microsoft Teams client (web, desktop, or mobile) where users interact with your app.</span></span>
1. <span data-ttu-id="f79ce-126">Ваше приложение, служба, Рабочий процесс или веб-сайт, которые выполняют необходимую логику, хранение данных и вызовы API для управления приложением.</span><span class="sxs-lookup"><span data-stu-id="f79ce-126">Your app, service, workflow, or website that performs the necessary logic, data storage, and API calls to power your app.</span></span>
1. <span data-ttu-id="f79ce-127">Ваш пакет приложения, который вы используете для установки приложения в Teams.</span><span class="sxs-lookup"><span data-stu-id="f79ce-127">Your app package, which you use to install the app in Teams.</span></span> <span data-ttu-id="f79ce-128">Он содержит метаданные приложения (имя, значки и т. д.) и указатели на службы.</span><span class="sxs-lookup"><span data-stu-id="f79ce-128">It contains app metadata (name, icons, etc.) and pointers to your services.</span></span>

## <a name="next-step"></a><span data-ttu-id="f79ce-129">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="f79ce-129">Next step</span></span>

<span data-ttu-id="f79ce-130">Теперь все готово к работе!</span><span class="sxs-lookup"><span data-stu-id="f79ce-130">That's all for now, let's get started!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f79ce-131">Создание и запуск первого приложения</span><span class="sxs-lookup"><span data-stu-id="f79ce-131">Build and run your first app</span></span>](build-and-run-with-toolkit.md)
