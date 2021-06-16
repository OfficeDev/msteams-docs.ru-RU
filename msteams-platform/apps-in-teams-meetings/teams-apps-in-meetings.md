---
title: Приложения для Teams собраний
author: laujan
description: обзор приложений в Teams собраниях в зависимости от роли участника и пользователя
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams apps meetings user participant role api
ms.openlocfilehash: 69016f818a333cb4f7cecc252539e076838a0735
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949653"
---
# <a name="apps-for-teams-meetings"></a><span data-ttu-id="c928f-104">Приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="c928f-104">Apps for Teams meetings</span></span>

<span data-ttu-id="c928f-105">Собрания позволяют совместное сотрудничество, партнерство, информированное общение и общие отзывы на инклюзивном и активном форуме.</span><span class="sxs-lookup"><span data-stu-id="c928f-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="c928f-106">Приложение для собраний может предоставлять пользовательский интерфейс для каждого этапа жизненного цикла собрания, включая опыт предварительного собрания, собрания и приложения после собрания, в зависимости от состояния участника.</span><span class="sxs-lookup"><span data-stu-id="c928f-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting, and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="c928f-107">Пользователи могут получать доступ к приложениям во время собраний с помощью галереи вкладок, например:</span><span class="sxs-lookup"><span data-stu-id="c928f-107">The users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="c928f-108">Предустановка доски Kanban.</span><span class="sxs-lookup"><span data-stu-id="c928f-108">Pre-stage a Kanban board.</span></span>
* <span data-ttu-id="c928f-109">Запустите диалоговое окно для действий в собрании.</span><span class="sxs-lookup"><span data-stu-id="c928f-109">Launch an in-meeting actionable dialog.</span></span>
* <span data-ttu-id="c928f-110">Создание опроса после собрания.</span><span class="sxs-lookup"><span data-stu-id="c928f-110">Create a post-meeting survey.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/nKAy5rNDus4]

<span data-ttu-id="c928f-111">В этой статье представлен обзор возможностей приложения для собраний, ссылок на API, включить и настроить приложения для собраний, а также настраиваемые сцены режима together в Teams.</span><span class="sxs-lookup"><span data-stu-id="c928f-111">This article provides an overview of meeting app extensibility, API references, enable and configure apps for meetings, and custom Together Mode scenes in Teams.</span></span>

<span data-ttu-id="c928f-112">Вы можете улучшить свой опыт собраний с помощью функции расширения собраний, которая позволяет интегрировать приложения в собраниях.</span><span class="sxs-lookup"><span data-stu-id="c928f-112">You can enhance your meeting experience by using the meeting extensibility feature, which enables you to integrate your apps within meetings.</span></span> <span data-ttu-id="c928f-113">Он также включает различные этапы жизненного цикла собрания, где можно интегрировать вкладки, боты и расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="c928f-113">It also includes different stages of a meeting lifecycle, where you can integrate tabs, bots, and messaging extensions.</span></span> <span data-ttu-id="c928f-114">С помощью API-интерфейсов доступности собраний можно определить различные роли участников и типы пользователей, получать события собраний, создавать диалоги на собрании и так далее.</span><span class="sxs-lookup"><span data-stu-id="c928f-114">With meetings extensibility APIs, you can identify different participant roles and user types, get meeting events, generate in-meeting dialogs, and so on.</span></span>

<span data-ttu-id="c928f-115">Чтобы настроить Teams приложениями для собраний, вы можете включить приложения для собраний Teams, обновив манифест приложения, а также настроить приложения для сценариев собраний.</span><span class="sxs-lookup"><span data-stu-id="c928f-115">To customize Teams with apps for meetings, you can enable your apps for Teams meetings by updating your app manifest and you can also configure your apps for meeting scenarios.</span></span>

<span data-ttu-id="c928f-116">Новая функция настраиваемой сцены Режима совместной работы позволяет пользователям совместно работать на собрании со своей командой в одном месте, не будучи разделенными коробками.</span><span class="sxs-lookup"><span data-stu-id="c928f-116">The new custom Together Mode scenes feature enables users to collaborate in a meeting with their team in one place without being separated by boxes.</span></span>

## <a name="see-also"></a><span data-ttu-id="c928f-117">См. также</span><span class="sxs-lookup"><span data-stu-id="c928f-117">See also</span></span>

* [<span data-ttu-id="c928f-118">Tab</span><span class="sxs-lookup"><span data-stu-id="c928f-118">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="c928f-119">Бот</span><span class="sxs-lookup"><span data-stu-id="c928f-119">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="c928f-120">Расширение для обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="c928f-120">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="c928f-121">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="c928f-121">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="c928f-122">Необходимые условия и ссылки на API для приложений в собраниях Teams</span><span class="sxs-lookup"><span data-stu-id="c928f-122">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)
* [<span data-ttu-id="c928f-123">Настраиваемые сцены режима "Вместе"</span><span class="sxs-lookup"><span data-stu-id="c928f-123">Custom Together Mode scenes</span></span>](~/apps-in-teams-meetings/teams-together-mode.md)

## <a name="next-step"></a><span data-ttu-id="c928f-124">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="c928f-124">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c928f-125">Расширяемость приложения для собраний</span><span class="sxs-lookup"><span data-stu-id="c928f-125">Meeting app extensibility</span></span>](meeting-app-extensibility.md)
