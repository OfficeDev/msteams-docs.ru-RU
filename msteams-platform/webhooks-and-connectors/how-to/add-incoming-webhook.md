---
title: Создание входящих веб-ок
author: laujan
description: описывает, как добавить входящий веб-Teams приложение и опубликовать внешние запросы для Teams с входящие веб-окки
keywords: команды вкладки исходят веб-ок
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 53fe9725148579325386fa4677bebb61fdb72c56
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140142"
---
# <a name="create-incoming-webhook"></a><span data-ttu-id="44c26-104">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="44c26-104">Create Incoming Webhook</span></span>

<span data-ttu-id="44c26-105">Входящий веб-сайт позволяет любым внешним приложениям обмениваться контентом в Teams каналах.</span><span class="sxs-lookup"><span data-stu-id="44c26-105">Incoming Webhook allows any external apps to share content in Teams channels.</span></span> <span data-ttu-id="44c26-106">Эти веб-сайты используются в качестве средств отслеживания и уведомления.</span><span class="sxs-lookup"><span data-stu-id="44c26-106">These webhooks are used as tracking and notifying tools.</span></span> <span data-ttu-id="44c26-107">Они предоставляют уникальный URL-адрес, на который отправляется полезное сообщение JSON с сообщением в формате карты.</span><span class="sxs-lookup"><span data-stu-id="44c26-107">They provide a unique URL, to which you send a JSON payload with a message in card format.</span></span> <span data-ttu-id="44c26-108">Карты — это контейнеры пользовательского интерфейса, которые включают контент и действия, связанные с одной темой.</span><span class="sxs-lookup"><span data-stu-id="44c26-108">Cards are user interface containers that include content and actions related to a single topic.</span></span> <span data-ttu-id="44c26-109">Teams использовать карты в следующих возможностях:</span><span class="sxs-lookup"><span data-stu-id="44c26-109">Teams use cards within the following capabilities:</span></span>

* <span data-ttu-id="44c26-110">боты;</span><span class="sxs-lookup"><span data-stu-id="44c26-110">Bots</span></span>
* <span data-ttu-id="44c26-111">расширения для обмена сообщениями;</span><span class="sxs-lookup"><span data-stu-id="44c26-111">Messaging extensions</span></span>
* <span data-ttu-id="44c26-112">Соединители</span><span class="sxs-lookup"><span data-stu-id="44c26-112">Connectors</span></span>

## <a name="key-features-of-incoming-webhook"></a><span data-ttu-id="44c26-113">Ключевые функции входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="44c26-113">Key features of Incoming Webhook</span></span>

<span data-ttu-id="44c26-114">В следующей таблице представлены функции и описание входящих webhook:</span><span class="sxs-lookup"><span data-stu-id="44c26-114">The following table provides the features and description of Incoming Webhook:</span></span>

| <span data-ttu-id="44c26-115">Возможности</span><span class="sxs-lookup"><span data-stu-id="44c26-115">Features</span></span> | <span data-ttu-id="44c26-116">Description</span><span class="sxs-lookup"><span data-stu-id="44c26-116">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="44c26-117">Адаптивные карты с помощью входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="44c26-117">Adaptive Cards using an Incoming Webhook</span></span>|<span data-ttu-id="44c26-118">Адаптивные карты можно отправить через входящие веб-окки.</span><span class="sxs-lookup"><span data-stu-id="44c26-118">Adaptive Cards can be sent through Incoming Webhooks.</span></span> <span data-ttu-id="44c26-119">Дополнительные сведения см. в [странице Send Adaptive Cards using Incoming Webhooks.](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)</span><span class="sxs-lookup"><span data-stu-id="44c26-119">For more information, see [Send Adaptive Cards using Incoming Webhooks](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook).</span></span>|
|<span data-ttu-id="44c26-120">Actionable messaging support</span><span class="sxs-lookup"><span data-stu-id="44c26-120">Actionable messaging support</span></span>|<span data-ttu-id="44c26-121">Карточки сообщений для действий поддерживаются во всех Office 365, включая Teams.</span><span class="sxs-lookup"><span data-stu-id="44c26-121">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="44c26-122">Если вы отправляете сообщения через карты, необходимо использовать формат карточки сообщений.</span><span class="sxs-lookup"><span data-stu-id="44c26-122">If you send messages through cards, you must use the actionable message card format.</span></span> <span data-ttu-id="44c26-123">Дополнительные сведения см. в [старых справочных](/outlook/actionable-messages/message-card-reference) данных карточки сообщений и игровой [площадке карточки сообщений.](https://messagecardplayground.azurewebsites.net)</span><span class="sxs-lookup"><span data-stu-id="44c26-123">For more information, see [legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and [message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="44c26-124">Независимая поддержка обмена сообщениями HTTPS</span><span class="sxs-lookup"><span data-stu-id="44c26-124">Independent HTTPS messaging support</span></span>|<span data-ttu-id="44c26-125">Карточки предоставляют сведения четко и последовательно.</span><span class="sxs-lookup"><span data-stu-id="44c26-125">Cards provide information clearly and consistently.</span></span> <span data-ttu-id="44c26-126">Любой инструмент или фреймворк, который может отправлять запросы HTTPS POST, может отправлять сообщения Teams через входящий веб-сайт.</span><span class="sxs-lookup"><span data-stu-id="44c26-126">Any tool or framework that can send HTTPS POST requests, can send messages to Teams through an Incoming Webhook.</span></span>|
|<span data-ttu-id="44c26-127">Поддержка Markdown</span><span class="sxs-lookup"><span data-stu-id="44c26-127">Markdown support</span></span>|<span data-ttu-id="44c26-128">Все текстовые поля в картах обмена сообщениями, которые можно использовать для действий, поддерживают базовый Markdown.</span><span class="sxs-lookup"><span data-stu-id="44c26-128">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="44c26-129">Не используйте HTML-разметку в картах.</span><span class="sxs-lookup"><span data-stu-id="44c26-129">Do not use HTML markup in your cards.</span></span> <span data-ttu-id="44c26-130">HTML игнорируется и обрабатывается как обычный текст.</span><span class="sxs-lookup"><span data-stu-id="44c26-130">HTML is ignored and treated as plain text.</span></span>|
|<span data-ttu-id="44c26-131">Конфигурация scoped</span><span class="sxs-lookup"><span data-stu-id="44c26-131">Scoped configuration</span></span>|<span data-ttu-id="44c26-132">Входящий веб-сайт масштабирован и настроен на уровне канала.</span><span class="sxs-lookup"><span data-stu-id="44c26-132">Incoming Webhook is scoped and configured at the channel level.</span></span>|
|<span data-ttu-id="44c26-133">Безопасные определения ресурсов</span><span class="sxs-lookup"><span data-stu-id="44c26-133">Secure resource definitions</span></span>|<span data-ttu-id="44c26-134">Сообщения отформатированы в виде полезной нагрузки JSON.</span><span class="sxs-lookup"><span data-stu-id="44c26-134">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="44c26-135">Эта декларативная структура обмена сообщениями предотвращает вставку вредоносного кода.</span><span class="sxs-lookup"><span data-stu-id="44c26-135">This declarative messaging structure prevents the insertion of malicious code.</span></span>|

> [!NOTE]
> * <span data-ttu-id="44c26-136">Teams ботов, расширений обмена сообщениями, входящих веб-пользователей и поддержки адаптивных карт Bot Framework, открытой платформы платформы кросс-карт.</span><span class="sxs-lookup"><span data-stu-id="44c26-136">Teams bots, messaging extensions, Incoming Webhook, and the Bot Framework support Adaptive Cards, an open cross card platform framework.</span></span> <span data-ttu-id="44c26-137">В [настоящее время Teams не](../../webhooks-and-connectors/how-to/connectors-creating.md) поддерживают адаптивные карты.</span><span class="sxs-lookup"><span data-stu-id="44c26-137">Currently, [Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not support Adaptive Cards.</span></span> <span data-ttu-id="44c26-138">Тем не менее, можно создать [поток,](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) который публикует адаптивные карты в Teams канал.</span><span class="sxs-lookup"><span data-stu-id="44c26-138">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>
> * <span data-ttu-id="44c26-139">Дополнительные сведения о картах и веб-сайтах см. в странице [Adaptive cards and Incoming Webhooks.](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)</span><span class="sxs-lookup"><span data-stu-id="44c26-139">For more information on cards and webhooks, see [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span></span>

## <a name="create-incoming-webhook"></a><span data-ttu-id="44c26-140">Создание входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="44c26-140">Create Incoming Webhook</span></span>

<span data-ttu-id="44c26-141">**Добавление входящих веб-ок в Teams канал**</span><span class="sxs-lookup"><span data-stu-id="44c26-141">**To add an Incoming Webhook to a Teams channel**</span></span>

1. <span data-ttu-id="44c26-142">Перейдите к каналу, в котором необходимо добавить веб-ок и &#8226;&#8226;&#8226; **дополнительные** параметры из верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="44c26-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="44c26-143">Выберите **соединителей** из меню отсев:</span><span class="sxs-lookup"><span data-stu-id="44c26-143">Select **Connectors** from the dropdown menu:</span></span>

    ![Выбор соединитетеля](~/assets/images/connectors.png)

1. <span data-ttu-id="44c26-145">Поиск **входящих веб-ок** и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="44c26-145">Search for **Incoming Webhook** and select **Add**.</span></span>
1. <span data-ttu-id="44c26-146">Выберите **Настройка,** укайте имя и загрузите изображение для веб-сайта, если требуется:</span><span class="sxs-lookup"><span data-stu-id="44c26-146">Select **Configure**, provide a name, and upload an image for your webhook if required:</span></span>

    ![Настройка кнопки](~/assets/images/configure.png)

1. <span data-ttu-id="44c26-148">В диалоговом окне представлен уникальный URL-адрес канала.</span><span class="sxs-lookup"><span data-stu-id="44c26-148">The dialog window presents a unique URL that maps to the channel.</span></span> <span data-ttu-id="44c26-149">Скопируйте и сохраните URL-адрес веб-сайта, чтобы отправить сведения в Microsoft Teams и выбрать **Готово:**</span><span class="sxs-lookup"><span data-stu-id="44c26-149">Copy and save the webhook URL, to send information to Microsoft Teams and select **Done**:</span></span>

    ![Уникальный URL-адрес](~/assets/images/url.png)

<span data-ttu-id="44c26-151">Веб-сайт доступен в Teams канале.</span><span class="sxs-lookup"><span data-stu-id="44c26-151">The webhook is available in the Teams channel.</span></span>

> [!NOTE]
> <span data-ttu-id="44c26-152">В Teams выберите **разрешения Параметры** членов, позволяющие участникам создавать, обновлять и удалять соединители, чтобы любой член группы может добавлять, изменять или удалять  >    >  соединителю.</span><span class="sxs-lookup"><span data-stu-id="44c26-152">In Teams, select **Settings** > **Member permissions** > **Allow members to create, update, and remove connectors**, so that any team member can add, modify, or delete a connector.</span></span>

## <a name="remove-incoming-webhook"></a><span data-ttu-id="44c26-153">Удаление входящих веб-ок</span><span class="sxs-lookup"><span data-stu-id="44c26-153">Remove Incoming Webhook</span></span>

<span data-ttu-id="44c26-154">**Удаление входящих веб-ок с Teams канала**</span><span class="sxs-lookup"><span data-stu-id="44c26-154">**To remove an Incoming Webhook from a Teams channel**</span></span>

1. <span data-ttu-id="44c26-155">Перейдите на канал.</span><span class="sxs-lookup"><span data-stu-id="44c26-155">Go to the channel.</span></span>
1. <span data-ttu-id="44c26-156">Выберите &#8226;&#8226;&#8226; **дополнительные параметры** из верхней панели навигации.</span><span class="sxs-lookup"><span data-stu-id="44c26-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="44c26-157">Выберите **соединителей** из меню отсев.</span><span class="sxs-lookup"><span data-stu-id="44c26-157">Select **Connectors** from the dropdown menu.</span></span>
1. <span data-ttu-id="44c26-158">Слева в статье **Управление** выберите **Настроено**.</span><span class="sxs-lookup"><span data-stu-id="44c26-158">On the left, under **Manage**, select **Configured**.</span></span>
1. <span data-ttu-id="44c26-159">Выберите **< *1*>,** чтобы увидеть список текущих соединитений:</span><span class="sxs-lookup"><span data-stu-id="44c26-159">Select the **<*1*> Configured** to see a list of your current connectors:</span></span>

    ![Настроенный веб-сайт](~/assets/images/configured.png)

1. <span data-ttu-id="44c26-161">Выберите **Управление** рядом с соединитетелем, который необходимо удалить:</span><span class="sxs-lookup"><span data-stu-id="44c26-161">Select **Manage** next to the connector that you want to remove:</span></span>

    ![Управление веб-сайтом](~/assets/images/manage.png)

1. <span data-ttu-id="44c26-163">Выберите **Удаление:**</span><span class="sxs-lookup"><span data-stu-id="44c26-163">Select **Remove**:</span></span>

    ![Удаление веб-ок](~/assets/images/remove.png)

    <span data-ttu-id="44c26-165">Появится диалоговое окно **Remove Configuration:**</span><span class="sxs-lookup"><span data-stu-id="44c26-165">The **Remove Configuration** dialog box appears:</span></span>

    ![Удаление конфигурации](~/assets/images/removeconfiguration.png)

1. <span data-ttu-id="44c26-167">Заполните поля диалоговых полей и контрольных ящиков и выберите **Удаление:**</span><span class="sxs-lookup"><span data-stu-id="44c26-167">Complete the dialog box fields and checkboxes and select **Remove**:</span></span>

    ![Окончательное удаление](~/assets/images/finalremove.png)

    <span data-ttu-id="44c26-169">Веб-сайт удаляется из Teams канала.</span><span class="sxs-lookup"><span data-stu-id="44c26-169">The webhook is removed from the Teams channel.</span></span>

## <a name="see-also"></a><span data-ttu-id="44c26-170">См. также</span><span class="sxs-lookup"><span data-stu-id="44c26-170">See also</span></span>

* [<span data-ttu-id="44c26-171">Создание исходятого веб-окка</span><span class="sxs-lookup"><span data-stu-id="44c26-171">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [<span data-ttu-id="44c26-172">Создание соединителя Office 365</span><span class="sxs-lookup"><span data-stu-id="44c26-172">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="44c26-173">Создание и отправка сообщений</span><span class="sxs-lookup"><span data-stu-id="44c26-173">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
