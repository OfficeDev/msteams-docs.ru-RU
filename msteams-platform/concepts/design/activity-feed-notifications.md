---
title: Проектирование уведомлений каналов активности
author: heath-hamilton
description: Узнайте, как создать уведомления о канале активности для Teams приложения и получить Microsoft Teams пользовательского интерфейса.
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 61a2a6da2a5ed0cb3126b9798094b06c575c9b6c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631360"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a><span data-ttu-id="0f44e-103">Проектирование уведомлений каналов активности для Microsoft Teams приложения</span><span class="sxs-lookup"><span data-stu-id="0f44e-103">Designing activity feed notifications for your Microsoft Teams app</span></span>

<span data-ttu-id="0f44e-104">Канал действий — это поверхность для доступа пользователей к уведомлениям в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0f44e-104">The activity feed is a surface for users to access their notifications in Microsoft Teams.</span></span> <span data-ttu-id="0f44e-105">Канал сохраняет уведомления за последние четыре недели.</span><span class="sxs-lookup"><span data-stu-id="0f44e-105">The feed retains notifications from the past four weeks.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0f44e-106">Desktop</span><span class="sxs-lookup"><span data-stu-id="0f44e-106">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="В примере отображается уведомление приложения, отображаемая в Teams канале действий." border="false":::

# <a name="mobile"></a>[<span data-ttu-id="0f44e-108">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="0f44e-108">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="В примере показано уведомление приложения, отображаемое в Teams канале активности на мобильном телефоне." border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="0f44e-110">Анатомия</span><span class="sxs-lookup"><span data-stu-id="0f44e-110">Anatomy</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="Разработка анатомии уведомления Teams канала действий." border="false":::

|<span data-ttu-id="0f44e-112">Счетчик</span><span class="sxs-lookup"><span data-stu-id="0f44e-112">Counter</span></span>|<span data-ttu-id="0f44e-113">Описание</span><span class="sxs-lookup"><span data-stu-id="0f44e-113">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0f44e-114">1</span><span class="sxs-lookup"><span data-stu-id="0f44e-114">1</span></span>|<span data-ttu-id="0f44e-115">**Аватар:** Показывает, кто инициировал действие.</span><span class="sxs-lookup"><span data-stu-id="0f44e-115">**Avatar**: Shows who initiated the activity.</span></span>|
|<span data-ttu-id="0f44e-116">2</span><span class="sxs-lookup"><span data-stu-id="0f44e-116">2</span></span>|<span data-ttu-id="0f44e-117">**Значок типа действия и приложения:** описывает тип действия.</span><span class="sxs-lookup"><span data-stu-id="0f44e-117">**Activity type/app icon**: Depicts the type of activity.</span></span> <span data-ttu-id="0f44e-118">Для уведомлений приложения значок строки заменяется значком приложения.</span><span class="sxs-lookup"><span data-stu-id="0f44e-118">For app notifications, the line icon is replaced with an app icon.</span></span>|
|<span data-ttu-id="0f44e-119">3</span><span class="sxs-lookup"><span data-stu-id="0f44e-119">3</span></span>|<span data-ttu-id="0f44e-120">**Название (первая строка): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span><span class="sxs-lookup"><span data-stu-id="0f44e-120">**Title (first line): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span></span> <span data-ttu-id="0f44e-121">*Причина.* Описывает действие.</span><span class="sxs-lookup"><span data-stu-id="0f44e-121">*Reason*: Describes the activity.</span></span>|
|<span data-ttu-id="0f44e-122">4 </span><span class="sxs-lookup"><span data-stu-id="0f44e-122">4</span></span>|<span data-ttu-id="0f44e-123">**Timestamp**: Показывает, когда действие произошло.</span><span class="sxs-lookup"><span data-stu-id="0f44e-123">**Timestamp**: Shows when the activity happened.</span></span>|
|<span data-ttu-id="0f44e-124">5 </span><span class="sxs-lookup"><span data-stu-id="0f44e-124">5</span></span>|<span data-ttu-id="0f44e-125">**Расположение (вторая строка)**: показывает, где происходило действие в Teams.</span><span class="sxs-lookup"><span data-stu-id="0f44e-125">**Location (second line)**: Shows where the activity happened in Teams.</span></span>|
|<span data-ttu-id="0f44e-126">6 </span><span class="sxs-lookup"><span data-stu-id="0f44e-126">6</span></span>|<span data-ttu-id="0f44e-127">**Tertiary information (third line)**: Optional.</span><span class="sxs-lookup"><span data-stu-id="0f44e-127">**Tertiary information (third line)**: Optional.</span></span> <span data-ttu-id="0f44e-128">Показывает предварительный текст или дополнительные сведения.</span><span class="sxs-lookup"><span data-stu-id="0f44e-128">Shows preview text or additional information.</span></span>|

## <a name="types-of-activity-feed-notification-cards"></a><span data-ttu-id="0f44e-129">Типы карт уведомлений о канале активности</span><span class="sxs-lookup"><span data-stu-id="0f44e-129">Types of activity feed notification cards</span></span>

<span data-ttu-id="0f44e-130">В следующих вариантах отображаются типы карт уведомлений о канале активности.</span><span class="sxs-lookup"><span data-stu-id="0f44e-130">The following variants show the kinds of activity feed notification cards you can display.</span></span> <span data-ttu-id="0f44e-131">Логотип приложения заменяет аватар пользователя для уведомлений, созданных приложениями.</span><span class="sxs-lookup"><span data-stu-id="0f44e-131">The app logo replaces the user avatar for app-generated notifications.</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Варианты Teams ленты действий." border="false":::

## <a name="manage-activity-feed-notifications"></a><span data-ttu-id="0f44e-133">Управление уведомлениями о канале действий</span><span class="sxs-lookup"><span data-stu-id="0f44e-133">Manage activity feed notifications</span></span>

<span data-ttu-id="0f44e-134">Пользователи могут управлять уведомлениями, отправленные из приложения на Teams параметров.</span><span class="sxs-lookup"><span data-stu-id="0f44e-134">Users can manage notifications sent from your app in the Teams settings page.</span></span>

## <a name="related-system-notifications"></a><span data-ttu-id="0f44e-135">Связанные системные уведомления</span><span class="sxs-lookup"><span data-stu-id="0f44e-135">Related system notifications</span></span>

<span data-ttu-id="0f44e-136">Каждое действие создает системные уведомления.</span><span class="sxs-lookup"><span data-stu-id="0f44e-136">Each activity generates a system notification.</span></span> <span data-ttu-id="0f44e-137">Отображаемые данные зависят от настройки пользователя в параметрах уведомлений.</span><span class="sxs-lookup"><span data-stu-id="0f44e-137">What displays depends on what the user configures in their notification settings.</span></span> <span data-ttu-id="0f44e-138">Пользователи также могут выбрать стиль уведомлений на основе своей операционной системы.</span><span class="sxs-lookup"><span data-stu-id="0f44e-138">Users can also choose a notification style based on their operating system.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="0f44e-139">Desktop</span><span class="sxs-lookup"><span data-stu-id="0f44e-139">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="Варианты Teams на разных операционных системах." border="false":::

|<span data-ttu-id="0f44e-141">Счетчик</span><span class="sxs-lookup"><span data-stu-id="0f44e-141">Counter</span></span>|<span data-ttu-id="0f44e-142">Описание</span><span class="sxs-lookup"><span data-stu-id="0f44e-142">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0f44e-143">1</span><span class="sxs-lookup"><span data-stu-id="0f44e-143">1</span></span>|<span data-ttu-id="0f44e-144">Teams настраиваемый</span><span class="sxs-lookup"><span data-stu-id="0f44e-144">Teams custom</span></span>|
|<span data-ttu-id="0f44e-145">2</span><span class="sxs-lookup"><span data-stu-id="0f44e-145">2</span></span>|<span data-ttu-id="0f44e-146">Windows</span><span class="sxs-lookup"><span data-stu-id="0f44e-146">Windows</span></span>|
|<span data-ttu-id="0f44e-147">3</span><span class="sxs-lookup"><span data-stu-id="0f44e-147">3</span></span>|<span data-ttu-id="0f44e-148">Mac</span><span class="sxs-lookup"><span data-stu-id="0f44e-148">Mac</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="0f44e-149">Мобильные устройства</span><span class="sxs-lookup"><span data-stu-id="0f44e-149">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Варианты Teams на Android и iOS." border="false":::

|<span data-ttu-id="0f44e-151">Счетчик</span><span class="sxs-lookup"><span data-stu-id="0f44e-151">Counter</span></span>|<span data-ttu-id="0f44e-152">Описание</span><span class="sxs-lookup"><span data-stu-id="0f44e-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="0f44e-153">1</span><span class="sxs-lookup"><span data-stu-id="0f44e-153">1</span></span>|<span data-ttu-id="0f44e-154">Android</span><span class="sxs-lookup"><span data-stu-id="0f44e-154">Android</span></span>|
|<span data-ttu-id="0f44e-155">2</span><span class="sxs-lookup"><span data-stu-id="0f44e-155">2</span></span>|<span data-ttu-id="0f44e-156">iOS</span><span class="sxs-lookup"><span data-stu-id="0f44e-156">iOS</span></span>|

---

## <a name="next-step"></a><span data-ttu-id="0f44e-157">Следующий этап</span><span class="sxs-lookup"><span data-stu-id="0f44e-157">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0f44e-158">Реализация уведомлений о канале действий</span><span class="sxs-lookup"><span data-stu-id="0f44e-158">Implement activity feed notifications</span></span>](/graph/teams-send-activityfeednotifications)
