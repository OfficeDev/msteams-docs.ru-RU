---
title: Поддержка единого входа для ботов
description: Описывает, как получить токен пользователя. В настоящее время разработчик ботов может использовать знак в карте или службу лазурного бота с поддержкой карты OAuth.
keywords: токен, токен пользователя, поддержка SSO для ботов
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a43c2a46561149ff97d039a3ba8fe9f4472e2073
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566096"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="87e7d-105">Поддержка ботов с одним ва-пом (SSO)</span><span class="sxs-lookup"><span data-stu-id="87e7d-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="87e7d-106">Одноэтажная аутентификация в Azure Active Directory (AAD) сводит к минимуму количество случаев, когда пользователи должны вводить свой знак в учетные данные, молча обновляя маркер аутентификации.</span><span class="sxs-lookup"><span data-stu-id="87e7d-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="87e7d-107">Если пользователи соглашаются использовать ваше приложение, им не нужно снова предоставлять согласие на другом устройстве и они могут войти в приложение автоматически.</span><span class="sxs-lookup"><span data-stu-id="87e7d-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="87e7d-108">Поток похож на поток поддержки [Microsoft Teams SSO,](../../../tabs/how-to/authentication/auth-aad-sso.md)однако, разница в протоколе о том, как бот запрашивает [токены](#request-a-bot-token) [и получает ответы.](#receive-the-bot-token)</span><span class="sxs-lookup"><span data-stu-id="87e7d-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="87e7d-109">OAuth 2.0 является открытым стандартом для проверки подлинности и авторизации, используемой AAD и многими другими поставщиками идентификации.</span><span class="sxs-lookup"><span data-stu-id="87e7d-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="87e7d-110">Базовое понимание OAuth 2.0 является необходимым условием для работы с аутентификацией в Teams.</span><span class="sxs-lookup"><span data-stu-id="87e7d-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="87e7d-111">Бот SSO во время выполнения</span><span class="sxs-lookup"><span data-stu-id="87e7d-111">Bot SSO at runtime</span></span>

![Bot SSO на диаграмме времени выполнения](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="87e7d-113">Выполните следующие шаги, чтобы получить токены аутентификации и бот-приложений:</span><span class="sxs-lookup"><span data-stu-id="87e7d-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="87e7d-114">Бот отправляет сообщение с OAuthCard, которая содержит `tokenExchangeResource` свойство.</span><span class="sxs-lookup"><span data-stu-id="87e7d-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="87e7d-115">В нем Teams, чтобы получить токен аутентификации для приложения бота.</span><span class="sxs-lookup"><span data-stu-id="87e7d-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="87e7d-116">Пользователь получает сообщения во всех конечных точках активных пользователей.</span><span class="sxs-lookup"><span data-stu-id="87e7d-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="87e7d-117">Пользователь может иметь более одной активной конечной точки за один раз.</span><span class="sxs-lookup"><span data-stu-id="87e7d-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="87e7d-118">Токен бота получен из каждой активной конечной точки пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="87e7d-119">Приложение должно быть установлено в личном прицеле для поддержки SSO.</span><span class="sxs-lookup"><span data-stu-id="87e7d-119">The app must be installed in personal scope for SSO support.</span></span>

1. <span data-ttu-id="87e7d-120">Если текущий пользователь использует приложение бота в первый раз, появляется запрос, запрашивающий пользователя сделать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="87e7d-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="87e7d-121">При необходимости предоставьте согласие.</span><span class="sxs-lookup"><span data-stu-id="87e7d-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="87e7d-122">Обработать проверку проверки подлинности, например двухфакторную аутентификацию.</span><span class="sxs-lookup"><span data-stu-id="87e7d-122">Handle step-up authentication, such as two-factor authentication.</span></span>

1. <span data-ttu-id="87e7d-123">Teams запрашивает токен приложения бота из конечной точки AAD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

1. <span data-ttu-id="87e7d-124">AAD отправляет токен приложения бота в Teams приложение.</span><span class="sxs-lookup"><span data-stu-id="87e7d-124">AAD sends the bot application token to the Teams application.</span></span>

1. <span data-ttu-id="87e7d-125">Teams отправляет токен боту как часть объекта значения, возвращенного действием вызова с **именем войти/tokenExchange.**</span><span class="sxs-lookup"><span data-stu-id="87e7d-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
1. <span data-ttu-id="87e7d-126">Разобраный маркер в приложении бота предоставляет необходимую информацию, такую как адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="87e7d-127">Разработка SSO Teams бота</span><span class="sxs-lookup"><span data-stu-id="87e7d-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="87e7d-128">Выполните следующие шаги по разработке SSO Teams бота:</span><span class="sxs-lookup"><span data-stu-id="87e7d-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="87e7d-129">[Зарегистрируйте приложение через портал AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="87e7d-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
1. <span data-ttu-id="87e7d-130">[Обновите Teams приложение для вашего бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="87e7d-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
1. <span data-ttu-id="87e7d-131">[Добавьте код для запроса и получения токена бота.](#add-the-code-to-request-and-receive-a-bot-token)</span><span class="sxs-lookup"><span data-stu-id="87e7d-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="87e7d-132">Зарегистрируйте приложение через портал AAD</span><span class="sxs-lookup"><span data-stu-id="87e7d-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="87e7d-133">Шаги по регистрации приложения через портал AAD аналогичны потоку [вкладок SSO.](../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="87e7d-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="87e7d-134">Выполните следующие шаги для регистрации приложения:</span><span class="sxs-lookup"><span data-stu-id="87e7d-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="87e7d-135">Зарегистрируйте новое приложение в Azure Active Directory [- портал App Registrations.](https://go.microsoft.com/fwlink/?linkid=2083908)</span><span class="sxs-lookup"><span data-stu-id="87e7d-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="87e7d-136">Выберите **новую регистрацию**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-136">Select **New Registration**.</span></span> <span data-ttu-id="87e7d-137">В **Регистре отображается** страница заявки.</span><span class="sxs-lookup"><span data-stu-id="87e7d-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="87e7d-138">На странице **регистрации приложения** введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="87e7d-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="87e7d-139">**Введите имя** для приложения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="87e7d-140">Выберите **типы поддерживаемых счетов,** выберите одного арендатора или тип многотенантной учетной записи.</span><span class="sxs-lookup"><span data-stu-id="87e7d-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="87e7d-141">Пользователи не запрашиваются для согласия и получают токены доступа сразу, если приложение AAD зарегистрировано в том же арендаторе, где они делают запрос на аутентификацию в Teams.</span><span class="sxs-lookup"><span data-stu-id="87e7d-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="87e7d-142">Однако пользователи должны дать согласие на получение разрешений, если приложение AAD зарегистрировано в другом арендаторе.</span><span class="sxs-lookup"><span data-stu-id="87e7d-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="87e7d-143">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-143">Choose **Register**.</span></span>
4. <span data-ttu-id="87e7d-144">На странице обзора скопировать и сохранить **идентификатор приложения (клиента).**</span><span class="sxs-lookup"><span data-stu-id="87e7d-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="87e7d-145">Вы нуждаетеся в нем позже при обновлении Teams приложения манифест.</span><span class="sxs-lookup"><span data-stu-id="87e7d-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="87e7d-146">В разделе **Управление** выберите **Предоставление API**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="87e7d-147">Если вы строите автономный бот, введите идентификатор приложения URI как `api://botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="87e7d-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="87e7d-148">Здесь **YourBotId** ваш идентификатор приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="87e7d-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="87e7d-149">Если вы строите приложение с ботом и вкладкой, введите идентификатор приложения URI как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="87e7d-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="87e7d-150">Выберите разрешения, которые нужны вашему приложению для конечной точки AAD, и, по желанию, для microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="87e7d-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="87e7d-151">[Предоставление разрешений на](/azure/active-directory/develop/v2-permissions-and-consent) Teams настольных, веб- и мобильных приложений.</span><span class="sxs-lookup"><span data-stu-id="87e7d-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="87e7d-152">Выберите **Добавить область**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="87e7d-153">В панели, которая открывается, добавьте клиентское приложение, `access_as_user` введя в качестве **имени область.**</span><span class="sxs-lookup"><span data-stu-id="87e7d-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="87e7d-154">Область "access_as_user", используемая для добавления клиент-приложения, предназначена для "Администраторов и пользователей".</span><span class="sxs-lookup"><span data-stu-id="87e7d-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="87e7d-155">Вы должны знать о следующих важных ограничениях:</span><span class="sxs-lookup"><span data-stu-id="87e7d-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="87e7d-156">Поддерживаются только разрешения microsoft Graph уровня пользователя, такие как электронная почта, профиль, offline_access и OpenId.</span><span class="sxs-lookup"><span data-stu-id="87e7d-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="87e7d-157">Если вам нужен доступ к другим Graph, например, `User.Read` `Mail.Read` или, [см.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)</span><span class="sxs-lookup"><span data-stu-id="87e7d-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="87e7d-158">Доменное имя вашего приложения должно быть таким же, как доменное имя, которое вы зарегистрировали для вашего приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="87e7d-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="87e7d-159">Несколько доменов на приложение в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="87e7d-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="87e7d-160">Приложения, которые используют `azurewebsites.net` домен, не поддерживаются, поскольку он является общим и может быть угрозой безопасности.</span><span class="sxs-lookup"><span data-stu-id="87e7d-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="87e7d-161">Обновление портала Azure с подключением OAuth</span><span class="sxs-lookup"><span data-stu-id="87e7d-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="87e7d-162">Выполните следующие шаги по обновлению портала Azure с подключением OAuth:</span><span class="sxs-lookup"><span data-stu-id="87e7d-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="87e7d-163">На портале Azure перейдите на **регистрацию приложений.**</span><span class="sxs-lookup"><span data-stu-id="87e7d-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="87e7d-164">Перейдите **на разрешения API**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-164">Go to **API Permissions**.</span></span> <span data-ttu-id="87e7d-165">Выберите **Добавить разрешение**  >  **Microsoft**  >  **Graph, а затем** добавить следующие разрешения от Microsoft Graph API:</span><span class="sxs-lookup"><span data-stu-id="87e7d-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="87e7d-166">User.Read (включен по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="87e7d-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="87e7d-167">email</span><span class="sxs-lookup"><span data-stu-id="87e7d-167">email</span></span>
    * <span data-ttu-id="87e7d-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="87e7d-168">offline_access</span></span>
    * <span data-ttu-id="87e7d-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="87e7d-169">OpenId</span></span>
    * <span data-ttu-id="87e7d-170">profile</span><span class="sxs-lookup"><span data-stu-id="87e7d-170">profile</span></span>

3. <span data-ttu-id="87e7d-171">На портале Azure перейдите на **регистрацию бот-каналов.**</span><span class="sxs-lookup"><span data-stu-id="87e7d-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="87e7d-172">Выберите **Параметры** на левом стекле и **выберите Настройку добавления** **в разделе OAuth Connection Параметры** разделе.</span><span class="sxs-lookup"><span data-stu-id="87e7d-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![Вид SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="87e7d-174">Выполните следующие шаги для завершения **формы «Новая настройка** соединения»:</span><span class="sxs-lookup"><span data-stu-id="87e7d-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="87e7d-175">**В заявке** AAD может потребоваться неявный грант.</span><span class="sxs-lookup"><span data-stu-id="87e7d-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="87e7d-176">**Введите имя** на **странице Настройка нового** соединения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="87e7d-177">Это имя, которое упоминается в настройках кода службы бота в *шаге 5* [Bot SSO во время выполнения.](#bot-sso-at-runtime)</span><span class="sxs-lookup"><span data-stu-id="87e7d-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="87e7d-178">Из **сервиса-поставщика** высадки, выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="87e7d-179">Введите учетные данные клиента, **такие как идентификатор** **клиента и секрет** клиента для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="87e7d-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="87e7d-180">Для **URL-адреса Exchange, используйте** значение сферы, определенное [в обновлении вашего Teams приложения для вашего бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="87e7d-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="87e7d-181">URL-Exchange Token указывает SDK, что это приложение AAD настроено для SSO.</span><span class="sxs-lookup"><span data-stu-id="87e7d-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="87e7d-182">В поле **идентификатора арендатора** введите *общий*.</span><span class="sxs-lookup"><span data-stu-id="87e7d-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="87e7d-183">Добавьте все **области, настроенные** при указании разрешений в API для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="87e7d-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="87e7d-184">При условии, что идентификатор Клиента и Клиент секрет, токен-магазин обменивает токен на графический токен с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="87e7d-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="87e7d-185">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="87e7d-185">Select **Save**.</span></span>

    ![Представление настроек VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="87e7d-187">Обновите Teams приложение для вашего бота</span><span class="sxs-lookup"><span data-stu-id="87e7d-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="87e7d-188">Если приложение содержит автономного бота, то используйте следующий код, чтобы добавить новые свойства в Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="87e7d-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="87e7d-189">Если приложение содержит бота и вкладку, то используйте следующий код, чтобы добавить новые свойства в Teams приложения:</span><span class="sxs-lookup"><span data-stu-id="87e7d-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="87e7d-190">**webApplicationInfo** является родителем следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="87e7d-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="87e7d-191">**id** - Идентификатор клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="87e7d-192">Это идентификатор приложения, который вы получили в рамках регистрации приложения с AAD.</span><span class="sxs-lookup"><span data-stu-id="87e7d-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="87e7d-193">**ресурс** - домен и поддомен вашего приложения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="87e7d-194">Это тот же URI, включая протокол, `api://` который вы зарегистрировали при `scope` создании вашего приложения в [Регистре через портал AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="87e7d-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="87e7d-195">Вы не должны включать `access_as_user` путь в свой ресурс.</span><span class="sxs-lookup"><span data-stu-id="87e7d-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="87e7d-196">Доменная часть этого URI должна соответствовать домену и субдоменам, используемым в URL-адресах вашего Teams приложения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="87e7d-197">Добавить код для запроса и получения токена бота</span><span class="sxs-lookup"><span data-stu-id="87e7d-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="87e7d-198">Запрос токена бота</span><span class="sxs-lookup"><span data-stu-id="87e7d-198">Request a bot token</span></span>

<span data-ttu-id="87e7d-199">Запрос на токен является обычным запросом сообщений POST с использованием существующей схемы сообщения.</span><span class="sxs-lookup"><span data-stu-id="87e7d-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="87e7d-200">Он включен в приложения OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="87e7d-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="87e7d-201">Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и похожа на карту.</span><span class="sxs-lookup"><span data-stu-id="87e7d-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="87e7d-202">Teams рассматривает этот запрос как тихое приобретение токенов, `TokenExchangeResource` если недвижимость заполнена на карте.</span><span class="sxs-lookup"><span data-stu-id="87e7d-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="87e7d-203">Для Teams канал, только `Id` свойство, которое однозначно идентифицирует запрос токенов, выполнено.</span><span class="sxs-lookup"><span data-stu-id="87e7d-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="87e7d-204">Данные Microsoft Bot Framework `OAuthPrompt` или `MultiProviderAuthDialog` поддерживаются для проверки подлинности SSO.</span><span class="sxs-lookup"><span data-stu-id="87e7d-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="87e7d-205">Если пользователь использует приложение в первый раз и требуется согласие пользователя, следующее диалоговое окно, как представляется, продолжается с опытом согласия:</span><span class="sxs-lookup"><span data-stu-id="87e7d-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![Согласие диалоговое окно](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="87e7d-207">Когда пользователь выбирает **Продолжить ,** происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="87e7d-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="87e7d-208">Если бот определяет кнопку в записи, знак потока для ботов срабатывает аналогично знаку потока из кнопки карты OAuth в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="87e7d-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="87e7d-209">Разработчик должен решить, какие разрешения требуют согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="87e7d-210">Этот подход рекомендуется, если вам требуется токен с разрешениями за пределами `openId` .</span><span class="sxs-lookup"><span data-stu-id="87e7d-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="87e7d-211">Например, если вы хотите обменять токен на ресурсы графика.</span><span class="sxs-lookup"><span data-stu-id="87e7d-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="87e7d-212">Если бот не предоставляет кнопку в записи на карту OAuth, для минимального набора разрешений требуется согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="87e7d-213">Этот маркер полезен для базовой аутентификации и получения адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="87e7d-214">Запрос токенов на C'a без кнопки ва-подвок</span><span class="sxs-lookup"><span data-stu-id="87e7d-214">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="87e7d-215">Получение токена бота</span><span class="sxs-lookup"><span data-stu-id="87e7d-215">Receive the bot token</span></span>

<span data-ttu-id="87e7d-216">Ответ с маркером отправляется через действие вызова с той же схемой, что и другие действия вызова, которые боты получают сегодня.</span><span class="sxs-lookup"><span data-stu-id="87e7d-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="87e7d-217">Разница лишь в имени вызова, **ввименеле/токене и** поле **значения.**</span><span class="sxs-lookup"><span data-stu-id="87e7d-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="87e7d-218">Поле **значения** содержит Id , **строку** первоначального запроса на получить токен и поле **токена,** значение строки, включая токен.</span><span class="sxs-lookup"><span data-stu-id="87e7d-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="87e7d-219">Вы можете получить несколько ответов на данный запрос, если пользователь имеет несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="87e7d-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="87e7d-220">Вы должны вывести ответы с маркером.</span><span class="sxs-lookup"><span data-stu-id="87e7d-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="87e7d-221">Код C-кода для обработки действия вызова</span><span class="sxs-lookup"><span data-stu-id="87e7d-221">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="87e7d-222">Тип `turnContext.activity.value` [TokenExchangeInvokeRequest и содержит токен,](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) который может быть использован вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="87e7d-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="87e7d-223">Вы должны хранить токены по причинам производительности и обновлять их.</span><span class="sxs-lookup"><span data-stu-id="87e7d-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="87e7d-224">Сбой обмена токенов</span><span class="sxs-lookup"><span data-stu-id="87e7d-224">Token exchange failure</span></span>

<span data-ttu-id="87e7d-225">В случае сбоя обмена токенов используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="87e7d-225">In case of token exchange failure, use the following code:</span></span>

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

<span data-ttu-id="87e7d-226">Чтобы понять, что делает бот, когда обмен токенов не может вызвать запрос согласия, см.</span><span class="sxs-lookup"><span data-stu-id="87e7d-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="87e7d-227">Никакие действия пользователя не должны быть приняты, поскольку бот выполняет действия, когда обмен токенов терпит неудачу.</span><span class="sxs-lookup"><span data-stu-id="87e7d-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="87e7d-228">Клиент начинает разговор с ботом, запуская сценарий OAuth.</span><span class="sxs-lookup"><span data-stu-id="87e7d-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="87e7d-229">Бот отправляет клиенту карту OAuth.</span><span class="sxs-lookup"><span data-stu-id="87e7d-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="87e7d-230">Клиент перехватывает карту OAuth перед отображением ее пользователю и проверяет, содержит ли она `TokenExchangeResource` свойство.</span><span class="sxs-lookup"><span data-stu-id="87e7d-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="87e7d-231">Если свойство существует, клиент отправляет `TokenExchangeInvokeRequest` бота.</span><span class="sxs-lookup"><span data-stu-id="87e7d-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="87e7d-232">Клиент должен иметь обмениваемый токен для пользователя, который должен быть токеном Azure AD v2 и чья аудитория должна быть такой же, как `TokenExchangeResource.Uri` собственность.</span><span class="sxs-lookup"><span data-stu-id="87e7d-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="87e7d-233">Клиент отправляет действие вызова боту со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="87e7d-233">The client sends an invoke activity to the bot with the following code:</span></span>

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. <span data-ttu-id="87e7d-234">Бот обрабатывает и `TokenExchangeInvokeRequest` возвращает обратно `TokenExchangeInvokeResponse` клиенту.</span><span class="sxs-lookup"><span data-stu-id="87e7d-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="87e7d-235">Клиент должен подождать, пока он не получит `TokenExchangeInvokeResponse` .</span><span class="sxs-lookup"><span data-stu-id="87e7d-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. <span data-ttu-id="87e7d-236">Если `TokenExchangeInvokeResponse` имеет a , то клиент не показывает карту `status` `200` OAuth.</span><span class="sxs-lookup"><span data-stu-id="87e7d-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="87e7d-237">Посмотреть [нормальное изображение потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="87e7d-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="87e7d-238">Для любого `status` другого или `TokenExchangeInvokeResponse` если не получено, то клиент показывает карту OAuth пользователю.</span><span class="sxs-lookup"><span data-stu-id="87e7d-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="87e7d-239">Посмотреть [изображение обратного потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="87e7d-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="87e7d-240">Это гарантирует, что поток SSO возвращается к нормальному потоку OAuthCard в случае каких-либо ошибок или неудовлетворенных зависимостей, таких как согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="87e7d-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="87e7d-241">Обновление образца аута</span><span class="sxs-lookup"><span data-stu-id="87e7d-241">Update the auth sample</span></span>

<span data-ttu-id="87e7d-242">Откройте [Teams, а затем](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) выполните следующие шаги, чтобы обновить его:</span><span class="sxs-lookup"><span data-stu-id="87e7d-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="87e7d-243">Обновление TeamsBot для обработки deduping входящего запроса, включив следующий код:</span><span class="sxs-lookup"><span data-stu-id="87e7d-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="87e7d-244">Обновление, `appsettings.json` чтобы включить пароль и `botId` имя соединения, определенное [в обновлении портала Azure с подключением OAuth.](#update-the-azure-portal-with-the-oauth-connection)</span><span class="sxs-lookup"><span data-stu-id="87e7d-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="87e7d-245">Обновите манифест и `token.botframework.com` убедитесь, что он находится в списке действительных доменов.</span><span class="sxs-lookup"><span data-stu-id="87e7d-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="87e7d-246">Для получения дополнительной [информации, Teams образца аута](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="87e7d-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="87e7d-247">Завехайте манифест с изображениями профиля и установите его в Teams.</span><span class="sxs-lookup"><span data-stu-id="87e7d-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="87e7d-248">Пример кода</span><span class="sxs-lookup"><span data-stu-id="87e7d-248">Code sample</span></span>
|<span data-ttu-id="87e7d-249">**Название образца**</span><span class="sxs-lookup"><span data-stu-id="87e7d-249">**Sample name**</span></span> | <span data-ttu-id="87e7d-250">**Описание**</span><span class="sxs-lookup"><span data-stu-id="87e7d-250">**Description**</span></span> |<span data-ttu-id="87e7d-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="87e7d-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="87e7d-252">Бот фреймвок SDK</span><span class="sxs-lookup"><span data-stu-id="87e7d-252">Bot framework SDK</span></span> | <span data-ttu-id="87e7d-253">Пример для использования бота фреймворка SDK.</span><span class="sxs-lookup"><span data-stu-id="87e7d-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="87e7d-254">View</span><span class="sxs-lookup"><span data-stu-id="87e7d-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
