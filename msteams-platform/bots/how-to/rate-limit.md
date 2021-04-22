---
title: Оптимизация бота с ограничением скорости в Teams
description: Ограничение скорости и лучшие практики в Microsoft Teams
ms.topic: conceptual
keywords: ограничения скорости командных ботов
ms.openlocfilehash: 690d09e4a3b611c024f32d3776ca73e42d63ee7f
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922505"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="628f6-104">Оптимизация бота с ограничением скорости в Teams</span><span class="sxs-lookup"><span data-stu-id="628f6-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="628f6-105">Ограничение скорости — это метод, ограничивающий сообщения определенной максимальной частотой.</span><span class="sxs-lookup"><span data-stu-id="628f6-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="628f6-106">В общем принципе ваше приложение должно ограничить количество сообщений, которые оно публикует, отдельным чатом или разговором по каналу.</span><span class="sxs-lookup"><span data-stu-id="628f6-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="628f6-107">Это обеспечивает оптимальное впечатление и сообщения не отображаются в качестве нежелательной почты для пользователей.</span><span class="sxs-lookup"><span data-stu-id="628f6-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="628f6-108">Для защиты Microsoft Teams и ее пользователей API-бота предоставляют ограничение скорости для входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="628f6-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="628f6-109">Приложения, которые преодолеют это ограничение, получают `HTTP 429 Too Many Requests` состояние ошибки.</span><span class="sxs-lookup"><span data-stu-id="628f6-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="628f6-110">Все запросы подчиняются одной и той же политике ограничения скорости, включая отправку сообщений, список каналов и извлечение реестра.</span><span class="sxs-lookup"><span data-stu-id="628f6-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="628f6-111">Поскольку точные значения ограничений скорости могут изменяться, ваше приложение должно реализовать соответствующее поведение при возврате `HTTP 429 Too Many Requests` API.</span><span class="sxs-lookup"><span data-stu-id="628f6-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="628f6-112">Ограничения скорости обработки</span><span class="sxs-lookup"><span data-stu-id="628f6-112">Handle rate limits</span></span>

<span data-ttu-id="628f6-113">При выдаче SDK-операции Bot Builder можно обрабатывать и `Microsoft.Rest.HttpOperationException` проверять код состояния.</span><span class="sxs-lookup"><span data-stu-id="628f6-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="628f6-114">В следующем коде показан пример ограничения скорости обработки:</span><span class="sxs-lookup"><span data-stu-id="628f6-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="628f6-115">После обработки ограничений скорости для ботов можно обрабатывать ответы с `HTTP 429` помощью экспоненциального отработки.</span><span class="sxs-lookup"><span data-stu-id="628f6-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="628f6-116">Обработка `HTTP 429` ответов</span><span class="sxs-lookup"><span data-stu-id="628f6-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="628f6-117">В общем, необходимо принять простые меры предосторожности, чтобы избежать получения `HTTP 429` ответов.</span><span class="sxs-lookup"><span data-stu-id="628f6-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="628f6-118">Например, не следует выдавать несколько запросов в один и тот же личный или каналный разговор.</span><span class="sxs-lookup"><span data-stu-id="628f6-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="628f6-119">Вместо этого создайте пакет запросов API.</span><span class="sxs-lookup"><span data-stu-id="628f6-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="628f6-120">Использование экспоненциального отработки со случайным испугом — это рекомендуемый способ обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="628f6-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="628f6-121">Это гарантирует, что в нескольких запросах не будут вводиться столкновения при повторном запросе.</span><span class="sxs-lookup"><span data-stu-id="628f6-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="628f6-122">После обработки ответов можно перейти к примеру для обнаружения `HTTP 429` временных исключений.</span><span class="sxs-lookup"><span data-stu-id="628f6-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="628f6-123">Обнаружение примера временных исключений</span><span class="sxs-lookup"><span data-stu-id="628f6-123">Detect transient exceptions example</span></span>

<span data-ttu-id="628f6-124">В следующем коде показан пример использования экспоненциального отработки с помощью преходящего блока обработки ошибок приложения:</span><span class="sxs-lookup"><span data-stu-id="628f6-124">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="628f6-125">Вы можете выполнять отработку и повторное выполнение с помощью [обработки временных ошибок.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="628f6-125">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="628f6-126">Инструкции по получению и установке пакета NuGet см. в добавлении к решению блока обработки [сбоя.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="628f6-126">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="628f6-127">См. [также переходную обработку с ошибками.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="628f6-127">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="628f6-128">После того, как вы пройдите по примеру обнаружения временных исключений, перейдите по примеру экспоненциального обратного степеня.</span><span class="sxs-lookup"><span data-stu-id="628f6-128">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="628f6-129">Вы можете использовать экспоненциальный отбой вместо повторной работы по сбоям.</span><span class="sxs-lookup"><span data-stu-id="628f6-129">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="628f6-130">Пример backoff</span><span class="sxs-lookup"><span data-stu-id="628f6-130">Backoff example</span></span>

<span data-ttu-id="628f6-131">Помимо обнаружения ограничений скорости, вы также можете выполнить экспоненциальный отсев.</span><span class="sxs-lookup"><span data-stu-id="628f6-131">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="628f6-132">В следующем коде показан пример экспоненциального отсевов:</span><span class="sxs-lookup"><span data-stu-id="628f6-132">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="628f6-133">Можно также выполнить выполнение метода `System.Action` с помощью политики повторного выполнения, описанной в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="628f6-133">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="628f6-134">В ссылаемой библиотеке также можно указать фиксированный интервал или механизм линейного отсевов.</span><span class="sxs-lookup"><span data-stu-id="628f6-134">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="628f6-135">Храните значение и стратегию в файле конфигурации для настройки и настройки значений во время запуска.</span><span class="sxs-lookup"><span data-stu-id="628f6-135">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="628f6-136">Дополнительные сведения см. [в шаблонах повторного получения.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="628f6-136">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="628f6-137">Вы также можете обрабатывать ограничение скорости с помощью каждого бота в потоке.</span><span class="sxs-lookup"><span data-stu-id="628f6-137">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="628f6-138">Ограничение на один бот на поток</span><span class="sxs-lookup"><span data-stu-id="628f6-138">Per bot per thread limit</span></span>

<span data-ttu-id="628f6-139">Ограничение для каждого бота в потоке управляет трафиком, который может создаваться ботом в одном разговоре.</span><span class="sxs-lookup"><span data-stu-id="628f6-139">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="628f6-140">Беседа 1:1 между ботом и пользователем, групповым чатом или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="628f6-140">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="628f6-141">Таким образом, если приложение отправляет по одному сообщению бота каждому пользователю, ограничение потока не затормажается.</span><span class="sxs-lookup"><span data-stu-id="628f6-141">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="628f6-142">Ограничение потока в 3600 секунд и 1800 операций применяется только в том случае, если несколько сообщений бота отправляются одному пользователю.</span><span class="sxs-lookup"><span data-stu-id="628f6-142">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="628f6-143">Глобальное ограничение для каждого клиента — 30 запросов в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="628f6-143">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="628f6-144">Таким образом, общее число сообщений бота в секунду не должно пересекать ограничение потока.</span><span class="sxs-lookup"><span data-stu-id="628f6-144">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="628f6-145">Разделение сообщений на уровне службы приводит к большему, чем ожидалось, RPS.</span><span class="sxs-lookup"><span data-stu-id="628f6-145">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="628f6-146">Если вас беспокоит приближение к ограничениям, необходимо реализовать стратегию [обратного выхода.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="628f6-146">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="628f6-147">Значения, предоставляемые в этом разделе, являются только для оценки.</span><span class="sxs-lookup"><span data-stu-id="628f6-147">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="628f6-148">В следующей таблице содержится ограничение для каждого бота на поток:</span><span class="sxs-lookup"><span data-stu-id="628f6-148">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="628f6-149">Сценарий</span><span class="sxs-lookup"><span data-stu-id="628f6-149">Scenario</span></span> | <span data-ttu-id="628f6-150">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="628f6-150">Time period in seconds</span></span> | <span data-ttu-id="628f6-151">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="628f6-151">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="628f6-152">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-152">Send to conversation</span></span> | <span data-ttu-id="628f6-153">1</span><span class="sxs-lookup"><span data-stu-id="628f6-153">1</span></span> | <span data-ttu-id="628f6-154">7 </span><span class="sxs-lookup"><span data-stu-id="628f6-154">7</span></span> |
| <span data-ttu-id="628f6-155">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-155">Send to conversation</span></span> | <span data-ttu-id="628f6-156">2</span><span class="sxs-lookup"><span data-stu-id="628f6-156">2</span></span> | <span data-ttu-id="628f6-157">8 </span><span class="sxs-lookup"><span data-stu-id="628f6-157">8</span></span> |
| <span data-ttu-id="628f6-158">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-158">Send to conversation</span></span> | <span data-ttu-id="628f6-159">30</span><span class="sxs-lookup"><span data-stu-id="628f6-159">30</span></span> | <span data-ttu-id="628f6-160">60</span><span class="sxs-lookup"><span data-stu-id="628f6-160">60</span></span> |
| <span data-ttu-id="628f6-161">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-161">Send to conversation</span></span> | <span data-ttu-id="628f6-162">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-162">3600</span></span> | <span data-ttu-id="628f6-163">1800</span><span class="sxs-lookup"><span data-stu-id="628f6-163">1800</span></span> |
| <span data-ttu-id="628f6-164">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-164">Create conversation</span></span> | <span data-ttu-id="628f6-165">1</span><span class="sxs-lookup"><span data-stu-id="628f6-165">1</span></span> | <span data-ttu-id="628f6-166">7 </span><span class="sxs-lookup"><span data-stu-id="628f6-166">7</span></span> |
| <span data-ttu-id="628f6-167">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-167">Create conversation</span></span> | <span data-ttu-id="628f6-168">2</span><span class="sxs-lookup"><span data-stu-id="628f6-168">2</span></span> | <span data-ttu-id="628f6-169">8 </span><span class="sxs-lookup"><span data-stu-id="628f6-169">8</span></span> |
| <span data-ttu-id="628f6-170">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-170">Create conversation</span></span> | <span data-ttu-id="628f6-171">30</span><span class="sxs-lookup"><span data-stu-id="628f6-171">30</span></span> | <span data-ttu-id="628f6-172">60</span><span class="sxs-lookup"><span data-stu-id="628f6-172">60</span></span> |
| <span data-ttu-id="628f6-173">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-173">Create conversation</span></span> | <span data-ttu-id="628f6-174">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-174">3600</span></span> | <span data-ttu-id="628f6-175">1800</span><span class="sxs-lookup"><span data-stu-id="628f6-175">1800</span></span> |
| <span data-ttu-id="628f6-176">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-176">Get conversation members</span></span>| <span data-ttu-id="628f6-177">1</span><span class="sxs-lookup"><span data-stu-id="628f6-177">1</span></span> | <span data-ttu-id="628f6-178">14 </span><span class="sxs-lookup"><span data-stu-id="628f6-178">14</span></span> |
| <span data-ttu-id="628f6-179">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-179">Get conversation members</span></span>| <span data-ttu-id="628f6-180">2</span><span class="sxs-lookup"><span data-stu-id="628f6-180">2</span></span> | <span data-ttu-id="628f6-181">16 </span><span class="sxs-lookup"><span data-stu-id="628f6-181">16</span></span> |
| <span data-ttu-id="628f6-182">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-182">Get conversation members</span></span>| <span data-ttu-id="628f6-183">30</span><span class="sxs-lookup"><span data-stu-id="628f6-183">30</span></span> | <span data-ttu-id="628f6-184">120</span><span class="sxs-lookup"><span data-stu-id="628f6-184">120</span></span> |
| <span data-ttu-id="628f6-185">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-185">Get conversation members</span></span>| <span data-ttu-id="628f6-186">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-186">3600</span></span> | <span data-ttu-id="628f6-187">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-187">3600</span></span> |
| <span data-ttu-id="628f6-188">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-188">Get conversations</span></span> | <span data-ttu-id="628f6-189">1</span><span class="sxs-lookup"><span data-stu-id="628f6-189">1</span></span> | <span data-ttu-id="628f6-190">14 </span><span class="sxs-lookup"><span data-stu-id="628f6-190">14</span></span> |
| <span data-ttu-id="628f6-191">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-191">Get conversations</span></span> | <span data-ttu-id="628f6-192">2</span><span class="sxs-lookup"><span data-stu-id="628f6-192">2</span></span> | <span data-ttu-id="628f6-193">16 </span><span class="sxs-lookup"><span data-stu-id="628f6-193">16</span></span> |
| <span data-ttu-id="628f6-194">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-194">Get conversations</span></span> | <span data-ttu-id="628f6-195">30</span><span class="sxs-lookup"><span data-stu-id="628f6-195">30</span></span> | <span data-ttu-id="628f6-196">120</span><span class="sxs-lookup"><span data-stu-id="628f6-196">120</span></span> |
| <span data-ttu-id="628f6-197">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-197">Get conversations</span></span> | <span data-ttu-id="628f6-198">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-198">3600</span></span> | <span data-ttu-id="628f6-199">3600</span><span class="sxs-lookup"><span data-stu-id="628f6-199">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="628f6-200">Предыдущие версии и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API отстают.</span><span class="sxs-lookup"><span data-stu-id="628f6-200">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="628f6-201">Они отлаговываются до пяти запросов в минуту и возвращают не более 10 000 участников на каждую команду.</span><span class="sxs-lookup"><span data-stu-id="628f6-201">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="628f6-202">Чтобы обновить SDK bot Framework и код для использования последних конечных точек API с paginated, см. в рубрике Изменения API bot для членов команды и [чата.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="628f6-202">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="628f6-203">Вы также можете обрабатывать ограничение скорости с помощью ограничения потока для всех ботов.</span><span class="sxs-lookup"><span data-stu-id="628f6-203">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="628f6-204">Ограничение потока для всех ботов</span><span class="sxs-lookup"><span data-stu-id="628f6-204">Per thread limit for all bots</span></span>

<span data-ttu-id="628f6-205">Ограничение потока для всех ботов контролирует трафик, который всем ботам разрешено создавать в одном диалоге.</span><span class="sxs-lookup"><span data-stu-id="628f6-205">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="628f6-206">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="628f6-206">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="628f6-207">В следующей таблице содержится ограничение потока для всех ботов:</span><span class="sxs-lookup"><span data-stu-id="628f6-207">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="628f6-208">Сценарий</span><span class="sxs-lookup"><span data-stu-id="628f6-208">Scenario</span></span> | <span data-ttu-id="628f6-209">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="628f6-209">Time period in seconds</span></span> | <span data-ttu-id="628f6-210">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="628f6-210">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="628f6-211">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-211">Send to conversation</span></span> | <span data-ttu-id="628f6-212">1</span><span class="sxs-lookup"><span data-stu-id="628f6-212">1</span></span> | <span data-ttu-id="628f6-213">14 </span><span class="sxs-lookup"><span data-stu-id="628f6-213">14</span></span> |
| <span data-ttu-id="628f6-214">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="628f6-214">Send to conversation</span></span> | <span data-ttu-id="628f6-215">2</span><span class="sxs-lookup"><span data-stu-id="628f6-215">2</span></span> | <span data-ttu-id="628f6-216">16 </span><span class="sxs-lookup"><span data-stu-id="628f6-216">16</span></span> |
| <span data-ttu-id="628f6-217">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-217">Create conversation</span></span> | <span data-ttu-id="628f6-218">1</span><span class="sxs-lookup"><span data-stu-id="628f6-218">1</span></span> | <span data-ttu-id="628f6-219">14 </span><span class="sxs-lookup"><span data-stu-id="628f6-219">14</span></span> |
| <span data-ttu-id="628f6-220">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-220">Create conversation</span></span> | <span data-ttu-id="628f6-221">2</span><span class="sxs-lookup"><span data-stu-id="628f6-221">2</span></span> | <span data-ttu-id="628f6-222">16 </span><span class="sxs-lookup"><span data-stu-id="628f6-222">16</span></span> |
| <span data-ttu-id="628f6-223">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-223">Create conversation</span></span>| <span data-ttu-id="628f6-224">1</span><span class="sxs-lookup"><span data-stu-id="628f6-224">1</span></span> | <span data-ttu-id="628f6-225">14 </span><span class="sxs-lookup"><span data-stu-id="628f6-225">14</span></span> |
| <span data-ttu-id="628f6-226">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-226">Create conversation</span></span>| <span data-ttu-id="628f6-227">2</span><span class="sxs-lookup"><span data-stu-id="628f6-227">2</span></span> | <span data-ttu-id="628f6-228">16 </span><span class="sxs-lookup"><span data-stu-id="628f6-228">16</span></span> |
| <span data-ttu-id="628f6-229">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-229">Get conversation members</span></span>| <span data-ttu-id="628f6-230">1</span><span class="sxs-lookup"><span data-stu-id="628f6-230">1</span></span> | <span data-ttu-id="628f6-231">28</span><span class="sxs-lookup"><span data-stu-id="628f6-231">28</span></span> |
| <span data-ttu-id="628f6-232">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-232">Get conversation members</span></span>| <span data-ttu-id="628f6-233">2</span><span class="sxs-lookup"><span data-stu-id="628f6-233">2</span></span> | <span data-ttu-id="628f6-234">32</span><span class="sxs-lookup"><span data-stu-id="628f6-234">32</span></span> |
| <span data-ttu-id="628f6-235">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-235">Get conversations</span></span> | <span data-ttu-id="628f6-236">1</span><span class="sxs-lookup"><span data-stu-id="628f6-236">1</span></span> | <span data-ttu-id="628f6-237">28</span><span class="sxs-lookup"><span data-stu-id="628f6-237">28</span></span> |
| <span data-ttu-id="628f6-238">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="628f6-238">Get conversations</span></span> | <span data-ttu-id="628f6-239">2</span><span class="sxs-lookup"><span data-stu-id="628f6-239">2</span></span> | <span data-ttu-id="628f6-240">32</span><span class="sxs-lookup"><span data-stu-id="628f6-240">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="628f6-241">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="628f6-241">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="628f6-242">Боты для звонков и собраний</span><span class="sxs-lookup"><span data-stu-id="628f6-242">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

