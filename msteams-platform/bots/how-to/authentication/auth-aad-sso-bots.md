---
title: Поддержка единого входа для ботов
description: Описывает, как получить маркер пользователя. В настоящее время разработчик бота может использовать вход в карточку или службу лазурного бота с поддержкой карты OAuth.
keywords: маркер, маркер пользователя, поддержка SSO для ботов
ms.topic: conceptual
ms.openlocfilehash: dad36f52a3e23c00f8725e2e906308339629bb05
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753534"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="ff35a-105">Поддержка единого входного знака (SSO) для ботов</span><span class="sxs-lookup"><span data-stu-id="ff35a-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="ff35a-106">Одновековая проверка подлинности в Azure Active Directory (AAD) минимизирует количество случаев, когда пользователям необходимо вводить свой знак в учетных данных, молча освежая маркер проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ff35a-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="ff35a-107">Если пользователи соглашаются использовать ваше приложение, они не должны предоставлять согласие снова на другом устройстве и могут войти автоматически.</span><span class="sxs-lookup"><span data-stu-id="ff35a-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="ff35a-108">Поток похож на поток поддержки [SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)вкладки Microsoft Teams, однако разница в [](#request-a-bot-token) протоколе заключается в том, как бот запрашивает маркеры и получает [ответы.](#receive-the-bot-token)</span><span class="sxs-lookup"><span data-stu-id="ff35a-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="ff35a-109">OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый AAD и многими другими поставщиками удостоверений.</span><span class="sxs-lookup"><span data-stu-id="ff35a-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="ff35a-110">Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="ff35a-111">Bot SSO во время запуска</span><span class="sxs-lookup"><span data-stu-id="ff35a-111">Bot SSO at runtime</span></span>

![Bot SSO на схеме времени запуска](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="ff35a-113">Выполните следующие действия, чтобы получить маркеры проверки подлинности и бот-приложений:</span><span class="sxs-lookup"><span data-stu-id="ff35a-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="ff35a-114">Бот отправляет сообщение с помощью OAuthCard с `tokenExchangeResource` свойством.</span><span class="sxs-lookup"><span data-stu-id="ff35a-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="ff35a-115">Он сообщает Teams, чтобы получить маркер проверки подлинности для приложения-бота.</span><span class="sxs-lookup"><span data-stu-id="ff35a-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="ff35a-116">Пользователь получает сообщения на всех активных конечных точках пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="ff35a-117">У пользователя одновременно может быть несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ff35a-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="ff35a-118">Маркер бота получается с каждой конечной точки активного пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="ff35a-119">Приложение должно быть установлено в личном поле для поддержки SSO.</span><span class="sxs-lookup"><span data-stu-id="ff35a-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="ff35a-120">Если текущий пользователь впервые использует приложение-бот, появляется запрос с просьбой сделать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="ff35a-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="ff35a-121">Предоставление согласия при необходимости.</span><span class="sxs-lookup"><span data-stu-id="ff35a-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="ff35a-122">Обработка этапной проверки подлинности, например двух факторов проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ff35a-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="ff35a-123">Teams запрашивает маркер приложения-бота из конечной точки AAD для текущего пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="ff35a-124">AAD отправляет маркер приложения-бота в приложение Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="ff35a-125">Teams отправляет маркер боту в составе объекта значения, возвращаемого в результате действия вызова с именем **sign-in/tokenExchange.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="ff35a-126">Разбиванный маркер в бот-приложении предоставляет необходимые сведения, например адрес электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="ff35a-127">Разработка бота SSO Teams</span><span class="sxs-lookup"><span data-stu-id="ff35a-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="ff35a-128">Выполните следующие действия по разработке бота SSO Teams:</span><span class="sxs-lookup"><span data-stu-id="ff35a-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="ff35a-129">[Регистрация приложения на портале AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="ff35a-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="ff35a-130">[Обновление манифеста приложения Teams для бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="ff35a-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="ff35a-131">[Добавьте код для запроса и получения маркера бота.](#add-the-code-to-request-and-receive-a-bot-token)</span><span class="sxs-lookup"><span data-stu-id="ff35a-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="ff35a-132">Регистрация приложения на портале AAD</span><span class="sxs-lookup"><span data-stu-id="ff35a-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="ff35a-133">Действия по регистрации приложения через портал AAD похожи на поток [SSO вкладки.](../../../tabs/how-to/authentication/auth-aad-sso.md)</span><span class="sxs-lookup"><span data-stu-id="ff35a-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="ff35a-134">Выполните следующие действия для регистрации приложения:</span><span class="sxs-lookup"><span data-stu-id="ff35a-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="ff35a-135">Регистрация нового приложения на [портале Регистрации приложений Azure Active Directory.](https://go.microsoft.com/fwlink/?linkid=2083908)</span><span class="sxs-lookup"><span data-stu-id="ff35a-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="ff35a-136">Выберите **новую регистрацию.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-136">Select **New Registration**.</span></span> <span data-ttu-id="ff35a-137">Появится **страница "Регистрация** приложения".</span><span class="sxs-lookup"><span data-stu-id="ff35a-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="ff35a-138">На странице **Регистрация приложения** введите следующие значения:</span><span class="sxs-lookup"><span data-stu-id="ff35a-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="ff35a-139">Введите **имя** приложения.</span><span class="sxs-lookup"><span data-stu-id="ff35a-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="ff35a-140">Выберите **поддерживаемые типы учетных записей,** выберите один клиент или многотенантный тип учетной записи.</span><span class="sxs-lookup"><span data-stu-id="ff35a-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="ff35a-141">Пользователи не запрашиваются для получения согласия и им сразу же выдают маркеры доступа, если приложение AAD зарегистрировано в том же клиенте, где они делают запрос на проверку подлинности в Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="ff35a-142">Однако пользователи должны предоставить согласие на разрешения, если приложение AAD зарегистрировано в другом клиенте.</span><span class="sxs-lookup"><span data-stu-id="ff35a-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="ff35a-143">Нажмите кнопку **Зарегистрировать**.</span><span class="sxs-lookup"><span data-stu-id="ff35a-143">Choose **Register**.</span></span>
4. <span data-ttu-id="ff35a-144">На странице обзор скопируйте и сохраните ID приложения **(клиента).**</span><span class="sxs-lookup"><span data-stu-id="ff35a-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="ff35a-145">Это необходимо позднее при обновлении манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="ff35a-146">В разделе **Управление** выберите **Предоставление API**.</span><span class="sxs-lookup"><span data-stu-id="ff35a-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="ff35a-147">Если вы строите автономный бот, введите URI приложения ID как `api://botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="ff35a-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="ff35a-148">Здесь **YourBotId** — это ваш ID приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="ff35a-149">Если вы строите приложение с помощью бота и вкладки, введите URI ID приложения как `api://fully-qualified-domain-name.com/botid-{YourBotId}` .</span><span class="sxs-lookup"><span data-stu-id="ff35a-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="ff35a-150">Выберите разрешения, необходимые приложению для конечной точки AAD и, необязательно, для Microsoft Graph.</span><span class="sxs-lookup"><span data-stu-id="ff35a-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="ff35a-151">[Предоставление разрешений](/azure/active-directory/develop/v2-permissions-and-consent) для настольных, веб-приложений и мобильных приложений Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="ff35a-152">Выберите **Добавить область**.</span><span class="sxs-lookup"><span data-stu-id="ff35a-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="ff35a-153">На открываемой панели добавьте клиентские приложения, введите `access_as_user` имя **Scope.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="ff35a-154">Область "access_as_user" для добавления клиентского приложения для "Администраторы и пользователи".</span><span class="sxs-lookup"><span data-stu-id="ff35a-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="ff35a-155">Необходимо помнить о следующих важных ограничениях:</span><span class="sxs-lookup"><span data-stu-id="ff35a-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="ff35a-156">Поддерживаются только разрешения API Microsoft Graph на уровне пользователей, такие как электронная почта, профиль, offline_access и OpenId.</span><span class="sxs-lookup"><span data-stu-id="ff35a-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="ff35a-157">Если вам нужен доступ к другим областьм Microsoft Graph, например или `User.Read` `Mail.Read` , см. [рекомендуемое обходное решение.](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)</span><span class="sxs-lookup"><span data-stu-id="ff35a-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="ff35a-158">Доменное имя приложения должно быть таким же, как доменное имя, которое вы зарегистрировали для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="ff35a-159">Несколько доменов в приложении в настоящее время не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="ff35a-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="ff35a-160">Приложения, которые используют домен, не поддерживаются, так как они являются распространенными и `azurewebsites.net` могут быть угрозой безопасности.</span><span class="sxs-lookup"><span data-stu-id="ff35a-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="ff35a-161">Обновление портала Azure с подключением OAuth</span><span class="sxs-lookup"><span data-stu-id="ff35a-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="ff35a-162">Выполните следующие действия по обновлению портала Azure с подключением OAuth:</span><span class="sxs-lookup"><span data-stu-id="ff35a-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="ff35a-163">На портале Azure перейдите к **регистрациям приложений.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="ff35a-164">Перейдите **к разрешениям API.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-164">Go to **API Permissions**.</span></span> <span data-ttu-id="ff35a-165">Выберите **Добавить разрешения,** делегированные Microsoft Graph, а затем добавьте следующие разрешения из  >    >  API Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="ff35a-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="ff35a-166">User.Read (включен по умолчанию)</span><span class="sxs-lookup"><span data-stu-id="ff35a-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="ff35a-167">email</span><span class="sxs-lookup"><span data-stu-id="ff35a-167">email</span></span>
    * <span data-ttu-id="ff35a-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="ff35a-168">offline_access</span></span>
    * <span data-ttu-id="ff35a-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="ff35a-169">OpenId</span></span>
    * <span data-ttu-id="ff35a-170">profile</span><span class="sxs-lookup"><span data-stu-id="ff35a-170">profile</span></span>

3. <span data-ttu-id="ff35a-171">На портале Azure перейдите к **регистрации бот-каналов.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="ff35a-172">Выберите **Параметры** на левой области и выберите **параметр Добавить** в разделе Параметры подключения **OAuth.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![Представление SSOBotHandle2](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="ff35a-174">Выполните следующие действия для завершения **формы параметра "Новое подключение":**</span><span class="sxs-lookup"><span data-stu-id="ff35a-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="ff35a-175">**Неявный** грант может потребоваться в приложении AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="ff35a-176">Введите **имя** на странице **Параметр нового подключения.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="ff35a-177">Это имя, которое упоминается в параметрах кода службы бота в *шаге 5* bot [SSO во время запуска.](#bot-sso-at-runtime)</span><span class="sxs-lookup"><span data-stu-id="ff35a-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="ff35a-178">Из **выпадаемого** поставщика услуг выберите **Azure Active Directory v2**.</span><span class="sxs-lookup"><span data-stu-id="ff35a-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="ff35a-179">Введите учетные данные клиента, такие как **client id** и **client secret** для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="ff35a-180">Для **URL-адреса Exchange маркеров** используйте значение области, определенное в манифесте [приложения Update your Teams для бота.](#update-your-teams-application-manifest-for-your-bot)</span><span class="sxs-lookup"><span data-stu-id="ff35a-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="ff35a-181">URL-адрес Exchange token указывает на SDK, что это приложение AAD настроено для SSO.</span><span class="sxs-lookup"><span data-stu-id="ff35a-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="ff35a-182">В поле **"ID клиента"** введите *общие .*</span><span class="sxs-lookup"><span data-stu-id="ff35a-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="ff35a-183">Добавьте все **области, настроенные** при указании разрешений на API ниже по течению для приложения AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="ff35a-184">С помощью секрета client id и Client, магазин маркеров обменивается маркером для маркера графа с определенными разрешениями.</span><span class="sxs-lookup"><span data-stu-id="ff35a-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="ff35a-185">Нажмите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="ff35a-185">Select **Save**.</span></span>

    ![Представление параметра VuSSOBotConnection](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="ff35a-187">Обновление манифеста приложения Teams для бота</span><span class="sxs-lookup"><span data-stu-id="ff35a-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="ff35a-188">Если приложение содержит автономный бот, используйте следующий код, чтобы добавить новые свойства в манифест приложений Teams:</span><span class="sxs-lookup"><span data-stu-id="ff35a-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="ff35a-189">Если приложение содержит бот и вкладку, используйте следующий код, чтобы добавить новые свойства в манифест приложений Teams:</span><span class="sxs-lookup"><span data-stu-id="ff35a-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="ff35a-190">**webApplicationInfo** является родителем следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="ff35a-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="ff35a-191">**id** — ID клиента приложения.</span><span class="sxs-lookup"><span data-stu-id="ff35a-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="ff35a-192">Это ID приложения, полученный в рамках регистрации приложения в AAD.</span><span class="sxs-lookup"><span data-stu-id="ff35a-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="ff35a-193">**ресурс** — домен и поддомен приложения.</span><span class="sxs-lookup"><span data-stu-id="ff35a-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="ff35a-194">Это тот же URI, в том числе протокол, зарегистрированный при создании приложения в Зарегистрировать приложение `api://` `scope` через портал [AAD.](#register-your-app-through-the-aad-portal)</span><span class="sxs-lookup"><span data-stu-id="ff35a-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="ff35a-195">Не следует включать путь `access_as_user` в ресурс.</span><span class="sxs-lookup"><span data-stu-id="ff35a-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="ff35a-196">Доменная часть этого URI должна соответствовать домену и поддоменам, используемым в URL-адресах манифеста приложения Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="ff35a-197">Добавление кода для запроса и получения маркера бота</span><span class="sxs-lookup"><span data-stu-id="ff35a-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="ff35a-198">Запрос маркера бота</span><span class="sxs-lookup"><span data-stu-id="ff35a-198">Request a bot token</span></span>

<span data-ttu-id="ff35a-199">Запрос на токен — это обычный запрос сообщения POST с помощью существующей схемы сообщений.</span><span class="sxs-lookup"><span data-stu-id="ff35a-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="ff35a-200">Он входит в вложения OAuthCard.</span><span class="sxs-lookup"><span data-stu-id="ff35a-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="ff35a-201">Схема для класса OAuthCard определена в [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) и похожа на карточку для регистрации.</span><span class="sxs-lookup"><span data-stu-id="ff35a-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="ff35a-202">Teams рассматривает этот запрос как бесшумное приобретение маркера, если свойство `TokenExchangeResource` заполнено на карте.</span><span class="sxs-lookup"><span data-stu-id="ff35a-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="ff35a-203">В канале Teams зачтется только свойство, которое однозначно определяет запрос `Id` маркера.</span><span class="sxs-lookup"><span data-stu-id="ff35a-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="ff35a-204">Microsoft Bot Framework `OAuthPrompt` или `MultiProviderAuthDialog` поддерживается для проверки подлинности SSO.</span><span class="sxs-lookup"><span data-stu-id="ff35a-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="ff35a-205">Если пользователь использует приложение в первый раз и требуется согласие пользователя, следующий диалоговое окно, как представляется, продолжится с опытом согласия:</span><span class="sxs-lookup"><span data-stu-id="ff35a-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

![Диалоговое окно Согласия](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="ff35a-207">Когда пользователь выбирает **Продолжить,** происходят следующие события:</span><span class="sxs-lookup"><span data-stu-id="ff35a-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="ff35a-208">Если бот определяет кнопку вход, запускается вход в поток ботов, аналогичный входу в потоке с кнопки карточки OAuth в потоке сообщений.</span><span class="sxs-lookup"><span data-stu-id="ff35a-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="ff35a-209">Разработчик должен решить, какие разрешения требуют согласия пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="ff35a-210">Этот подход рекомендуется, если требуется маркер с разрешениями за пределами `openId` .</span><span class="sxs-lookup"><span data-stu-id="ff35a-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="ff35a-211">Например, если вы хотите обменять маркер на ресурсы графа.</span><span class="sxs-lookup"><span data-stu-id="ff35a-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="ff35a-212">Если бот не предоставляет кнопку вход на карту OAuth, для минимального набора разрешений требуется согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="ff35a-213">Этот маркер полезен для базовой проверки подлинности и получения адреса электронной почты пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="ff35a-214">C# маркера без кнопки вход</span><span class="sxs-lookup"><span data-stu-id="ff35a-214">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="ff35a-215">Получение маркера бота</span><span class="sxs-lookup"><span data-stu-id="ff35a-215">Receive the bot token</span></span>

<span data-ttu-id="ff35a-216">Ответ с маркером отправляется с помощью действия вызова с той же схемой, что и другие действия вызова, которые получают сегодня боты.</span><span class="sxs-lookup"><span data-stu-id="ff35a-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="ff35a-217">Единственное отличие — это имя вызова, **вход/tokenExchange** и **поле значений.**</span><span class="sxs-lookup"><span data-stu-id="ff35a-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="ff35a-218">Поле **значений** содержит **Id**, строку начального запроса  на токен и поле маркера, строковую величину, включая маркер.</span><span class="sxs-lookup"><span data-stu-id="ff35a-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="ff35a-219">Вы можете получить несколько ответов на заданный запрос, если у пользователя есть несколько активных конечных точек.</span><span class="sxs-lookup"><span data-stu-id="ff35a-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="ff35a-220">Необходимо оттапликировать ответы с помощью маркера.</span><span class="sxs-lookup"><span data-stu-id="ff35a-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="ff35a-221">C# для обработки действия вызова</span><span class="sxs-lookup"><span data-stu-id="ff35a-221">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="ff35a-222">Имеет `turnContext.activity.value` тип [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) и содержит маркер, который может быть дополнительно использован вашим ботом.</span><span class="sxs-lookup"><span data-stu-id="ff35a-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="ff35a-223">Вы должны хранить маркеры из соображений производительности и обновлять их.</span><span class="sxs-lookup"><span data-stu-id="ff35a-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="ff35a-224">Сбой обмена маркерами</span><span class="sxs-lookup"><span data-stu-id="ff35a-224">Token exchange failure</span></span>

<span data-ttu-id="ff35a-225">В случае сбоя обмена маркерами используйте следующий код:</span><span class="sxs-lookup"><span data-stu-id="ff35a-225">In case of token exchange failure, use the following code:</span></span>

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

<span data-ttu-id="ff35a-226">Чтобы понять, что делает бот, если биржа маркеров не запускает запрос на согласие, см. следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ff35a-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="ff35a-227">Никаких действий пользователя не требуется, так как бот принимает действия при сбой обмена маркерами.</span><span class="sxs-lookup"><span data-stu-id="ff35a-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="ff35a-228">Клиент начинает беседу с ботом, запускающий сценарий OAuth.</span><span class="sxs-lookup"><span data-stu-id="ff35a-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="ff35a-229">Бот отправляет клиенту карту OAuth.</span><span class="sxs-lookup"><span data-stu-id="ff35a-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="ff35a-230">Клиент перехватывает карту OAuth перед ее отображением пользователю и проверяет, содержит ли она `TokenExchangeResource` свойство.</span><span class="sxs-lookup"><span data-stu-id="ff35a-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="ff35a-231">Если свойство существует, клиент отправляет `TokenExchangeInvokeRequest` боту.</span><span class="sxs-lookup"><span data-stu-id="ff35a-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="ff35a-232">Клиент должен иметь обменяемый маркер для пользователя, который должен быть маркером Azure AD v2 и аудитория которого должна быть такой же, как `TokenExchangeResource.Uri` свойство.</span><span class="sxs-lookup"><span data-stu-id="ff35a-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="ff35a-233">Клиент отправляет боту действие вызова со следующим кодом:</span><span class="sxs-lookup"><span data-stu-id="ff35a-233">The client sends an invoke activity to the bot with the following code:</span></span>

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

5. <span data-ttu-id="ff35a-234">Бот обрабатывает и `TokenExchangeInvokeRequest` возвращает обратно `TokenExchangeInvokeResponse` клиенту.</span><span class="sxs-lookup"><span data-stu-id="ff35a-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="ff35a-235">Клиент должен подождать, пока он получит `TokenExchangeInvokeResponse` .</span><span class="sxs-lookup"><span data-stu-id="ff35a-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

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

6. <span data-ttu-id="ff35a-236">Если `TokenExchangeInvokeResponse` у клиента есть a, клиент не показывает карту `status` `200` OAuth.</span><span class="sxs-lookup"><span data-stu-id="ff35a-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="ff35a-237">См. [изображение нормального потока.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff35a-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="ff35a-238">Для любого другого или если не получено, клиент показывает пользователю карточку `status` `TokenExchangeInvokeResponse` OAuth.</span><span class="sxs-lookup"><span data-stu-id="ff35a-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="ff35a-239">См. [изображение потока отката.](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="ff35a-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="ff35a-240">Это гарантирует, что поток SSO возвращается к нормальному потоку OAuthCard в случае ошибок или невыполнения зависимостей, таких как согласие пользователя.</span><span class="sxs-lookup"><span data-stu-id="ff35a-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="ff35a-241">Обновление примера auth</span><span class="sxs-lookup"><span data-stu-id="ff35a-241">Update the auth sample</span></span>

<span data-ttu-id="ff35a-242">Пример [auth Open Teams,](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) а затем выполните следующие действия, чтобы обновить его:</span><span class="sxs-lookup"><span data-stu-id="ff35a-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="ff35a-243">Обнови команду TeamsBot для обработки отработки входящих запросов, включив в нее следующий код:</span><span class="sxs-lookup"><span data-stu-id="ff35a-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="ff35a-244">Обновление, включив пароль и имя подключения, определенное в обновлении портала Azure с подключением `appsettings.json` `botId` [OAuth.](#update-the-azure-portal-with-the-oauth-connection)</span><span class="sxs-lookup"><span data-stu-id="ff35a-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="ff35a-245">Обнови манифест и `token.botframework.com` убедитесь, что он находится в допустимом списке доменов.</span><span class="sxs-lookup"><span data-stu-id="ff35a-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="ff35a-246">Дополнительные сведения см. в [примере teams auth](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span><span class="sxs-lookup"><span data-stu-id="ff35a-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="ff35a-247">Zip манифест с изображениями профиля и установить его в Teams.</span><span class="sxs-lookup"><span data-stu-id="ff35a-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="ff35a-248">Пример кода</span><span class="sxs-lookup"><span data-stu-id="ff35a-248">Code sample</span></span>
|<span data-ttu-id="ff35a-249">**Пример имени**</span><span class="sxs-lookup"><span data-stu-id="ff35a-249">**Sample name**</span></span> | <span data-ttu-id="ff35a-250">**Описание**</span><span class="sxs-lookup"><span data-stu-id="ff35a-250">**Description**</span></span> |<span data-ttu-id="ff35a-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="ff35a-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="ff35a-252">SDK для базы ботов</span><span class="sxs-lookup"><span data-stu-id="ff35a-252">Bot framework SDK</span></span> | <span data-ttu-id="ff35a-253">Пример для использования SDK-базы ботов.</span><span class="sxs-lookup"><span data-stu-id="ff35a-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="ff35a-254">View</span><span class="sxs-lookup"><span data-stu-id="ff35a-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
