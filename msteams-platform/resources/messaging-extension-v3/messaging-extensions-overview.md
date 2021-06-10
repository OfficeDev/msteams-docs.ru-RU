---
title: Разработка расширений обмена сообщениями
description: Описывает, как начать работу с расширениями обмена сообщениями в Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: расширения обмена сообщениями команд
ms.openlocfilehash: 2301a9af7574c193c7327bb45e38f91bedc73793
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020606"
---
# <a name="develop-messaging-extensions-for-microsoft-teams"></a><span data-ttu-id="87709-104">Разработка расширений обмена сообщениями для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="87709-104">Develop messaging extensions for Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

<span data-ttu-id="87709-105">Расширения обмена сообщениями — это мощный способ для пользователей взаимодействовать с приложением из Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="87709-105">Messaging extensions are a powerful way for users to engage with your app from Microsoft Teams.</span></span> <span data-ttu-id="87709-106">С помощью этой возможности пользователи могут запрашивать или отправлять сведения в службу и из вашей службы и отправлять эти сведения в виде карт прямо в сообщение.</span><span class="sxs-lookup"><span data-stu-id="87709-106">With this capability, users can query or post information to and from your service and post that information, in the form of cards, right into a message.</span></span>

![Пример карточки расширения обмена сообщениями](~/assets/images/compose-extensions/ceexample.png)

<span data-ttu-id="87709-108">Расширения обмена сообщениями отображаются в нижней части окне композитной части.</span><span class="sxs-lookup"><span data-stu-id="87709-108">Messaging extensions appear along the bottom of the compose box.</span></span> <span data-ttu-id="87709-109">Некоторые из них встроены, например в Emoji, Giphy и Sticker.</span><span class="sxs-lookup"><span data-stu-id="87709-109">A few are built in, such as Emoji, Giphy, and Sticker.</span></span> <span data-ttu-id="87709-110">Выберите **кнопку Дополнительные** параметры **(&#8943;),** чтобы увидеть другие расширения обмена сообщениями, в том числе те, которые вы добавляете из галереи приложений или самостоятельно загрузите.</span><span class="sxs-lookup"><span data-stu-id="87709-110">Choose the **More Options** (**&#8943;**) button to see other messaging extensions, including those you add from the app gallery or upload yourself.</span></span>

<span data-ttu-id="87709-111">Как использовать расширения обмена сообщениями?</span><span class="sxs-lookup"><span data-stu-id="87709-111">How would you use messaging extensions?</span></span> <span data-ttu-id="87709-112">Вот несколько возможностей:</span><span class="sxs-lookup"><span data-stu-id="87709-112">Here are a few possibilities:</span></span>

* <span data-ttu-id="87709-113">Элементы работы и ошибки</span><span class="sxs-lookup"><span data-stu-id="87709-113">Work items and bugs</span></span>
* <span data-ttu-id="87709-114">Билеты на поддержку клиентов</span><span class="sxs-lookup"><span data-stu-id="87709-114">Customer support tickets</span></span>
* <span data-ttu-id="87709-115">Диаграммы и отчеты об использовании</span><span class="sxs-lookup"><span data-stu-id="87709-115">Usage charts and reports</span></span>
* <span data-ttu-id="87709-116">Изображения и медиаконтент</span><span class="sxs-lookup"><span data-stu-id="87709-116">Images and media content</span></span>
* <span data-ttu-id="87709-117">Возможности и руководства по продажам</span><span class="sxs-lookup"><span data-stu-id="87709-117">Sales opportunities and leads</span></span>

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="87709-118">Типы расширений обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="87709-118">Types of messaging extensions</span></span>

<span data-ttu-id="87709-119">Существует в основном два типа расширений обмена сообщениями, которые можно создать для Teams сегодня.</span><span class="sxs-lookup"><span data-stu-id="87709-119">There's primarily two kinds of messaging extensions you can create for Teams today.</span></span> <span data-ttu-id="87709-120">Следующие темы будут направлять вас в процессе их создания:</span><span class="sxs-lookup"><span data-stu-id="87709-120">The following topics will guide you through the process of creating them:</span></span>

* <span data-ttu-id="87709-121">[Расширения обмена сообщениями на основе](~/resources/messaging-extension-v3/search-extensions.md)поиска: Запрос службы для получения сведений и вставка их в сообщение.</span><span class="sxs-lookup"><span data-stu-id="87709-121">[Search based messaging extensions](~/resources/messaging-extension-v3/search-extensions.md): Query your service for information and insert that into a message.</span></span> <span data-ttu-id="87709-122">Пример: просмотр элемента работы</span><span class="sxs-lookup"><span data-stu-id="87709-122">Example: Lookup a work item</span></span>
* <span data-ttu-id="87709-123">[Расширения обмена сообщениями на](~/resources/messaging-extension-v3/create-extensions.md)основе действий: сбор сведений от пользователя и отправка в службу 3-й стороны.</span><span class="sxs-lookup"><span data-stu-id="87709-123">[Action-based messaging extensions](~/resources/messaging-extension-v3/create-extensions.md): Collect information from the user and post to a 3rd party service.</span></span> <span data-ttu-id="87709-124">Пример: Создание элемента работы</span><span class="sxs-lookup"><span data-stu-id="87709-124">Example: Create a work item</span></span>
