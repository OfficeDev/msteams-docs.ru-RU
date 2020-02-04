---
title: Добавление проверки подлинности для ленты Teams
author: clearab
description: Добавление проверки подлинности OAuth для почтового робота в Microsoft Teams.
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 63d06100f69a5dc3777bdfb20b3231a85dce1f04
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675327"
---
# <a name="add-authentication-to-your-teams-bot"></a><span data-ttu-id="c3195-103">Добавление проверки подлинности для ленты Teams</span><span class="sxs-lookup"><span data-stu-id="c3195-103">Add authentication to your Teams bot</span></span>

<span data-ttu-id="c3195-104">Иногда может потребоваться создать боты в Microsoft Teams, которые могут получать доступ к ресурсам от имени пользователя, например к почтовой службе.</span><span class="sxs-lookup"><span data-stu-id="c3195-104">There are times when you may need to create bots in Microsoft Teams that can access resources on behalf of the user, such as a mail service.</span></span>

<span data-ttu-id="c3195-105">В этой статье показано, как использовать проверку подлинности SDK для Azure Bot службы Azure на основе OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="c3195-105">This article demonstrates how to use Azure Bot Service v4 SDK authentication, based on OAuth 2.0.</span></span> <span data-ttu-id="c3195-106">Это упрощает разработку Bot, который может использовать маркеры проверки подлинности на основе учетных данных пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3195-106">This makes it easier to develop a bot that can use authentication tokens based on the user's credentials.</span></span> <span data-ttu-id="c3195-107">Ключевое значение ALL — это использование **поставщиков удостоверений**, как мы будем видеть позже.</span><span class="sxs-lookup"><span data-stu-id="c3195-107">Key in all this is the use of **identity providers**, as we will see later.</span></span>

<span data-ttu-id="c3195-108">OAuth 2,0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c3195-108">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="c3195-109">Базовое понимание OAuth 2,0 является необходимым условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="c3195-109">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

<span data-ttu-id="c3195-110">В разделе [OAuth 2 упрощено](https://aka.ms/oauth2-simplified) основные сведения и [OAuth 2,0](https://oauth.net/2/) для полной спецификации.</span><span class="sxs-lookup"><span data-stu-id="c3195-110">See [OAuth 2 Simplified](https://aka.ms/oauth2-simplified) for a basic understanding, and [OAuth 2.0](https://oauth.net/2/) for the complete specification.</span></span>

<span data-ttu-id="c3195-111">Дополнительные сведения о том, как служба Azure Bot обрабатывает проверку подлинности, можно узнать [в статье Проверка подлинности пользователей в беседе](https://aka.ms/azure-bot-authentication).</span><span class="sxs-lookup"><span data-stu-id="c3195-111">For more information about how the Azure Bot Service handles authentication, see [User authentication within a conversation](https://aka.ms/azure-bot-authentication).</span></span>

<span data-ttu-id="c3195-112">В данной статье вы узнаете следующее.</span><span class="sxs-lookup"><span data-stu-id="c3195-112">In this article you'll learn:</span></span>

- <span data-ttu-id="c3195-113">**Создание ленты с включенной проверкой подлинности**.</span><span class="sxs-lookup"><span data-stu-id="c3195-113">**How to create an authentication-enabled bot**.</span></span> <span data-ttu-id="c3195-114">Вы будете использовать [CS – auth – Sample][teams-auth-bot] для обработки учетных данных пользователя и создания маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-114">You'll use [cs-auth-sample][teams-auth-bot] to handle user sign-in credentials and the generating the authentication token.</span></span>
- <span data-ttu-id="c3195-115">**Как развернуть Bot в Azure и связать его с поставщиком удостоверений**.</span><span class="sxs-lookup"><span data-stu-id="c3195-115">**How to deploy the bot to Azure and associate it with an identity provider**.</span></span> <span data-ttu-id="c3195-116">Поставщик выдает маркер, основанный на учетных данных пользователя для входа.</span><span class="sxs-lookup"><span data-stu-id="c3195-116">The provider issues a token based on user sign-in credentials.</span></span> <span data-ttu-id="c3195-117">С помощью маркера Bot можно получить доступ к ресурсам, таким как почтовая служба, которая требует проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-117">The bot can use the token to access resources, such as a mail service, which require authentication.</span></span> <span data-ttu-id="c3195-118">Для получения дополнительных сведений см [процесс проверки подлинности Microsoft Teams для Боты](auth-flow-bot.md).</span><span class="sxs-lookup"><span data-stu-id="c3195-118">For more information see  [Microsoft Teams authentication flow for bots](auth-flow-bot.md).</span></span>
- <span data-ttu-id="c3195-119">**Интеграция программы Bot в Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="c3195-119">**How to integrate the bot within Microsoft Teams**.</span></span> <span data-ttu-id="c3195-120">После интеграции ленты вы сможете войти и обмениваться сообщениями в чате.</span><span class="sxs-lookup"><span data-stu-id="c3195-120">Once the bot has been integrated, you can sign in and exchange messages with it in a chat.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3195-121">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c3195-121">Prerequisites</span></span>

- <span data-ttu-id="c3195-122">Знание [основ Bot][concept-basics], [Управление состоянием][concept-state], [Библиотека диалоговых окон][concept-dialogs]и [реализация последовательного процесса беседы][simple-dialog].</span><span class="sxs-lookup"><span data-stu-id="c3195-122">Knowledge of [bot basics][concept-basics], [managing state][concept-state], the [dialogs library][concept-dialogs], and how to [implement sequential conversation flow][simple-dialog].</span></span>
- <span data-ttu-id="c3195-123">Сведения о разработке Azure и OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="c3195-123">Knowledge of Azure and OAuth 2.0 development.</span></span>
- <span data-ttu-id="c3195-124">Visual Studio 2017 или более поздней версии, а также Git.</span><span class="sxs-lookup"><span data-stu-id="c3195-124">Visual Studio 2017 or later and Git.</span></span>
- <span data-ttu-id="c3195-125">Учетная запись Azure.</span><span class="sxs-lookup"><span data-stu-id="c3195-125">Azure account.</span></span> <span data-ttu-id="c3195-126">При необходимости вы можете создать [бесплатную учетную запись Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c3195-126">If needed, you can create an [Azure free account](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="c3195-127">Приведенный ниже пример.</span><span class="sxs-lookup"><span data-stu-id="c3195-127">The following sample.</span></span>

    | <span data-ttu-id="c3195-128">Пример</span><span class="sxs-lookup"><span data-stu-id="c3195-128">Sample</span></span> | <span data-ttu-id="c3195-129">Версия Ботбуилдер</span><span class="sxs-lookup"><span data-stu-id="c3195-129">BotBuilder version</span></span> | <span data-ttu-id="c3195-130">Демонстрирующего</span><span class="sxs-lookup"><span data-stu-id="c3195-130">Demonstrates</span></span> |
    |:---|:---:|:---|
    | <span data-ttu-id="c3195-131">**Проверка подлинности с помощью подлинности** в [CS – auth — пример][teams-auth-bot]</span><span class="sxs-lookup"><span data-stu-id="c3195-131">**Bot authentication** in [cs-auth-sample][teams-auth-bot]</span></span> | <span data-ttu-id="c3195-132">IPv4</span><span class="sxs-lookup"><span data-stu-id="c3195-132">v4</span></span> | <span data-ttu-id="c3195-133">Поддержка Оаускард</span><span class="sxs-lookup"><span data-stu-id="c3195-133">OAuthCard support</span></span> |
    | <span data-ttu-id="c3195-134">Простая **Проверка подлинности** в [Python – auth — пример][teams-auth-bot-py]</span><span class="sxs-lookup"><span data-stu-id="c3195-134">**Bot authentication** in [python-auth-sample][teams-auth-bot-py]</span></span> | <span data-ttu-id="c3195-135">IPv4</span><span class="sxs-lookup"><span data-stu-id="c3195-135">v4</span></span> | <span data-ttu-id="c3195-136">Поддержка Оаускард</span><span class="sxs-lookup"><span data-stu-id="c3195-136">OAuthCard support</span></span> |

## <a name="create-the-resource-group"></a><span data-ttu-id="c3195-137">Создание группы ресурсов</span><span class="sxs-lookup"><span data-stu-id="c3195-137">Create the resource group</span></span>

<span data-ttu-id="c3195-138">Группа ресурсов и план обслуживания не являются строго обязательными, но они позволяют удобно освобождать создаваемые ресурсы.</span><span class="sxs-lookup"><span data-stu-id="c3195-138">The resource group and the service plan aren't strictly necessary, but they allow you to conveniently release the resources you create.</span></span> <span data-ttu-id="c3195-139">Это хорошая практика по обеспечению упорядочения ресурсов и управления ими.</span><span class="sxs-lookup"><span data-stu-id="c3195-139">This is good practice for keeping your resources organized and manageable.</span></span>

<span data-ttu-id="c3195-140">Группа ресурсов используется для создания отдельных ресурсов для Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c3195-140">You use a resource group to create individual resources for the Bot Framework.</span></span> <span data-ttu-id="c3195-141">Для повышения производительности убедитесь, что эти ресурсы расположены в одном и том же регионе Azure.</span><span class="sxs-lookup"><span data-stu-id="c3195-141">For performance, ensure that these resources are located in the same Azure region.</span></span>

1. <span data-ttu-id="c3195-142">В браузере Войдите на [**портал Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c3195-142">In your browser, sign into the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c3195-143">В левой панели навигации выберите пункт **группы ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c3195-143">In the left navigation panel, select **Resource groups**.</span></span>
1. <span data-ttu-id="c3195-144">В левом верхнем углу отображаемого окна выберите **Добавить** вкладку, чтобы создать новую группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c3195-144">In the upper left of the displayed window, select **Add** tab to create a new resource group.</span></span> <span data-ttu-id="c3195-145">Вам будет предложено указать следующее:</span><span class="sxs-lookup"><span data-stu-id="c3195-145">You'll be prompted to provide the following:</span></span>
    1. <span data-ttu-id="c3195-146">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="c3195-146">**Subscription**.</span></span> <span data-ttu-id="c3195-147">Используйте существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="c3195-147">Use your existing subscription.</span></span>
    1. <span data-ttu-id="c3195-148">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c3195-148">**Resource group**.</span></span> <span data-ttu-id="c3195-149">Введите имя группы ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c3195-149">Enter the name for the resource group.</span></span> <span data-ttu-id="c3195-150">Например, может быть *теамсресаурцеграуп*.</span><span class="sxs-lookup"><span data-stu-id="c3195-150">An example could be  *TeamsResourceGroup*.</span></span> <span data-ttu-id="c3195-151">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="c3195-151">Remember that the name must be unique.</span></span>
    1. <span data-ttu-id="c3195-152">В раскрывающемся меню **Region (регион** ) выберите *Запад США*или регион близко к приложениям.</span><span class="sxs-lookup"><span data-stu-id="c3195-152">From the **Region** drop-down menu, select *West US*, or a region close to your applications.</span></span>
    1. <span data-ttu-id="c3195-153">Нажмите кнопку " **Просмотр и создание** ".</span><span class="sxs-lookup"><span data-stu-id="c3195-153">Select the **Review and create** button.</span></span> <span data-ttu-id="c3195-154">Вы должны увидеть баннер с прочтением *пройденной проверки*.</span><span class="sxs-lookup"><span data-stu-id="c3195-154">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="c3195-155">Нажмите кнопку **создать** .</span><span class="sxs-lookup"><span data-stu-id="c3195-155">Select the **Create** button.</span></span> <span data-ttu-id="c3195-156">Создание группы ресурсов может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c3195-156">It may take a few minutes to create the resource group.</span></span>

> [!TIP]
> <span data-ttu-id="c3195-157">Как и в случае с ресурсами, которые вы создадите позже в этом руководстве, рекомендуется закрепить эту группу ресурсов на панели мониторинга для упрощения доступа.</span><span class="sxs-lookup"><span data-stu-id="c3195-157">As with the resources you'll create later in this tutorial, it's a good idea to pin this resource group to your dashboard for easy access.</span></span> <span data-ttu-id="c3195-158">Если вы хотите сделать это, нажмите значок ПИН-кода & # 128204; в верхнем правом углу панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c3195-158">If you'd like to do so, select the pin icon &#128204; in the upper right of the dashboard.</span></span>

## <a name="create-the-service-plan"></a><span data-ttu-id="c3195-159">Создание плана обслуживания</span><span class="sxs-lookup"><span data-stu-id="c3195-159">Create the service plan</span></span>

1. <span data-ttu-id="c3195-160">На [**портале Azure**][azure-portal]в левой панели навигации выберите пункт **создать ресурс**.</span><span class="sxs-lookup"><span data-stu-id="c3195-160">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Create a resource**.</span></span>
1. <span data-ttu-id="c3195-161">В поле поиска введите *план обслуживания приложений*.</span><span class="sxs-lookup"><span data-stu-id="c3195-161">In the search box, type *App Service Plan*.</span></span> <span data-ttu-id="c3195-162">Выберите карточку **плана обслуживания приложений** из результатов поиска.</span><span class="sxs-lookup"><span data-stu-id="c3195-162">Select the **App Service Plan** card from the search results.</span></span>
1. <span data-ttu-id="c3195-163">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3195-163">Select **Create**.</span></span>
1. <span data-ttu-id="c3195-164">Вам будет предложено указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="c3195-164">You'll be asked to provide the following information:</span></span>
    1. <span data-ttu-id="c3195-165">**Подписка**.</span><span class="sxs-lookup"><span data-stu-id="c3195-165">**Subscription**.</span></span> <span data-ttu-id="c3195-166">Вы можете использовать существующую подписку.</span><span class="sxs-lookup"><span data-stu-id="c3195-166">You can use an existing subscription.</span></span>
    1. <span data-ttu-id="c3195-167">**Группа ресурсов**.</span><span class="sxs-lookup"><span data-stu-id="c3195-167">**Resource Group**.</span></span> <span data-ttu-id="c3195-168">Выберите ранее созданную группу.</span><span class="sxs-lookup"><span data-stu-id="c3195-168">Select the group you created earlier.</span></span>
    1. <span data-ttu-id="c3195-169">**Name (имя**).</span><span class="sxs-lookup"><span data-stu-id="c3195-169">**Name**.</span></span> <span data-ttu-id="c3195-170">Введите имя для плана обслуживания.</span><span class="sxs-lookup"><span data-stu-id="c3195-170">Enter the name for the service plan.</span></span> <span data-ttu-id="c3195-171">Например, может быть *теамссервицеплан*.</span><span class="sxs-lookup"><span data-stu-id="c3195-171">An example could be  *TeamsServicePlan*.</span></span> <span data-ttu-id="c3195-172">Помните, что имя должно быть уникальным в пределах группы.</span><span class="sxs-lookup"><span data-stu-id="c3195-172">Remember that the name must be unique, within the group.</span></span>
    1. <span data-ttu-id="c3195-173">**Операционная система**.</span><span class="sxs-lookup"><span data-stu-id="c3195-173">**Operating System**.</span></span> <span data-ttu-id="c3195-174">Выберите *Windows* или применяемую ОС.</span><span class="sxs-lookup"><span data-stu-id="c3195-174">Select *Windows* or your applicable OS.</span></span>
    1. <span data-ttu-id="c3195-175">**Область**.</span><span class="sxs-lookup"><span data-stu-id="c3195-175">**Region**.</span></span> <span data-ttu-id="c3195-176">Выберите *Запад США* или регион, близкий к приложениям.</span><span class="sxs-lookup"><span data-stu-id="c3195-176">Select *West US* or a region close to your applications.</span></span>
    1. <span data-ttu-id="c3195-177">**Ценовая**Категория.</span><span class="sxs-lookup"><span data-stu-id="c3195-177">**Pricing Tier**.</span></span> <span data-ttu-id="c3195-178">Убедитесь, что выбран пункт " *Стандартная S1* ".</span><span class="sxs-lookup"><span data-stu-id="c3195-178">Make sure that *Standard S1* is selected.</span></span> <span data-ttu-id="c3195-179">Это значение должно быть задано по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c3195-179">This should be the default value.</span></span>
    1. <span data-ttu-id="c3195-180">Нажмите кнопку " **Просмотр и создание** ".</span><span class="sxs-lookup"><span data-stu-id="c3195-180">Select the **Review and create** button.</span></span> <span data-ttu-id="c3195-181">Вы должны увидеть баннер с прочтением *пройденной проверки*.</span><span class="sxs-lookup"><span data-stu-id="c3195-181">You should see a banner that reads *Validation passed*.</span></span>
    1. <span data-ttu-id="c3195-182">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3195-182">Select **Create**.</span></span> <span data-ttu-id="c3195-183">Создание плана служб приложений может занять несколько минут.</span><span class="sxs-lookup"><span data-stu-id="c3195-183">It may take a few minutes to create the app service plan.</span></span> <span data-ttu-id="c3195-184">План будет указан в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c3195-184">The plan will be listed in the resource group.</span></span>

## <a name="create-the-bot-channels-registration"></a><span data-ttu-id="c3195-185">Создание регистрации каналов канала ленты</span><span class="sxs-lookup"><span data-stu-id="c3195-185">Create the bot channels registration</span></span>

<span data-ttu-id="c3195-186">Регистрация каналов ленты регистрирует веб-службу в качестве ленты с помощью Bot Framework, если у вас есть идентификатор приложения Microsoft и пароль приложения (секрет клиента).</span><span class="sxs-lookup"><span data-stu-id="c3195-186">The bot channels registration registers your web service as a bot with the Bot Framework, provided you have a Microsoft App Id and App password (client secret).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3195-187">Зарегистрировать его можно только в том случае, если он не размещен в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3195-187">You only need to register your bot if it is not hosted in Azure.</span></span> <span data-ttu-id="c3195-188">Если вы [создали объект Bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) через портал Azure, он уже зарегистрирован в службе.</span><span class="sxs-lookup"><span data-stu-id="c3195-188">If you [created a bot](/azure/bot-service/abs-quickstart?view=azure-bot-service-4.0&viewFallbackFrom=azure-bot-service-3.0) through the Azure portal then it is already registered with the service.</span></span> <span data-ttu-id="c3195-189">Если вы создали пошаговую [среду](https://dev.botframework.com/bots/new) с Bot или [аппстудио](~/concepts/build-and-test/app-studio-overview.md) , она не зарегистрирована в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3195-189">If you created your bot through the [Bot Framework](https://dev.botframework.com/bots/new) or [AppStudio](~/concepts/build-and-test/app-studio-overview.md) your bot isn't registered in Azure.</span></span>

[!INCLUDE [bot channels registration steps](~/includes/bots/azure-bot-channels-registration.md)]

<span data-ttu-id="c3195-190">После того как Azure создаст ресурс регистрации, он будет включен в список "Группа ресурсов".</span><span class="sxs-lookup"><span data-stu-id="c3195-190">After Azure has created the registration resource it will be included in the resource group list.</span></span>  

![Группа регистрации каналов приложений для ленты](../../../assets/images/authentication/auth-bot-channels-registration-group.PNG)

> [!NOTE]
> <span data-ttu-id="c3195-192">В ресурсе регистрации каналов канала ленты будет отображаться **глобальный** регион, даже если вы выбрали Запад US.</span><span class="sxs-lookup"><span data-stu-id="c3195-192">The Bot Channels Registration resource will show the **Global** region even if you selected West US.</span></span> <span data-ttu-id="c3195-193">Это ожидается.</span><span class="sxs-lookup"><span data-stu-id="c3195-193">This is expected.</span></span>

<span data-ttu-id="c3195-194">Более подробную информацию можно найти в статье Создание почтового [робота для Teams](../create-a-bot-for-teams.md).</span><span class="sxs-lookup"><span data-stu-id="c3195-194">For more information, see [Create a bot for Teams](../create-a-bot-for-teams.md).</span></span>

## <a name="create-the-identity-provider"></a><span data-ttu-id="c3195-195">Создание поставщика удостоверений</span><span class="sxs-lookup"><span data-stu-id="c3195-195">Create the identity provider</span></span>

<span data-ttu-id="c3195-196">Вам необходим поставщик удостоверений, который можно использовать для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-196">You need an identity provider that can be used for authentication.</span></span>
<span data-ttu-id="c3195-197">В этой процедуре используется поставщик Azure AD; Кроме того, можно использовать другие поставщики удостоверений, поддерживаемые службой Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3195-197">In this procedure you'll use an Azure AD provider; other Azure AD supported identity providers can also be used.</span></span>

1. <span data-ttu-id="c3195-198">На [**портале Azure**][azure-portal]на левой панели навигации выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3195-198">In the [**Azure portal**][azure-portal], on the left navigation panel, select **Azure Active Directory**.</span></span>
    > [!TIP]
    > <span data-ttu-id="c3195-199">Вам потребуется создать и зарегистрировать этот ресурс Azure AD в клиенте, в котором вы можете предоставить согласие на делегирование разрешений, запрашиваемых приложением.</span><span class="sxs-lookup"><span data-stu-id="c3195-199">You'll need to create and register this Azure AD resource in a tenant in which you can consent to delegate permissions requested by an application.</span></span>
    > <span data-ttu-id="c3195-200">Инструкции по созданию клиента можно узнать в статье [доступ к порталу и создание клиента](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span><span class="sxs-lookup"><span data-stu-id="c3195-200">For instruction on creating a tenant, see [Access the portal and create a tenant](/azure/active-directory/fundamentals/active-directory-access-create-new-tenant).</span></span>
1. <span data-ttu-id="c3195-201">В левой панели выберите пункт **Регистрация приложений**.</span><span class="sxs-lookup"><span data-stu-id="c3195-201">In the left panel, select **App registrations**.</span></span>
1. <span data-ttu-id="c3195-202">На правой панели выберите **новую вкладку регистрация** в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="c3195-202">In the right panel, select the **New registration** tab, in the upper left.</span></span>
1. <span data-ttu-id="c3195-203">Вам будет предложено указать следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="c3195-203">You'll be asked to provide the following information:</span></span>
   1. <span data-ttu-id="c3195-204">**Name (имя**).</span><span class="sxs-lookup"><span data-stu-id="c3195-204">**Name**.</span></span> <span data-ttu-id="c3195-205">Введите имя приложения.</span><span class="sxs-lookup"><span data-stu-id="c3195-205">Enter the name for the application.</span></span> <span data-ttu-id="c3195-206">Например, может быть *боттеамсидентити*.</span><span class="sxs-lookup"><span data-stu-id="c3195-206">An example could be  *BotTeamsIdentity*.</span></span> <span data-ttu-id="c3195-207">Помните, что имя должно быть уникальным.</span><span class="sxs-lookup"><span data-stu-id="c3195-207">Remember that the name must be unique.</span></span>
   1. <span data-ttu-id="c3195-208">Выберите **Поддерживаемые типы учетных записей** для вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="c3195-208">Select the **Supported account types** for your application.</span></span> <span data-ttu-id="c3195-209">Выберите *учетные записи в любом каталоге организации (любой Azure AD Active Directory) и личных учетных записях Майкрософт (например, Skype, Xbox)*.</span><span class="sxs-lookup"><span data-stu-id="c3195-209">Select *Accounts in any organizational directory (Any Azure AD directory - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)*.</span></span>
   1. <span data-ttu-id="c3195-210">Для **URI перенаправления**:</span><span class="sxs-lookup"><span data-stu-id="c3195-210">For the **Redirect URI**:</span></span><br/>
       <span data-ttu-id="c3195-211">&#x2713;выбрать **веб-сайт**.</span><span class="sxs-lookup"><span data-stu-id="c3195-211">&#x2713;Select **Web**.</span></span> <br/>
       <span data-ttu-id="c3195-212">&#x2713; задать URL-адрес `https://token.botframework.com/.auth/web/redirect`.</span><span class="sxs-lookup"><span data-stu-id="c3195-212">&#x2713; Set the URL to `https://token.botframework.com/.auth/web/redirect`.</span></span>
   1. <span data-ttu-id="c3195-213">Выберите **регистр**.</span><span class="sxs-lookup"><span data-stu-id="c3195-213">Select **Register**.</span></span>

1. <span data-ttu-id="c3195-214">После создания Azure отображает страницу **обзора** приложения.</span><span class="sxs-lookup"><span data-stu-id="c3195-214">Once it is created, Azure displays the **Overview** page for the app.</span></span> <span data-ttu-id="c3195-215">Скопируйте и сохраните следующие сведения в файле:</span><span class="sxs-lookup"><span data-stu-id="c3195-215">Copy and save the following information to a file:</span></span>

    1. <span data-ttu-id="c3195-216">Значение **идентификатора Application (Client)** .</span><span class="sxs-lookup"><span data-stu-id="c3195-216">The **Application (client) ID** value.</span></span> <span data-ttu-id="c3195-217">Это значение будет использоваться позже в качестве *идентификатора клиента* при регистрации этого приложения удостоверений Azure с помощью программы Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-217">You'll use this value later as the *Client ID* when you register this Azure identity application with your bot.</span></span>
    1. <span data-ttu-id="c3195-218">Значение **идентификатора каталога (клиента)** .</span><span class="sxs-lookup"><span data-stu-id="c3195-218">The **Directory (tenant) ID** value.</span></span> <span data-ttu-id="c3195-219">Вы также можете использовать это значение позже, как *идентификатор клиента* для регистрации этого приложения удостоверения Azure с помощью программы Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-219">You'll also use this value later as the *Tenant ID* to register this Azure identity application with your bot.</span></span>

1. <span data-ttu-id="c3195-220">В левой панели выберите **сертификаты & секреты** , чтобы создать секрет клиента для приложения.</span><span class="sxs-lookup"><span data-stu-id="c3195-220">In the left panel, select **Certificates & secrets** to create a client secret for your application.</span></span>

   1. <span data-ttu-id="c3195-221">В разделе **секреты клиента**выберите &#x2795; **новый секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="c3195-221">Under **Client secrets**, select &#x2795; **New client secret**.</span></span>
   1. <span data-ttu-id="c3195-222">Добавьте описание для идентификации этого секрета от других пользователей, которые, возможно, потребуется создать для этого приложения, например " *приложение идентификации Bot" в Teams*.</span><span class="sxs-lookup"><span data-stu-id="c3195-222">Add a description to identify this secret from others you might need to create for this app, such as *Bot identity app in Teams*.</span></span>
   1. <span data-ttu-id="c3195-223">Установите **срок действия** выбранных элементов.</span><span class="sxs-lookup"><span data-stu-id="c3195-223">Set **Expires** to your selection.</span></span>
   1. <span data-ttu-id="c3195-224">Нажмите кнопку **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="c3195-224">Select **Add**.</span></span>
   1. <span data-ttu-id="c3195-225">Перед выходом из этой страницы **запишите секрет**.</span><span class="sxs-lookup"><span data-stu-id="c3195-225">Before leaving this page, **record the secret**.</span></span> <span data-ttu-id="c3195-226">Это значение будет использоваться позже в качестве _секрета клиента_ при регистрации приложения Azure AD с помощью программы Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-226">You'll use this value later as the _Client secret_ when you register your Azure AD application with your bot.</span></span>

### <a name="configure-the-identity-provider-connection-and-register-it-with-the-bot"></a><span data-ttu-id="c3195-227">Настройка подключения к поставщику удостоверений и его регистрация с помощью Bot</span><span class="sxs-lookup"><span data-stu-id="c3195-227">Configure the identity provider connection and register it with the bot</span></span>

1. <span data-ttu-id="c3195-228">На [**портале Azure**][azure-portal]выберите группу ресурсов на панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="c3195-228">In the [**Azure portal**][azure-portal], select your resource group from the dashboard.</span></span>
1. <span data-ttu-id="c3195-229">Выберите ссылку для регистрации канала ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-229">Select your bot channel registration link.</span></span>
1. <span data-ttu-id="c3195-230">На странице ресурс выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c3195-230">On the resource page, select **Settings**.</span></span>
1. <span data-ttu-id="c3195-231">В разделе **Параметры подключения OAuth** в нижней части страницы нажмите кнопку **Добавить параметр**.</span><span class="sxs-lookup"><span data-stu-id="c3195-231">Under **OAuth Connection Settings** near the bottom of the page, select **Add Setting**.</span></span>
1. <span data-ttu-id="c3195-232">Заполните форму следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3195-232">Complete the form as follows:</span></span>

    1. <span data-ttu-id="c3195-233">**Name (имя**).</span><span class="sxs-lookup"><span data-stu-id="c3195-233">**Name**.</span></span> <span data-ttu-id="c3195-234">Введите имя подключения.</span><span class="sxs-lookup"><span data-stu-id="c3195-234">Enter a name for the connection.</span></span> <span data-ttu-id="c3195-235">Это имя будет использоваться в `appsettings.json` файле Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-235">You'll use this name in your bot in the `appsettings.json` file.</span></span> <span data-ttu-id="c3195-236">Например, *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="c3195-236">For example *BotTeamsAuthADv1*.</span></span>
    1. <span data-ttu-id="c3195-237">**Поставщик услуг**.</span><span class="sxs-lookup"><span data-stu-id="c3195-237">**Service Provider**.</span></span> <span data-ttu-id="c3195-238">Выберите **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c3195-238">Select **Azure Active Directory**.</span></span> <span data-ttu-id="c3195-239">После выбора этого поля будут отображены поля, связанные с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c3195-239">Once you select this, the Azure AD-specific fields will be displayed.</span></span>
    1. <span data-ttu-id="c3195-240">**Идентификатор клиента**. Введите идентификатор приложения (клиента), записанный для приложения поставщика удостоверений Azure, в описанных выше шагах.</span><span class="sxs-lookup"><span data-stu-id="c3195-240">**Client id**. Enter the Application (client) ID that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c3195-241">**Секрет клиента**.</span><span class="sxs-lookup"><span data-stu-id="c3195-241">**Client secret**.</span></span> <span data-ttu-id="c3195-242">Введите секретный код, записанный для приложения поставщика удостоверений Azure, в описанных выше шагах.</span><span class="sxs-lookup"><span data-stu-id="c3195-242">Enter the secret that you recorded for your Azure identity provider app in the steps above.</span></span>
    1. <span data-ttu-id="c3195-243">**Тип гранта**.</span><span class="sxs-lookup"><span data-stu-id="c3195-243">**Grant Type**.</span></span> <span data-ttu-id="c3195-244">Введите `authorization_code`.</span><span class="sxs-lookup"><span data-stu-id="c3195-244">Enter `authorization_code`.</span></span>
    1. <span data-ttu-id="c3195-245">**URL-адрес для входа**.</span><span class="sxs-lookup"><span data-stu-id="c3195-245">**Login URL**.</span></span> <span data-ttu-id="c3195-246">Введите `https://login.microsoftonline.com`.</span><span class="sxs-lookup"><span data-stu-id="c3195-246">Enter `https://login.microsoftonline.com`.</span></span>
    1. <span data-ttu-id="c3195-247">**Идентификатор клиента**введите **идентификатор каталога (клиента)** , записанный ранее для своего приложения-удостоверения Azure, или **Общий** , в зависимости от поддерживаемого типа учетной записи, выбранной при создании приложения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c3195-247">**Tenant ID**, enter the **Directory (tenant) ID** that you recorded earlier for your Azure identity app or **common** depending on the supported account type selected when you created the identity provider app.</span></span> <span data-ttu-id="c3195-248">Чтобы выбрать значение, которое нужно назначить, выполните следующие условия:</span><span class="sxs-lookup"><span data-stu-id="c3195-248">To decide which value to assign follow these criteria:</span></span>

        - <span data-ttu-id="c3195-249">Если вы выбрали *учетные записи только в этом каталоге организации (только Microsoft AAD — один клиент)* или *учетные записи в любом организационном каталоге (Microsoft AAD Active Directory — несколько клиентов)* , введите **идентификатор клиента** , записанный ранее для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="c3195-249">If you selected either *Accounts in this organizational directory only (Microsoft only - Single tenant)* or *Accounts in any organizational directory(Microsoft AAD directory - Multi tenant)* enter the **tenant ID** you recorded earlier for the AAD app.</span></span> <span data-ttu-id="c3195-250">Это будет клиент, связанный с пользователями, которые могут пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-250">This will be the tenant associated with the users who can be authenticated.</span></span>

        - <span data-ttu-id="c3195-251">Если вы выбрали *учетные записи в любом организационном каталоге (например, Skype, Xbox, Outlook)* , введите слово **Common** , а не идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="c3195-251">If you selected *Accounts in any organizational directory (Any AAD directory - Multi tenant and personal Microsoft accounts e.g. Skype, Xbox, Outlook)* enter the word **common** instead of a tenant ID.</span></span> <span data-ttu-id="c3195-252">В противном случае приложение AAD проверит подлинность клиента, идентификатор которого был выбран и исключит личные учетные записи Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c3195-252">Otherwise, the AAD app will verify through the tenant whose ID was selected and exclude personal Microsoft accounts.</span></span>

    <span data-ttu-id="c3195-253">высоты.</span><span class="sxs-lookup"><span data-stu-id="c3195-253">h.</span></span> <span data-ttu-id="c3195-254">Введите в поле `https://graph.microsoft.com/` **URL-адрес ресурса**.</span><span class="sxs-lookup"><span data-stu-id="c3195-254">For **Resource URL**, enter `https://graph.microsoft.com/`.</span></span> <span data-ttu-id="c3195-255">Этот параметр не используется в текущем примере кода.</span><span class="sxs-lookup"><span data-stu-id="c3195-255">This is not used in the current code sample.</span></span>  
    <span data-ttu-id="c3195-256">узнать.</span><span class="sxs-lookup"><span data-stu-id="c3195-256">i.</span></span> <span data-ttu-id="c3195-257">Оставьте **области** пустыми.</span><span class="sxs-lookup"><span data-stu-id="c3195-257">Leave **Scopes** blank.</span></span> <span data-ttu-id="c3195-258">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-258">The following image is an example:</span></span>

    ![Строка подключения Боты приложения Teams для проверки подлинности adv1](../../../assets/images/authentication/auth-bot-identity-connection-adv1.png)

1. <span data-ttu-id="c3195-260">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="c3195-260">Select **Save**.</span></span>

### <a name="test-the-connection"></a><span data-ttu-id="c3195-261">Проверка подключения</span><span class="sxs-lookup"><span data-stu-id="c3195-261">Test the connection</span></span>

1. <span data-ttu-id="c3195-262">Выберите запись подключения, чтобы открыть только что созданное подключение.</span><span class="sxs-lookup"><span data-stu-id="c3195-262">Select the connection entry to open the connection you just created.</span></span>
1. <span data-ttu-id="c3195-263">В верхней части панели **параметров подключения поставщика услуг** выберите пункт **проверить подключение** .</span><span class="sxs-lookup"><span data-stu-id="c3195-263">Select **Test Connection** at the top of the **Service Provider Connection Setting** panel.</span></span>
1. <span data-ttu-id="c3195-264">При первом запуске откроется новое окно браузера, предлагающее выбрать учетную запись.</span><span class="sxs-lookup"><span data-stu-id="c3195-264">The first time you do this will open a new browser window asking you to select an account.</span></span> <span data-ttu-id="c3195-265">Выберите один из них.</span><span class="sxs-lookup"><span data-stu-id="c3195-265">Select the one you want to use.</span></span>
1. <span data-ttu-id="c3195-266">После этого вам будет предложено разрешить поставщику удостоверений использовать ваши данные (учетные данные).</span><span class="sxs-lookup"><span data-stu-id="c3195-266">Next, you'll be asked to allow to the identity provider to use your data (credentials).</span></span> <span data-ttu-id="c3195-267">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-267">The following image is an example:</span></span>

    ![Строка подключения Боты приложения Teams для проверки подлинности adv1](../../../assets/images/authentication/auth-bot-connection-test-accept.PNG)

1. <span data-ttu-id="c3195-269">Нажмите кнопку **принять**.</span><span class="sxs-lookup"><span data-stu-id="c3195-269">Select **Accept**.</span></span>
1. <span data-ttu-id="c3195-270">После этого необходимо перенаправить вас на **пробное \<подключение к странице "-connection-Name> SUCCEEDED** .</span><span class="sxs-lookup"><span data-stu-id="c3195-270">This should then redirect you to a **Test Connection to \<your-connection-name> Succeeded** page.</span></span> <span data-ttu-id="c3195-271">Обновите страницу при возникновении ошибки.</span><span class="sxs-lookup"><span data-stu-id="c3195-271">Refresh the page if you get an error.</span></span> <span data-ttu-id="c3195-272">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-272">The following image is an example:</span></span>

  ![Строка подключения Боты приложения Teams для проверки подлинности adv1](../../../assets/images/authentication/auth-bot-connection-test-token.PNG)

<span data-ttu-id="c3195-274">Имя подключения используется кодом ленты для получения маркеров проверки подлинности пользователей.</span><span class="sxs-lookup"><span data-stu-id="c3195-274">The connection name is used by the bot code to retrieve user authentication tokens.</span></span>

## <a name="prepare-the-bot-sample-code"></a><span data-ttu-id="c3195-275">Подготовка примера кода для Bot</span><span class="sxs-lookup"><span data-stu-id="c3195-275">Prepare the bot sample code</span></span>

<span data-ttu-id="c3195-276">После выполнения предварительных настроек рассмотрим создание объекта Bot для использования в этой статье.</span><span class="sxs-lookup"><span data-stu-id="c3195-276">With the preliminary settings done, let's focus on the creation of the bot to use in this article.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="c3195-277">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="c3195-277">C#/.NET</span></span>](#tab/dotnet)

1. <span data-ttu-id="c3195-278">Clone [CS — auth — пример][teams-auth-bot].</span><span class="sxs-lookup"><span data-stu-id="c3195-278">Clone [cs-auth-sample][teams-auth-bot].</span></span>
1. <span data-ttu-id="c3195-279">Запустите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3195-279">Launch Visual Studio.</span></span>
1. <span data-ttu-id="c3195-280">На панели инструментов выберите **файл > открыть > проект/решение** и откройте проект Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-280">From the toolbar select **File -> Open -> Project/Solution** and open the bot project.</span></span>
1. <span data-ttu-id="c3195-281">В C# обновите **appSettings. JSON** следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c3195-281">In C# Update **appsettings.json** as follows:</span></span>

    - <span data-ttu-id="c3195-282">Задайте `ConnectionName` имя подключения поставщика удостоверений, добавленное к регистрации канала ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-282">Set `ConnectionName` to the name of the identity provider connection you added to the bot channel registration.</span></span> <span data-ttu-id="c3195-283">В этом примере используется имя *BotTeamsAuthADv1*.</span><span class="sxs-lookup"><span data-stu-id="c3195-283">The name we used in this example is *BotTeamsAuthADv1*.</span></span>
    - <span data-ttu-id="c3195-284">Установите `MicrosoftAppId` для **идентификатора приложения** , сохраненного во время регистрации канала ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-284">Set `MicrosoftAppId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="c3195-285">Укажите `MicrosoftAppPassword` **секрет клиента** , сохраненный во время регистрации канала ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-285">Set `MicrosoftAppPassword` to the **customer secret** you saved at the time of the bot channel registration.</span></span>
    - <span data-ttu-id="c3195-286">Задайте для `ConnectionName` параметра имя подключения поставщика удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c3195-286">Set the `ConnectionName` to the name of the identity provider connection.</span></span> 

    <span data-ttu-id="c3195-287">В зависимости от символов в тайне Bot может потребоваться, чтобы в XML-коде заменяться паролем.</span><span class="sxs-lookup"><span data-stu-id="c3195-287">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="c3195-288">Например, любой амперсанд (&) необходимо закодировать как `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="c3195-288">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

     [!code-json[appsettings](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/appsettings.json?range=1-5)]

1. <span data-ttu-id="c3195-289">В обозревателе решений перейдите `TeamsAppManifest` к папке, откройте `manifest.json` и установите `id` `botId` **идентификатор приложения** , сохраненного во время регистрации канала ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-289">In the Solution Explorer, navigate to the `TeamsAppManifest` folder, open `manifest.json` and set `id` and `botId` to the **bot App ID** you saved at the time of the bot channel registration.</span></span>

# <a name="pythontabpython"></a>[<span data-ttu-id="c3195-290">Python</span><span class="sxs-lookup"><span data-stu-id="c3195-290">Python</span></span>](#tab/python)

1. <span data-ttu-id="c3195-291">Клонировать пример [проверки подлинности][teams-auth-bot-py] с помощью кода Bot в репозитории GitHub.</span><span class="sxs-lookup"><span data-stu-id="c3195-291">Clone the sample [Teams bot authentication][teams-auth-bot-py] from the github repository.</span></span>
1. <span data-ttu-id="c3195-292">Обновление **config.py**:</span><span class="sxs-lookup"><span data-stu-id="c3195-292">Update **config.py**:</span></span>

    - <span data-ttu-id="c3195-293">Укажите `ConnectionName` имя параметра подключения OAuth, добавленного к почтовому роботу.</span><span class="sxs-lookup"><span data-stu-id="c3195-293">Set `ConnectionName` to the name of the OAuth connection setting you added to your bot.</span></span>
    - <span data-ttu-id="c3195-294">Задайте `MicrosoftAppId` идентификатор `MicrosoftAppPassword` приложения и секрет приложения для пользователя Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-294">Set `MicrosoftAppId` and `MicrosoftAppPassword` to your bot's app ID and app secret.</span></span>

      <span data-ttu-id="c3195-295">В зависимости от символов в тайне Bot может потребоваться, чтобы в XML-коде заменяться паролем.</span><span class="sxs-lookup"><span data-stu-id="c3195-295">Depending on the characters in your bot secret, you may need to XML escape the password.</span></span> <span data-ttu-id="c3195-296">Например, любой амперсанд (&) необходимо закодировать как `&amp;`.</span><span class="sxs-lookup"><span data-stu-id="c3195-296">For example, any ampersands (&) will need to be encoded as `&amp;`.</span></span>

      [!code-python[config](~/../botbuilder-samples/samples/python/46.teams-auth/config.py?range=14-16)]

---

### <a name="deploy-the-bot-to-azure"></a><span data-ttu-id="c3195-297">Развертывание ленты в Azure</span><span class="sxs-lookup"><span data-stu-id="c3195-297">Deploy the bot to Azure</span></span>

<span data-ttu-id="c3195-298">Чтобы развернуть Bot, выполните действия, описанные в разделе как [развернуть Bot в Azure](https://aka.ms/azure-bot-deployment-cli).</span><span class="sxs-lookup"><span data-stu-id="c3195-298">To deploy the bot, follow the steps in the how to [Deploy your bot to Azure](https://aka.ms/azure-bot-deployment-cli).</span></span>

<span data-ttu-id="c3195-299">Кроме того, в Visual Studio можно выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c3195-299">Alternatively, while in Visual Studio, you can follow these steps:</span></span>

1. <span data-ttu-id="c3195-300">В *обозревателе решений* Visual Studio выберите и удерживайте (или щелкните правой кнопкой мыши) имя проекта.</span><span class="sxs-lookup"><span data-stu-id="c3195-300">In Visual Studio *Solution Explorer* select and hold (or right-click) the project name.</span></span>
1. <span data-ttu-id="c3195-301">В раскрывающемся меню выберите пункт **опубликовать**.</span><span class="sxs-lookup"><span data-stu-id="c3195-301">In the drop-down menu, select **Publish**.</span></span>
1. <span data-ttu-id="c3195-302">В отображаемом окне выберите **новую** ссылку.</span><span class="sxs-lookup"><span data-stu-id="c3195-302">In the displayed window, select the **New** link.</span></span>
1. <span data-ttu-id="c3195-303">В диалоговом окне в левой части окна выберите пункт **служба приложений** и **Создайте новую** .</span><span class="sxs-lookup"><span data-stu-id="c3195-303">In the dialog window, select **App Service** on the left and **Create New** on the right.</span></span>
1. <span data-ttu-id="c3195-304">Нажмите кнопку **опубликовать** .</span><span class="sxs-lookup"><span data-stu-id="c3195-304">Select the **Publish** button.</span></span>
1. <span data-ttu-id="c3195-305">В следующем диалоговом окне введите необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="c3195-305">In the next dialog window, enter the required information.</span></span> <span data-ttu-id="c3195-306">Ниже приведен пример.</span><span class="sxs-lookup"><span data-stu-id="c3195-306">The following is an example:</span></span>

   ![Проверка подлинности App — служба](../../../assets/images/authentication/auth-bot-app-service.png)

1. <span data-ttu-id="c3195-308">Нажмите кнопку **Создать**.</span><span class="sxs-lookup"><span data-stu-id="c3195-308">Select **Create**.</span></span>
1. <span data-ttu-id="c3195-309">Если развертывание завершается успешно, оно должно отображаться в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3195-309">If the deployment completes successfully, you should see it reflected in Visual Studio.</span></span> <span data-ttu-id="c3195-310">Кроме того, в браузере, используемом по умолчанию, отображается страница, в *которой выполняется подготовка ленты*.</span><span class="sxs-lookup"><span data-stu-id="c3195-310">Moreover, a page is displayed in your default browser saying *Your bot is ready!*.</span></span> <span data-ttu-id="c3195-311">URL-адрес будет выглядеть следующим образом: `https://botteamsauth.azurewebsites.net/`.</span><span class="sxs-lookup"><span data-stu-id="c3195-311">The URL will be similar to this: `https://botteamsauth.azurewebsites.net/`.</span></span> <span data-ttu-id="c3195-312">Сохраните его в файл.</span><span class="sxs-lookup"><span data-stu-id="c3195-312">Save it to a file.</span></span>
1. <span data-ttu-id="c3195-313">В браузере перейдите на [**портал Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c3195-313">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c3195-314">Проверьте группу ресурсов, элемент Bot должен быть указан вместе с другими ресурсами.</span><span class="sxs-lookup"><span data-stu-id="c3195-314">Check your resource group, the bot should be listed along with the other resources.</span></span> <span data-ttu-id="c3195-315">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-315">The following image is an example:</span></span>

    ![Teams — Bot/auth – App – Service — группа](../../../assets/images/authentication/auth-bot-app-service-in-group.png)

1. <span data-ttu-id="c3195-317">В группе ресурсов выберите имя для регистрации канала канала ленты (ссылка).</span><span class="sxs-lookup"><span data-stu-id="c3195-317">In the resource group, select the bot channel registration name (link).</span></span>
1. <span data-ttu-id="c3195-318">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c3195-318">In the left panel, select **Settings**.</span></span>
1. <span data-ttu-id="c3195-319">В поле **Конечная точка для обмена сообщениями** введите URL-адрес `api/messages`, полученный выше.</span><span class="sxs-lookup"><span data-stu-id="c3195-319">In the **Messaging endpoint** box, enter the URL obtained above followed by `api/messages`.</span></span> <span data-ttu-id="c3195-320">Пример: `https://botteamsauth.azurewebsites.net/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="c3195-320">This is an example: `https://botteamsauth.azurewebsites.net/api/messages`.</span></span>
1. <span data-ttu-id="c3195-321">Нажмите кнопку **сохранить** в левом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="c3195-321">Select the **Save** button in the upper left.</span></span>

## <a name="test-the-bot-using-the-emulator"></a><span data-ttu-id="c3195-322">Тестирование ленты с помощью эмулятора</span><span class="sxs-lookup"><span data-stu-id="c3195-322">Test the bot using the Emulator</span></span>

<span data-ttu-id="c3195-323">Если вы еще не сделали этого, установите [эмулятор Microsoft Bot Framework](https://aka.ms/bot-framework-emulator-readme).</span><span class="sxs-lookup"><span data-stu-id="c3195-323">If you haven't done it already, install the [Microsoft Bot Framework Emulator](https://aka.ms/bot-framework-emulator-readme).</span></span> <span data-ttu-id="c3195-324">См. также [Отладка с помощью эмулятора](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span><span class="sxs-lookup"><span data-stu-id="c3195-324">See also [Debug with the Emulator](https://aka.ms/bot-framework-emulator-debug-with-emulator).</span></span>

<span data-ttu-id="c3195-325">Для работы с примером входа в качестве примера необходимо настроить эмулятор, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c3195-325">In order for the bot sample login to work you must configure the Emulator as shown below.</span></span>

### <a name="configure-the-emulator-for-authentication"></a><span data-ttu-id="c3195-326">Настройка эмулятора для проверки подлинности</span><span class="sxs-lookup"><span data-stu-id="c3195-326">Configure the Emulator for authentication</span></span>

<span data-ttu-id="c3195-327">Если для ленты требуется проверка подлинности, необходимо настроить эмулятор, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="c3195-327">If a bot requires authentication, you must configure the Emulator as shown below.</span></span>

1. <span data-ttu-id="c3195-328">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="c3195-328">Start the Emulator.</span></span>
1. <span data-ttu-id="c3195-329">В симуляторе выберите значок шестеренки &#9881; в левом нижнем углу или на вкладке **Параметры эмулятора** в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="c3195-329">In the Emulator, select the gear icon &#9881; in the bottom left, or the **Emulator Settings** tab in the upper right.</span></span>
1. <span data-ttu-id="c3195-330">Установите флажок, используя **токены проверки подлинности версии 1,0**.</span><span class="sxs-lookup"><span data-stu-id="c3195-330">Check the box by **Use version 1.0 authentication tokens**.</span></span>
1. <span data-ttu-id="c3195-331">Введите локальный путь к средству **ngrok** .</span><span class="sxs-lookup"><span data-stu-id="c3195-331">Enter the local path to the **ngrok** tool.</span></span> <span data-ttu-id="c3195-332">*Посетите* [вики-сайт](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok))поngrokного туннелирования для ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-332">*See* the Bot Framework Emulator / ngrok tunneling integration [Wiki](https://github.com/Microsoft/BotFramework-Emulator/wiki/Tunneling-(ngrok)).</span></span> <span data-ttu-id="c3195-333">Для получения дополнительных сведений о средстве обратитесь к разделу [ngrok](https://ngrok.com/).</span><span class="sxs-lookup"><span data-stu-id="c3195-333">For more tool information, see [ngrok](https://ngrok.com/).</span></span>
1. <span data-ttu-id="c3195-334">Установите флажок, выполнив **ngrok при запуске эмулятора**.</span><span class="sxs-lookup"><span data-stu-id="c3195-334">Check the box by **Run ngrok when the Emulator starts up**.</span></span>
1. <span data-ttu-id="c3195-335">Нажмите кнопку **сохранить** .</span><span class="sxs-lookup"><span data-stu-id="c3195-335">Select the **Save** button.</span></span>

<span data-ttu-id="c3195-336">Когда Bot отображает карточку входа и пользователь выбирает кнопку входа, эмулятор открывает страницу, с помощью которой пользователь может войти в систему с помощью поставщика проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-336">When the bot displays a sign-in card and the user selects the sign-in button, the Emulator opens a page that the user can use to sign in with the authentication provider.</span></span>
<span data-ttu-id="c3195-337">После того как пользователь сделает это, поставщик создает маркер пользователя и отправляет его в Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-337">Once the user does so, the provider generates a user token and sends it to the bot.</span></span> <span data-ttu-id="c3195-338">После этого Bot может работать от имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3195-338">After that, the bot can act on behalf of the user.</span></span>

### <a name="test-the-bot-locally"></a><span data-ttu-id="c3195-339">Тестирование ленты на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="c3195-339">Test the bot locally</span></span>

<span data-ttu-id="c3195-340">После того как вы настроили механизм проверки подлинности, вы можете выполнить собственно тестирование Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-340">After you have configured the authentication mechanism, you can perform the actual bot testing.</span></span>  

1. <span data-ttu-id="c3195-341">Запустите образец Bot на локальном компьютере, используя Visual Studio, например.</span><span class="sxs-lookup"><span data-stu-id="c3195-341">Run the bot sample locally on your machine, via Visual Studio for example.</span></span>
1. <span data-ttu-id="c3195-342">Запустите эмулятор.</span><span class="sxs-lookup"><span data-stu-id="c3195-342">Start the Emulator.</span></span>
1. <span data-ttu-id="c3195-343">Нажмите кнопку **Открыть Bot** .</span><span class="sxs-lookup"><span data-stu-id="c3195-343">Select the **Open bot** button.</span></span>
1. <span data-ttu-id="c3195-344">В **URL-адресе Bot**введите локальный URL-адрес Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-344">In the **Bot URL**, enter the bot's local URL.</span></span> <span data-ttu-id="c3195-345">Как правило `http://localhost:3978/api/messages`,.</span><span class="sxs-lookup"><span data-stu-id="c3195-345">Usually, `http://localhost:3978/api/messages`.</span></span>
1. <span data-ttu-id="c3195-346">В поле **идентификатор приложения Microsoft** введите код приложения Bot из `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="c3195-346">In the **Microsoft App ID** enter the bot's app ID from `appsettings.json`.</span></span>
1. <span data-ttu-id="c3195-347">В поле **пароль Microsoft App** введите пароль приложения Bot в поле `appsettings.json`.</span><span class="sxs-lookup"><span data-stu-id="c3195-347">In the **Microsoft App password** enter the bot's app password from the `appsettings.json`.</span></span>
1. <span data-ttu-id="c3195-348">Нажмите кнопку **подключить**.</span><span class="sxs-lookup"><span data-stu-id="c3195-348">Select **Connect**.</span></span>
1. <span data-ttu-id="c3195-349">После завершения работы с Bot введите любой текст, чтобы отобразить карточку входа.</span><span class="sxs-lookup"><span data-stu-id="c3195-349">After the bot is up and running, enter any text to display the sign-in card.</span></span>
1. <span data-ttu-id="c3195-350">Нажмите кнопку **войти** .</span><span class="sxs-lookup"><span data-stu-id="c3195-350">Select the **Sign in** button.</span></span>
1. <span data-ttu-id="c3195-351">Откроется всплывающее диалоговое окно для **подтверждения открытия URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="c3195-351">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="c3195-352">Это необходимо для того, чтобы пользователь почтового робота (вы) мог пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-352">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="c3195-353">Нажмите кнопку **подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="c3195-353">Select **Confirm**.</span></span>
1. <span data-ttu-id="c3195-354">При появлении запроса выберите учетную запись соответствующей учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3195-354">If asked, select the applicable user's account.</span></span>
1. <span data-ttu-id="c3195-355">В зависимости от того, какая конфигурация использовалась для эмулятора, вы получаете одно из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="c3195-355">Depending which configuration you used for the Emulator, you get one of the following:</span></span>
    1. <span data-ttu-id="c3195-356">**Использование кода проверки при входе**</span><span class="sxs-lookup"><span data-stu-id="c3195-356">**Using sign-in verification code**</span></span>  
      <span data-ttu-id="c3195-357">&#x2713; открывается окно, в котором отображается код проверки.</span><span class="sxs-lookup"><span data-stu-id="c3195-357">&#x2713; A window is opened displaying the validation code.</span></span>  
      <span data-ttu-id="c3195-358">&#x2713; скопировать и ввести код проверки в поле чата, чтобы завершить вход.</span><span class="sxs-lookup"><span data-stu-id="c3195-358">&#x2713; Copy and enter the validation code into the chat box to complete the sign-in.</span></span>
    1. <span data-ttu-id="c3195-359">**Использование маркеров проверки подлинности**.</span><span class="sxs-lookup"><span data-stu-id="c3195-359">**Using authentication tokens**.</span></span>  
      <span data-ttu-id="c3195-360">&#x2713; вы вошли в систему в соответствии с вашими учетными данными.</span><span class="sxs-lookup"><span data-stu-id="c3195-360">&#x2713; You're logged in based on your credentials.</span></span>

    <span data-ttu-id="c3195-361">На следующем рисунке показан пример пользовательского интерфейса ленты после входа в систему.</span><span class="sxs-lookup"><span data-stu-id="c3195-361">The following image is an example of the bot UI after you've logged in:</span></span>

    ![подлинность эмулятора входа Bot](../../../assets/images/authentication/auth-bot-login-emulator.PNG)

1. <span data-ttu-id="c3195-363">Если вы выберете **Да** , когда приглашение *будет просматривать ваш маркер?*, вы получите ответ, аналогичный следующему:</span><span class="sxs-lookup"><span data-stu-id="c3195-363">If you select **Yes** when the bot asks *Would you like to view your token?*, you'll get a response similar to the following:</span></span>

    ![маркер для проверки подлинности канала входа на Bot](../../../assets/images/authentication/auth-bot-login-emulator-token.png)

1. <span data-ttu-id="c3195-365">Введите **logout** во входном поле чата, чтобы выйти из системы. Он освобождает маркер пользователя, и Bot не сможет действовать от вашего имени, пока вы не выполните вход в систему.</span><span class="sxs-lookup"><span data-stu-id="c3195-365">Enter **logout** in the input chat box to sign out. This releases the user token, and the bot won't be able to act on your behalf until you sign in again.</span></span>

> [!NOTE]
> <span data-ttu-id="c3195-366">Для проверки подлинности с помощью Bot требуется **Служба соединителя Bot**.</span><span class="sxs-lookup"><span data-stu-id="c3195-366">Bot authentication requires use of the **Bot Connector Service**.</span></span> <span data-ttu-id="c3195-367">Служба получает доступ к сведениям о регистрации каналов ленты для Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-367">The service accesses the bot channels registration information for your bot.</span></span>

## <a name="test-the-deployed-bot"></a><span data-ttu-id="c3195-368">Тестирование развернутой ленты</span><span class="sxs-lookup"><span data-stu-id="c3195-368">Test the deployed bot</span></span>

<!--There are several testing scenarios here. Ideally, we'd have a separate article on the what, why, 
and when for these, and just reference that from here, along with the set of steps that exercises the bot code.-->

1. <span data-ttu-id="c3195-369">В браузере перейдите на [**портал Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c3195-369">In your browser, navigate to the [**Azure portal**][azure-portal].</span></span>
1. <span data-ttu-id="c3195-370">Найдите группу ресурсов.</span><span class="sxs-lookup"><span data-stu-id="c3195-370">Find your resource group.</span></span>
1. <span data-ttu-id="c3195-371">Выберите ссылку ресурс.</span><span class="sxs-lookup"><span data-stu-id="c3195-371">Select the resource link.</span></span> <span data-ttu-id="c3195-372">Отобразится страница ресурса.</span><span class="sxs-lookup"><span data-stu-id="c3195-372">The resource page is displayed.</span></span>
1. <span data-ttu-id="c3195-373">На странице ресурс выберите пункт **Проверка в веб-чата**.</span><span class="sxs-lookup"><span data-stu-id="c3195-373">In the resource page, select **Test in Web Chat**.</span></span> <span data-ttu-id="c3195-374">Начнется запуск ленты и отображается предварительно заданные приветствия.</span><span class="sxs-lookup"><span data-stu-id="c3195-374">The bot starts and displays the predefined greetings.</span></span>
1. <span data-ttu-id="c3195-375">Введите что-либо в поле Chat.</span><span class="sxs-lookup"><span data-stu-id="c3195-375">Type anything in the chat box.</span></span>
1. <span data-ttu-id="c3195-376">Выберите поле **Вход** .</span><span class="sxs-lookup"><span data-stu-id="c3195-376">Select the **Sign in** box.</span></span>
1. <span data-ttu-id="c3195-377">Откроется всплывающее диалоговое окно для **подтверждения открытия URL-адреса**.</span><span class="sxs-lookup"><span data-stu-id="c3195-377">A pop-up dialog is displayed to **Confirm Open URL**.</span></span> <span data-ttu-id="c3195-378">Это необходимо для того, чтобы пользователь почтового робота (вы) мог пройти проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-378">This is to allow the bot's user (you) to be authenticated.</span></span>  
1. <span data-ttu-id="c3195-379">Нажмите кнопку **подтвердить**.</span><span class="sxs-lookup"><span data-stu-id="c3195-379">Select **Confirm**.</span></span>
1. <span data-ttu-id="c3195-380">При появлении запроса выберите учетную запись соответствующей учетной записи пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3195-380">If asked, select the applicable user's account.</span></span>
    <span data-ttu-id="c3195-381">На следующем рисунке показан пример пользовательского интерфейса ленты после входа:</span><span class="sxs-lookup"><span data-stu-id="c3195-381">The following image is an example of the bot UI after you have logged in:</span></span>

    ![развернутая учетная запись Bot авторизации](../../../assets/images/authentication/auth-bot-login-deployed.PNG)<span data-ttu-id="c3195-383">.</span><span class="sxs-lookup"><span data-stu-id="c3195-383">.</span></span>

1. <span data-ttu-id="c3195-384">Нажмите кнопку **Да** , чтобы отобразить маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-384">Select the **Yes** button to display your authentication token.</span></span> <span data-ttu-id="c3195-385">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-385">The following image is an example:</span></span>

    ![маркер проверки подлинности, развернутый маркер входа](../../../assets/images/authentication/auth-bot-login-deployed-token.PNG)<span data-ttu-id="c3195-387">.</span><span class="sxs-lookup"><span data-stu-id="c3195-387">.</span></span>

1. <span data-ttu-id="c3195-388">Введите Logout, чтобы выйти из системы.</span><span class="sxs-lookup"><span data-stu-id="c3195-388">Enter logout to sign out.</span></span>

    ![подлинность развернутого выхода в Bot](../../../assets/images/authentication/auth-bot-deployed-logout.PNG)

> [!NOTE]
> <span data-ttu-id="c3195-390">Если у вас возникли проблемы с входом в систему, попробуйте снова проверить подключение, как описано в предыдущих шагах.</span><span class="sxs-lookup"><span data-stu-id="c3195-390">If you're having problems signing in, try to test the connection again as described in the previous steps.</span></span> <span data-ttu-id="c3195-391">Это может привести к повторному созданию маркера проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="c3195-391">This could recreate the authentication token.</span></span>
> <span data-ttu-id="c3195-392">С помощью клиента веб-чата ленты в Azure может потребоваться выполнить вход несколько раз, чтобы проверка подлинности была установлена правильно.</span><span class="sxs-lookup"><span data-stu-id="c3195-392">With the Bot Framework Web Chat client in Azure, you may need to sign in several times before the authentication is established correctly.</span></span>

## <a name="install-and-test-the-bot-in-teams"></a><span data-ttu-id="c3195-393">Установка и тестирование программы Bot в Teams</span><span class="sxs-lookup"><span data-stu-id="c3195-393">Install and test the bot in Teams</span></span>

1. <span data-ttu-id="c3195-394">В проекте `TeamsAppManifest` Bot убедитесь, что папка содержит `manifest.json` вместе с файлами `outline.png` и. `color.png`</span><span class="sxs-lookup"><span data-stu-id="c3195-394">In your bot project, ensure that the `TeamsAppManifest` folder contains the `manifest.json` along with an `outline.png` and `color.png` files.</span></span>
1. <span data-ttu-id="c3195-395">В обозревателе решений перейдите к `TeamsAppManifest` папке.</span><span class="sxs-lookup"><span data-stu-id="c3195-395">In Solution Explorer, navigate to the `TeamsAppManifest` folder.</span></span> <span data-ttu-id="c3195-396">Изменить `manifest.json` , назначая следующие значения:</span><span class="sxs-lookup"><span data-stu-id="c3195-396">Edit `manifest.json` by assigning the following values:</span></span>
    1. <span data-ttu-id="c3195-397">Убедитесь, что **код приложения-робота** , полученный во время регистрации канала ленты, назначен `id` и. `botId`</span><span class="sxs-lookup"><span data-stu-id="c3195-397">Ensure that the **bot App ID** you received at the time of the bot channel registration is assigned to `id` and `botId`.</span></span>
    1. <span data-ttu-id="c3195-398">Назначьте это значение: `validDomains: [ "token.botframework.com" ]`.</span><span class="sxs-lookup"><span data-stu-id="c3195-398">Assign this value: `validDomains: [ "token.botframework.com" ]`.</span></span>
1. <span data-ttu-id="c3195-399">Выбор и **почтовые индексы** для `manifest.json` `outline.png`и `color.png` файлов.</span><span class="sxs-lookup"><span data-stu-id="c3195-399">Select and **zip** the `manifest.json`, `outline.png`, and `color.png` files.</span></span>
1. <span data-ttu-id="c3195-400">Откройте **Microsoft Teams**.</span><span class="sxs-lookup"><span data-stu-id="c3195-400">Open **Microsoft Teams**.</span></span>
1. <span data-ttu-id="c3195-401">В нижней панели слева щелкните **значок приложения**.</span><span class="sxs-lookup"><span data-stu-id="c3195-401">In the left panel, at the bottom, select the **Apps icon**.</span></span>
1. <span data-ttu-id="c3195-402">На правой панели в нижней части выберите **Отправить пользовательское приложение**.</span><span class="sxs-lookup"><span data-stu-id="c3195-402">In the right panel, at the bottom, select **Upload a custom app**.</span></span>
1. <span data-ttu-id="c3195-403">Перейдите к `TeamsAppManifest` папке и отправьте манифест ZIP.</span><span class="sxs-lookup"><span data-stu-id="c3195-403">Navigate to the `TeamsAppManifest` folder and upload the zipped manifest.</span></span>
<span data-ttu-id="c3195-404">Отобразится следующий мастер:</span><span class="sxs-lookup"><span data-stu-id="c3195-404">The following wizard is displayed:</span></span>

    ![Отправка подлинности команд ленты i](../../../assets/images/authentication/auth-bot-teams-upload.png)

1. <span data-ttu-id="c3195-406">Нажмите кнопку **Добавить в группу** .</span><span class="sxs-lookup"><span data-stu-id="c3195-406">Select the **Add to a team** button.</span></span>
1. <span data-ttu-id="c3195-407">В следующем окне выберите группу, в которой вы хотите использовать элемент Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-407">In the next window, select the team where you want to use the bot.</span></span>
1. <span data-ttu-id="c3195-408">Нажмите кнопку **Настройка ленты** .</span><span class="sxs-lookup"><span data-stu-id="c3195-408">Select the **Set up a bot** button.</span></span>
1. <span data-ttu-id="c3195-409">Выберите три точки (&#x25cf;&#x25cf;&#x25cf;) на левой панели.</span><span class="sxs-lookup"><span data-stu-id="c3195-409">Select the three dots (&#x25cf;&#x25cf;&#x25cf;) in the left panel.</span></span> <span data-ttu-id="c3195-410">Затем выберите значок **app Studio (App Studio** ).</span><span class="sxs-lookup"><span data-stu-id="c3195-410">Then select the **App Studio** icon.</span></span>
1. <span data-ttu-id="c3195-411">Перейдите на вкладку **редактор манифестов** . Вы увидите значок для отправленного ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-411">Select the **Manifest editor** tab. You should see the icon for the bot you uploaded.</span></span>
1. <span data-ttu-id="c3195-412">Кроме того, вы увидите, что в списке бесед, который вы можете использовать для обмена сообщениями с роботом, указан в качестве контакта.</span><span class="sxs-lookup"><span data-stu-id="c3195-412">Also, you should be able to see the bot listed as a contact in the chat list that you can use to exchange messages with the bot.</span></span>

### <a name="testing-the-bot-locally-in-teams"></a><span data-ttu-id="c3195-413">Тестирование ленты на локальном компьютере в Teams</span><span class="sxs-lookup"><span data-stu-id="c3195-413">Testing the bot locally in Teams</span></span>

<span data-ttu-id="c3195-414">Microsoft Teams — это полностью облачный продукт, требующий, чтобы все службы, к которым он обращается, были доступны из облака с помощью конечных точек HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c3195-414">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="c3195-415">Таким образом, чтобы включить "bot" (наш образец) для работы в Teams, необходимо либо опубликовать код в выбранном вами облаке, либо сделать локальный экземпляр доступным извне с помощью средства **туннелирования** .</span><span class="sxs-lookup"><span data-stu-id="c3195-415">Therefore, to enable the bot (our sample) to work in Teams, you need to either publish the code to the cloud of your choice, or make a locally running instance externally accessible via a **tunneling** tool.</span></span> <span data-ttu-id="c3195-416">Мы рекомендуем [ngrok](https://ngrok.com/download), который создает доступ к внешнему URL-адресу для порта, который вы откроете локально на вашем компьютере.</span><span class="sxs-lookup"><span data-stu-id="c3195-416">We recommend  [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span>
<span data-ttu-id="c3195-417">Чтобы настроить ngrok в процессе подготовки к запуску приложения Microsoft Teams, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c3195-417">To set up ngrok in preparation for running your Microsoft Teams app locally, follow these steps:</span></span>

1. <span data-ttu-id="c3195-418">В окне терминала перейдите к каталогу, в котором `ngrok.exe` установлен.</span><span class="sxs-lookup"><span data-stu-id="c3195-418">In a terminal window, go the directory where you have `ngrok.exe` installed.</span></span> <span data-ttu-id="c3195-419">Рекомендуется установить для *переменной среды* путь, указывающий на нее.</span><span class="sxs-lookup"><span data-stu-id="c3195-419">We suggest setting the *environment variable* path to point to it.</span></span>
1. <span data-ttu-id="c3195-420">Запустите, например `ngrok http 3978 --host-header=localhost:3978`.</span><span class="sxs-lookup"><span data-stu-id="c3195-420">Run, for example, `ngrok http 3978 --host-header=localhost:3978`.</span></span> <span data-ttu-id="c3195-421">При необходимости замените номер порта.</span><span class="sxs-lookup"><span data-stu-id="c3195-421">Replace the port number as needed.</span></span>
<span data-ttu-id="c3195-422">Будет запущен ngrok для прослушивания указанного порта.</span><span class="sxs-lookup"><span data-stu-id="c3195-422">This launches ngrok to listen on the port you specify.</span></span> <span data-ttu-id="c3195-423">В качестве возврата вы получите URL-адрес с внешним адресом, допустимый до тех пор, пока работает ngrok.</span><span class="sxs-lookup"><span data-stu-id="c3195-423">In return, it gives you an externally addressable URL, valid for as long as ngrok is running.</span></span> <span data-ttu-id="c3195-424">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-424">The following image is an example:</span></span>

    ![Строка подключения Боты приложения Teams для проверки подлинности adv1](../../../assets/images/authentication/auth-bot-ngrok-start.PNG)<span data-ttu-id="c3195-426">.</span><span class="sxs-lookup"><span data-stu-id="c3195-426">.</span></span>

1. <span data-ttu-id="c3195-427">Скопируйте HTTPS адрес переадресации.</span><span class="sxs-lookup"><span data-stu-id="c3195-427">Copy the forwarding HTTPS address.</span></span> <span data-ttu-id="c3195-428">Он должен иметь следующий вид: `https://dea822bf.ngrok.io/`.</span><span class="sxs-lookup"><span data-stu-id="c3195-428">It should be similar to the following: `https://dea822bf.ngrok.io/`.</span></span>
1. <span data-ttu-id="c3195-429">Append `/api/messages` — получение `https://dea822bf.ngrok.io/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="c3195-429">Append `/api/messages` to obtain `https://dea822bf.ngrok.io/api/messages`.</span></span> <span data-ttu-id="c3195-430">Это **Конечная точка сообщений** для Bot, выполняемая локально на компьютере и доступная через Интернет в чате в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="c3195-430">This is the **messages endpoint** for the bot running locally on your machine and reachable over the web in a chat in Microsoft Teams.</span></span>
1. <span data-ttu-id="c3195-431">Один из последних действий — обновление конечной точки сообщений развернутой ленты.</span><span class="sxs-lookup"><span data-stu-id="c3195-431">One final step to perform is to update the messages endpoint of the deployed bot.</span></span> <span data-ttu-id="c3195-432">В этом примере мы развернули элемент Bot в Azure.</span><span class="sxs-lookup"><span data-stu-id="c3195-432">In the example, we deployed the bot in Azure.</span></span> <span data-ttu-id="c3195-433">Итак, \* \* выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="c3195-433">So \*\*let's perform these steps:</span></span>
    1. <span data-ttu-id="c3195-434">В браузере перейдите на [**портал Azure**][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="c3195-434">In your browser navigate to the [**Azure portal**][azure-portal].</span></span>
    1. <span data-ttu-id="c3195-435">Выберите **регистрацию канала Bot**.</span><span class="sxs-lookup"><span data-stu-id="c3195-435">Select your **Bot Channel Registration**.</span></span>
    1. <span data-ttu-id="c3195-436">В левой панели выберите **Параметры**.</span><span class="sxs-lookup"><span data-stu-id="c3195-436">In the left panel, select **Settings**.</span></span>
    1. <span data-ttu-id="c3195-437">На правой панели в поле **Конечная точка обмена сообщениями** введите URL-адрес ngrok в нашем примере `https://dea822bf.ngrok.io/api/messages`.</span><span class="sxs-lookup"><span data-stu-id="c3195-437">In the right panel, in the **Messaging endpoint** box, enter the ngrok URL, in our example, `https://dea822bf.ngrok.io/api/messages`.</span></span>
1. <span data-ttu-id="c3195-438">Запустите Bot на локальном компьютере, например в режиме отладки Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3195-438">Start your bot locally, for example in Visual Studio debug mode.</span></span>
1. <span data-ttu-id="c3195-439">Протестируйте Bot при локальном запуске с помощью **тестового веб-чата**портала Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="c3195-439">Test the bot while running locally using the Bot Framework portal's **Test Web chat**.</span></span> <span data-ttu-id="c3195-440">Как и эмулятор, этот тест не позволяет получить доступ к функциональным возможностям, характерным для Teams.</span><span class="sxs-lookup"><span data-stu-id="c3195-440">Like the Emulator, this test doesn't allow you to access Teams-specific functionality.</span></span>
1. <span data-ttu-id="c3195-441">В окне терминала, где `ngrok` работает, можно видеть HTTP-трафик между Bot и клиентом веб-чата.</span><span class="sxs-lookup"><span data-stu-id="c3195-441">In the terminal window where `ngrok` is running you can see HTTP traffic between the bot and the web chat client.</span></span> <span data-ttu-id="c3195-442">Если требуется более подробное представление, в окне браузера введите `http://127.0.0.1:4040` , полученное из предыдущего окна терминала.</span><span class="sxs-lookup"><span data-stu-id="c3195-442">If you want a more detailed view, in a browser window enter `http://127.0.0.1:4040` you obtained from the previous terminal window.</span></span> <span data-ttu-id="c3195-443">Ниже приведен пример такого изображения.</span><span class="sxs-lookup"><span data-stu-id="c3195-443">The following image is an example:</span></span>

    ![Проверка подлинности ngrok Teams i Teams](../../../assets/images/authentication/auth-bot-teams-ngrok-testing.png)<span data-ttu-id="c3195-445">.</span><span class="sxs-lookup"><span data-stu-id="c3195-445">.</span></span>

> [!NOTE]
> <span data-ttu-id="c3195-446">Если остановить и перезапустить ngrok, URL-адрес изменится.</span><span class="sxs-lookup"><span data-stu-id="c3195-446">If you stop and restart ngrok, the URL changes.</span></span> <span data-ttu-id="c3195-447">Чтобы использовать ngrok в проекте и в зависимости от используемых возможностей, необходимо обновить все URL-ссылки.</span><span class="sxs-lookup"><span data-stu-id="c3195-447">To use ngrok in your project, and depending on the capabilities you're using, you must update all URL references.</span></span>

## <a name="additional-information"></a><span data-ttu-id="c3195-448">Дополнительные сведения</span><span class="sxs-lookup"><span data-stu-id="c3195-448">Additional information</span></span>

### <a name="teamsappmanifestmanifestjson"></a><span data-ttu-id="c3195-449">Теамсаппманифест/manifest. JSON</span><span class="sxs-lookup"><span data-stu-id="c3195-449">TeamsAppManifest/manifest.json</span></span>

<span data-ttu-id="c3195-450">Этот манифест содержит сведения, необходимые Microsoft Teams для связи с Bot.</span><span class="sxs-lookup"><span data-stu-id="c3195-450">This manifest contains information needed by Microsoft Teams to connect with the bot.</span></span>  

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

<span data-ttu-id="c3195-451">При использовании проверки подлинности Teams немного отличается от других каналов, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="c3195-451">With authentication, Teams behaves slightly differently than other channels, as explained below.</span></span>

### <a name="handling-invoke-activity"></a><span data-ttu-id="c3195-452">Обработка действия Invoke</span><span class="sxs-lookup"><span data-stu-id="c3195-452">Handling Invoke Activity</span></span>

<span data-ttu-id="c3195-453">**Действие Invoke** отправляется на сервер робота, а не на событие, используемое другими каналами.</span><span class="sxs-lookup"><span data-stu-id="c3195-453">An **Invoke Activity** is sent to the bot rather than the Event Activity used by other channels.</span></span>
<span data-ttu-id="c3195-454">Это делается с помощью дочерних классов **активитихандлер**.</span><span class="sxs-lookup"><span data-stu-id="c3195-454">This is done by sub-classing the **ActivityHandler**.</span></span>

<span data-ttu-id="c3195-455">**Боты/Диалогбот. CS**</span><span class="sxs-lookup"><span data-stu-id="c3195-455">**Bots/DialogBot.cs**</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="c3195-456">ЯЗЫК C#/.НЕТ</span><span class="sxs-lookup"><span data-stu-id="c3195-456">C#/.NET</span></span>](#tab/dotnet)

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/DialogBot.cs?range=19-51)]

<span data-ttu-id="c3195-457">**Боты/Теамсбот. CS**</span><span class="sxs-lookup"><span data-stu-id="c3195-457">**Bots/TeamsBot.cs**</span></span>

<span data-ttu-id="c3195-458">*Действие Invoke* необходимо перенаправить в диалоговое окно, если используется **оауспромпт** .</span><span class="sxs-lookup"><span data-stu-id="c3195-458">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-csharp[ActivityHandler](~/../botbuilder-samples/samples/csharp_dotnetcore/46.teams-auth/Bots/TeamsBot.cs?range=34-42)]

#### <a name="teamsactivityhandlercs"></a><span data-ttu-id="c3195-459">TeamsActivityHandler.cs</span><span class="sxs-lookup"><span data-stu-id="c3195-459">TeamsActivityHandler.cs</span></span>

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

# <a name="pythontabpython"></a>[<span data-ttu-id="c3195-460">Python</span><span class="sxs-lookup"><span data-stu-id="c3195-460">Python</span></span>](#tab/python)

<span data-ttu-id="c3195-461">**Боты/dialog_bot. Корректировка**</span><span class="sxs-lookup"><span data-stu-id="c3195-461">**bots/dialog_bot.py**</span></span>

[!code-python[ActivityHandler](~/../botbuilder-samples/samples/python/46.teams-auth/bots/dialog_bot.py?range=10-42)]

<span data-ttu-id="c3195-462">**Боты/teams_bot. Корректировка**</span><span class="sxs-lookup"><span data-stu-id="c3195-462">**bots/teams_bot.py**</span></span>

<span data-ttu-id="c3195-463">*Действие Invoke* необходимо перенаправить в диалоговое окно, если используется **оауспромпт** .</span><span class="sxs-lookup"><span data-stu-id="c3195-463">The *Invoke Activity* must be forwarded to the dialog if the **OAuthPrompt** is used.</span></span>

[!code-python[on_token_response_event](~/../botbuilder-samples/samples/python/46.teams-auth/bots/teams_bot.py?range=38-45)] 

<span data-ttu-id="c3195-464">**диалоговые окна/main_dialog. Корректировка**</span><span class="sxs-lookup"><span data-stu-id="c3195-464">**dialogs/main_dialog.py**</span></span>

<span data-ttu-id="c3195-465">На шаге диалогового окна используйте `begin_dialog` для запуска приглашения OAuth, в котором пользователю предлагается выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="c3195-465">Within a dialog step, use `begin_dialog` to start the OAuth prompt, which asks the user to sign in.</span></span>

- <span data-ttu-id="c3195-466">Если пользователь уже выполнил вход, будет создано событие отклика маркера без запроса пользователя.</span><span class="sxs-lookup"><span data-stu-id="c3195-466">If the user is already signed in, this will generate a token response event, without prompting the user.</span></span>
- <span data-ttu-id="c3195-467">В противном случае пользователю будет предложено выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="c3195-467">Otherwise, this will prompt the user to sign in.</span></span> <span data-ttu-id="c3195-468">Служба Azure Bot отправляет событие ответа маркера после того, как пользователь попытается выполнить вход.</span><span class="sxs-lookup"><span data-stu-id="c3195-468">The Azure Bot Service sends the token response event after the user attempts to sign in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=48-49)]

<span data-ttu-id="c3195-469">На следующем этапе диалога проверьте наличие маркера в результатах предыдущего действия.</span><span class="sxs-lookup"><span data-stu-id="c3195-469">Within the following dialog step, check for the presence of a token in the result from the previous step.</span></span> <span data-ttu-id="c3195-470">Если значение не равно null, пользователь успешно выполнил вход.</span><span class="sxs-lookup"><span data-stu-id="c3195-470">If it is not null, the user successfully signed in.</span></span>

[!code-python[Add OAuthPrompt](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/main_dialog.py?range=54-65)]

<span data-ttu-id="c3195-471">**диалоговые окна/logout_dialog. Корректировка**</span><span class="sxs-lookup"><span data-stu-id="c3195-471">**dialogs/logout_dialog.py**</span></span>

[!code-python[allow logout](~/../botbuilder-samples/samples/python/46.teams-auth/dialogs/logout_dialog.py?range=29-36&highlight=6)]

---

## <a name="further-reading"></a><span data-ttu-id="c3195-472">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c3195-472">Further reading</span></span>

- [<span data-ttu-id="c3195-473">Добавление проверки подлинности в Bot через службу Bot Azure</span><span class="sxs-lookup"><span data-stu-id="c3195-473">Add authentication to your bot via Azure Bot Service</span></span>](https://aka.ms/azure-bot-add-authentication)

<!-- Footnote-style links -->

[azure-portal]: https://ms.portal.azure.com

[concept-basics]: https://docs.microsoft.com/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0
[concept-state]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-state?view=azure-bot-service-4.0
[concept-dialogs]: https://docs.microsoft.com/azure/bot-service/bot-builder-concept-dialog?view=azure-bot-service-4.0
[simple-dialog]: https://docs.microsoft.com/azure/bot-service/bot-builder-dialog-manage-conversation-flow?view=azure-bot-service-4.0

[teams-auth-bot]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth

[teams-auth-bot-py]: https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/python/46.teams-auth

[azure-aad-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview
[aad-registration-blade]: https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredAppsPreview