---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик ботов может использовать карточку для входов или службу ботов Azure с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка службы SSO для ботов
ms.topic: conceptual
ms.openlocfilehash: 55b930ba50eede6ac970fbe0f901d418605f3f91
ms.sourcegitcommit: 5662bf23fafdbcc6d06f826a647f3696cd17f5e5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/22/2021
ms.locfileid: "49935256"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="6217b-105">Поддержка единого входов (SSO) для ботов</span><span class="sxs-lookup"><span data-stu-id="6217b-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="6217b-106">Проверка подлинности с единым входом в Azure Active Directory (AAD) минимизирует количество случаев, когда пользователям необходимо вводить свои учетные данные путем обновления маркера проверки подлинности автоматически.</span><span class="sxs-lookup"><span data-stu-id="6217b-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="6217b-107">Если пользователи соглашаются использовать ваше приложение, им не нужно повторно предоставлять согласие на другом устройстве и они могут автоматически входить в приложение.</span><span class="sxs-lookup"><span data-stu-id="6217b-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="6217b-108">Поток похож на тот, который поддерживается службой [SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)для вкладок Microsoft [](#request-a-bot-token) Teams, однако разница заключается в протоколе запроса маркеров и получения ответов [ботом.](#receive-the-bot-token)</span><span class="sxs-lookup"><span data-stu-id="6217b-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="6217b-109">OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый AAD и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="6217b-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="6217b-110">Базовое понимание OAuth 2.0 является необходимым условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="6217b-111">Бот SSO во время работы</span><span class="sxs-lookup"><span data-stu-id="6217b-111">Bot SSO at runtime</span></span>

![Схема SSO бота во время работы](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="6217b-113">Выполните следующие действия, чтобы получить аутентификацию и маркеры приложения-бота:</span><span class="sxs-lookup"><span data-stu-id="6217b-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="6217b-114">Бот отправляет сообщение со свойством OAuthCard. `tokenExchangeResource`</span><span class="sxs-lookup"><span data-stu-id="6217b-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="6217b-115">Он сообщает Teams, что необходимо получить маркер проверки подлинности для приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="6217b-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="6217b-116">Пользователь получает сообщения на всех активных конечных точках пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="6217b-117">Пользователь может одновременно иметь несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="6217b-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="6217b-118">Маркер бота получается от каждой активной конечной точки пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="6217b-119">Приложение должно быть установлено в личной области для поддержки SSO.</span><span class="sxs-lookup"><span data-stu-id="6217b-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="6217b-120">Если текущий пользователь использует ваше приложение-бот в первый раз, появится запрос с запросом на одно из следующих этапов:</span><span class="sxs-lookup"><span data-stu-id="6217b-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="6217b-121">Предоставление согласия при необходимости.</span><span class="sxs-lookup"><span data-stu-id="6217b-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="6217b-122">Обработка проверки подлинности с пошаговой проверкой подлинности, например двух факторов.</span><span class="sxs-lookup"><span data-stu-id="6217b-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="6217b-123">Teams запрашивает маркер приложения-бота из конечной точки AAD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="6217b-124">AAD отправляет маркер приложения-бота в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="6217b-125">Teams отправляет маркер боту как часть объекта значения, возвращаемого действием вызова с именем **sign-in/tokenExchange.**</span><span class="sxs-lookup"><span data-stu-id="6217b-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="6217b-126">Разноравневый маркер в приложении-боте предоставляет необходимые сведения, например адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="6217b-127">Разработка бота SSO Teams</span><span class="sxs-lookup"><span data-stu-id="6217b-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="6217b-128">Выполните следующие действия, чтобы разработать бот Для SSO Teams:</span><span class="sxs-lookup"><span data-stu-id="6217b-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="6217b-129">[Зарегистрируйте свое приложение на портале AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="6217b-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="6217b-130">[Обновите манифест приложения Teams для бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="6217b-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="6217b-131">[Добавьте код для запроса и получения маркера бота.](#add-the-code-to-request-and-receive-a-bot-token)</span><span class="sxs-lookup"><span data-stu-id="6217b-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="6217b-132">Регистрация приложения на портале AAD</span><span class="sxs-lookup"><span data-stu-id="6217b-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="6217b-133">Действия для регистрации приложения на портале AAD похожи на поток [SSO табули.](../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="6217b-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="6217b-134">Чтобы зарегистрировать приложение, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="6217b-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="6217b-135">Зарегистрируйте новое приложение на [портале Регистрации приложений Azure Active Directory.](https://go.microsoft.com/fwlink/?linkid=2083908)</span><span class="sxs-lookup"><span data-stu-id="6217b-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="6217b-136">Выберите **новую регистрацию.**</span><span class="sxs-lookup"><span data-stu-id="6217b-136">Select **New Registration**.</span></span> <span data-ttu-id="6217b-137">Появится **страница "Регистрация** приложения".</span><span class="sxs-lookup"><span data-stu-id="6217b-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="6217b-138">На странице **"Регистрация приложения"** введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="6217b-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="6217b-139">Введите **имя** приложения.</span><span class="sxs-lookup"><span data-stu-id="6217b-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="6217b-140">Выберите **поддерживаемые типы учетных записей,** выберите один клиент или тип мультитенантной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="6217b-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="6217b-141">Пользователи не запрашивают согласие и сразу им ируются маркеры доступа, если приложение AAD зарегистрировано в том же клиенте, где они делают запрос на проверку подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="6217b-142">Однако пользователи должны предоставить согласие на предоставление разрешений, если приложение AAD зарегистрировано в другом клиенте.</span><span class="sxs-lookup"><span data-stu-id="6217b-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="6217b-143">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="6217b-143">Choose **Register**.</span></span>
4. <span data-ttu-id="6217b-144">На странице обзора скопируйте и сохраните ИД приложения **(клиента).**</span><span class="sxs-lookup"><span data-stu-id="6217b-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="6217b-145">Оно потребуется позже при обновлении манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="6217b-146">В разделе **Управление** выберите **Предоставление API**.</span><span class="sxs-lookup"><span data-stu-id="6217b-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="6217b-147">Если вы строите автономный бот, введите URI ИД приложения как `api://botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="6217b-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="6217b-148">Здесь **YourBotId** — ваш ИД приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="6217b-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="6217b-149">Если вы строите приложение с помощью бота и вкладки, введите URI ИД приложения как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="6217b-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="6217b-150">Выберите разрешения, необходимые приложению для конечной точки AAD и (при желании) для Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="6217b-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="6217b-151">[Предоставление разрешений для](/azure/active-directory/develop/v2-permissions-and-consent) классических, веб-и мобильных приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="6217b-152">Выберите **"Добавить область".**</span><span class="sxs-lookup"><span data-stu-id="6217b-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="6217b-153">На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **области.**</span><span class="sxs-lookup"><span data-stu-id="6217b-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="6217b-154">Область "access_as_user", используемая для добавления клиентского приложения, — "Администраторы и пользователи".</span><span class="sxs-lookup"><span data-stu-id="6217b-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="6217b-155">Необходимо помнить о следующих важных ограничениях:</span><span class="sxs-lookup"><span data-stu-id="6217b-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="6217b-156">Поддерживаются только разрешения API Microsoft Graph на уровне пользователя, такие как электронная почта, профиль, offline_access и OpenId.</span><span class="sxs-lookup"><span data-stu-id="6217b-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="6217b-157">Если вам нужен доступ к другим областьм Microsoft Graph, например или, см. `User.Read` `Mail.Read` [рекомендуемое решение.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)</span><span class="sxs-lookup"><span data-stu-id="6217b-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes).</span></span>
    > * <span data-ttu-id="6217b-158">Доменное имя приложения должно быть таким же, как и доменное имя, зарегистрированное для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="6217b-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="6217b-159">Несколько доменов на приложение в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="6217b-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="6217b-160">Приложения, которые используют домен, не поддерживаются, так как они являются общими и `azurewebsites.net` могут быть угрозой безопасности.</span><span class="sxs-lookup"><span data-stu-id="6217b-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="6217b-161">Обновление портала Azure с помощью подключения OAuth</span><span class="sxs-lookup"><span data-stu-id="6217b-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="6217b-162">Выполните следующие действия, чтобы обновить портал Azure с подключением OAuth:</span><span class="sxs-lookup"><span data-stu-id="6217b-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="6217b-163">На портале Azure перейдите к процедуре **регистрации каналов ботов.**</span><span class="sxs-lookup"><span data-stu-id="6217b-163">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="6217b-164">Перейдите **к разрешениям API.**</span><span class="sxs-lookup"><span data-stu-id="6217b-164">Go to **API Permissions**.</span></span> <span data-ttu-id="6217b-165">Выберите **"Добавить разрешения microsoft**  >  **Graph**  >  **Delegated permissions",** а затем добавьте следующие разрешения из API Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="6217b-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="6217b-166">User.Read (включен по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="6217b-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="6217b-167">email</span><span class="sxs-lookup"><span data-stu-id="6217b-167">email</span></span>
    * <span data-ttu-id="6217b-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="6217b-168">offline_access</span></span>
    * <span data-ttu-id="6217b-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="6217b-169">OpenId</span></span>
    * <span data-ttu-id="6217b-170">profile</span><span class="sxs-lookup"><span data-stu-id="6217b-170">profile</span></span>

3. <span data-ttu-id="6217b-171">Выберите **"Параметры"** в левой области и выберите "Добавить **параметр"** в разделе "Параметры подключения **OAuth".**</span><span class="sxs-lookup"><span data-stu-id="6217b-171">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. <span data-ttu-id="6217b-173">Выполните следующие действия, чтобы заполнить форму **"Создать параметр подключения":**</span><span class="sxs-lookup"><span data-stu-id="6217b-173">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="6217b-174">**В приложении** AAD может потребоваться неявное предоставление.</span><span class="sxs-lookup"><span data-stu-id="6217b-174">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="6217b-175">Введите **имя на** странице **"Новый параметр подключения".**</span><span class="sxs-lookup"><span data-stu-id="6217b-175">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="6217b-176">Это имя, на которое ссылается код службы ботов в *шаге 5* bot [SSO во время работы.](#bot-sso-at-runtime)</span><span class="sxs-lookup"><span data-stu-id="6217b-176">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="6217b-177">В **выпадаемом каталоге "Поставщик** услуг" выберите **Azure Active Directory 2.**</span><span class="sxs-lookup"><span data-stu-id="6217b-177">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="6217b-178">Введите учетные данные клиента, такие как **ид клиента** и **секрет** клиента для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="6217b-178">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="6217b-179">Для **URL-адреса Exchange маркера** используйте значение области, определенное в манифесте приложения [Teams для бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="6217b-179">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="6217b-180">URL-адрес Exchange маркеров указывает SDK, что это приложение AAD настроено для SSO.</span><span class="sxs-lookup"><span data-stu-id="6217b-180">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="6217b-181">В поле **"ИД клиента"** *введите общий.*</span><span class="sxs-lookup"><span data-stu-id="6217b-181">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="6217b-182">Добавьте все **области, настроенные** при указании разрешений для нисходящего API для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="6217b-182">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="6217b-183">При условии, что в хранилище маркеров есть ИД клиента и секрет клиента, он обменивается маркером на маркер графа с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="6217b-183">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="6217b-184">Выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="6217b-184">Select **Save**.</span></span>

    ![Представление Параметров VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="6217b-186">Обновление манифеста приложения Teams для бота</span><span class="sxs-lookup"><span data-stu-id="6217b-186">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="6217b-187">Если приложение содержит автономный бот, используйте следующий код для добавления новых свойств в манифест приложения Teams:</span><span class="sxs-lookup"><span data-stu-id="6217b-187">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="6217b-188">Если приложение содержит бота и вкладку, используйте следующий код для добавления новых свойств в манифест приложения Teams:</span><span class="sxs-lookup"><span data-stu-id="6217b-188">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="6217b-189">**webApplicationInfo является** родительским элементом следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="6217b-189">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="6217b-190">**id** — ИД клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="6217b-190">**id** - The client ID of the application.</span></span> <span data-ttu-id="6217b-191">Это ИД приложения, полученный при регистрации приложения в AAD.</span><span class="sxs-lookup"><span data-stu-id="6217b-191">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="6217b-192">**resource** — домен и поддомен приложения.</span><span class="sxs-lookup"><span data-stu-id="6217b-192">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="6217b-193">Это тот же URI, включая протокол, зарегистрированный при создании приложения на портале `api://` `scope` [AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="6217b-193">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="6217b-194">Не следует включать `access_as_user` путь в ресурс.</span><span class="sxs-lookup"><span data-stu-id="6217b-194">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="6217b-195">Доменная часть этого URI должна соответствовать домену и поддоменам, используемым в URL-адресах манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-195">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="6217b-196">Добавление кода для запроса и получения маркера бота</span><span class="sxs-lookup"><span data-stu-id="6217b-196">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="6217b-197">Запрос маркера бота</span><span class="sxs-lookup"><span data-stu-id="6217b-197">Request a bot token</span></span>

<span data-ttu-id="6217b-198">Запрос на токен — это обычный запрос post с использованием существующей схемы сообщения.</span><span class="sxs-lookup"><span data-stu-id="6217b-198">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="6217b-199">Он включается во вложения OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="6217b-199">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="6217b-200">Схема для класса OAuthCard определена в [microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и аналогична карточке для входов.</span><span class="sxs-lookup"><span data-stu-id="6217b-200">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="6217b-201">Teams обрабатывает этот запрос как получение маркера в тихом режиме, если свойство `TokenExchangeResource` заполнено на карточке.</span><span class="sxs-lookup"><span data-stu-id="6217b-201">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="6217b-202">Для канала Teams засчитано только свойство, уникальным образом идентифицирует запрос `Id` маркера.</span><span class="sxs-lookup"><span data-stu-id="6217b-202">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="6217b-203">Для проверки подлинности SSO поддерживается Microsoft Bot Framework `OAuthPrompt` `MultiProviderAuthDialog` или microsoft Bot Framework.</span><span class="sxs-lookup"><span data-stu-id="6217b-203">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="6217b-204">Если пользователь использует приложение в первый раз и требуется согласие пользователя, отображается следующее диалоговое окно для продолжения работы с согласием:</span><span class="sxs-lookup"><span data-stu-id="6217b-204">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![Диалоговое окно "Согласие"](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="6217b-206">Когда пользователь выбирает **"Продолжить",** происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="6217b-206">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="6217b-207">Если бот определяет кнопку для входов, запускается поток входов для ботов, аналогичный потоку входов с кнопки карточки OAuth в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="6217b-207">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="6217b-208">Разработчик должен решить, какие разрешения требуют согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-208">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="6217b-209">Этот подход рекомендуется, если вам требуется маркер с разрешениями, которые выходят за `openId` рамки.</span><span class="sxs-lookup"><span data-stu-id="6217b-209">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="6217b-210">Например, если вы хотите обменять маркер на ресурсы graph.</span><span class="sxs-lookup"><span data-stu-id="6217b-210">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="6217b-211">Если бот не предоставляет кнопку для регистрации на карте OAuth, для минимального набора разрешений требуется согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-211">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="6217b-212">Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="6217b-212">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="6217b-213">Запрос маркера C# без кнопки для регистрации</span><span class="sxs-lookup"><span data-stu-id="6217b-213">C# token request without a sign-in button</span></span>

```csharp
    var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

       await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receive-the-bot-token"></a><span data-ttu-id="6217b-214">Получение маркера бота</span><span class="sxs-lookup"><span data-stu-id="6217b-214">Receive the bot token</span></span>

<span data-ttu-id="6217b-215">Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие действия вызова, которые боты получают сегодня.</span><span class="sxs-lookup"><span data-stu-id="6217b-215">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="6217b-216">Единственное отличие состоит в имени вызова, **входе/маркереExchange** и **поле значения.**</span><span class="sxs-lookup"><span data-stu-id="6217b-216">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="6217b-217">Поле **значения** содержит **ID**, строку исходного запроса  для получения маркера и поля маркера, строку, включаемую маркер.</span><span class="sxs-lookup"><span data-stu-id="6217b-217">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="6217b-218">Если у пользователя несколько активных конечных точек, вы можете получить несколько ответов на заданный запрос.</span><span class="sxs-lookup"><span data-stu-id="6217b-218">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="6217b-219">Необходимо отлагонять ответы с помощью маркера.</span><span class="sxs-lookup"><span data-stu-id="6217b-219">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="6217b-220">Код C# для обработки действия вызова</span><span class="sxs-lookup"><span data-stu-id="6217b-220">C# code to handle the invoke activity</span></span>

```csharp
    protected override async Task<InvokeResponse> OnInvokeActivityAsync
    (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                try
                {
                    if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                    {
                        await OnTokenResponseEventAsync(turnContext, cancellationToken);
                        return new InvokeResponse() { Status = 200 };
                    }
                    else
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                    }
                }
                catch (InvokeResponseException e)
                {
                    return e.CreateInvokeResponse();
                }
            }
```

<span data-ttu-id="6217b-221">Тип `turnContext.activity.value` [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) содержит маркер, который может дополнительно использоваться ботом.</span><span class="sxs-lookup"><span data-stu-id="6217b-221">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="6217b-222">Для повышения производительности маркеры необходимо хранить и обновлять.</span><span class="sxs-lookup"><span data-stu-id="6217b-222">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="update-the-auth-sample"></a><span data-ttu-id="6217b-223">Обновление примера auth</span><span class="sxs-lookup"><span data-stu-id="6217b-223">Update the auth sample</span></span>

<span data-ttu-id="6217b-224">Откройте [пример auth Teams](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) и выполните следующие действия, чтобы обновить его:</span><span class="sxs-lookup"><span data-stu-id="6217b-224">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="6217b-225">Обновив TeamsBot для обработки отладки входящих запросов, включив следующий код:</span><span class="sxs-lookup"><span data-stu-id="6217b-225">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

    ```csharp
        protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
        protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
            {
                await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
            }
    ```
  
2. <span data-ttu-id="6217b-226">Обновление с использованием пароля и имени подключения, определенного на портале Azure с подключением `appsettings.json` `botId` [OAuth.](#update-the-azure-portal-with-the-oauth-connection)</span><span class="sxs-lookup"><span data-stu-id="6217b-226">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="6217b-227">Обновим манифест и `token.botframework.com` убедитесь, что он находится в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="6217b-227">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="6217b-228">Дополнительные сведения см. в [примере auth Teams.](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)</span><span class="sxs-lookup"><span data-stu-id="6217b-228">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="6217b-229">Замейте манифест изображениями профилей и установите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="6217b-229">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="6217b-230">Дополнительные примеры кода</span><span class="sxs-lookup"><span data-stu-id="6217b-230">Additional code samples</span></span>

* <span data-ttu-id="6217b-231">[Пример C# с использованием bot Framework SDK.](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)</span><span class="sxs-lookup"><span data-stu-id="6217b-231">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>
