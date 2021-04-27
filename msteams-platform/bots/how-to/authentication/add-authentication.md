---
title: Добавление проверки подлинности в бот Teams
author: clearab
description: Добавление проверки подлинности OAuth в бот в Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: d54d7fadb13626bb38de3a907b966f026cc6c485
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020954"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="32918-103">Добавление проверки подлинности в бот Teams</span><span class="sxs-lookup"><span data-stu-id="32918-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="32918-104">Иногда может потребоваться создать в Microsoft Teams боты, которые могут получать доступ к ресурсам от имени пользователя, например к почтовой службе.</span><span class="sxs-lookup"><span data-stu-id="32918-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="32918-105">В этой статье показано, как использовать проверку подлинности Azure Bot Service v4 SDK на основе OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="32918-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="32918-106">Это упрощает разработку бота, который может использовать маркеры проверки подлинности на основе учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="32918-107">Ключом во всем этом является использование поставщиков **удостоверений,** как мы увидим позже.</span><span class="sxs-lookup"><span data-stu-id="32918-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="32918-108">OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="32918-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="32918-109">Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="32918-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="32918-110">В этой области см. упрощенную версию [OAuth 2](https://aka.ms/oauth2-simplified) для базового понимания и [OAuth 2.0](https://oauth.net/2/) для полной спецификации.</span><span class="sxs-lookup"><span data-stu-id="32918-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="32918-111">Дополнительные сведения о том, как служба Azure Bot обрабатывает проверку подлинности, см. в записи проверки подлинности пользователей [в ходе беседы.](https://aka.ms/azure-bot-authentication)</span><span class="sxs-lookup"><span data-stu-id="32918-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="32918-112">В данной статье вы узнаете следующее.</span><span class="sxs-lookup"><span data-stu-id="32918-112">In this article you'll learn:</span></span>

- <span data-ttu-id="32918-113">**Создание бота с поддержкой проверки подлинности.**</span><span class="sxs-lookup"><span data-stu-id="32918-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="32918-114">Вы будете использовать [cs-auth-sample][teams-auth-bot-cs] для обработки учетных данных входа пользователя и создания маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="32918-115">**Развертывание бота в Azure и его связывание с поставщиком удостоверений.**</span><span class="sxs-lookup"><span data-stu-id="32918-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="32918-116">Поставщик выдает маркер на основе учетных данных входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="32918-117">Бот может использовать маркер для доступа к ресурсам, например к почтовой службе, для которой требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="32918-118">Дополнительные сведения см. [в потоке проверки подлинности Microsoft Teams для ботов.](auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="32918-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="32918-119">**Интеграция бота в Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="32918-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="32918-120">После интеграции бота можно войти и обмениваться сообщениями с ним в чате.</span><span class="sxs-lookup"><span data-stu-id="32918-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="32918-121">Необходимые условия</span><span class="sxs-lookup"><span data-stu-id="32918-121">Prerequisites</span></span>

- <span data-ttu-id="32918-122">Знание основ [бота,][concept-basics] [управление состоянием,][concept-state]библиотека диалогов [и][concept-dialogs]реализация [последовательного потока беседы.][simple-dialog]</span><span class="sxs-lookup"><span data-stu-id="32918-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="32918-123">Знание разработки Azure и OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="32918-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="32918-124">Текущие версии Visual Studio Git.</span><span class="sxs-lookup"><span data-stu-id="32918-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="32918-125">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="32918-125">Azure account.</span></span> <span data-ttu-id="32918-126">При необходимости можно создать бесплатную учетную запись [Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="32918-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="32918-127">Следующий пример.</span><span class="sxs-lookup"><span data-stu-id="32918-127">The following sample.</span></span>

    | <span data-ttu-id="32918-128">Пример</span><span class="sxs-lookup"><span data-stu-id="32918-128">Sample</span></span> | <span data-ttu-id="32918-129">Версия BotBuilder</span><span class="sxs-lookup"><span data-stu-id="32918-129">BotBuilder version</span></span> | <span data-ttu-id="32918-130">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="32918-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="32918-131">**Проверка подлинности ботов** [в cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="32918-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="32918-132">v4</span><span class="sxs-lookup"><span data-stu-id="32918-132">v4</span></span> | <span data-ttu-id="32918-133">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="32918-133">OAuthCard support</span></span> |
    | <span data-ttu-id="32918-134">**Проверка подлинности ботов** [в примере js-auth][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="32918-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="32918-135">v4</span><span class="sxs-lookup"><span data-stu-id="32918-135">v4</span></span>| <span data-ttu-id="32918-136">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="32918-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="32918-137">**Проверка подлинности ботов** [в py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="32918-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="32918-138">v4</span><span class="sxs-lookup"><span data-stu-id="32918-138">v4</span></span> | <span data-ttu-id="32918-139">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="32918-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="32918-140">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="32918-140">Create the resource group</span></span>

<span data-ttu-id="32918-141">Группа ресурсов и план службы не являются строго необходимыми, но они позволяют удобно выпускать ресурсы, которые вы создаете.</span><span class="sxs-lookup"><span data-stu-id="32918-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="32918-142">Это хорошая практика для сохраняющихся и управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32918-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="32918-143">Вы используете группу ресурсов для создания отдельных ресурсов для Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="32918-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="32918-144">Для производительности убедитесь, что эти ресурсы находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="32918-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="32918-145">В браузере вопишитесь на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="32918-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="32918-146">В левой панели навигации выберите **группы Ресурсов.**</span><span class="sxs-lookup"><span data-stu-id="32918-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="32918-147">В верхней левой части отображаемого окна выберите вкладку **Добавить,** чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32918-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="32918-148">Вам будет предложено предоставить следующее:</span><span class="sxs-lookup"><span data-stu-id="32918-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="32918-149">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="32918-149">**Subscription**.</span></span> <span data-ttu-id="32918-150">Используйте существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="32918-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="32918-151">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="32918-151">**Resource group**.</span></span> <span data-ttu-id="32918-152">Введите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32918-152">Enter the name for the resource group.</span></span> <span data-ttu-id="32918-153">Примером может быть  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="32918-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="32918-154">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="32918-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="32918-155">Из **выпадаемого** меню Region выберите *Запад США* или регион, близкий к вашим приложениям.</span><span class="sxs-lookup"><span data-stu-id="32918-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="32918-156">Выберите **кнопку Обзор и создайте** кнопку.</span><span class="sxs-lookup"><span data-stu-id="32918-156">Select the **Review and create** button.</span></span> <span data-ttu-id="32918-157">Вы должны увидеть баннер, который считывал *пройденную проверку.*</span><span class="sxs-lookup"><span data-stu-id="32918-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="32918-158">Выберите **кнопку Создать.**</span><span class="sxs-lookup"><span data-stu-id="32918-158">Select the **Create** button.</span></span> <span data-ttu-id="32918-159">Создание группы ресурсов может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="32918-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="32918-160">Как и в случае с ресурсами, которые будут создаваться в этом руководстве, для легкого доступа к этой группе ресурсов необходимо прикрепить эту группу ресурсов к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="32918-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="32918-161">Если вы хотите это сделать, выберите значок пин-&#128204; в правом верхнем справа от панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="32918-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="32918-162">Создание плана службы</span><span class="sxs-lookup"><span data-stu-id="32918-162">Create the service plan</span></span>

1. <span data-ttu-id="32918-163">На [**портале Azure**][azure-portal]на левой панели навигации выберите **Создание ресурса.**</span><span class="sxs-lookup"><span data-stu-id="32918-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="32918-164">В поле поиска введите *план службы приложения.*</span><span class="sxs-lookup"><span data-stu-id="32918-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="32918-165">Выберите карту **плана службы приложений** из результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="32918-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="32918-166">Нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32918-166">Select **Create**.</span></span>
1. <span data-ttu-id="32918-167">Вам будет предложено предоставить следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="32918-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="32918-168">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="32918-168">**Subscription**.</span></span> <span data-ttu-id="32918-169">Можно использовать существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="32918-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="32918-170">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="32918-170">**Resource Group**.</span></span> <span data-ttu-id="32918-171">Выберите группу, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="32918-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="32918-172">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="32918-172">**Name**.</span></span> <span data-ttu-id="32918-173">Введите имя для плана службы.</span><span class="sxs-lookup"><span data-stu-id="32918-173">Enter the name for the service plan.</span></span> <span data-ttu-id="32918-174">Примером может быть  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="32918-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="32918-175">Помните, что имя должно быть уникальным в группе.</span><span class="sxs-lookup"><span data-stu-id="32918-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="32918-176">**Операционная система**.</span><span class="sxs-lookup"><span data-stu-id="32918-176">**Operating System**.</span></span> <span data-ttu-id="32918-177">Выберите *Windows* или применимую ОС.</span><span class="sxs-lookup"><span data-stu-id="32918-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="32918-178">**Область**.</span><span class="sxs-lookup"><span data-stu-id="32918-178">**Region**.</span></span> <span data-ttu-id="32918-179">Выберите *Запад США* или регион, близкий к приложениям.</span><span class="sxs-lookup"><span data-stu-id="32918-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="32918-180">**Уровень цен.**</span><span class="sxs-lookup"><span data-stu-id="32918-180">**Pricing Tier**.</span></span> <span data-ttu-id="32918-181">Убедитесь, *что выбран стандартный S1.*</span><span class="sxs-lookup"><span data-stu-id="32918-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="32918-182">Это должно быть значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="32918-182">This should be the default value.</span></span>
    1. <span data-ttu-id="32918-183">Выберите **кнопку Обзор и создайте** кнопку.</span><span class="sxs-lookup"><span data-stu-id="32918-183">Select the **Review and create** button.</span></span> <span data-ttu-id="32918-184">Вы должны увидеть баннер, который считывал *пройденную проверку.*</span><span class="sxs-lookup"><span data-stu-id="32918-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="32918-185">Нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32918-185">Select **Create**.</span></span> <span data-ttu-id="32918-186">Создание плана службы приложений может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="32918-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="32918-187">План будет указан в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32918-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="32918-188">Создание регистрации каналов бота</span><span class="sxs-lookup"><span data-stu-id="32918-188">Create the bot channels registration</span></span>

<span data-ttu-id="32918-189">Регистрация каналов бота регистрирует веб-службу в качестве бота с помощью bot Framework при условии, что у вас есть код Microsoft App и пароль приложения (секрет клиента).</span><span class="sxs-lookup"><span data-stu-id="32918-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32918-190">Необходимо зарегистрировать бот только в том случае, если он не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="32918-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="32918-191">Если вы [создали бот через](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) портал Azure, он уже зарегистрирован в службе.</span><span class="sxs-lookup"><span data-stu-id="32918-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="32918-192">Если вы создали бот через [bot Framework](https://dev.botframework.com/bots/new) или [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) ваш бот не зарегистрирован в Azure.</span><span class="sxs-lookup"><span data-stu-id="32918-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="32918-193">Ресурс регистрации каналов ботов будет показывать **глобальный** регион, даже если вы выбрали Западный США.</span><span class="sxs-lookup"><span data-stu-id="32918-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="32918-194">Это ожидаемо.</span><span class="sxs-lookup"><span data-stu-id="32918-194">This is expected.</span></span>

<span data-ttu-id="32918-195">Дополнительные сведения см. в [дополнительных сведениях о создании бота для Teams.](../create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="32918-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="32918-196">Создание поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="32918-196">Create the identity provider</span></span>

<span data-ttu-id="32918-197">Вам нужен поставщик удостоверений, который можно использовать для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="32918-198">В этой процедуре вы будете использовать поставщика Azure AD; другие поставщики удостоверений, поддерживаемые Azure AD, также могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="32918-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="32918-199">На [**портале Azure**][azure-portal]на левой панели навигации выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32918-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="32918-200">Необходимо создать и зарегистрировать этот ресурс Azure AD в клиенте, в котором вы можете дать согласие на делегирование разрешений, запрашиваемого приложением.</span><span class="sxs-lookup"><span data-stu-id="32918-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="32918-201">Инструкции по созданию клиента см. в [сайте Access the portal и create a tenant.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)</span><span class="sxs-lookup"><span data-stu-id="32918-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="32918-202">В левой панели выберите **регистрации приложений.**</span><span class="sxs-lookup"><span data-stu-id="32918-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="32918-203">В правой панели выберите вкладку **Новая регистрация** в верхней левой части.</span><span class="sxs-lookup"><span data-stu-id="32918-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="32918-204">Вам будет предложено предоставить следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="32918-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="32918-205">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="32918-205">**Name**.</span></span> <span data-ttu-id="32918-206">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="32918-206">Enter the name for the application.</span></span> <span data-ttu-id="32918-207">Примером может быть *botTeamsIdentity.*</span><span class="sxs-lookup"><span data-stu-id="32918-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="32918-208">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="32918-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="32918-209">Выберите типы **поддерживаемых учетных записей** для приложения.</span><span class="sxs-lookup"><span data-stu-id="32918-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="32918-210">Выберите учетные записи в любом организационном каталоге *(любой каталог Azure AD - Multitenant)* и личных учетных записях Майкрософт (например, Skype, Xbox).</span><span class="sxs-lookup"><span data-stu-id="32918-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="32918-211">Для **URI перенаправления:**</span><span class="sxs-lookup"><span data-stu-id="32918-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="32918-212">&#x2713;Выберите **Веб**.</span><span class="sxs-lookup"><span data-stu-id="32918-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="32918-213">&#x2713; установите URL-адрес. `https://token.botframework.com/.auth/web/redirect`</span><span class="sxs-lookup"><span data-stu-id="32918-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="32918-214">Нажмите **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="32918-214">Select **Register**.</span></span>

1. <span data-ttu-id="32918-215">После создания Azure отображает страницу **Обзор** для приложения.</span><span class="sxs-lookup"><span data-stu-id="32918-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="32918-216">Копирование и сохранение следующих сведений в файле:</span><span class="sxs-lookup"><span data-stu-id="32918-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="32918-217">Значение **ID приложения (клиента).**</span><span class="sxs-lookup"><span data-stu-id="32918-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="32918-218">Это значение будет позже  использовать в качестве идентификатора клиента при регистрации этого приложения удостоверений Azure в боте.</span><span class="sxs-lookup"><span data-stu-id="32918-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="32918-219">**ID-значение Directory (tenant).**</span><span class="sxs-lookup"><span data-stu-id="32918-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="32918-220">Это значение также будет позже использовать в качестве идентификатора *клиента* для регистрации этого приложения удостоверений Azure в боте.</span><span class="sxs-lookup"><span data-stu-id="32918-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="32918-221">На левой панели выберите **сертификаты &,** чтобы создать клиентскую тайну для приложения.</span><span class="sxs-lookup"><span data-stu-id="32918-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="32918-222">В **статье Секреты клиента** выберите &#x2795; новый секрет **клиента**.</span><span class="sxs-lookup"><span data-stu-id="32918-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="32918-223">Добавьте описание, чтобы идентифицировать этот секрет от других пользователей, которые могут потребоваться создать для этого приложения, например приложения удостоверения bot *в Teams.*</span><span class="sxs-lookup"><span data-stu-id="32918-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="32918-224">Срок **действия набора истекает** в выборе.</span><span class="sxs-lookup"><span data-stu-id="32918-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="32918-225">Нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32918-225">Select **Add**.</span></span>
   1. <span data-ttu-id="32918-226">Перед выходом с этой страницы **зафиксировать секрет**.</span><span class="sxs-lookup"><span data-stu-id="32918-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="32918-227">Это значение будет позже использовать в качестве секрета _клиента_ при регистрации приложения Azure AD в боте.</span><span class="sxs-lookup"><span data-stu-id="32918-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="32918-228">Настройка подключения поставщика удостоверений и регистрация его с помощью бота</span><span class="sxs-lookup"><span data-stu-id="32918-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="32918-229">Примечание. Существует два варианта для поставщиков услуг здесь: Azure AD V1 и Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="32918-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="32918-230">Здесь резюмируют различия между [](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)двумя поставщиками, но в целом V2 обеспечивает большую гибкость в отношении изменения разрешений ботов.</span><span class="sxs-lookup"><span data-stu-id="32918-230">The differences between the two providers are summarized [here](https://docs.microsoft.com/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="32918-231">Разрешения API graph перечислены в поле областей, и по мере их добавлений боты позволяют пользователям соглашаться на новые разрешения при следующем входе.</span><span class="sxs-lookup"><span data-stu-id="32918-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="32918-232">Для V1 согласие бота должно быть удалено пользователем для получения новых разрешений, которые будут предложены в диалоговом окне OAuth.</span><span class="sxs-lookup"><span data-stu-id="32918-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="32918-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="32918-233">Azure AD V1</span></span>

1. <span data-ttu-id="32918-234">На [**портале Azure**][azure-portal]выберите группу ресурсов из панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="32918-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="32918-235">Выберите ссылку на регистрацию канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="32918-236">На странице ресурса выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="32918-236">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="32918-237">В статье Параметры подключения **OAuth** в нижней части страницы выберите **Параметр Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32918-237">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="32918-238">Заполните форму следующим образом:</span><span class="sxs-lookup"><span data-stu-id="32918-238">Complete the form as follows:</span></span>

    1. <span data-ttu-id="32918-239">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="32918-239">**Name**.</span></span> <span data-ttu-id="32918-240">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="32918-240">Enter a name for the connection.</span></span> <span data-ttu-id="32918-241">Вы будете использовать это имя в боте в `appsettings.json` файле.</span><span class="sxs-lookup"><span data-stu-id="32918-241">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="32918-242">Например, *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="32918-242">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="32918-243">**Поставщик услуг**.</span><span class="sxs-lookup"><span data-stu-id="32918-243">**Service Provider**.</span></span> <span data-ttu-id="32918-244">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="32918-244">Select **Azure Active Directory**.</span></span> <span data-ttu-id="32918-245">После этого будут отображаться поля Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32918-245">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="32918-246">**Client id**. Введите идентификатор приложения (клиента), записанный для приложения-поставщика удостоверений Azure в вышеуказанных действиях.</span><span class="sxs-lookup"><span data-stu-id="32918-246">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="32918-247">**Секрет клиента.**</span><span class="sxs-lookup"><span data-stu-id="32918-247">**Client secret**.</span></span> <span data-ttu-id="32918-248">Введите секрет, записанный для приложения-поставщика удостоверений Azure в шагах выше.</span><span class="sxs-lookup"><span data-stu-id="32918-248">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="32918-249">**Тип гранта**.</span><span class="sxs-lookup"><span data-stu-id="32918-249">**Grant Type**.</span></span> <span data-ttu-id="32918-250">Введите `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="32918-250">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="32918-251">**URL-адрес входа.**</span><span class="sxs-lookup"><span data-stu-id="32918-251">**Login URL**.</span></span> <span data-ttu-id="32918-252">Введите `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="32918-252">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="32918-253">**Идентификатор клиента** введите идентификатор **Directory (tenant),** записанный ранее для приложения  удостоверений Azure или распространенный в зависимости от поддерживаемого типа учетной записи, выбранного при создания приложения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="32918-253">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="32918-254">Чтобы определить, какое значение назначить, выполните указанные критерии:</span><span class="sxs-lookup"><span data-stu-id="32918-254">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="32918-255">Если вы выбрали только учетные записи в этом организационном каталоге (только Microsoft - один *клиент)* или учетные записи в любом организационном каталоге *(каталог Microsoft AAD . Multi tenant)* введите **ID** клиента, записанный ранее для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="32918-255">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="32918-256">Это будет клиент, связанный с пользователями, которые могут быть проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-256">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="32918-257">Если вы выбрали учетные записи в любом организационном каталоге (любой каталог AAD — многоъемные учетные записи Клиента и личные учетные записи Майкрософт, например  *Skype, Xbox, Outlook),* введите общее слово вместо ID клиента.</span><span class="sxs-lookup"><span data-stu-id="32918-257">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="32918-258">В противном случае приложение AAD проверяется через клиента, у которого был выбран ID, и исключает личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="32918-258">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="32918-259">h.</span><span class="sxs-lookup"><span data-stu-id="32918-259">h.</span></span> <span data-ttu-id="32918-260">Для **URL-адреса ресурса** введите `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="32918-260">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="32918-261">Это не используется в текущем примере кода.</span><span class="sxs-lookup"><span data-stu-id="32918-261">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="32918-262">i.</span><span class="sxs-lookup"><span data-stu-id="32918-262">i.</span></span> <span data-ttu-id="32918-263">Оставьте **области пустыми.**</span><span class="sxs-lookup"><span data-stu-id="32918-263">Leave **Scopes** blank.</span></span> <span data-ttu-id="32918-264">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-264">The following image is an example:</span></span>

    ![teams bots app auth connection string adv1 view](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="32918-266">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="32918-266">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="32918-267">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="32918-267">Azure AD V2</span></span>

1. <span data-ttu-id="32918-268">На [**портале Azure**][azure-portal]выберите группу ресурсов из панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="32918-268">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="32918-269">Выберите ссылку на регистрацию канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-269">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="32918-270">На странице ресурса выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="32918-270">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="32918-271">В статье Параметры подключения **OAuth** в нижней части страницы выберите **Параметр Добавить**.</span><span class="sxs-lookup"><span data-stu-id="32918-271">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="32918-272">Заполните форму следующим образом:</span><span class="sxs-lookup"><span data-stu-id="32918-272">Complete the form as follows:</span></span>

    1. <span data-ttu-id="32918-273">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="32918-273">**Name**.</span></span> <span data-ttu-id="32918-274">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="32918-274">Enter a name for the connection.</span></span> <span data-ttu-id="32918-275">Вы будете использовать это имя в боте в `appsettings.json` файле.</span><span class="sxs-lookup"><span data-stu-id="32918-275">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="32918-276">Например *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="32918-276">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="32918-277">**Поставщик услуг**.</span><span class="sxs-lookup"><span data-stu-id="32918-277">**Service Provider**.</span></span> <span data-ttu-id="32918-278">Выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="32918-278">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="32918-279">После этого будут отображаться поля Azure AD.</span><span class="sxs-lookup"><span data-stu-id="32918-279">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="32918-280">**Client id**. Введите идентификатор приложения (клиента), записанный для приложения-поставщика удостоверений Azure в вышеуказанных действиях.</span><span class="sxs-lookup"><span data-stu-id="32918-280">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="32918-281">**Секрет клиента.**</span><span class="sxs-lookup"><span data-stu-id="32918-281">**Client secret**.</span></span> <span data-ttu-id="32918-282">Введите секрет, записанный для приложения-поставщика удостоверений Azure в шагах выше.</span><span class="sxs-lookup"><span data-stu-id="32918-282">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="32918-283">**URL-адрес Exchange Token Exchange.**</span><span class="sxs-lookup"><span data-stu-id="32918-283">**Token Exchange URL**.</span></span> <span data-ttu-id="32918-284">Оставьте этот пробел.</span><span class="sxs-lookup"><span data-stu-id="32918-284">Leave this blank.</span></span>
    1. <span data-ttu-id="32918-285">**Идентификатор клиента** введите идентификатор **Directory (tenant),** записанный ранее для приложения  удостоверений Azure или распространенный в зависимости от поддерживаемого типа учетной записи, выбранного при создания приложения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="32918-285">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="32918-286">Чтобы определить, какое значение назначить, выполните указанные критерии:</span><span class="sxs-lookup"><span data-stu-id="32918-286">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="32918-287">Если вы выбрали только учетные записи в этом организационном каталоге (только Microsoft - один *клиент)* или учетные записи в любом организационном каталоге *(каталог Microsoft AAD . Multi tenant)* введите **ID** клиента, записанный ранее для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="32918-287">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="32918-288">Это будет клиент, связанный с пользователями, которые могут быть проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-288">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="32918-289">Если вы выбрали учетные записи в любом организационном каталоге (любой каталог AAD — многоъемные учетные записи Клиента и личные учетные записи Майкрософт, например  *Skype, Xbox, Outlook),* введите общее слово вместо ID клиента.</span><span class="sxs-lookup"><span data-stu-id="32918-289">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="32918-290">В противном случае приложение AAD проверяется через клиента, у которого был выбран ID, и исключает личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="32918-290">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="32918-291">Для **областей** введите список разрешений, относячимый к пространству, для этого приложения требуется, например: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="32918-291">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="32918-292">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="32918-292">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="32918-293">Тестирование подключения</span><span class="sxs-lookup"><span data-stu-id="32918-293">Test the connection</span></span>

1. <span data-ttu-id="32918-294">Выберите запись подключения, чтобы открыть только что созданное подключение.</span><span class="sxs-lookup"><span data-stu-id="32918-294">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="32918-295">Выберите **подключение к тесту** в верхней части панели **параметра подключения поставщика** услуг.</span><span class="sxs-lookup"><span data-stu-id="32918-295">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="32918-296">При первом этом откроется новое окно браузера с просьбой выбрать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="32918-296">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="32918-297">Выберите тот, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="32918-297">Select the one you want to use.</span></span>
1. <span data-ttu-id="32918-298">Далее вам будет предложено разрешить поставщику удостоверений использовать данные (учетные данные).</span><span class="sxs-lookup"><span data-stu-id="32918-298">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="32918-299">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-299">The following image is an example:</span></span>

    ![teams bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="32918-301">Выберите **Accept**.</span><span class="sxs-lookup"><span data-stu-id="32918-301">Select **Accept**.</span></span>
1. <span data-ttu-id="32918-302">Это должно перенаправить вас на страницу **Тестовая подключение \<your-connection-name> к успешной** странице.</span><span class="sxs-lookup"><span data-stu-id="32918-302">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="32918-303">Обновите страницу, если вы получите ошибку.</span><span class="sxs-lookup"><span data-stu-id="32918-303">Refresh the page if you get an error.</span></span> <span data-ttu-id="32918-304">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-304">The following image is an example:</span></span>

  ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="32918-306">Имя подключения используется кодом бота для получения маркеров проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="32918-306">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="32918-307">Подготовка кода образца бота</span><span class="sxs-lookup"><span data-stu-id="32918-307">Prepare the bot sample code</span></span>

<span data-ttu-id="32918-308">С помощью предварительных параметров давайте сосредоточимся на создании бота, который будет использовать в этой статье.</span><span class="sxs-lookup"><span data-stu-id="32918-308">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="32918-309">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="32918-309">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="32918-310">Клон [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="32918-310">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="32918-311">Запуск Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32918-311">Launch Visual Studio.</span></span>
1. <span data-ttu-id="32918-312">На панели инструментов выберите **Файл -> -> Project/Solution** и откройте бот-проект.</span><span class="sxs-lookup"><span data-stu-id="32918-312">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="32918-313">В C# обновление **appsettings.jsв** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="32918-313">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="32918-314">Установите `ConnectionName` имя подключения поставщика удостоверений, добавленного к регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-314">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="32918-315">Имя, которое мы использовали в этом *примере, — BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="32918-315">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="32918-316">Установите `MicrosoftAppId` для **бота ID приложения,** сохраненного во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-316">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="32918-317">Установите `MicrosoftAppPassword` секрет **клиента,** сохраненный во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-317">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="32918-318">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="32918-318">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="32918-319">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="32918-319">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="32918-320">В обозревателе решений перейдите в папку, откройте и установите, а также в бот App ID, сохраненный во время регистрации `TeamsAppManifest` `manifest.json` канала `id` `botId` бота. </span><span class="sxs-lookup"><span data-stu-id="32918-320">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="32918-321">JavaScript</span><span class="sxs-lookup"><span data-stu-id="32918-321">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="32918-322">Клон [узла-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="32918-322">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="32918-323">В консоли перейдите к проекту:</span><span class="sxs-lookup"><span data-stu-id="32918-323">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="32918-324">Установка модулей</span><span class="sxs-lookup"><span data-stu-id="32918-324">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="32918-325">Обновление **конфигурации .env** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="32918-325">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="32918-326">Установите `MicrosoftAppId` для **бота ID приложения,** сохраненного во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-326">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="32918-327">Установите `MicrosoftAppPassword` секрет **клиента,** сохраненный во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="32918-327">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="32918-328">Установите имя подключения поставщика `connectionName` удостоверений.</span><span class="sxs-lookup"><span data-stu-id="32918-328">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="32918-329">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="32918-329">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="32918-330">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="32918-330">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="32918-331">В папке откройте и установите свой microsoft App ID и бот App `teamsAppManifest` `manifest.json` `id` **ID,** сохраненный во время регистрации канала `botId` бота. </span><span class="sxs-lookup"><span data-stu-id="32918-331">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="32918-332">Python</span><span class="sxs-lookup"><span data-stu-id="32918-332">Python</span></span>](#tab/python)

1. <span data-ttu-id="32918-333">Клонировать [py-auth-пример][teams-auth-bot-py] из хранилища github.</span><span class="sxs-lookup"><span data-stu-id="32918-333">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="32918-334">Обновление **config.py:**</span><span class="sxs-lookup"><span data-stu-id="32918-334">Update **config.py**:</span></span>

    - <span data-ttu-id="32918-335">`ConnectionName`Задайте имя параметра подключения OAuth, добавленного в бот.</span><span class="sxs-lookup"><span data-stu-id="32918-335">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="32918-336">Настройка и секрет приложения и ID приложения вашего `MicrosoftAppId` `MicrosoftAppPassword` бота.</span><span class="sxs-lookup"><span data-stu-id="32918-336">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="32918-337">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="32918-337">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="32918-338">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="32918-338">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="32918-339">Развертывание бота в Azure</span><span class="sxs-lookup"><span data-stu-id="32918-339">Deploy the bot to Azure</span></span>

<span data-ttu-id="32918-340">Чтобы развернуть бот, выполните действия по развертыванию бота [в Azure.](https://aka.ms/azure-bot-deployment-cli)</span><span class="sxs-lookup"><span data-stu-id="32918-340">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="32918-341">Кроме того, в Visual Studio вы можете следовать следующим шагам:</span><span class="sxs-lookup"><span data-stu-id="32918-341">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="32918-342">В Visual Studio *Обозреватель* решений выберите и удерживайте (или правой кнопкой мыши) имя проекта.</span><span class="sxs-lookup"><span data-stu-id="32918-342">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="32918-343">В выпадаемом меню выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="32918-343">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="32918-344">В отображаемом окне выберите новую **ссылку.**</span><span class="sxs-lookup"><span data-stu-id="32918-344">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="32918-345">В диалоговом окне выберите **Службу приложений** слева и **создайте новое** справа.</span><span class="sxs-lookup"><span data-stu-id="32918-345">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="32918-346">Выберите **кнопку Публикация.**</span><span class="sxs-lookup"><span data-stu-id="32918-346">Select the **Publish** button.</span></span>
1. <span data-ttu-id="32918-347">В следующем диалоговом окне введите требуемую информацию.</span><span class="sxs-lookup"><span data-stu-id="32918-347">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="32918-348">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="32918-348">The following is an example:</span></span>

   ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="32918-350">Нажмите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="32918-350">Select **Create**.</span></span>
1. <span data-ttu-id="32918-351">Если развертывание успешно завершено, вы должны увидеть его отражение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="32918-351">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="32918-352">Кроме того, страница отображается в браузере по умолчанию, *говоря, что ваш бот готов!.*</span><span class="sxs-lookup"><span data-stu-id="32918-352">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="32918-353">URL-адрес будет похож на этот: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="32918-353">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="32918-354">Сохраните его в файле.</span><span class="sxs-lookup"><span data-stu-id="32918-354">Save it to a file.</span></span>
1. <span data-ttu-id="32918-355">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="32918-355">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="32918-356">Проверьте группу ресурсов, бот должен быть указан вместе с другими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="32918-356">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="32918-357">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-357">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="32918-359">В группе ресурсов выберите имя регистрации канала бота (ссылка).</span><span class="sxs-lookup"><span data-stu-id="32918-359">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="32918-360">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="32918-360">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="32918-361">В **окне конечной точки обмена сообщениями** введите URL-адрес, полученный выше, а затем `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="32918-361">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="32918-362">Вот пример: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="32918-362">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="32918-363">Выберите **кнопку Сохранить** в левом верхнем верхней части.</span><span class="sxs-lookup"><span data-stu-id="32918-363">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="32918-364">Тестирование бота с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="32918-364">Test the bot using the Emulator</span></span>

<span data-ttu-id="32918-365">Если вы еще этого не сделали, установите [эмулятор Microsoft Bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="32918-365">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="32918-366">См. [также отладку с эмулятором](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="32918-366">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="32918-367">Чтобы образец бота работал, необходимо настроить эмулятор, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="32918-367">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="32918-368">Настройка эмулятора для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="32918-368">Configure the Emulator for authentication</span></span>

<span data-ttu-id="32918-369">Если боту требуется проверка подлинности, необходимо настроить эмулятор, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="32918-369">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="32918-370">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="32918-370">Start the Emulator.</span></span>
1. <span data-ttu-id="32918-371">В эмуляторе выберите значок передачи &#9881; в левом  нижнем низу или вкладку Параметры эмулятора в правом верхнем.</span><span class="sxs-lookup"><span data-stu-id="32918-371">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="32918-372">Проверьте поле с помощью маркеров проверки подлинности версии **1.0.**</span><span class="sxs-lookup"><span data-stu-id="32918-372">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="32918-373">Введите локальный путь к **средству ngrok.**</span><span class="sxs-lookup"><span data-stu-id="32918-373">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="32918-374">*См.* эмулятор bot Framework / интеграция тоннелей ngrok [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span><span class="sxs-lookup"><span data-stu-id="32918-374">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="32918-375">Дополнительные сведения об инструментах см. [в сайте ngrok.](https://ngrok.com/)</span><span class="sxs-lookup"><span data-stu-id="32918-375">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="32918-376">Проверьте поле run **ngrok при запуске эмулятора.**</span><span class="sxs-lookup"><span data-stu-id="32918-376">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="32918-377">Выберите **кнопку Сохранить.**</span><span class="sxs-lookup"><span data-stu-id="32918-377">Select the **Save** button.</span></span>

<span data-ttu-id="32918-378">Когда бот отображает входную карточку и пользователь выбирает кнопку вход, эмулятор открывает страницу, которую пользователь может использовать для регистрации с поставщиком проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-378">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="32918-379">После этого пользователь создает маркер пользователя и отправляет его боту.</span><span class="sxs-lookup"><span data-stu-id="32918-379">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="32918-380">После этого бот может действовать от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-380">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="32918-381">Локальное тестирование бота</span><span class="sxs-lookup"><span data-stu-id="32918-381">Test the bot locally</span></span>

<span data-ttu-id="32918-382">После настройки механизма проверки подлинности можно выполнить фактическое тестирование бота.</span><span class="sxs-lookup"><span data-stu-id="32918-382">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="32918-383">Запустите образец бота локально на компьютере, Visual Studio например.</span><span class="sxs-lookup"><span data-stu-id="32918-383">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="32918-384">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="32918-384">Start the Emulator.</span></span>
1. <span data-ttu-id="32918-385">Выберите **кнопку Открыть бот.**</span><span class="sxs-lookup"><span data-stu-id="32918-385">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="32918-386">В **URL-адресе бота** введите локальный URL-адрес бота.</span><span class="sxs-lookup"><span data-stu-id="32918-386">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="32918-387">Обычно `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="32918-387">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="32918-388">В **ID приложения Майкрософт** введите ID приложения бота из `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="32918-388">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="32918-389">В пароле **Microsoft App** введите пароль приложения бота из `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="32918-389">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="32918-390">Выберите **Подключение**.</span><span class="sxs-lookup"><span data-stu-id="32918-390">Select **Connect**.</span></span>
1. <span data-ttu-id="32918-391">После запуска бота введите любой текст, чтобы отобразить карту входа.</span><span class="sxs-lookup"><span data-stu-id="32918-391">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="32918-392">Выберите **кнопку Вход.**</span><span class="sxs-lookup"><span data-stu-id="32918-392">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="32918-393">Всплывающее диалоговое окно отображается для подтверждения **открытого URL-адреса.**</span><span class="sxs-lookup"><span data-stu-id="32918-393">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="32918-394">Это позволяет пользователю бота (вам) быть аутентификацией.</span><span class="sxs-lookup"><span data-stu-id="32918-394">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="32918-395">Выберите **Подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="32918-395">Select **Confirm**.</span></span>
1. <span data-ttu-id="32918-396">При запросе выберите учетную запись соответствующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-396">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="32918-397">В зависимости от конфигурации эмулятора вы получаете одну из следующих конфигураций:</span><span class="sxs-lookup"><span data-stu-id="32918-397">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="32918-398">**Использование кода проверки входных данных**</span><span class="sxs-lookup"><span data-stu-id="32918-398">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="32918-399">&#x2713; открывается окно с кодом проверки.</span><span class="sxs-lookup"><span data-stu-id="32918-399">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="32918-400">&#x2713; и введите код проверки в поле чата для завершения входа.</span><span class="sxs-lookup"><span data-stu-id="32918-400">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="32918-401">**Использование маркеров проверки подлинности.**</span><span class="sxs-lookup"><span data-stu-id="32918-401">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="32918-402">&#x2713; вы вошли в систему на основе учетных данных.</span><span class="sxs-lookup"><span data-stu-id="32918-402">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="32918-403">Ниже приводится пример пользовательского интерфейса бота после входа в систему:</span><span class="sxs-lookup"><span data-stu-id="32918-403">The following image is an example of the bot UI after you've logged in:</span></span>

    ![Эмулятор входа в auth bot](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="32918-405">Если вы выберите **Да,** когда бот спросит, хотите ли вы просмотреть *маркер?* Вы получите ответ, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="32918-405">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Маркер эмулятора входа в auth bot](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="32918-407">Введите **вход в** поле входного чата, чтобы выйти из нее. Это освобождает маркер пользователя, и бот не сможет действовать от вашего имени, пока вы не вопишите снова.</span><span class="sxs-lookup"><span data-stu-id="32918-407">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="32918-408">Проверка подлинности ботов требует использования **службы соединителя ботов.**</span><span class="sxs-lookup"><span data-stu-id="32918-408">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="32918-409">Служба имеет доступ к данным о регистрации каналов бота для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="32918-409">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="32918-410">Тестирование развернутого бота</span><span class="sxs-lookup"><span data-stu-id="32918-410">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="32918-411">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="32918-411">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="32918-412">Найдите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="32918-412">Find your resource group.</span></span>
1. <span data-ttu-id="32918-413">Выберите ссылку ресурса.</span><span class="sxs-lookup"><span data-stu-id="32918-413">Select the resource link.</span></span> <span data-ttu-id="32918-414">Отображается страница ресурса.</span><span class="sxs-lookup"><span data-stu-id="32918-414">The resource page is displayed.</span></span>
1. <span data-ttu-id="32918-415">На странице ресурса выберите **Тест в веб-чате**.</span><span class="sxs-lookup"><span data-stu-id="32918-415">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="32918-416">Бот запускает и отображает заранее задавленные приветствия.</span><span class="sxs-lookup"><span data-stu-id="32918-416">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="32918-417">Введите что-либо в окне чата.</span><span class="sxs-lookup"><span data-stu-id="32918-417">Type anything in the chat box.</span></span>
1. <span data-ttu-id="32918-418">Выберите **вход в поле.**</span><span class="sxs-lookup"><span data-stu-id="32918-418">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="32918-419">Всплывающее диалоговое окно отображается для подтверждения **открытого URL-адреса.**</span><span class="sxs-lookup"><span data-stu-id="32918-419">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="32918-420">Это позволяет пользователю бота (вам) быть аутентификацией.</span><span class="sxs-lookup"><span data-stu-id="32918-420">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="32918-421">Выберите **Подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="32918-421">Select **Confirm**.</span></span>
1. <span data-ttu-id="32918-422">При запросе выберите учетную запись соответствующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-422">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="32918-423">Ниже приводится пример пользовательского интерфейса бота после входа в систему:</span><span class="sxs-lookup"><span data-stu-id="32918-423">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Развернутый вход бота auth](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="32918-425">.</span><span class="sxs-lookup"><span data-stu-id="32918-425">.</span></span>

1. <span data-ttu-id="32918-426">Выберите **кнопку Да,** чтобы отобразить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-426">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="32918-427">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-427">The following image is an example:</span></span>

    ![Развернутый маркер входа бота auth](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="32918-429">.</span><span class="sxs-lookup"><span data-stu-id="32918-429">.</span></span>

1. <span data-ttu-id="32918-430">Введите вход, чтобы выйти.</span><span class="sxs-lookup"><span data-stu-id="32918-430">Enter logout to sign out.</span></span>

    ![развернутый журнал auth bot](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="32918-432">Если у вас возникли проблемы с входом, попробуйте проверить подключение снова, как описано в предыдущих действиях.</span><span class="sxs-lookup"><span data-stu-id="32918-432">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="32918-433">Это может воссоздать маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="32918-433">This could recreate the authentication token.</span></span>
> <span data-ttu-id="32918-434">С клиентом веб-чата Bot Framework в Azure вам может потребоваться несколько раз войти, прежде чем проверка подлинности будет установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="32918-434">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="32918-435">Установка и тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="32918-435">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="32918-436">В проекте бота убедитесь, что папка `TeamsAppManifest` содержит вместе `manifest.json` с `outline.png` файлами и `color.png` файлами.</span><span class="sxs-lookup"><span data-stu-id="32918-436">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="32918-437">В Обозревателе решений перейдите в `TeamsAppManifest` папку.</span><span class="sxs-lookup"><span data-stu-id="32918-437">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="32918-438">Изменить, `manifest.json` назначив следующие значения:</span><span class="sxs-lookup"><span data-stu-id="32918-438">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="32918-439">Убедитесь, что полученный во время регистрации канала бота **ID** приложения-бота назначен и `id` `botId` .</span><span class="sxs-lookup"><span data-stu-id="32918-439">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="32918-440">Назначение этого значения: `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="32918-440">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="32918-441">Выберите и **zip** `manifest.json` , и `outline.png` `color.png` файлы.</span><span class="sxs-lookup"><span data-stu-id="32918-441">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="32918-442">Откройте **Microsoft Teams.**</span><span class="sxs-lookup"><span data-stu-id="32918-442">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="32918-443">В левой панели в нижней части выберите **значок Apps**.</span><span class="sxs-lookup"><span data-stu-id="32918-443">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="32918-444">В правой панели в нижней части выберите **Загрузите настраиваемые приложения.**</span><span class="sxs-lookup"><span data-stu-id="32918-444">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="32918-445">Перейдите в `TeamsAppManifest` папку и загрузите манифест с молнией.</span><span class="sxs-lookup"><span data-stu-id="32918-445">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="32918-446">Отображается следующий мастер:</span><span class="sxs-lookup"><span data-stu-id="32918-446">The following wizard is displayed:</span></span>

    ![Отправка команд auth bot](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="32918-448">Нажмите кнопку **Добавить в группу**.</span><span class="sxs-lookup"><span data-stu-id="32918-448">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="32918-449">В следующем окне выберите команду, в которой нужно использовать бот.</span><span class="sxs-lookup"><span data-stu-id="32918-449">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="32918-450">Выберите **кнопку Настройка бота.**</span><span class="sxs-lookup"><span data-stu-id="32918-450">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="32918-451">Выберите три точки (&#x25cf;&#x25cf;&#x25cf;) в левой панели.</span><span class="sxs-lookup"><span data-stu-id="32918-451">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="32918-452">Затем выберите **значок App Studio.**</span><span class="sxs-lookup"><span data-stu-id="32918-452">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="32918-453">Выберите **вкладку Редактор Манифеста.** Вы должны увидеть значок для загруженного бота.</span><span class="sxs-lookup"><span data-stu-id="32918-453">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="32918-454">Кроме того, вы должны иметь возможность видеть бота, перечисленных в качестве контакта в списке чата, который можно использовать для обмена сообщениями с ботом.</span><span class="sxs-lookup"><span data-stu-id="32918-454">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="32918-455">Тестирование бота локально в Teams</span><span class="sxs-lookup"><span data-stu-id="32918-455">Testing the bot locally in Teams</span></span>

<span data-ttu-id="32918-456">Microsoft Teams — это полностью облачный продукт, для этого необходимо, чтобы все службы, к ним доступ, были доступны в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="32918-456">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="32918-457">Поэтому для того, чтобы бот (наш пример) работал в Teams, необходимо либо опубликовать код в облаке по вашему выбору, либо сделать локально запущенный экземпляр внешне доступным с помощью средства тоннелей. </span><span class="sxs-lookup"><span data-stu-id="32918-457">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="32918-458">Рекомендуется  [ngrok,](https://ngrok.com/download)который создает внешне адресируемый URL-адрес для порта, который вы открываете локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="32918-458">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="32918-459">Чтобы настроить ngrok в процессе подготовки к локальному запуску приложения Microsoft Teams, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="32918-459">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="32918-460">В окне терминала перейдите к каталогу, в котором вы `ngrok.exe` установили.</span><span class="sxs-lookup"><span data-stu-id="32918-460">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="32918-461">Мы предлагаем указать на *него* путь переменной среды.</span><span class="sxs-lookup"><span data-stu-id="32918-461">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="32918-462">Запустите, например, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="32918-462">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="32918-463">Замените номер порта по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="32918-463">Replace the port number as needed.</span></span>
<span data-ttu-id="32918-464">В этом случае запускается ngrok для прослушивания в порту, который вы указываете.</span><span class="sxs-lookup"><span data-stu-id="32918-464">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="32918-465">Взамен он предоставляет внешне адресируемый URL-адрес, допустимый до тех пор, пока запущен ngrok.</span><span class="sxs-lookup"><span data-stu-id="32918-465">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="32918-466">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-466">The following image is an example:</span></span>

    ![teams bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="32918-468">.</span><span class="sxs-lookup"><span data-stu-id="32918-468">.</span></span>

1. <span data-ttu-id="32918-469">Скопируйте адрес HTTPS-переададки.</span><span class="sxs-lookup"><span data-stu-id="32918-469">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="32918-470">Он должен быть похож на следующее: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="32918-470">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="32918-471">Приложение `/api/messages` для получения `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="32918-471">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="32918-472">Это **конечная точка** сообщений для бота, запущенного локально на компьютере и достигаемого через Интернет в чате в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="32918-472">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="32918-473">Последний шаг для выполнения — обновление конечной точки сообщений развернутого бота.</span><span class="sxs-lookup"><span data-stu-id="32918-473">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="32918-474">В примере мы развернули бот в Azure.</span><span class="sxs-lookup"><span data-stu-id="32918-474">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="32918-475">Итак, \*\*давайте выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="32918-475">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="32918-476">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="32918-476">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="32918-477">Выберите **регистрацию бот-канала.**</span><span class="sxs-lookup"><span data-stu-id="32918-477">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="32918-478">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="32918-478">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="32918-479">В правой панели в конечную точку **обмена** сообщениями введите URL-адрес ngrok в нашем `https://dea822bf.ngrok.io/api/messages` примере.</span><span class="sxs-lookup"><span data-stu-id="32918-479">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="32918-480">Запустите бот локально, например в режиме Visual Studio отлаживания.</span><span class="sxs-lookup"><span data-stu-id="32918-480">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="32918-481">Тестирование бота при локальном запуске с помощью тестового веб-чата портала Bot **Framework.**</span><span class="sxs-lookup"><span data-stu-id="32918-481">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="32918-482">Как и эмулятор, этот тест не позволяет получить доступ к функциональным возможностям, определенным для Teams.</span><span class="sxs-lookup"><span data-stu-id="32918-482">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="32918-483">В окне терминала, где работает, можно увидеть трафик HTTP между `ngrok` ботом и клиентом веб-чата.</span><span class="sxs-lookup"><span data-stu-id="32918-483">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="32918-484">Если вам нужно более подробное представление, в окно браузера введите `http://127.0.0.1:4040` вас, полученную из предыдущего окна терминала.</span><span class="sxs-lookup"><span data-stu-id="32918-484">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="32918-485">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="32918-485">The following image is an example:</span></span>

    ![Auth bot teams ngrok testing](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="32918-487">.</span><span class="sxs-lookup"><span data-stu-id="32918-487">.</span></span>

> [!NOTE]
> <span data-ttu-id="32918-488">Если остановить и перезапустить ngrok, URL-адрес изменится.</span><span class="sxs-lookup"><span data-stu-id="32918-488">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="32918-489">Чтобы использовать ngrok в проекте и в зависимости от возможностей, которые вы используете, необходимо обновить все ссылки на URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="32918-489">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="32918-490">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="32918-490">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="32918-491">TeamsAppManifest/manifest.js</span><span class="sxs-lookup"><span data-stu-id="32918-491">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="32918-492">В этом манифесте содержатся сведения, необходимые Microsoft Teams для подключения к боту.</span><span class="sxs-lookup"><span data-stu-id="32918-492">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0.0",
  "id": "",
  "packageName": "com.teams.auth.bot",
  "developer": {
    "name": "TeamsBotAuth",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.teams.com/privacy",
    "termsOfUseUrl": "https://www.teams.com/termsofuse"
  },
  "icons": {
    "color": "color.png",
    "outline": "outline.png"
  },
  "name": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "description": {
    "short": "TeamsBotAuth",
    "full": "Teams Bot Authentication"
  },
  "accentColor": "#FFFFFF",
  "bots": [
    {
      "botId": "",
      "scopes": [
        "groupchat",
        "team"
      ],
      "supportsFiles": false,
      "isNotificationOnly": false
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [ "token.botframework.com" ]
}
```

<span data-ttu-id="32918-493">В результате проверки подлинности Teams ведет себя немного иначе, чем другие каналы, как поясняется ниже.</span><span class="sxs-lookup"><span data-stu-id="32918-493">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="32918-494">Обработка действия вызовов</span><span class="sxs-lookup"><span data-stu-id="32918-494">Handling Invoke Activity</span></span>

<span data-ttu-id="32918-495">Действие **invoke отправляется** боту, а не действию событий, используемой другими каналами.</span><span class="sxs-lookup"><span data-stu-id="32918-495">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="32918-496">Это делается путем подклассинга **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="32918-496">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="32918-497">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="32918-497">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="32918-498">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="32918-498">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="32918-499">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="32918-499">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="32918-500">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="32918-500">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="32918-501">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="32918-501">TeamsActivityHandler.cs</span></span>

```csharp

protected virtual Task OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    switch (turnContext.Activity.Name)
    {
        case "signin/verifyState":
            return OnSigninVerifyStateAsync(turnContext, cancellationToken);

        default:
            return Task.CompletedTask;
    }
}

protected virtual Task OnSigninVerifyStateAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    return Task.CompletedTask;
}
```

# <a name="javascript"></a>[<span data-ttu-id="32918-502">JavaScript</span><span class="sxs-lookup"><span data-stu-id="32918-502">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="32918-503">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="32918-503">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="32918-504">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="32918-504">**bots/teamsBot.js**</span></span>

<span data-ttu-id="32918-505">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="32918-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="32918-506">**диалоги/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="32918-506">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="32918-507">В диалоговом шаге используйте `beginDialog` для запуска запроса OAuth, в котором пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="32918-507">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="32918-508">Если пользователь уже подписан, это создает событие отклика маркеров без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-508">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="32918-509">В противном случае пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="32918-509">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="32918-510">Служба ботов Azure отправляет событие отклика маркера после попытки пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="32918-510">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="32918-511">В следующем диалоговом шаге проверьте наличие маркера в результате предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="32918-511">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="32918-512">Если это не null, пользователь успешно вписался.</span><span class="sxs-lookup"><span data-stu-id="32918-512">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="32918-513">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="32918-513">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="32918-514">Python</span><span class="sxs-lookup"><span data-stu-id="32918-514">Python</span></span>](#tab/python-sample)

<span data-ttu-id="32918-515">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="32918-515">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="32918-516">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="32918-516">**bots/teams_bot.py**</span></span>

<span data-ttu-id="32918-517">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="32918-517">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="32918-518">**диалоги/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="32918-518">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="32918-519">В диалоговом шаге используйте `begin_dialog` для запуска запроса OAuth, в котором пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="32918-519">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="32918-520">Если пользователь уже подписан, это создает событие отклика маркеров без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="32918-520">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="32918-521">В противном случае пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="32918-521">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="32918-522">Служба ботов Azure отправляет событие отклика маркера после попытки пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="32918-522">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="32918-523">В следующем диалоговом шаге проверьте наличие маркера в результате предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="32918-523">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="32918-524">Если это не null, пользователь успешно вписался.</span><span class="sxs-lookup"><span data-stu-id="32918-524">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="32918-525">**диалоги/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="32918-525">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

> [!div class="nextstepaction"]
> [<span data-ttu-id="32918-526">Узнайте о добавлении проверки подлинности с помощью службы Azure Bot</span><span class="sxs-lookup"><span data-stu-id="32918-526">Learn about adding authentication via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
