---
title: Добавление проверки подлинности в Teams бота
author: clearab
description: Добавление проверки подлинности OAuth в бот в Microsoft Teams.
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 36cb6f3de6f97af1d01512175923b79f69f630ad
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566006"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="92118-103">Добавление проверки подлинности в Teams бота</span><span class="sxs-lookup"><span data-stu-id="92118-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="92118-104">Иногда может потребоваться создать в Microsoft Teams боты, которые могут получать доступ к ресурсам от имени пользователя, например к почтовой службе.</span><span class="sxs-lookup"><span data-stu-id="92118-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="92118-105">В этой статье показано, как использовать проверку подлинности Azure Bot Service v4 SDK на основе OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="92118-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="92118-106">Это упрощает разработку бота, который может использовать маркеры проверки подлинности на основе учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="92118-107">Ключом во всем этом является использование поставщиков **удостоверений,** как мы увидим позже.</span><span class="sxs-lookup"><span data-stu-id="92118-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="92118-108">OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="92118-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="92118-109">Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="92118-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="92118-110">В этой области см. упрощенную версию [OAuth 2](https://aka.ms/oauth2-simplified) для базового понимания и [OAuth 2.0](https://oauth.net/2/) для полной спецификации.</span><span class="sxs-lookup"><span data-stu-id="92118-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="92118-111">Дополнительные сведения о том, как служба Azure Bot обрабатывает проверку подлинности, см. в записи проверки подлинности пользователей [в ходе беседы.](https://aka.ms/azure-bot-authentication)</span><span class="sxs-lookup"><span data-stu-id="92118-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="92118-112">В данной статье вы узнаете следующее.</span><span class="sxs-lookup"><span data-stu-id="92118-112">In this article you'll learn:</span></span>

- <span data-ttu-id="92118-113">**Создание бота с поддержкой проверки подлинности.**</span><span class="sxs-lookup"><span data-stu-id="92118-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="92118-114">Вы будете использовать [cs-auth-sample][teams-auth-bot-cs] для обработки учетных данных входа пользователя и создания маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-114">You'll use [cs-auth-sample][teams-auth-bot-cs] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="92118-115">**Развертывание бота в Azure и его связывание с поставщиком удостоверений.**</span><span class="sxs-lookup"><span data-stu-id="92118-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="92118-116">Поставщик выдает маркер на основе учетных данных входа пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="92118-117">Бот может использовать маркер для доступа к ресурсам, например к почтовой службе, для которой требуется проверка подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="92118-118">Дополнительные сведения [см. Microsoft Teams поток проверки подлинности для ботов.](auth-flow-bot.md)</span><span class="sxs-lookup"><span data-stu-id="92118-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="92118-119">**Интеграция бота в Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="92118-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="92118-120">После интеграции бота можно войти и обмениваться сообщениями с ним в чате.</span><span class="sxs-lookup"><span data-stu-id="92118-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="92118-121">Предварительные условия</span><span class="sxs-lookup"><span data-stu-id="92118-121">Prerequisites</span></span>

- <span data-ttu-id="92118-122">Знание основ [бота,][concept-basics] [управление состоянием,][concept-state]библиотека диалогов [и][concept-dialogs]реализация [последовательного потока беседы.][simple-dialog]</span><span class="sxs-lookup"><span data-stu-id="92118-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="92118-123">Знание разработки Azure и OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="92118-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="92118-124">Текущие версии Visual Studio Git.</span><span class="sxs-lookup"><span data-stu-id="92118-124">The current versions of Visual Studio and Git.</span></span>
- <span data-ttu-id="92118-125">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="92118-125">Azure account.</span></span> <span data-ttu-id="92118-126">При необходимости можно создать бесплатную учетную запись [Azure.](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="92118-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="92118-127">Следующий пример:</span><span class="sxs-lookup"><span data-stu-id="92118-127">The following sample:</span></span>

    | <span data-ttu-id="92118-128">Пример</span><span class="sxs-lookup"><span data-stu-id="92118-128">Sample</span></span> | <span data-ttu-id="92118-129">Версия BotBuilder</span><span class="sxs-lookup"><span data-stu-id="92118-129">BotBuilder version</span></span> | <span data-ttu-id="92118-130">Демонстрация</span><span class="sxs-lookup"><span data-stu-id="92118-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="92118-131">**Проверка подлинности ботов** [в cs-auth-sample][teams-auth-bot-cs]</span><span class="sxs-lookup"><span data-stu-id="92118-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot-cs]</span></span> | <span data-ttu-id="92118-132">v4</span><span class="sxs-lookup"><span data-stu-id="92118-132">v4</span></span> | <span data-ttu-id="92118-133">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="92118-133">OAuthCard support</span></span> |
    | <span data-ttu-id="92118-134">**Проверка подлинности ботов** [в примере js-auth][teams-auth-bot-js]</span><span class="sxs-lookup"><span data-stu-id="92118-134">**Bot authentication** in [js-auth-sample][teams-auth-bot-js]</span></span> | <span data-ttu-id="92118-135">v4</span><span class="sxs-lookup"><span data-stu-id="92118-135">v4</span></span>| <span data-ttu-id="92118-136">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="92118-136">OAuthCard support</span></span>  |
    | <span data-ttu-id="92118-137">**Проверка подлинности ботов** [в py-auth-sample][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="92118-137">**Bot authentication** in [py-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="92118-138">v4</span><span class="sxs-lookup"><span data-stu-id="92118-138">v4</span></span> | <span data-ttu-id="92118-139">Поддержка OAuthCard</span><span class="sxs-lookup"><span data-stu-id="92118-139">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="92118-140">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="92118-140">Create the resource group</span></span>

<span data-ttu-id="92118-141">Группа ресурсов и план службы не являются строго необходимыми, но они позволяют удобно выпускать ресурсы, которые вы создаете.</span><span class="sxs-lookup"><span data-stu-id="92118-141">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="92118-142">Это хорошая практика для сохраняющихся и управляемых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92118-142">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="92118-143">Вы используете группу ресурсов для создания отдельных ресурсов для Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="92118-143">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="92118-144">Для производительности убедитесь, что эти ресурсы находятся в одном регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="92118-144">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="92118-145">В браузере вопишитесь на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="92118-145">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="92118-146">В левой панели навигации выберите **группы Ресурсов.**</span><span class="sxs-lookup"><span data-stu-id="92118-146">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="92118-147">В верхней левой части отображаемого окна выберите вкладку **Добавить,** чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92118-147">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="92118-148">Вам будет предложено предоставить следующее:</span><span class="sxs-lookup"><span data-stu-id="92118-148">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="92118-149">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="92118-149">**Subscription**.</span></span> <span data-ttu-id="92118-150">Используйте существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="92118-150">Use your existing subscription.</span></span>
    1. <span data-ttu-id="92118-151">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="92118-151">**Resource group**.</span></span> <span data-ttu-id="92118-152">Введите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92118-152">Enter the name for the resource group.</span></span> <span data-ttu-id="92118-153">Примером может быть  *TeamsResourceGroup*.</span><span class="sxs-lookup"><span data-stu-id="92118-153">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="92118-154">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="92118-154">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="92118-155">Из **выпадаемого** меню Region выберите *Запад США* или регион, близкий к вашим приложениям.</span><span class="sxs-lookup"><span data-stu-id="92118-155">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="92118-156">Выберите **кнопку Обзор и создайте** кнопку.</span><span class="sxs-lookup"><span data-stu-id="92118-156">Select the **Review and create** button.</span></span> <span data-ttu-id="92118-157">Вы должны увидеть баннер, который считывал *пройденную проверку.*</span><span class="sxs-lookup"><span data-stu-id="92118-157">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="92118-158">Выберите **кнопку Создать.**</span><span class="sxs-lookup"><span data-stu-id="92118-158">Select the **Create** button.</span></span> <span data-ttu-id="92118-159">Создание группы ресурсов может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="92118-159">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="92118-160">Как и в случае с ресурсами, которые будут создаваться в этом руководстве, для легкого доступа к этой группе ресурсов необходимо прикрепить эту группу ресурсов к панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="92118-160">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="92118-161">Если вы хотите это сделать, выберите значок пин-&#128204; в правом верхнем справа от панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="92118-161">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="92118-162">Создание плана службы</span><span class="sxs-lookup"><span data-stu-id="92118-162">Create the service plan</span></span>

1. <span data-ttu-id="92118-163">На [**портале Azure**][azure-portal]на левой панели навигации выберите **Создание ресурса.**</span><span class="sxs-lookup"><span data-stu-id="92118-163">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="92118-164">В поле поиска введите *план службы приложения.*</span><span class="sxs-lookup"><span data-stu-id="92118-164">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="92118-165">Выберите карту **плана службы приложений** из результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="92118-165">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="92118-166">Выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="92118-166">Select **Create**.</span></span>
1. <span data-ttu-id="92118-167">Вам будет предложено предоставить следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="92118-167">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="92118-168">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="92118-168">**Subscription**.</span></span> <span data-ttu-id="92118-169">Можно использовать существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="92118-169">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="92118-170">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="92118-170">**Resource Group**.</span></span> <span data-ttu-id="92118-171">Выберите группу, созданную ранее.</span><span class="sxs-lookup"><span data-stu-id="92118-171">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="92118-172">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="92118-172">**Name**.</span></span> <span data-ttu-id="92118-173">Введите имя для плана службы.</span><span class="sxs-lookup"><span data-stu-id="92118-173">Enter the name for the service plan.</span></span> <span data-ttu-id="92118-174">Примером может быть  *TeamsServicePlan*.</span><span class="sxs-lookup"><span data-stu-id="92118-174">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="92118-175">Помните, что имя должно быть уникальным в группе.</span><span class="sxs-lookup"><span data-stu-id="92118-175">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="92118-176">**Операционная система**.</span><span class="sxs-lookup"><span data-stu-id="92118-176">**Operating System**.</span></span> <span data-ttu-id="92118-177">Выберите *Windows* или применимую ОС.</span><span class="sxs-lookup"><span data-stu-id="92118-177">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="92118-178">**Область**.</span><span class="sxs-lookup"><span data-stu-id="92118-178">**Region**.</span></span> <span data-ttu-id="92118-179">Выберите *Запад США* или регион, близкий к приложениям.</span><span class="sxs-lookup"><span data-stu-id="92118-179">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="92118-180">**Уровень цен.**</span><span class="sxs-lookup"><span data-stu-id="92118-180">**Pricing Tier**.</span></span> <span data-ttu-id="92118-181">Убедитесь, *что выбран стандартный S1.*</span><span class="sxs-lookup"><span data-stu-id="92118-181">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="92118-182">Это должно быть значение по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="92118-182">This should be the default value.</span></span>
    1. <span data-ttu-id="92118-183">Выберите **кнопку Обзор и создайте** кнопку.</span><span class="sxs-lookup"><span data-stu-id="92118-183">Select the **Review and create** button.</span></span> <span data-ttu-id="92118-184">Вы должны увидеть баннер, который считывал *пройденную проверку.*</span><span class="sxs-lookup"><span data-stu-id="92118-184">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="92118-185">Выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="92118-185">Select **Create**.</span></span> <span data-ttu-id="92118-186">Создание плана службы приложений может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="92118-186">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="92118-187">План будет указан в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92118-187">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="92118-188">Создание регистрации каналов бота</span><span class="sxs-lookup"><span data-stu-id="92118-188">Create the bot channels registration</span></span>

<span data-ttu-id="92118-189">Регистрация каналов бота регистрирует веб-службу в качестве бота с помощью bot Framework при условии, что у вас есть код Microsoft App и пароль приложения (секрет клиента).</span><span class="sxs-lookup"><span data-stu-id="92118-189">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="92118-190">Необходимо зарегистрировать бот только в том случае, если он не находится в Azure.</span><span class="sxs-lookup"><span data-stu-id="92118-190">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="92118-191">Если вы [создали бот через](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) портал Azure, он уже зарегистрирован в службе.</span><span class="sxs-lookup"><span data-stu-id="92118-191">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0&preserve-view=true) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="92118-192">Если вы создали бот через [bot Framework](https://dev.botframework.com/bots/new) или [AppStudio,](~/concepts/build-and-test/app-studio-overview.md) ваш бот не зарегистрирован в Azure.</span><span class="sxs-lookup"><span data-stu-id="92118-192">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

> [!NOTE]
> <span data-ttu-id="92118-193">Ресурс регистрации каналов ботов будет показывать **глобальный** регион, даже если вы выбрали Западный США.</span><span class="sxs-lookup"><span data-stu-id="92118-193">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="92118-194">Это ожидаемо.</span><span class="sxs-lookup"><span data-stu-id="92118-194">This is expected.</span></span>

<span data-ttu-id="92118-195">Дополнительные сведения см. в дополнительных сведениях о создании [бота для Teams.](../create-a-bot-for-teams.md)</span><span class="sxs-lookup"><span data-stu-id="92118-195">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="92118-196">Создание поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="92118-196">Create the identity provider</span></span>

<span data-ttu-id="92118-197">Вам нужен поставщик удостоверений, который можно использовать для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-197">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="92118-198">В этой процедуре вы будете использовать поставщика Azure AD; другие поставщики удостоверений, поддерживаемые Azure AD, также могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="92118-198">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="92118-199">На [**портале Azure**][azure-portal]на левой панели навигации выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92118-199">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="92118-200">Необходимо создать и зарегистрировать этот ресурс Azure AD в клиенте, в котором вы можете дать согласие на делегирование разрешений, запрашиваемого приложением.</span><span class="sxs-lookup"><span data-stu-id="92118-200">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="92118-201">Инструкции по созданию клиента см. в [сайте Access the portal и create a tenant.](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)</span><span class="sxs-lookup"><span data-stu-id="92118-201">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="92118-202">В левой панели выберите **регистрации приложений.**</span><span class="sxs-lookup"><span data-stu-id="92118-202">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="92118-203">В правой панели выберите вкладку **Новая регистрация** в верхней левой части.</span><span class="sxs-lookup"><span data-stu-id="92118-203">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="92118-204">Вам будет предложено предоставить следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="92118-204">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="92118-205">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="92118-205">**Name**.</span></span> <span data-ttu-id="92118-206">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="92118-206">Enter the name for the application.</span></span> <span data-ttu-id="92118-207">Примером может быть *botTeamsIdentity.*</span><span class="sxs-lookup"><span data-stu-id="92118-207">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="92118-208">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="92118-208">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="92118-209">Выберите типы **поддерживаемых учетных записей** для приложения.</span><span class="sxs-lookup"><span data-stu-id="92118-209">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="92118-210">Выберите учетные записи в любом организационном каталоге *(любой каталог Azure AD - Multitenant)* и личных учетных записях Майкрософт (например, Skype Xbox).</span><span class="sxs-lookup"><span data-stu-id="92118-210">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="92118-211">Для **URI перенаправления:**</span><span class="sxs-lookup"><span data-stu-id="92118-211">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="92118-212">&#x2713;Выберите **Веб**.</span><span class="sxs-lookup"><span data-stu-id="92118-212">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="92118-213">&#x2713; установите URL-адрес. `https://token.botframework.com/.auth/web/redirect`</span><span class="sxs-lookup"><span data-stu-id="92118-213">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="92118-214">Нажмите **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="92118-214">Select **Register**.</span></span>

1. <span data-ttu-id="92118-215">После создания Azure отображает страницу **Обзор** для приложения.</span><span class="sxs-lookup"><span data-stu-id="92118-215">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="92118-216">Копирование и сохранение следующих сведений в файле:</span><span class="sxs-lookup"><span data-stu-id="92118-216">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="92118-217">Значение **ID приложения (клиента).**</span><span class="sxs-lookup"><span data-stu-id="92118-217">The **Application (client) ID** value.</span></span> <span data-ttu-id="92118-218">Это значение будет позже  использовать в качестве идентификатора клиента при регистрации этого приложения удостоверений Azure в боте.</span><span class="sxs-lookup"><span data-stu-id="92118-218">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="92118-219">**ID-значение Directory (tenant).**</span><span class="sxs-lookup"><span data-stu-id="92118-219">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="92118-220">Это значение также будет позже использовать в качестве идентификатора *клиента* для регистрации этого приложения удостоверений Azure в боте.</span><span class="sxs-lookup"><span data-stu-id="92118-220">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="92118-221">На левой панели выберите **сертификаты &,** чтобы создать клиентскую тайну для приложения.</span><span class="sxs-lookup"><span data-stu-id="92118-221">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="92118-222">В **статье Секреты клиента** выберите &#x2795; новый секрет **клиента**.</span><span class="sxs-lookup"><span data-stu-id="92118-222">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="92118-223">Добавьте описание, чтобы идентифицировать этот секрет от других пользователей, которые могут потребоваться создать для этого приложения, например приложения удостоверения *бота* в Teams .</span><span class="sxs-lookup"><span data-stu-id="92118-223">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="92118-224">Срок **действия набора истекает** в выборе.</span><span class="sxs-lookup"><span data-stu-id="92118-224">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="92118-225">Нажмите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="92118-225">Select **Add**.</span></span>
   1. <span data-ttu-id="92118-226">Перед выходом с этой страницы **зафиксировать секрет**.</span><span class="sxs-lookup"><span data-stu-id="92118-226">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="92118-227">Это значение будет позже использовать в качестве секрета _клиента_ при регистрации приложения Azure AD в боте.</span><span class="sxs-lookup"><span data-stu-id="92118-227">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="92118-228">Настройка подключения поставщика удостоверений и регистрация его с помощью бота</span><span class="sxs-lookup"><span data-stu-id="92118-228">Configure the identity provider connection and register it with the bot</span></span>

<span data-ttu-id="92118-229">Примечание. Существует два варианта для поставщиков услуг здесь: Azure AD V1 и Azure AD V2.</span><span class="sxs-lookup"><span data-stu-id="92118-229">Note-there are two options for Service Providers here-Azure AD V1 and Azure AD V2.</span></span>  <span data-ttu-id="92118-230">Здесь резюмируют различия между [](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison)двумя поставщиками, но в целом V2 обеспечивает большую гибкость в отношении изменения разрешений ботов.</span><span class="sxs-lookup"><span data-stu-id="92118-230">The differences between the two providers are summarized [here](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison), but in general, V2 provides more flexibility with respect to changing bot permissions.</span></span>  <span data-ttu-id="92118-231">Graph Разрешения API перечислены в поле областей, и по мере их добавлений боты позволяют пользователям соглашаться на новые разрешения при следующем входе.</span><span class="sxs-lookup"><span data-stu-id="92118-231">Graph API permissions are listed in the scopes field, and as new ones are added, bots will allow users to consent to the new permissions on the next sign in.</span></span>  <span data-ttu-id="92118-232">Для V1 согласие бота должно быть удалено пользователем для получения новых разрешений, которые будут предложены в диалоговом окне OAuth.</span><span class="sxs-lookup"><span data-stu-id="92118-232">For V1, the bot consent must be deleted by the user for new permissions to be prompted in the OAuth dialog.</span></span> 

#### <a name="azure-ad-v1"></a><span data-ttu-id="92118-233">Azure AD V1</span><span class="sxs-lookup"><span data-stu-id="92118-233">Azure AD V1</span></span>

1. <span data-ttu-id="92118-234">На [**портале Azure**][azure-portal]выберите группу ресурсов из панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="92118-234">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="92118-235">Выберите ссылку на регистрацию канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-235">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="92118-236">Откройте страницу ресурса и выберите **Конфигурация** в **Параметры.**</span><span class="sxs-lookup"><span data-stu-id="92118-236">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="92118-237">Выберите **Добавить подключение OAuth Параметры**.</span><span class="sxs-lookup"><span data-stu-id="92118-237">Select **Add OAuth Connection Settings**.</span></span>    
<span data-ttu-id="92118-238">На следующей странице ресурса отображается соответствующий выбор:</span><span class="sxs-lookup"><span data-stu-id="92118-238">The following image displays the corresponding selection in the resource page:</span></span>  
<span data-ttu-id="92118-239">![Конфигурация SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="92118-239">![SampleAppDemoBot configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span>
1. <span data-ttu-id="92118-240">Заполните форму следующим образом:</span><span class="sxs-lookup"><span data-stu-id="92118-240">Complete the form as follows:</span></span>

    1. <span data-ttu-id="92118-241">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="92118-241">**Name**.</span></span> <span data-ttu-id="92118-242">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="92118-242">Enter a name for the connection.</span></span> <span data-ttu-id="92118-243">Вы будете использовать это имя в боте в `appsettings.json` файле.</span><span class="sxs-lookup"><span data-stu-id="92118-243">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="92118-244">Например, *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="92118-244">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="92118-245">**Поставщик услуг**.</span><span class="sxs-lookup"><span data-stu-id="92118-245">**Service Provider**.</span></span> <span data-ttu-id="92118-246">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="92118-246">Select **Azure Active Directory**.</span></span> <span data-ttu-id="92118-247">После этого будут отображаться поля Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92118-247">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="92118-248">**Client id**. Введите идентификатор приложения (клиента), записанный для приложения-поставщика удостоверений Azure в вышеуказанных действиях.</span><span class="sxs-lookup"><span data-stu-id="92118-248">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="92118-249">**Секрет клиента.**</span><span class="sxs-lookup"><span data-stu-id="92118-249">**Client secret**.</span></span> <span data-ttu-id="92118-250">Введите секрет, записанный для приложения-поставщика удостоверений Azure в шагах выше.</span><span class="sxs-lookup"><span data-stu-id="92118-250">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="92118-251">**Тип гранта**.</span><span class="sxs-lookup"><span data-stu-id="92118-251">**Grant Type**.</span></span> <span data-ttu-id="92118-252">Введите `authorization_code` .</span><span class="sxs-lookup"><span data-stu-id="92118-252">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="92118-253">**URL-адрес входа.**</span><span class="sxs-lookup"><span data-stu-id="92118-253">**Login URL**.</span></span> <span data-ttu-id="92118-254">Введите `https://login.microsoftonline.com` .</span><span class="sxs-lookup"><span data-stu-id="92118-254">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="92118-255">**Идентификатор клиента** введите идентификатор **Directory (tenant),** записанный ранее для приложения  удостоверений Azure или распространенный в зависимости от поддерживаемого типа учетной записи, выбранного при создания приложения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="92118-255">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="92118-256">Чтобы определить, какое значение назначить, выполните указанные критерии:</span><span class="sxs-lookup"><span data-stu-id="92118-256">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="92118-257">Если вы выбрали только учетные записи в этом организационном каталоге (только Microsoft - один *клиент)* или учетные записи в любом организационном каталоге *(каталог Microsoft AAD . Multi tenant)* введите **ID** клиента, записанный ранее для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="92118-257">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="92118-258">Это будет клиент, связанный с пользователями, которые могут быть проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-258">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="92118-259">Если вы выбрали учетные записи в любом организационном каталоге (любой каталог AAD - Multi *tenant and personal Microsoft accounts, например Skype, Xbox, Outlook)* введите слово **common,** а не iD клиента.</span><span class="sxs-lookup"><span data-stu-id="92118-259">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="92118-260">В противном случае приложение AAD проверяется через клиента, у которого был выбран ID, и исключает личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92118-260">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="92118-261">з.</span><span class="sxs-lookup"><span data-stu-id="92118-261">h.</span></span> <span data-ttu-id="92118-262">Для **URL-адреса ресурса** введите `https://graph.microsoft.com/` .</span><span class="sxs-lookup"><span data-stu-id="92118-262">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="92118-263">Это не используется в текущем примере кода.</span><span class="sxs-lookup"><span data-stu-id="92118-263">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="92118-264">и.</span><span class="sxs-lookup"><span data-stu-id="92118-264">i.</span></span> <span data-ttu-id="92118-265">Оставьте **области пустыми.**</span><span class="sxs-lookup"><span data-stu-id="92118-265">Leave **Scopes** blank.</span></span> <span data-ttu-id="92118-266">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-266">The following image is an example:</span></span>

    ![teams bots app auth connection string adv1 view](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="92118-268">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="92118-268">Select **Save**.</span></span>

#### <a name="azure-ad-v2"></a><span data-ttu-id="92118-269">Azure AD V2</span><span class="sxs-lookup"><span data-stu-id="92118-269">Azure AD V2</span></span>

1. <span data-ttu-id="92118-270">На [**портале Azure**][azure-portal]выберите группу ресурсов из панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="92118-270">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="92118-271">Выберите ссылку на регистрацию канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-271">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="92118-272">Откройте страницу ресурса и выберите **Конфигурация** в **Параметры.**</span><span class="sxs-lookup"><span data-stu-id="92118-272">Open the resource page and select **Configuration** under **Settings**.</span></span> 
1. <span data-ttu-id="92118-273">Выберите **Добавить подключение OAuth Параметры**.</span><span class="sxs-lookup"><span data-stu-id="92118-273">Select **Add OAuth Connection Settings**.</span></span>  
<span data-ttu-id="92118-274">На следующей странице ресурса отображается соответствующий выбор:</span><span class="sxs-lookup"><span data-stu-id="92118-274">The following image displays the corresponding selection in the resource page:</span></span>        
<span data-ttu-id="92118-275">![Конфигурация SampleAppDemoBot](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span><span class="sxs-lookup"><span data-stu-id="92118-275">![SampleAppDemoBot Configuration](~/assets/images/authentication/sample-app-demo-bot-configuration.png)</span></span> 

1. <span data-ttu-id="92118-276">Заполните форму следующим образом:</span><span class="sxs-lookup"><span data-stu-id="92118-276">Complete the form as follows:</span></span>

    1. <span data-ttu-id="92118-277">**Имя**.</span><span class="sxs-lookup"><span data-stu-id="92118-277">**Name**.</span></span> <span data-ttu-id="92118-278">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="92118-278">Enter a name for the connection.</span></span> <span data-ttu-id="92118-279">Вы будете использовать это имя в боте в `appsettings.json` файле.</span><span class="sxs-lookup"><span data-stu-id="92118-279">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="92118-280">Например *BotTeamsAuthADv2*.</span><span class="sxs-lookup"><span data-stu-id="92118-280">For example *BotTeamsAuthADv2*.</span></span>
    1. <span data-ttu-id="92118-281">**Поставщик услуг**.</span><span class="sxs-lookup"><span data-stu-id="92118-281">**Service Provider**.</span></span> <span data-ttu-id="92118-282">Выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="92118-282">Select **Azure Active Directory v2**.</span></span> <span data-ttu-id="92118-283">После этого будут отображаться поля Azure AD.</span><span class="sxs-lookup"><span data-stu-id="92118-283">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="92118-284">**Client id**. Введите идентификатор приложения (клиента), записанный для приложения-поставщика удостоверений Azure в вышеуказанных действиях.</span><span class="sxs-lookup"><span data-stu-id="92118-284">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="92118-285">**Секрет клиента.**</span><span class="sxs-lookup"><span data-stu-id="92118-285">**Client secret**.</span></span> <span data-ttu-id="92118-286">Введите секрет, записанный для приложения-поставщика удостоверений Azure в шагах выше.</span><span class="sxs-lookup"><span data-stu-id="92118-286">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="92118-287">**URL Exchange маркера**.</span><span class="sxs-lookup"><span data-stu-id="92118-287">**Token Exchange URL**.</span></span> <span data-ttu-id="92118-288">Оставьте этот пробел.</span><span class="sxs-lookup"><span data-stu-id="92118-288">Leave this blank.</span></span>
    1. <span data-ttu-id="92118-289">**Идентификатор клиента** введите идентификатор **Directory (tenant),** записанный ранее для приложения  удостоверений Azure или распространенный в зависимости от поддерживаемого типа учетной записи, выбранного при создания приложения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="92118-289">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="92118-290">Чтобы определить, какое значение назначить, выполните указанные критерии:</span><span class="sxs-lookup"><span data-stu-id="92118-290">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="92118-291">Если вы выбрали только учетные записи в этом организационном каталоге (только Microsoft - один *клиент)* или учетные записи в любом организационном каталоге *(каталог Microsoft AAD . Multi tenant)* введите **ID** клиента, записанный ранее для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="92118-291">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="92118-292">Это будет клиент, связанный с пользователями, которые могут быть проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-292">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="92118-293">Если вы выбрали учетные записи в любом организационном каталоге (любой каталог AAD - Multi *tenant and personal Microsoft accounts, например Skype, Xbox, Outlook)* введите слово **common,** а не iD клиента.</span><span class="sxs-lookup"><span data-stu-id="92118-293">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="92118-294">В противном случае приложение AAD проверяется через клиента, у которого был выбран ID, и исключает личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92118-294">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    1. <span data-ttu-id="92118-295">Для **областей** введите список разрешений, относячимый к пространству, для этого приложения требуется, например: User.Read User.ReadBasic.All Mail.Read</span><span class="sxs-lookup"><span data-stu-id="92118-295">For **Scopes**, enter a space-delimited list of graph permissions this application requires e.g.: User.Read User.ReadBasic.All Mail.Read</span></span> 

1. <span data-ttu-id="92118-296">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="92118-296">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="92118-297">Тестирование подключения</span><span class="sxs-lookup"><span data-stu-id="92118-297">Test the connection</span></span>

1. <span data-ttu-id="92118-298">Выберите запись подключения, чтобы открыть только что созданное подключение.</span><span class="sxs-lookup"><span data-stu-id="92118-298">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="92118-299">Выберите **подключение к тесту** в верхней части панели **параметра подключения поставщика** услуг.</span><span class="sxs-lookup"><span data-stu-id="92118-299">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="92118-300">При первом этом откроется новое окно браузера с просьбой выбрать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="92118-300">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="92118-301">Выберите тот, который вы хотите использовать.</span><span class="sxs-lookup"><span data-stu-id="92118-301">Select the one you want to use.</span></span>
1. <span data-ttu-id="92118-302">Далее вам будет предложено разрешить поставщику удостоверений использовать данные (учетные данные).</span><span class="sxs-lookup"><span data-stu-id="92118-302">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="92118-303">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-303">The following image is an example:</span></span>

    ![teams bot auth connection string adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="92118-305">Выберите **Accept**.</span><span class="sxs-lookup"><span data-stu-id="92118-305">Select **Accept**.</span></span>
1. <span data-ttu-id="92118-306">Это должно перенаправить вас на страницу **Тестовая подключение \<your-connection-name> к успешной** странице.</span><span class="sxs-lookup"><span data-stu-id="92118-306">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="92118-307">Обновите страницу, если вы получите ошибку.</span><span class="sxs-lookup"><span data-stu-id="92118-307">Refresh the page if you get an error.</span></span> <span data-ttu-id="92118-308">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-308">The following image is an example:</span></span>

    ![teams bots app auth connection str adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="92118-310">Имя подключения используется кодом бота для получения маркеров проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="92118-310">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="92118-311">Подготовка кода образца бота</span><span class="sxs-lookup"><span data-stu-id="92118-311">Prepare the bot sample code</span></span>

<span data-ttu-id="92118-312">С помощью предварительных параметров давайте сосредоточимся на создании бота, который будет использовать в этой статье.</span><span class="sxs-lookup"><span data-stu-id="92118-312">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="92118-313">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="92118-313">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="92118-314">Клон [cs-auth-sample][teams-auth-bot-cs].</span><span class="sxs-lookup"><span data-stu-id="92118-314">Clone [cs-auth-sample][teams-auth-bot-cs].</span></span>
1. <span data-ttu-id="92118-315">Запуск Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92118-315">Launch Visual Studio.</span></span>
1. <span data-ttu-id="92118-316">На панели инструментов выберите **Файл -> Open -> Project/Solution** и откройте бот-проект.</span><span class="sxs-lookup"><span data-stu-id="92118-316">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="92118-317">В C# обновление **appsettings.jsв** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="92118-317">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="92118-318">Установите `ConnectionName` имя подключения поставщика удостоверений, добавленного к регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-318">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="92118-319">Имя, которое мы использовали в этом *примере, — BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="92118-319">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="92118-320">Установите `MicrosoftAppId` для **бота ID приложения,** сохраненного во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-320">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="92118-321">Установите `MicrosoftAppPassword` секрет **клиента,** сохраненный во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-321">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>

    <span data-ttu-id="92118-322">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="92118-322">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="92118-323">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="92118-323">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="92118-324">В обозревателе решений перейдите в папку, откройте и установите, а также в бот App ID, сохраненный во время регистрации `TeamsAppManifest` `manifest.json` канала `id` `botId` бота. </span><span class="sxs-lookup"><span data-stu-id="92118-324">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="javascript"></a>[<span data-ttu-id="92118-325">JavaScript</span><span class="sxs-lookup"><span data-stu-id="92118-325">JavaScript</span></span>](#tab/node-js)

1. <span data-ttu-id="92118-326">Клон [узла-auth-sample][teams-auth-bot-js].</span><span class="sxs-lookup"><span data-stu-id="92118-326">Clone [node-auth-sample][teams-auth-bot-js].</span></span>
1. <span data-ttu-id="92118-327">В консоли перейдите к проекту:</span><span class="sxs-lookup"><span data-stu-id="92118-327">In a console, navigate to the project:</span></span> </br></br>
`cd samples/javascript_nodejs/46.teams`  
1. <span data-ttu-id="92118-328">Установка модулей</span><span class="sxs-lookup"><span data-stu-id="92118-328">Install modules</span></span></br></br>
`npm install`
1. <span data-ttu-id="92118-329">Обновление **конфигурации .env** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="92118-329">Update the **.env** configuration as follows:</span></span>

    - <span data-ttu-id="92118-330">Установите `MicrosoftAppId` для **бота ID приложения,** сохраненного во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-330">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="92118-331">Установите `MicrosoftAppPassword` секрет **клиента,** сохраненный во время регистрации канала бота.</span><span class="sxs-lookup"><span data-stu-id="92118-331">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="92118-332">Установите имя подключения поставщика `connectionName` удостоверений.</span><span class="sxs-lookup"><span data-stu-id="92118-332">Set the `connectionName` to the name of the identity provider connection.</span></span>
    <span data-ttu-id="92118-333">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="92118-333">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="92118-334">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="92118-334">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-javascript[settings](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/.env)]

1. <span data-ttu-id="92118-335">В папке откройте и установите свой microsoft App ID и бот App `teamsAppManifest` `manifest.json` `id` **ID,** сохраненный во время регистрации канала `botId` бота. </span><span class="sxs-lookup"><span data-stu-id="92118-335">In the `teamsAppManifest` folder, open `manifest.json` and set `id`  to your **Microsoft App ID** and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="python"></a>[<span data-ttu-id="92118-336">Python</span><span class="sxs-lookup"><span data-stu-id="92118-336">Python</span></span>](#tab/python)

1. <span data-ttu-id="92118-337">Клонировать [py-auth-пример][teams-auth-bot-py] из хранилища github.</span><span class="sxs-lookup"><span data-stu-id="92118-337">Clone [py-auth-sample][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="92118-338">Обновление **config.py:**</span><span class="sxs-lookup"><span data-stu-id="92118-338">Update **config.py**:</span></span>

    - <span data-ttu-id="92118-339">`ConnectionName`Задайте имя параметра подключения OAuth, добавленного в бот.</span><span class="sxs-lookup"><span data-stu-id="92118-339">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="92118-340">Настройка и секрет приложения и ID приложения вашего `MicrosoftAppId` `MicrosoftAppPassword` бота.</span><span class="sxs-lookup"><span data-stu-id="92118-340">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="92118-341">В зависимости от символов в секрете бота может потребоваться XML-пароль.</span><span class="sxs-lookup"><span data-stu-id="92118-341">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="92118-342">Например, любые амперанды (&) должны быть закодированы как `&amp;` .</span><span class="sxs-lookup"><span data-stu-id="92118-342">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="92118-343">Развертывание бота в Azure</span><span class="sxs-lookup"><span data-stu-id="92118-343">Deploy the bot to Azure</span></span>

<span data-ttu-id="92118-344">Чтобы развернуть бот, выполните действия по развертыванию бота [в Azure.](https://aka.ms/azure-bot-deployment-cli)</span><span class="sxs-lookup"><span data-stu-id="92118-344">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="92118-345">Кроме того, в Visual Studio вы можете следовать следующим шагам:</span><span class="sxs-lookup"><span data-stu-id="92118-345">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="92118-346">В Visual Studio *Обозреватель решений* выберите и удерживайте (или правой кнопкой мыши) имя проекта.</span><span class="sxs-lookup"><span data-stu-id="92118-346">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="92118-347">В выпадаемом меню выберите **Опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="92118-347">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="92118-348">В отображаемом окне выберите новую **ссылку.**</span><span class="sxs-lookup"><span data-stu-id="92118-348">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="92118-349">В диалоговом окне выберите **Службу приложений** слева и **создайте новое** справа.</span><span class="sxs-lookup"><span data-stu-id="92118-349">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="92118-350">Выберите **кнопку Публикация.**</span><span class="sxs-lookup"><span data-stu-id="92118-350">Select the **Publish** button.</span></span>
1. <span data-ttu-id="92118-351">В следующем диалоговом окне введите требуемую информацию.</span><span class="sxs-lookup"><span data-stu-id="92118-351">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="92118-352">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="92118-352">The following is an example:</span></span>

    ![auth-app-service](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="92118-354">Выберите пункт **Создать**.</span><span class="sxs-lookup"><span data-stu-id="92118-354">Select **Create**.</span></span>
1. <span data-ttu-id="92118-355">Если развертывание успешно завершено, вы должны увидеть его отражение в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="92118-355">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="92118-356">Кроме того, страница отображается в браузере по умолчанию, *говоря, что ваш бот готов!.*</span><span class="sxs-lookup"><span data-stu-id="92118-356">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="92118-357">URL-адрес будет похож на этот: `https://botteamsauth.azurewebsites.net/` .</span><span class="sxs-lookup"><span data-stu-id="92118-357">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="92118-358">Сохраните его в файле.</span><span class="sxs-lookup"><span data-stu-id="92118-358">Save it to a file.</span></span>
1. <span data-ttu-id="92118-359">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="92118-359">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="92118-360">Проверьте группу ресурсов, бот должен быть указан вместе с другими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="92118-360">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="92118-361">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-361">The following image is an example:</span></span>

    ![teams-bot-auth-app-service-group](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="92118-363">В группе ресурсов выберите имя регистрации канала бота (ссылка).</span><span class="sxs-lookup"><span data-stu-id="92118-363">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="92118-364">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="92118-364">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="92118-365">В **окне конечной точки обмена сообщениями** введите URL-адрес, полученный выше, а затем `api/messages` .</span><span class="sxs-lookup"><span data-stu-id="92118-365">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="92118-366">Вот пример: `https://botteamsauth.azurewebsites.net/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="92118-366">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="92118-367">Выберите **кнопку Сохранить** в левом верхнем верхней части.</span><span class="sxs-lookup"><span data-stu-id="92118-367">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="92118-368">Тестирование бота с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="92118-368">Test the bot using the Emulator</span></span>

<span data-ttu-id="92118-369">Если вы еще не сделали этого, установите [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="92118-369">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="92118-370">См. [также отладку с эмулятором](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="92118-370">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="92118-371">Чтобы войти в пример бота, необходимо настроить эмулятор.</span><span class="sxs-lookup"><span data-stu-id="92118-371">In order for the bot sample login to work you must configure the Emulator.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="92118-372">Настройка эмулятора для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="92118-372">Configure the Emulator for authentication</span></span>

<span data-ttu-id="92118-373">Если боту требуется проверка подлинности, необходимо настроить эмулятор.</span><span class="sxs-lookup"><span data-stu-id="92118-373">If a bot requires authentication, you must configure the Emulator.</span></span> <span data-ttu-id="92118-374">Настройка:</span><span class="sxs-lookup"><span data-stu-id="92118-374">To configure:</span></span>

1. <span data-ttu-id="92118-375">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="92118-375">Start the Emulator.</span></span>
1. <span data-ttu-id="92118-376">В эмуляторе выберите значок шестеренки &#9881; в левом нижнем низу или вкладку **Эмулятор** Параметры в правом верхнем.</span><span class="sxs-lookup"><span data-stu-id="92118-376">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="92118-377">Проверьте поле с помощью маркеров проверки подлинности версии **1.0.**</span><span class="sxs-lookup"><span data-stu-id="92118-377">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="92118-378">Введите локальный путь к **средству ngrok.**</span><span class="sxs-lookup"><span data-stu-id="92118-378">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="92118-379">*См.* Bot Framework Emulator /ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span><span class="sxs-lookup"><span data-stu-id="92118-379">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="92118-380">Дополнительные сведения об инструментах см. [в сайте ngrok.](https://ngrok.com/)</span><span class="sxs-lookup"><span data-stu-id="92118-380">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="92118-381">Проверьте поле run **ngrok при запуске эмулятора.**</span><span class="sxs-lookup"><span data-stu-id="92118-381">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="92118-382">Выберите **кнопку Сохранить.**</span><span class="sxs-lookup"><span data-stu-id="92118-382">Select the **Save** button.</span></span>

<span data-ttu-id="92118-383">Когда бот отображает входную карточку и пользователь выбирает кнопку вход, эмулятор открывает страницу, которую пользователь может использовать для регистрации с поставщиком проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-383">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="92118-384">После этого пользователь создает маркер пользователя и отправляет его боту.</span><span class="sxs-lookup"><span data-stu-id="92118-384">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="92118-385">После этого бот может действовать от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-385">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="92118-386">Локальное тестирование бота</span><span class="sxs-lookup"><span data-stu-id="92118-386">Test the bot locally</span></span>

<span data-ttu-id="92118-387">После настройки механизма проверки подлинности можно выполнить фактическое тестирование бота.</span><span class="sxs-lookup"><span data-stu-id="92118-387">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="92118-388">Запустите образец бота локально на компьютере, Visual Studio например.</span><span class="sxs-lookup"><span data-stu-id="92118-388">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="92118-389">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="92118-389">Start the Emulator.</span></span>
1. <span data-ttu-id="92118-390">Выберите **кнопку Открыть бот.**</span><span class="sxs-lookup"><span data-stu-id="92118-390">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="92118-391">В **URL-адресе бота** введите локальный URL-адрес бота.</span><span class="sxs-lookup"><span data-stu-id="92118-391">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="92118-392">Обычно `http://localhost:3978/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="92118-392">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="92118-393">В **ID приложения Майкрософт** введите ID приложения бота из `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="92118-393">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="92118-394">В пароле **Microsoft App** введите пароль приложения бота из `appsettings.json` .</span><span class="sxs-lookup"><span data-stu-id="92118-394">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="92118-395">Выберите **Подключение**.</span><span class="sxs-lookup"><span data-stu-id="92118-395">Select **Connect**.</span></span>
1. <span data-ttu-id="92118-396">После запуска бота введите любой текст, чтобы отобразить карту входа.</span><span class="sxs-lookup"><span data-stu-id="92118-396">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="92118-397">Выберите **кнопку Вход.**</span><span class="sxs-lookup"><span data-stu-id="92118-397">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="92118-398">Всплывающее диалоговое окно отображается для подтверждения **открытого URL-адреса.**</span><span class="sxs-lookup"><span data-stu-id="92118-398">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="92118-399">Это позволяет пользователю бота (вам) быть аутентификацией.</span><span class="sxs-lookup"><span data-stu-id="92118-399">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="92118-400">Выберите **Подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="92118-400">Select **Confirm**.</span></span>
1. <span data-ttu-id="92118-401">При запросе выберите учетную запись соответствующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-401">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="92118-402">В зависимости от конфигурации эмулятора вы получаете одну из следующих конфигураций:</span><span class="sxs-lookup"><span data-stu-id="92118-402">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="92118-403">**Использование кода проверки входных данных**</span><span class="sxs-lookup"><span data-stu-id="92118-403">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="92118-404">&#x2713; открывается окно с кодом проверки.</span><span class="sxs-lookup"><span data-stu-id="92118-404">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="92118-405">&#x2713; и введите код проверки в поле чата для завершения входа.</span><span class="sxs-lookup"><span data-stu-id="92118-405">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="92118-406">**Использование маркеров проверки подлинности.**</span><span class="sxs-lookup"><span data-stu-id="92118-406">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="92118-407">&#x2713; вы вошли в систему на основе учетных данных.</span><span class="sxs-lookup"><span data-stu-id="92118-407">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="92118-408">Ниже приводится пример пользовательского интерфейса бота после входа в систему:</span><span class="sxs-lookup"><span data-stu-id="92118-408">The following image is an example of the bot UI after you've logged in:</span></span>

    ![Эмулятор входа в auth bot](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="92118-410">Если вы выберите **Да,** когда бот спросит, хотите ли вы просмотреть *маркер?* Вы получите ответ, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="92118-410">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![Маркер эмулятора входа в auth bot](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="92118-412">Введите **вход в** поле входного чата, чтобы выйти из нее. Это освобождает маркер пользователя, и бот не сможет действовать от вашего имени, пока вы не вопишите снова.</span><span class="sxs-lookup"><span data-stu-id="92118-412">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="92118-413">Проверка подлинности ботов требует использования **службы соединителя ботов.**</span><span class="sxs-lookup"><span data-stu-id="92118-413">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="92118-414">Служба имеет доступ к данным о регистрации каналов бота для вашего бота.</span><span class="sxs-lookup"><span data-stu-id="92118-414">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="92118-415">Тестирование развернутого бота</span><span class="sxs-lookup"><span data-stu-id="92118-415">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="92118-416">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="92118-416">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="92118-417">Найдите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="92118-417">Find your resource group.</span></span>
1. <span data-ttu-id="92118-418">Выберите ссылку ресурса.</span><span class="sxs-lookup"><span data-stu-id="92118-418">Select the resource link.</span></span> <span data-ttu-id="92118-419">Отображается страница ресурса.</span><span class="sxs-lookup"><span data-stu-id="92118-419">The resource page is displayed.</span></span>
1. <span data-ttu-id="92118-420">На странице ресурса выберите **Тест в веб-чате**.</span><span class="sxs-lookup"><span data-stu-id="92118-420">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="92118-421">Бот запускает и отображает заранее задавленные приветствия.</span><span class="sxs-lookup"><span data-stu-id="92118-421">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="92118-422">Введите что-либо в окне чата.</span><span class="sxs-lookup"><span data-stu-id="92118-422">Type anything in the chat box.</span></span>
1. <span data-ttu-id="92118-423">Выберите **вход в поле.**</span><span class="sxs-lookup"><span data-stu-id="92118-423">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="92118-424">Всплывающее диалоговое окно отображается для подтверждения **открытого URL-адреса.**</span><span class="sxs-lookup"><span data-stu-id="92118-424">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="92118-425">Это позволяет пользователю бота (вам) быть аутентификацией.</span><span class="sxs-lookup"><span data-stu-id="92118-425">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="92118-426">Выберите **Подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="92118-426">Select **Confirm**.</span></span>
1. <span data-ttu-id="92118-427">При запросе выберите учетную запись соответствующего пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-427">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="92118-428">Ниже приводится пример пользовательского интерфейса бота после входа в систему:</span><span class="sxs-lookup"><span data-stu-id="92118-428">The following image is an example of the bot UI after you have logged in:</span></span>

    ![Развернутый вход бота auth](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="92118-430">.</span><span class="sxs-lookup"><span data-stu-id="92118-430">.</span></span>

1. <span data-ttu-id="92118-431">Выберите **кнопку Да,** чтобы отобразить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-431">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="92118-432">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-432">The following image is an example:</span></span>

    ![Развернутый маркер входа бота auth](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="92118-434">.</span><span class="sxs-lookup"><span data-stu-id="92118-434">.</span></span>

1. <span data-ttu-id="92118-435">Введите вход, чтобы выйти.</span><span class="sxs-lookup"><span data-stu-id="92118-435">Enter logout to sign out.</span></span>

    ![развернутый журнал auth bot](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="92118-437">Если у вас возникли проблемы с входом, попробуйте проверить подключение снова, как описано в предыдущих действиях.</span><span class="sxs-lookup"><span data-stu-id="92118-437">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="92118-438">Это может воссоздать маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="92118-438">This could recreate the authentication token.</span></span>
> <span data-ttu-id="92118-439">С клиентом веб-чата Bot Framework в Azure вам может потребоваться несколько раз войти, прежде чем проверка подлинности будет установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="92118-439">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="92118-440">Установка и тестирование бота в Teams</span><span class="sxs-lookup"><span data-stu-id="92118-440">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="92118-441">В проекте бота убедитесь, что папка `TeamsAppManifest` содержит вместе `manifest.json` с `outline.png` файлами и `color.png` файлами.</span><span class="sxs-lookup"><span data-stu-id="92118-441">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="92118-442">В Обозревателе решений перейдите в `TeamsAppManifest` папку.</span><span class="sxs-lookup"><span data-stu-id="92118-442">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="92118-443">Изменить, `manifest.json` назначив следующие значения:</span><span class="sxs-lookup"><span data-stu-id="92118-443">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="92118-444">Убедитесь, что полученный во время регистрации канала бота **ID** приложения-бота назначен и `id` `botId` .</span><span class="sxs-lookup"><span data-stu-id="92118-444">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="92118-445">Назначение этого значения: `validDomains: [ "token.botframework.com" ]` .</span><span class="sxs-lookup"><span data-stu-id="92118-445">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="92118-446">Выберите и **zip** `manifest.json` , и `outline.png` `color.png` файлы.</span><span class="sxs-lookup"><span data-stu-id="92118-446">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="92118-447">Откройте **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="92118-447">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="92118-448">В левой панели в нижней части выберите **значок Apps**.</span><span class="sxs-lookup"><span data-stu-id="92118-448">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="92118-449">В правой панели в нижней части выберите Upload **настраиваемом приложении.**</span><span class="sxs-lookup"><span data-stu-id="92118-449">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="92118-450">Перейдите в `TeamsAppManifest` папку и загрузите манифест с молнией.</span><span class="sxs-lookup"><span data-stu-id="92118-450">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="92118-451">Отображается следующий мастер:</span><span class="sxs-lookup"><span data-stu-id="92118-451">The following wizard is displayed:</span></span>

    ![Отправка команд auth bot](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="92118-453">Нажмите кнопку **Добавить в группу**.</span><span class="sxs-lookup"><span data-stu-id="92118-453">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="92118-454">В следующем окне выберите команду, в которой нужно использовать бот.</span><span class="sxs-lookup"><span data-stu-id="92118-454">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="92118-455">Выберите **кнопку Настройка бота.**</span><span class="sxs-lookup"><span data-stu-id="92118-455">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="92118-456">Выберите три точки (&#x25cf;&#x25cf;&#x25cf;) в левой панели.</span><span class="sxs-lookup"><span data-stu-id="92118-456">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="92118-457">Затем выберите **значок App Studio.**</span><span class="sxs-lookup"><span data-stu-id="92118-457">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="92118-458">Выберите **вкладку Редактор Манифеста.** Вы должны увидеть значок для загруженного бота.</span><span class="sxs-lookup"><span data-stu-id="92118-458">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="92118-459">Кроме того, вы должны иметь возможность видеть бота, перечисленных в качестве контакта в списке чата, который можно использовать для обмена сообщениями с ботом.</span><span class="sxs-lookup"><span data-stu-id="92118-459">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="92118-460">Тестирование бота локально в Teams</span><span class="sxs-lookup"><span data-stu-id="92118-460">Testing the bot locally in Teams</span></span>

<span data-ttu-id="92118-461">Microsoft Teams является полностью облачным продуктом, он требует, чтобы все доступные ему службы были доступны в облаке с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="92118-461">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="92118-462">Поэтому для того, чтобы бот (наш пример) работал в Teams, необходимо либо опубликовать код в облако по вашему выбору, либо  сделать локально запущенный экземпляр внешне доступным с помощью средства туннеля.</span><span class="sxs-lookup"><span data-stu-id="92118-462">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="92118-463">Рекомендуется  [ngrok,](https://ngrok.com/download)который создает внешне адресируемый URL-адрес для порта, который вы открываете локально на компьютере.</span><span class="sxs-lookup"><span data-stu-id="92118-463">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="92118-464">Чтобы настроить ngrok в процессе подготовки к локальному Microsoft Teams приложения, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="92118-464">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="92118-465">В окне терминала перейдите к каталогу, в котором вы `ngrok.exe` установили.</span><span class="sxs-lookup"><span data-stu-id="92118-465">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="92118-466">Мы предлагаем указать на *него* путь переменной среды.</span><span class="sxs-lookup"><span data-stu-id="92118-466">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="92118-467">Запустите, например, `ngrok http 3978 --host-header=localhost:3978` .</span><span class="sxs-lookup"><span data-stu-id="92118-467">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="92118-468">Замените номер порта по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="92118-468">Replace the port number as needed.</span></span>
<span data-ttu-id="92118-469">В этом случае запускается ngrok для прослушивания в порту, который вы указываете.</span><span class="sxs-lookup"><span data-stu-id="92118-469">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="92118-470">Взамен он предоставляет внешне адресируемый URL-адрес, допустимый до тех пор, пока запущен ngrok.</span><span class="sxs-lookup"><span data-stu-id="92118-470">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="92118-471">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-471">The following image is an example:</span></span>

    ![teams bot app auth connection string adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="92118-473">.</span><span class="sxs-lookup"><span data-stu-id="92118-473">.</span></span>

1. <span data-ttu-id="92118-474">Скопируйте адрес HTTPS-переададки.</span><span class="sxs-lookup"><span data-stu-id="92118-474">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="92118-475">Он должен быть похож на следующее: `https://dea822bf.ngrok.io/` .</span><span class="sxs-lookup"><span data-stu-id="92118-475">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="92118-476">Приложение `/api/messages` для получения `https://dea822bf.ngrok.io/api/messages` .</span><span class="sxs-lookup"><span data-stu-id="92118-476">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="92118-477">Это **конечная** точка сообщений для бота, запущенного локально на вашем компьютере и достигаемого в Интернете в чате в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="92118-477">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="92118-478">Последний шаг для выполнения — обновление конечной точки сообщений развернутого бота.</span><span class="sxs-lookup"><span data-stu-id="92118-478">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="92118-479">В примере мы развернули бот в Azure.</span><span class="sxs-lookup"><span data-stu-id="92118-479">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="92118-480">Итак, \*\*давайте выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="92118-480">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="92118-481">В браузере перейдите на портал [**Azure.**][azure-portal]</span><span class="sxs-lookup"><span data-stu-id="92118-481">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="92118-482">Выберите **регистрацию бот-канала.**</span><span class="sxs-lookup"><span data-stu-id="92118-482">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="92118-483">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="92118-483">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="92118-484">В правой панели в конечную точку **обмена** сообщениями введите URL-адрес ngrok в нашем `https://dea822bf.ngrok.io/api/messages` примере.</span><span class="sxs-lookup"><span data-stu-id="92118-484">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="92118-485">Запустите бот локально, например в режиме Visual Studio отлаживания.</span><span class="sxs-lookup"><span data-stu-id="92118-485">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="92118-486">Тестирование бота при локальном запуске с помощью тестового веб-чата портала Bot **Framework.**</span><span class="sxs-lookup"><span data-stu-id="92118-486">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="92118-487">Как и эмулятор, этот тест не позволяет получить доступ к Teams определенным функциям.</span><span class="sxs-lookup"><span data-stu-id="92118-487">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="92118-488">В окне терминала, где работает, можно увидеть трафик HTTP между `ngrok` ботом и клиентом веб-чата.</span><span class="sxs-lookup"><span data-stu-id="92118-488">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="92118-489">Если вам нужно более подробное представление, в окно браузера введите `http://127.0.0.1:4040` вас, полученную из предыдущего окна терминала.</span><span class="sxs-lookup"><span data-stu-id="92118-489">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="92118-490">В качестве примера приводится следующее изображение:</span><span class="sxs-lookup"><span data-stu-id="92118-490">The following image is an example:</span></span>

    ![Auth bot teams ngrok testing](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="92118-492">.</span><span class="sxs-lookup"><span data-stu-id="92118-492">.</span></span>

> [!NOTE]
> <span data-ttu-id="92118-493">Если остановить и перезапустить ngrok, URL-адрес изменится.</span><span class="sxs-lookup"><span data-stu-id="92118-493">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="92118-494">Чтобы использовать ngrok в проекте и в зависимости от возможностей, которые вы используете, необходимо обновить все ссылки на URL-адрес.</span><span class="sxs-lookup"><span data-stu-id="92118-494">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>
 

## <a name="additional-information"></a><span data-ttu-id="92118-495">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="92118-495">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="92118-496">TeamsAppManifest/manifest.js</span><span class="sxs-lookup"><span data-stu-id="92118-496">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="92118-497">Этот манифест содержит сведения, необходимые Microsoft Teams для подключения к боту:</span><span class="sxs-lookup"><span data-stu-id="92118-497">This manifest contains information needed by Microsoft Teams to connect with the bot:</span></span>  

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

<span data-ttu-id="92118-498">При проверке подлинности Teams ведет себя немного иначе, чем по другим каналам, как поясняется ниже.</span><span class="sxs-lookup"><span data-stu-id="92118-498">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="92118-499">Обработка действия вызовов</span><span class="sxs-lookup"><span data-stu-id="92118-499">Handling Invoke Activity</span></span>

<span data-ttu-id="92118-500">Действие **invoke отправляется** боту, а не действию событий, используемой другими каналами.</span><span class="sxs-lookup"><span data-stu-id="92118-500">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="92118-501">Это делается путем подклассинга **ActivityHandler**.</span><span class="sxs-lookup"><span data-stu-id="92118-501">This is done by sub-classing the **ActivityHandler**.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="92118-502">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="92118-502">C#/.NET</span></span>](#tab/dotnet-sample)

<span data-ttu-id="92118-503">**Bots/DialogBot.cs**</span><span class="sxs-lookup"><span data-stu-id="92118-503">**Bots/DialogBot.cs**</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="92118-504">**Bots/TeamsBot.cs**</span><span class="sxs-lookup"><span data-stu-id="92118-504">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="92118-505">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="92118-505">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="92118-506">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="92118-506">TeamsActivityHandler.cs</span></span>

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

# <a name="javascript"></a>[<span data-ttu-id="92118-507">JavaScript</span><span class="sxs-lookup"><span data-stu-id="92118-507">JavaScript</span></span>](#tab/node-js-dialog-sample)

<span data-ttu-id="92118-508">**bots/dialogBot.js**</span><span class="sxs-lookup"><span data-stu-id="92118-508">**bots/dialogBot.js**</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/dialogBot.js?range=4-46)]

<span data-ttu-id="92118-509">**bots/teamsBot.js**</span><span class="sxs-lookup"><span data-stu-id="92118-509">**bots/teamsBot.js**</span></span>

<span data-ttu-id="92118-510">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="92118-510">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-javascript[ActivityHandler](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/bots/teamsBot.js?range=4-33)]

<span data-ttu-id="92118-511">**диалоги/mainDialog.js**</span><span class="sxs-lookup"><span data-stu-id="92118-511">**dialogs/mainDialog.js**</span></span>

<span data-ttu-id="92118-512">В диалоговом шаге используйте `beginDialog` для запуска запроса OAuth, в котором пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="92118-512">Within a dialog step, use `beginDialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="92118-513">Если пользователь уже подписан, это создает событие отклика маркеров без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-513">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="92118-514">В противном случае пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="92118-514">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="92118-515">Служба ботов Azure отправляет событие отклика маркера после попытки пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="92118-515">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-52)]

<span data-ttu-id="92118-516">В следующем диалоговом шаге проверьте наличие маркера в результате предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="92118-516">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="92118-517">Если это не null, пользователь успешно вписался.</span><span class="sxs-lookup"><span data-stu-id="92118-517">If it is not null, the user successfully signed in.</span></span>

[!code-javascript[AddOAuthPrompt](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/mainDialog.js?range=50-64)]

<span data-ttu-id="92118-518">**bots/logoutDialog.js**</span><span class="sxs-lookup"><span data-stu-id="92118-518">**bots/logoutDialog.js**</span></span>

[!code-javascript[allow-logout](~/../botbuilder-samples/samples/javascript_nodejs/46.teams-auth/dialogs/logoutDialog.js?range=31-42&highlight=7)]

# <a name="python"></a>[<span data-ttu-id="92118-519">Python</span><span class="sxs-lookup"><span data-stu-id="92118-519">Python</span></span>](#tab/python-sample)

<span data-ttu-id="92118-520">**bots/dialog_bot.py**</span><span class="sxs-lookup"><span data-stu-id="92118-520">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="92118-521">**bots/teams_bot.py**</span><span class="sxs-lookup"><span data-stu-id="92118-521">**bots/teams_bot.py**</span></span>

<span data-ttu-id="92118-522">Если *используется* **OAuthPrompt,** в диалоговое окно необходимо перенаправлить действие Invoke Activity.</span><span class="sxs-lookup"><span data-stu-id="92118-522">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)]

<span data-ttu-id="92118-523">**диалоги/main_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="92118-523">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="92118-524">В диалоговом шаге используйте `begin_dialog` для запуска запроса OAuth, в котором пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="92118-524">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="92118-525">Если пользователь уже подписан, это создает событие отклика маркеров без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="92118-525">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="92118-526">В противном случае пользователь должен войти.</span><span class="sxs-lookup"><span data-stu-id="92118-526">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="92118-527">Служба ботов Azure отправляет событие отклика маркера после попытки пользователя войти.</span><span class="sxs-lookup"><span data-stu-id="92118-527">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="92118-528">В следующем диалоговом шаге проверьте наличие маркера в результате предыдущего шага.</span><span class="sxs-lookup"><span data-stu-id="92118-528">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="92118-529">Если это не null, пользователь успешно вписался.</span><span class="sxs-lookup"><span data-stu-id="92118-529">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=51-61)]

<span data-ttu-id="92118-530">**диалоги/logout_dialog.py**</span><span class="sxs-lookup"><span data-stu-id="92118-530">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="see-also"></a><span data-ttu-id="92118-531">См. также</span><span class="sxs-lookup"><span data-stu-id="92118-531">See also</span></span>

[<span data-ttu-id="92118-532">Добавление проверки подлинности через службу Azure Bot</span><span class="sxs-lookup"><span data-stu-id="92118-532">Add authentication through Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: /azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true
[concept-state]: /azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0&preserve-view=true
[concept-dialogs]: /azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0&preserve-view=true
[simple-dialog]: /azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0&preserve-view=true

[teams-auth-bot-cs]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[teams-auth-bot-js]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview
