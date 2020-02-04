---
title: Сопоставление вариантов использования с возможностями приложений
author: clearab
description: Выбор способа распространения приложения
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5ebfa73df9b4f2c83533a33fbc6366c2c0ccffb4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675494"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="2eccc-103">Сопоставление вариантов использования с возможностями приложений Teams</span><span class="sxs-lookup"><span data-stu-id="2eccc-103">Map your use cases to teams app capabilities</span></span>

<span data-ttu-id="2eccc-104">Если вы еще не сделали это, убедитесь, что вы тщательно [рассматривали свои варианты использования](~/concepts/design/map-use-cases.md) .</span><span class="sxs-lookup"><span data-stu-id="2eccc-104">If you haven't already, make sure you've [considered your use cases](~/concepts/design/map-use-cases.md) carefully.</span></span> <span data-ttu-id="2eccc-105">Кроме того, следует хорошо понимать [точки расширения и элементы пользовательского интерфейса](~/concepts/extensibility-points.md) , доступные для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="2eccc-105">You should also have a good understanding of the [extensibility points and UI elements](~/concepts/extensibility-points.md) available for your app.</span></span> <span data-ttu-id="2eccc-106">После определения *того, что* вы пытались решить, и *кого* вы его задаете, научитесь думать о *том, как*.</span><span class="sxs-lookup"><span data-stu-id="2eccc-106">Once you've figured out *what* your trying to solve, and *who* you're solving it for, it is time to start thinking about *how*.</span></span>

<span data-ttu-id="2eccc-107">Ниже приведены некоторые распространенные сценарии, а также выделены точки расширения и элементы пользовательского интерфейса, которые с ними работают.</span><span class="sxs-lookup"><span data-stu-id="2eccc-107">Below you'll find some common scenarios, and a selection of extensibility points and UI elements that work well with them.</span></span> <span data-ttu-id="2eccc-108">Он не предназначен для использования в качестве исчерпывающего списка, который поможет вам решить некоторые возможности, доступные вам и платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="2eccc-108">It isn't intended to be an exhaustive list, just to help you think through some of the possibilities available to you and the Teams platform.</span></span>

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a><span data-ttu-id="2eccc-109">Создание, совместное использование и совместная работа над элементами во внешней системе</span><span class="sxs-lookup"><span data-stu-id="2eccc-109">Create, share and collaborate on items in an external system</span></span>

<span data-ttu-id="2eccc-110">Приложение для Microsoft Teams — это отличный способ взаимодействия с данными, и существует множество точек интеграции, которые можно выбрать.</span><span class="sxs-lookup"><span data-stu-id="2eccc-110">App for Microsoft Teams are a great way to interact with your data, and there are a variety of integration points to choose from.</span></span>

* <span data-ttu-id="2eccc-111">Расширения обмена сообщениями с помощью команд поиска — поиск во внешних системах и общий доступ к результатам в виде интерактивной карточки.</span><span class="sxs-lookup"><span data-stu-id="2eccc-111">Messaging extensions with search commands - Search external systems and share the results as an interactive card.</span></span>

* <span data-ttu-id="2eccc-112">Расширения обмена сообщениями с командами действий — сбор сведений для вставки в хранилище данных или выполнения расширенного поиска.</span><span class="sxs-lookup"><span data-stu-id="2eccc-112">Messaging extensions with action commands - Collect information to insert into a data store or perform advanced searches.</span></span>

* <span data-ttu-id="2eccc-113">Вкладки — Создание встроенных веб-интерфейсов для просмотра, работы с данными и предоставления общего доступа к ним.</span><span class="sxs-lookup"><span data-stu-id="2eccc-113">Tabs - Create embedded web experiences to view, work with, and share data.</span></span>

* <span data-ttu-id="2eccc-114">Соединители и веб-перехватчики — простой способ отправки данных и отправки данных из клиента Teams.</span><span class="sxs-lookup"><span data-stu-id="2eccc-114">Connectors and webhooks - A simple way to push data into, and send data out of the Teams client.</span></span>

* <span data-ttu-id="2eccc-115">Модули задач — Интерактивные модальные формы из того места, где они должны собирать или отображать сведения.</span><span class="sxs-lookup"><span data-stu-id="2eccc-115">Task modules - Interactive modal forms from wherever you need them to collect or display information.</span></span>

## <a name="initiate-workflows-and-processes"></a><span data-ttu-id="2eccc-116">Запуск рабочих процессов и процессов</span><span class="sxs-lookup"><span data-stu-id="2eccc-116">Initiate workflows and processes</span></span>

<span data-ttu-id="2eccc-117">Иногда необходим быстрый способ запуска процесса или рабочего процесса во внешней системе.</span><span class="sxs-lookup"><span data-stu-id="2eccc-117">Sometimes you just need a quick way to start a process or workflow in an external system.</span></span>

* <span data-ttu-id="2eccc-118">Команды действий расширений обмена сообщениями — триггер из сообщений, позволяющий пользователям быстро отправлять содержимое сообщения в веб-службы.</span><span class="sxs-lookup"><span data-stu-id="2eccc-118">Messaging extensions action commands - Trigger from messages, allowing your users to quickly send the contents of a message to your web services.</span></span>

* <span data-ttu-id="2eccc-119">Модули задач — откройте их из вкладки, ленты или расширения обмена сообщениями, чтобы собрать сведения перед запуском рабочего процесса.</span><span class="sxs-lookup"><span data-stu-id="2eccc-119">Task modules - Open them from a tab, a bot, or a messaging extension to collect information before initiating a workflow.</span></span>

* <span data-ttu-id="2eccc-120">Беседа Боты — взаимодействие с пользователями с помощью текста и расширенных карточек.</span><span class="sxs-lookup"><span data-stu-id="2eccc-120">Conversational bots - Interact with your users through text and rich cards.</span></span>

* <span data-ttu-id="2eccc-121">Исходящие веб-перехватчики — хороший выбор для простого взаимодействия между двумя и другими разработчиками, когда вам не нужно создавать весь объект-робот.</span><span class="sxs-lookup"><span data-stu-id="2eccc-121">Outgoing webhooks - A good choice for a simple back-and-forth interaction when you don't need to build an entire conversational bot.</span></span>

## <a name="send-notifications-and-alerts"></a><span data-ttu-id="2eccc-122">Отправка уведомлений и оповещений</span><span class="sxs-lookup"><span data-stu-id="2eccc-122">Send notifications and alerts</span></span>

<span data-ttu-id="2eccc-123">Отправка асинхронных уведомлений и оповещений пользователям в Teams.</span><span class="sxs-lookup"><span data-stu-id="2eccc-123">Send asynchronous notifications and alerts to your users in Teams.</span></span> <span data-ttu-id="2eccc-124">Используйте интерактивные карточки для предоставления быстрого доступа к часто используемым действиям и ссылки на дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="2eccc-124">Use interactive cards to provide quick access to commonly used actions and links to additional information.</span></span>

* <span data-ttu-id="2eccc-125">Беседа Боты — отправка активных сообщений группам, каналам или отдельным пользователям.</span><span class="sxs-lookup"><span data-stu-id="2eccc-125">Conversational bots - Send proactive messages to groups, channels, or individual users.</span></span>

* <span data-ttu-id="2eccc-126">Соединители & входящих веб-Перехватчики позволяют каналу подписываться на получение сообщений.</span><span class="sxs-lookup"><span data-stu-id="2eccc-126">Connectors & incoming webhooks - Allow a channel to subscribe to receive messages.</span></span> <span data-ttu-id="2eccc-127">С помощью соединителя пользователи имеют возможность настроить подписку с помощью страницы конфигурации.</span><span class="sxs-lookup"><span data-stu-id="2eccc-127">With a connector let users tailor the subscription with a configuration page.</span></span>

## <a name="ask-questions-and-get-answers"></a><span data-ttu-id="2eccc-128">Задавайте вопросы и получайте ответы на них.</span><span class="sxs-lookup"><span data-stu-id="2eccc-128">Ask questions and get answers</span></span>

<span data-ttu-id="2eccc-129">У пользователей есть вопросы.</span><span class="sxs-lookup"><span data-stu-id="2eccc-129">People have questions.</span></span> <span data-ttu-id="2eccc-130">Вы, вероятно, получили множество ответов, хранящихся в другом месте.</span><span class="sxs-lookup"><span data-stu-id="2eccc-130">You've probably got a lot of the answers stored away somewhere.</span></span> <span data-ttu-id="2eccc-131">К сожалению, его часто очень трудно соединить друг с другом.</span><span class="sxs-lookup"><span data-stu-id="2eccc-131">Unfortunately, its often quite difficult to connect the two together.</span></span>

* <span data-ttu-id="2eccc-132">Боты — обработка на естественном языке, AI, машинное обучение, все буззвордс.</span><span class="sxs-lookup"><span data-stu-id="2eccc-132">Conversational bots - Natural language processing, AI, machine learning, all the buzzwords.</span></span> <span data-ttu-id="2eccc-133">Используйте устройство для подключения к серверу, созданное интеллектуальным облаком, для подключения пользователей к необходимым им ответам.</span><span class="sxs-lookup"><span data-stu-id="2eccc-133">Use a bot powered by the intelligent cloud to connect your users to the answers they need.</span></span>

* <span data-ttu-id="2eccc-134">С помощью вкладок внедрите существующий веб-портал в Teams или создайте версию, относящуюся к определенной группе, для дополнительных функций.</span><span class="sxs-lookup"><span data-stu-id="2eccc-134">Tabs - Embed your existing web portal in Teams, or create a Teams-specific version for added functionality.</span></span>

## <a name="get-social"></a><span data-ttu-id="2eccc-135">Получение социальных сетей</span><span class="sxs-lookup"><span data-stu-id="2eccc-135">Get social</span></span>

<span data-ttu-id="2eccc-136">Платформа для совместной работы — это, по сути, платформа социальных сетей.</span><span class="sxs-lookup"><span data-stu-id="2eccc-136">A collaboration platform is inherently a social platform.</span></span> <span data-ttu-id="2eccc-137">Позвольте вашей творческой стороне быть бесплатной и добавим к рабочему месту некоторое удовольствие.</span><span class="sxs-lookup"><span data-stu-id="2eccc-137">Let your creative side be free, and add some fun into your workplace.</span></span>

* <span data-ttu-id="2eccc-138">Все они отправляют шутки, предоставляют благодарностью, получают некоторые мемес, отменяют некоторые эмодзи или что угодно.</span><span class="sxs-lookup"><span data-stu-id="2eccc-138">All of them - Send jokes, give kudos, get some memes, toss out some emoji's or whatever else strikes your fancy.</span></span>

## <a name="anything-you-can-do-in-a-single-page-app-spa"></a><span data-ttu-id="2eccc-139">Все, что можно сделать в приложении с одной страницей (SPA)</span><span class="sxs-lookup"><span data-stu-id="2eccc-139">Anything you can do in a Single Page App (SPA)</span></span>

<span data-ttu-id="2eccc-140">Вкладки — это встроенные веб-страницы.</span><span class="sxs-lookup"><span data-stu-id="2eccc-140">Tabs are embedded web pages.</span></span> <span data-ttu-id="2eccc-141">Практически все, что можно сделать в отношении SPA, можно выполнить на вкладке Teams.</span><span class="sxs-lookup"><span data-stu-id="2eccc-141">Pretty much anything you can do in a SPA, you can do in a tab in Teams.</span></span> <span data-ttu-id="2eccc-142">Обратите внимание на вкладки группы "область" и "канал" для совместного использования, личные вкладки предназначены для... персональные возможности.</span><span class="sxs-lookup"><span data-stu-id="2eccc-142">Just be sure to pay attention to scope - group and channel tabs are for shared experiences, personal tabs are for ... personal experiences.</span></span> <span data-ttu-id="2eccc-143">Список всех элементов группы на вкладке канал можно отобразить на вкладке Личные.</span><span class="sxs-lookup"><span data-stu-id="2eccc-143">The team's list of stuff goes on the channel tab, the list of your stuff goes in the personal tab.</span></span>

## <a name="start-small"></a><span data-ttu-id="2eccc-144">Запуск малых</span><span class="sxs-lookup"><span data-stu-id="2eccc-144">Start small</span></span>

<span data-ttu-id="2eccc-145">Не знаете, с чего начать?</span><span class="sxs-lookup"><span data-stu-id="2eccc-145">Not sure where to start?</span></span> <span data-ttu-id="2eccc-146">Слишком большое значение слишком большое для вас.</span><span class="sxs-lookup"><span data-stu-id="2eccc-146">Feeling a bit overwhelmed with the awesome variety of options available to you?</span></span> <span data-ttu-id="2eccc-147">Не Фрет, выберите основной компонент приложения и запустите его.</span><span class="sxs-lookup"><span data-stu-id="2eccc-147">Don't fret, choose a core feature of your app and start there.</span></span> <span data-ttu-id="2eccc-148">Когда вы получите впечатление от передачи информации с помощью различных контекстов в Teams, вы значительно упрощаете изображение более сложного взаимодействия.</span><span class="sxs-lookup"><span data-stu-id="2eccc-148">Once you get a feel for the flow of information through the various contexts in Teams, it will be a lot simpler to picture a more complex interaction.</span></span>

## <a name="putting-it-all-together"></a><span data-ttu-id="2eccc-149">Готовое решение</span><span class="sxs-lookup"><span data-stu-id="2eccc-149">Putting it all together</span></span>

<span data-ttu-id="2eccc-150">С другой стороны, лучшие приложения, как правило, объединяют несколько функций, создавая приложение, которое применяет пользователей в правильном контексте с правильной функциональностью в нужное время.</span><span class="sxs-lookup"><span data-stu-id="2eccc-150">That being said, the best apps usually combine multiple features, creating an app that engages users in the right context with the right functionality at the right time.</span></span> <span data-ttu-id="2eccc-151">Не пытайтесь принудительно использовать функции в месте, так как у вас есть хороший одноранговый односторонняя пользователь, который не должен просто добавлять его в команду.</span><span class="sxs-lookup"><span data-stu-id="2eccc-151">Don't try to force functionality into a place it doesn't belong - just because you've got a good one-to-one conversational bot doesn't mean you should just add it to a team.</span></span> <span data-ttu-id="2eccc-152">Разные точки расширения хорошо подходят для разных целей; Поиграйте на свои сильные стороны, и ваше приложение будет наполняться.</span><span class="sxs-lookup"><span data-stu-id="2eccc-152">Different extensibility points are good for different things; play to their strengths and your app will shine.</span></span>
