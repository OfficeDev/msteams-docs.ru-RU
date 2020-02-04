---
title: Разработка расширений обмена сообщениями
description: Описывается начало работы с расширениями обмена сообщениями в Microsoft Teams.
keywords: расширения обмена сообщениями в Teams
ms.openlocfilehash: 6ba8f73d40f795a83f28707ef89c207c5d51d67c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675194"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="eb25e-104">Разработка расширений обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="eb25e-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="eb25e-105">Расширения обмена сообщениями — это мощный способ взаимодействия пользователей с приложением из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="eb25e-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="eb25e-106">С помощью этой возможности пользователи могут запрашивать или отправлять информацию в службу и из нее, а также отправлять эти сведения в виде карточек прямо в сообщение.</span><span class="sxs-lookup"><span data-stu-id="eb25e-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="eb25e-108">Расширения обмена сообщениями отображаются в нижней части поля "создание".</span><span class="sxs-lookup"><span data-stu-id="eb25e-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="eb25e-109">Встроены некоторые встроенные, такие как эмодзи, Giphy и наклейка.</span><span class="sxs-lookup"><span data-stu-id="eb25e-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="eb25e-110">Нажмите кнопку **Дополнительные параметры** (**&#8943;**), чтобы просмотреть другие расширения обмена сообщениями, в том числе добавленные из коллекции приложений или отправки вручную.</span><span class="sxs-lookup"><span data-stu-id="eb25e-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="eb25e-111">Как использовать расширения системы обмена сообщениями?</span><span class="sxs-lookup"><span data-stu-id="eb25e-111">How would you use messaging extensions?</span></span> <span data-ttu-id="eb25e-112">Вот несколько возможностей:</span><span class="sxs-lookup"><span data-stu-id="eb25e-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="eb25e-113">Рабочие элементы и ошибки</span><span class="sxs-lookup"><span data-stu-id="eb25e-113">Work items and bugs</span></span>
* <span data-ttu-id="eb25e-114">Билеты поддержки клиентов</span><span class="sxs-lookup"><span data-stu-id="eb25e-114">Customer support tickets</span></span>
* <span data-ttu-id="eb25e-115">Диаграммы использования и отчеты</span><span class="sxs-lookup"><span data-stu-id="eb25e-115">Usage charts and reports</span></span>
* <span data-ttu-id="eb25e-116">Изображения и мультимедийные материалы</span><span class="sxs-lookup"><span data-stu-id="eb25e-116">Images and media content</span></span>
* <span data-ttu-id="eb25e-117">Возможности продаж и интересы</span><span class="sxs-lookup"><span data-stu-id="eb25e-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="eb25e-118">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="eb25e-118">Types of messaging extensions</span></span>

<span data-ttu-id="eb25e-119">Существует два типа расширений обмена сообщениями, которые можно создать для Teams уже сегодня.</span><span class="sxs-lookup"><span data-stu-id="eb25e-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="eb25e-120">В следующих разделах описывается процесс создания:</span><span class="sxs-lookup"><span data-stu-id="eb25e-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="eb25e-121">[Расширения для обмена сообщениями на основе поиска](~/resources/messaging-extension-v3/search-extensions.md): Запросите службу для получения сведений и вставьте их в сообщение.</span><span class="sxs-lookup"><span data-stu-id="eb25e-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="eb25e-122">Пример: Поиск рабочего элемента</span><span class="sxs-lookup"><span data-stu-id="eb25e-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="eb25e-123">[Расширения для обмена сообщениями на основе действий](~/resources/messaging-extension-v3/create-extensions.md): сбор сведений от пользователя и публикация в сторонней службе.</span><span class="sxs-lookup"><span data-stu-id="eb25e-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="eb25e-124">Пример: создание рабочего элемента</span><span class="sxs-lookup"><span data-stu-id="eb25e-124">Example: Create a work item</span></span>
