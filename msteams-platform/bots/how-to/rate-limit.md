---
title: Оптимизация бота с ограничением скорости в Teams
description: Ограничение скорости и лучшие практики в Microsoft Teams
ms.topic: conceptual
keywords: ограничения скорости командных ботов
ms.openlocfilehash: 245c51fc736e5f888299535c3e50ec6232183623
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696999"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="3a36d-104">Оптимизация бота с ограничением скорости в Teams</span><span class="sxs-lookup"><span data-stu-id="3a36d-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="3a36d-105">Ограничение скорости — это метод, ограничивающий сообщения определенной максимальной частотой.</span><span class="sxs-lookup"><span data-stu-id="3a36d-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="3a36d-106">В общем принципе ваше приложение должно ограничить количество сообщений, которые оно публикует, отдельным чатом или разговором по каналу.</span><span class="sxs-lookup"><span data-stu-id="3a36d-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="3a36d-107">Это обеспечивает оптимальное впечатление и сообщения не отображаются в качестве нежелательной почты для пользователей.</span><span class="sxs-lookup"><span data-stu-id="3a36d-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="3a36d-108">Для защиты Microsoft Teams и ее пользователей API-бота предоставляют ограничение скорости для входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="3a36d-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="3a36d-109">Приложения, которые преодолеют это ограничение, получают `HTTP 429 Too Many Requests` состояние ошибки.</span><span class="sxs-lookup"><span data-stu-id="3a36d-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="3a36d-110">Все запросы подчиняются одной и той же политике ограничения скорости, включая отправку сообщений, список каналов и извлечение реестра.</span><span class="sxs-lookup"><span data-stu-id="3a36d-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="3a36d-111">Поскольку точные значения ограничений скорости могут изменяться, ваше приложение должно реализовать соответствующее поведение при возврате `HTTP 429 Too Many Requests` API.</span><span class="sxs-lookup"><span data-stu-id="3a36d-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="3a36d-112">Ограничения скорости обработки</span><span class="sxs-lookup"><span data-stu-id="3a36d-112">Handle rate limits</span></span>

<span data-ttu-id="3a36d-113">При выдаче SDK-операции Bot Builder можно обрабатывать и `Microsoft.Rest.HttpOperationException` проверять код состояния.</span><span class="sxs-lookup"><span data-stu-id="3a36d-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="3a36d-114">В следующем коде показан пример ограничения скорости обработки:</span><span class="sxs-lookup"><span data-stu-id="3a36d-114">The following code shows an example of handling rate limits:</span></span>

```csharp
try
{
    // Perform Bot Framework operation
    // for example, await connector.Conversations.UpdateActivityAsync(reply);
}
catch (HttpOperationException ex)
{
    if (ex.Response != null && (uint)ex.Response.StatusCode ==  429)
    {
        //Perform retry of the above operation/Action method
    }
}
```

<span data-ttu-id="3a36d-115">После обработки ограничений скорости для ботов можно обрабатывать ответы с `HTTP 429` помощью экспоненциального отработки.</span><span class="sxs-lookup"><span data-stu-id="3a36d-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="3a36d-116">Обработка `HTTP 429` ответов</span><span class="sxs-lookup"><span data-stu-id="3a36d-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="3a36d-117">В общем, необходимо принять простые меры предосторожности, чтобы избежать получения `HTTP 429` ответов.</span><span class="sxs-lookup"><span data-stu-id="3a36d-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="3a36d-118">Например, не следует выдавать несколько запросов в один и тот же личный или каналный разговор.</span><span class="sxs-lookup"><span data-stu-id="3a36d-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="3a36d-119">Вместо этого создайте пакет запросов API.</span><span class="sxs-lookup"><span data-stu-id="3a36d-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="3a36d-120">Использование экспоненциального отработки со случайным испугом — это рекомендуемый способ обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="3a36d-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="3a36d-121">Это гарантирует, что в нескольких запросах не будут вводиться столкновения при повторном запросе.</span><span class="sxs-lookup"><span data-stu-id="3a36d-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="3a36d-122">После обработки ответов можно перейти к примеру для обнаружения `HTTP 429` временных исключений.</span><span class="sxs-lookup"><span data-stu-id="3a36d-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="3a36d-123">Обнаружение примера временных исключений</span><span class="sxs-lookup"><span data-stu-id="3a36d-123">Detect transient exceptions example</span></span>

<span data-ttu-id="3a36d-124">В следующем коде показан пример использования экспоненциального отработки с помощью преходящего блока обработки ошибок приложения:</span><span class="sxs-lookup"><span data-stu-id="3a36d-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
    {
        // List of error codes to retry on
        List<int> transientErrorStatusCodes = new List<int>() { 429 };

        public bool IsTransient(Exception ex)
        {
            if (ex.Message.Contains("429"))
                return true;

            var httpOperationException = ex as HttpOperationException;
            if (httpOperationException != null)
            {
                return httpOperationException.Response != null &&
                        transientErrorStatusCodes.Contains((int)httpOperationException.Response.StatusCode);
            }

            return false;
        }
    }
```

<span data-ttu-id="3a36d-125">Вы можете выполнять отработку и повторное выполнение с помощью [обработки временных ошибок.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="3a36d-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="3a36d-126">Инструкции по получению и установке пакета NuGet см. в добавлении к решению блока обработки [сбоя.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="3a36d-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="3a36d-127">См. [также переходную обработку с ошибками.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="3a36d-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="3a36d-128">После того, как вы пройдите по примеру обнаружения временных исключений, перейдите по примеру экспоненциального обратного степеня.</span><span class="sxs-lookup"><span data-stu-id="3a36d-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="3a36d-129">Вы можете использовать экспоненциальный отбой вместо повторной работы по сбоям.</span><span class="sxs-lookup"><span data-stu-id="3a36d-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="3a36d-130">Пример backoff</span><span class="sxs-lookup"><span data-stu-id="3a36d-130">Backoff example</span></span>

<span data-ttu-id="3a36d-131">Помимо обнаружения ограничений скорости, вы также можете выполнить экспоненциальный отсев.</span><span class="sxs-lookup"><span data-stu-id="3a36d-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="3a36d-132">В следующем коде показан пример экспоненциального отсевов:</span><span class="sxs-lookup"><span data-stu-id="3a36d-132">The following code shows an example of exponential backoff:</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), exponentialBackoffRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync( (Activity)reply) ).ConfigureAwait(false);
```

<span data-ttu-id="3a36d-133">Можно также выполнить выполнение метода `System.Action` с помощью политики повторного выполнения, описанной в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="3a36d-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="3a36d-134">В ссылаемой библиотеке также можно указать фиксированный интервал или механизм линейного отсевов.</span><span class="sxs-lookup"><span data-stu-id="3a36d-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="3a36d-135">Храните значение и стратегию в файле конфигурации для настройки и настройки значений во время запуска.</span><span class="sxs-lookup"><span data-stu-id="3a36d-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="3a36d-136">Дополнительные сведения см. [в шаблонах повторного получения.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="3a36d-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="3a36d-137">Вы также можете обрабатывать ограничение скорости с помощью каждого бота в потоке.</span><span class="sxs-lookup"><span data-stu-id="3a36d-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="3a36d-138">Ограничение на один бот на поток</span><span class="sxs-lookup"><span data-stu-id="3a36d-138">Per bot per thread limit</span></span>

>[!NOTE]
> <span data-ttu-id="3a36d-139">Разделение сообщений на уровне службы приводит к большему, чем ожидалось, запросам в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="3a36d-139">Message splitting at the service level results in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="3a36d-140">Если вас беспокоит приближение к ограничениям, необходимо реализовать стратегию [обратного выхода.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="3a36d-140">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="3a36d-141">Значения, предоставляемые в этом разделе, являются только для оценки.</span><span class="sxs-lookup"><span data-stu-id="3a36d-141">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="3a36d-142">Ограничение для каждого бота в потоке управляет трафиком, который бот может создавать в одном разговоре.</span><span class="sxs-lookup"><span data-stu-id="3a36d-142">The per bot per thread limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="3a36d-143">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="3a36d-143">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="3a36d-144">В следующей таблице содержится ограничение для каждого бота на поток:</span><span class="sxs-lookup"><span data-stu-id="3a36d-144">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="3a36d-145">Сценарий</span><span class="sxs-lookup"><span data-stu-id="3a36d-145">Scenario</span></span> | <span data-ttu-id="3a36d-146">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="3a36d-146">Time period in seconds</span></span> | <span data-ttu-id="3a36d-147">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="3a36d-147">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a36d-148">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-148">Send to conversation</span></span> | <span data-ttu-id="3a36d-149">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-149">1</span></span> | <span data-ttu-id="3a36d-150">7 </span><span class="sxs-lookup"><span data-stu-id="3a36d-150">7</span></span> |
| <span data-ttu-id="3a36d-151">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-151">Send to conversation</span></span> | <span data-ttu-id="3a36d-152">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-152">2</span></span> | <span data-ttu-id="3a36d-153">8 </span><span class="sxs-lookup"><span data-stu-id="3a36d-153">8</span></span> |
| <span data-ttu-id="3a36d-154">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-154">Send to conversation</span></span> | <span data-ttu-id="3a36d-155">30</span><span class="sxs-lookup"><span data-stu-id="3a36d-155">30</span></span> | <span data-ttu-id="3a36d-156">60</span><span class="sxs-lookup"><span data-stu-id="3a36d-156">60</span></span> |
| <span data-ttu-id="3a36d-157">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-157">Send to conversation</span></span> | <span data-ttu-id="3a36d-158">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-158">3600</span></span> | <span data-ttu-id="3a36d-159">1800</span><span class="sxs-lookup"><span data-stu-id="3a36d-159">1800</span></span> |
| <span data-ttu-id="3a36d-160">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-160">Create conversation</span></span> | <span data-ttu-id="3a36d-161">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-161">1</span></span> | <span data-ttu-id="3a36d-162">7 </span><span class="sxs-lookup"><span data-stu-id="3a36d-162">7</span></span> |
| <span data-ttu-id="3a36d-163">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-163">Create conversation</span></span> | <span data-ttu-id="3a36d-164">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-164">2</span></span> | <span data-ttu-id="3a36d-165">8 </span><span class="sxs-lookup"><span data-stu-id="3a36d-165">8</span></span> |
| <span data-ttu-id="3a36d-166">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-166">Create conversation</span></span> | <span data-ttu-id="3a36d-167">30</span><span class="sxs-lookup"><span data-stu-id="3a36d-167">30</span></span> | <span data-ttu-id="3a36d-168">60</span><span class="sxs-lookup"><span data-stu-id="3a36d-168">60</span></span> |
| <span data-ttu-id="3a36d-169">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-169">Create conversation</span></span> | <span data-ttu-id="3a36d-170">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-170">3600</span></span> | <span data-ttu-id="3a36d-171">1800</span><span class="sxs-lookup"><span data-stu-id="3a36d-171">1800</span></span> |
| <span data-ttu-id="3a36d-172">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-172">Get conversation members</span></span>| <span data-ttu-id="3a36d-173">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-173">1</span></span> | <span data-ttu-id="3a36d-174">14 </span><span class="sxs-lookup"><span data-stu-id="3a36d-174">14</span></span> |
| <span data-ttu-id="3a36d-175">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-175">Get conversation members</span></span>| <span data-ttu-id="3a36d-176">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-176">2</span></span> | <span data-ttu-id="3a36d-177">16 </span><span class="sxs-lookup"><span data-stu-id="3a36d-177">16</span></span> |
| <span data-ttu-id="3a36d-178">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-178">Get conversation members</span></span>| <span data-ttu-id="3a36d-179">30</span><span class="sxs-lookup"><span data-stu-id="3a36d-179">30</span></span> | <span data-ttu-id="3a36d-180">120</span><span class="sxs-lookup"><span data-stu-id="3a36d-180">120</span></span> |
| <span data-ttu-id="3a36d-181">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-181">Get conversation members</span></span>| <span data-ttu-id="3a36d-182">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-182">3600</span></span> | <span data-ttu-id="3a36d-183">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-183">3600</span></span> |
| <span data-ttu-id="3a36d-184">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-184">Get conversations</span></span> | <span data-ttu-id="3a36d-185">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-185">1</span></span> | <span data-ttu-id="3a36d-186">14 </span><span class="sxs-lookup"><span data-stu-id="3a36d-186">14</span></span> |
| <span data-ttu-id="3a36d-187">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-187">Get conversations</span></span> | <span data-ttu-id="3a36d-188">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-188">2</span></span> | <span data-ttu-id="3a36d-189">16 </span><span class="sxs-lookup"><span data-stu-id="3a36d-189">16</span></span> |
| <span data-ttu-id="3a36d-190">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-190">Get conversations</span></span> | <span data-ttu-id="3a36d-191">30</span><span class="sxs-lookup"><span data-stu-id="3a36d-191">30</span></span> | <span data-ttu-id="3a36d-192">120</span><span class="sxs-lookup"><span data-stu-id="3a36d-192">120</span></span> |
| <span data-ttu-id="3a36d-193">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-193">Get conversations</span></span> | <span data-ttu-id="3a36d-194">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-194">3600</span></span> | <span data-ttu-id="3a36d-195">3600</span><span class="sxs-lookup"><span data-stu-id="3a36d-195">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="3a36d-196">Предыдущие версии и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API отстают.</span><span class="sxs-lookup"><span data-stu-id="3a36d-196">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="3a36d-197">Они отлаговываются до пяти запросов в минуту и возвращают не более 10 000 участников на каждую команду.</span><span class="sxs-lookup"><span data-stu-id="3a36d-197">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="3a36d-198">Чтобы обновить SDK bot Framework и код для использования последних конечных точек API с paginated, см. в рубрике Изменения API bot для членов команды и [чата.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="3a36d-198">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="3a36d-199">Вы также можете обрабатывать ограничение скорости с помощью ограничения потока для всех ботов.</span><span class="sxs-lookup"><span data-stu-id="3a36d-199">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="3a36d-200">Ограничение потока для всех ботов</span><span class="sxs-lookup"><span data-stu-id="3a36d-200">Per thread limit for all bots</span></span>

<span data-ttu-id="3a36d-201">Ограничение потока для всех ботов контролирует трафик, который всем ботам разрешено создавать в одном диалоге.</span><span class="sxs-lookup"><span data-stu-id="3a36d-201">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="3a36d-202">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="3a36d-202">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="3a36d-203">В следующей таблице содержится ограничение потока для всех ботов:</span><span class="sxs-lookup"><span data-stu-id="3a36d-203">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="3a36d-204">Сценарий</span><span class="sxs-lookup"><span data-stu-id="3a36d-204">Scenario</span></span> | <span data-ttu-id="3a36d-205">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="3a36d-205">Time period in seconds</span></span> | <span data-ttu-id="3a36d-206">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="3a36d-206">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3a36d-207">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-207">Send to conversation</span></span> | <span data-ttu-id="3a36d-208">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-208">1</span></span> | <span data-ttu-id="3a36d-209">14 </span><span class="sxs-lookup"><span data-stu-id="3a36d-209">14</span></span> |
| <span data-ttu-id="3a36d-210">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="3a36d-210">Send to conversation</span></span> | <span data-ttu-id="3a36d-211">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-211">2</span></span> | <span data-ttu-id="3a36d-212">16 </span><span class="sxs-lookup"><span data-stu-id="3a36d-212">16</span></span> |
| <span data-ttu-id="3a36d-213">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-213">Create conversation</span></span> | <span data-ttu-id="3a36d-214">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-214">1</span></span> | <span data-ttu-id="3a36d-215">14 </span><span class="sxs-lookup"><span data-stu-id="3a36d-215">14</span></span> |
| <span data-ttu-id="3a36d-216">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-216">Create conversation</span></span> | <span data-ttu-id="3a36d-217">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-217">2</span></span> | <span data-ttu-id="3a36d-218">16 </span><span class="sxs-lookup"><span data-stu-id="3a36d-218">16</span></span> |
| <span data-ttu-id="3a36d-219">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-219">Create conversation</span></span>| <span data-ttu-id="3a36d-220">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-220">1</span></span> | <span data-ttu-id="3a36d-221">14 </span><span class="sxs-lookup"><span data-stu-id="3a36d-221">14</span></span> |
| <span data-ttu-id="3a36d-222">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-222">Create conversation</span></span>| <span data-ttu-id="3a36d-223">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-223">2</span></span> | <span data-ttu-id="3a36d-224">16 </span><span class="sxs-lookup"><span data-stu-id="3a36d-224">16</span></span> |
| <span data-ttu-id="3a36d-225">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-225">Get conversation members</span></span>| <span data-ttu-id="3a36d-226">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-226">1</span></span> | <span data-ttu-id="3a36d-227">28</span><span class="sxs-lookup"><span data-stu-id="3a36d-227">28</span></span> |
| <span data-ttu-id="3a36d-228">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-228">Get conversation members</span></span>| <span data-ttu-id="3a36d-229">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-229">2</span></span> | <span data-ttu-id="3a36d-230">32</span><span class="sxs-lookup"><span data-stu-id="3a36d-230">32</span></span> |
| <span data-ttu-id="3a36d-231">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-231">Get conversations</span></span> | <span data-ttu-id="3a36d-232">1</span><span class="sxs-lookup"><span data-stu-id="3a36d-232">1</span></span> | <span data-ttu-id="3a36d-233">28</span><span class="sxs-lookup"><span data-stu-id="3a36d-233">28</span></span> |
| <span data-ttu-id="3a36d-234">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="3a36d-234">Get conversations</span></span> | <span data-ttu-id="3a36d-235">2</span><span class="sxs-lookup"><span data-stu-id="3a36d-235">2</span></span> | <span data-ttu-id="3a36d-236">32</span><span class="sxs-lookup"><span data-stu-id="3a36d-236">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="3a36d-237">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="3a36d-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3a36d-238">Боты вызовов и собраний</span><span class="sxs-lookup"><span data-stu-id="3a36d-238">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

