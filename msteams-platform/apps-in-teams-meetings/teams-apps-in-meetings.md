---
title: Приложения для Teams собраний
author: laujan
description: обзор приложений в Teams собраниях в зависимости от роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 1fdf3d55219d80d6953ffa0865b223dd626053f6
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649666"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="15653-104">Приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="15653-104">Apps for Teams meetings</span></span>

<span data-ttu-id="15653-105">Собрания позволяют совместное сотрудничество, партнерство, информированное общение и общие отзывы на инклюзивном и активном форуме.</span><span class="sxs-lookup"><span data-stu-id="15653-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="15653-106">Приложение для собраний может предоставлять пользовательский интерфейс для каждого этапа жизненного цикла собрания, включая опыт предварительного собрания, собрания и приложения после собрания, в зависимости от состояния участника.</span><span class="sxs-lookup"><span data-stu-id="15653-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="15653-107">Пользователи могут получать доступ к приложениям во время собраний с помощью галереи вкладок, например:</span><span class="sxs-lookup"><span data-stu-id="15653-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="15653-108">Предустановка доски Kanban.</span><span class="sxs-lookup"><span data-stu-id="15653-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="15653-109">Запустите диалоговое окно для действий в собрании.</span><span class="sxs-lookup"><span data-stu-id="15653-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="15653-110">Создание опроса после собрания.</span><span class="sxs-lookup"><span data-stu-id="15653-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="15653-111">В этой статье представлен обзор возможностей приложения для собраний, ссылок на API, включить и настроить приложения для собраний, а также режим совместной работы в Teams.</span><span class="sxs-lookup"><span data-stu-id="15653-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and Together Mode in Teams.</span></span>

<span data-ttu-id="15653-112">Вы можете улучшить свой опыт собраний с помощью функции расширения собраний, которая позволяет интегрировать приложения в собраниях.</span><span class="sxs-lookup"><span data-stu-id="15653-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="15653-113">Он также включает различные этапы жизненного цикла собрания, где можно интегрировать вкладки, боты и расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="15653-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="15653-114">С помощью API-интерфейсов доступности собраний можно определить различные роли участников и типы пользователей, получать события собраний, создавать диалоги на собрании и так далее.</span><span class="sxs-lookup"><span data-stu-id="15653-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="15653-115">Чтобы настроить Teams приложениями для собраний, вы можете включить приложения для собраний Teams, обновив манифест приложения, а также настроить приложения для сценариев собраний.</span><span class="sxs-lookup"><span data-stu-id="15653-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="15653-116">Новая функция Together Mode позволяет пользователям совместно работать на собрании со своей командой в одном месте, не будучи разделенными коробками.</span><span class="sxs-lookup"><span data-stu-id="15653-116">The new Together Mode feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="15653-117">См. также</span><span class="sxs-lookup"><span data-stu-id="15653-117">See also</span></span>

* [<span data-ttu-id="15653-118">Tab</span><span class="sxs-lookup"><span data-stu-id="15653-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="15653-119">Бот</span><span class="sxs-lookup"><span data-stu-id="15653-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="15653-120">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="15653-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="15653-121">Разработка приложения</span><span class="sxs-lookup"><span data-stu-id="15653-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="15653-122">Предпосылки и ссылки на API для приложений в Teams собраниях</span><span class="sxs-lookup"><span data-stu-id="15653-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="15653-123">Режим "Вместе"</span><span class="sxs-lookup"><span data-stu-id="15653-123">Together Mode</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="15653-124">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="15653-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="15653-125">Доступность приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="15653-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
