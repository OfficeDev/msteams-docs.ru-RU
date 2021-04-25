---
title: Оптимизация бота с ограничением скорости в Teams
description: Ограничение скорости и лучшие практики в Microsoft Teams
ms.topic: conceptual
keywords: ограничения скорости командных ботов
ms.openlocfilehash: 9a30d86a82a591c4a1125632fa7409780effb269
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995857"
---
# <a name="optimize-your-bot-with-rate-limiting-in-teams"></a><span data-ttu-id="c1258-104">Оптимизация бота с ограничением скорости в Teams</span><span class="sxs-lookup"><span data-stu-id="c1258-104">Optimize your bot with rate limiting in Teams</span></span>

<span data-ttu-id="c1258-105">Ограничение скорости — это метод, ограничивающий сообщения определенной максимальной частотой.</span><span class="sxs-lookup"><span data-stu-id="c1258-105">Rate limiting is a method to limit messages to a certain maximum frequency.</span></span> <span data-ttu-id="c1258-106">В общем принципе ваше приложение должно ограничить количество сообщений, которые оно публикует, отдельным чатом или разговором по каналу.</span><span class="sxs-lookup"><span data-stu-id="c1258-106">As a general principle, your application must limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="c1258-107">Это обеспечивает оптимальное впечатление и сообщения не отображаются в качестве нежелательной почты для пользователей.</span><span class="sxs-lookup"><span data-stu-id="c1258-107">This ensures an optimal experience and messages do not appear as spam to your users.</span></span>

<span data-ttu-id="c1258-108">Для защиты Microsoft Teams и ее пользователей API-бота предоставляют ограничение скорости для входящих запросов.</span><span class="sxs-lookup"><span data-stu-id="c1258-108">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="c1258-109">Приложения, которые преодолеют это ограничение, получают `HTTP 429 Too Many Requests` состояние ошибки.</span><span class="sxs-lookup"><span data-stu-id="c1258-109">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="c1258-110">Все запросы подчиняются одной и той же политике ограничения скорости, включая отправку сообщений, список каналов и извлечение реестра.</span><span class="sxs-lookup"><span data-stu-id="c1258-110">All requests are subject to the same rate limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="c1258-111">Поскольку точные значения ограничений скорости могут изменяться, ваше приложение должно реализовать соответствующее поведение при возврате `HTTP 429 Too Many Requests` API.</span><span class="sxs-lookup"><span data-stu-id="c1258-111">As the exact values of rate limits are subject to change, your application must implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handle-rate-limits"></a><span data-ttu-id="c1258-112">Ограничения скорости обработки</span><span class="sxs-lookup"><span data-stu-id="c1258-112">Handle rate limits</span></span>

<span data-ttu-id="c1258-113">При выдаче SDK-операции Bot Builder можно обрабатывать и `Microsoft.Rest.HttpOperationException` проверять код состояния.</span><span class="sxs-lookup"><span data-stu-id="c1258-113">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

<span data-ttu-id="c1258-114">В следующем коде показан пример ограничения скорости обработки:</span><span class="sxs-lookup"><span data-stu-id="c1258-114">The following code shows an example of handling rate limits:</span></span>

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

<span data-ttu-id="c1258-115">После обработки ограничений скорости для ботов можно обрабатывать ответы с `HTTP 429` помощью экспоненциального отработки.</span><span class="sxs-lookup"><span data-stu-id="c1258-115">After you handle rate limits for bots, you can handle `HTTP 429` responses using an exponential backoff.</span></span>

## <a name="handle-http-429-responses"></a><span data-ttu-id="c1258-116">Обработка `HTTP 429` ответов</span><span class="sxs-lookup"><span data-stu-id="c1258-116">Handle `HTTP 429` responses</span></span>

<span data-ttu-id="c1258-117">В общем, необходимо принять простые меры предосторожности, чтобы избежать получения `HTTP 429` ответов.</span><span class="sxs-lookup"><span data-stu-id="c1258-117">In general, you must take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="c1258-118">Например, не следует выдавать несколько запросов в один и тот же личный или каналный разговор.</span><span class="sxs-lookup"><span data-stu-id="c1258-118">For example, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="c1258-119">Вместо этого создайте пакет запросов API.</span><span class="sxs-lookup"><span data-stu-id="c1258-119">Instead, create a batch of the API requests.</span></span>

<span data-ttu-id="c1258-120">Использование экспоненциального отработки со случайным испугом — это рекомендуемый способ обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="c1258-120">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="c1258-121">Это гарантирует, что в нескольких запросах не будут вводиться столкновения при повторном запросе.</span><span class="sxs-lookup"><span data-stu-id="c1258-121">This ensures that multiple requests do not introduce collisions on retries.</span></span>

<span data-ttu-id="c1258-122">После обработки ответов можно перейти к примеру для обнаружения `HTTP 429` временных исключений.</span><span class="sxs-lookup"><span data-stu-id="c1258-122">After you handle `HTTP 429` responses, you can go through the example for detecting transient exceptions.</span></span>

> [!NOTE]
> <span data-ttu-id="c1258-123">Помимо повторного изменения кода **ошибки 429,** необходимо также повторно использовать коды **ошибок 412,** **502** и **504.**</span><span class="sxs-lookup"><span data-stu-id="c1258-123">In addition to retyring error code **429**, error codes **412**, **502**, and **504** must also be retried.</span></span>

## <a name="detect-transient-exceptions-example"></a><span data-ttu-id="c1258-124">Обнаружение примера временных исключений</span><span class="sxs-lookup"><span data-stu-id="c1258-124">Detect transient exceptions example</span></span>

<span data-ttu-id="c1258-125">В следующем коде показан пример использования экспоненциального отработки с помощью преходящего блока обработки ошибок приложения:</span><span class="sxs-lookup"><span data-stu-id="c1258-125">The following code shows an example of using exponential backoff using the transient fault handling application block:</span></span>

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

<span data-ttu-id="c1258-126">Вы можете выполнять отработку и повторное выполнение с помощью [обработки временных ошибок.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="c1258-126">You can perform backoff and retries using [transient fault handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="c1258-127">Инструкции по получению и установке пакета NuGet см. в добавлении к решению блока обработки [сбоя.](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)</span><span class="sxs-lookup"><span data-stu-id="c1258-127">For guidelines on obtaining and installing the NuGet package, see [adding the transient fault handling application block to your solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span></span> <span data-ttu-id="c1258-128">См. [также переходную обработку с ошибками.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="c1258-128">See also [transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

<span data-ttu-id="c1258-129">После того, как вы пройдите по примеру обнаружения временных исключений, перейдите по примеру экспоненциального обратного степеня.</span><span class="sxs-lookup"><span data-stu-id="c1258-129">After you go through the example for detecting transient exceptions, go through the exponential backoff example.</span></span> <span data-ttu-id="c1258-130">Вы можете использовать экспоненциальный отбой вместо повторной работы по сбоям.</span><span class="sxs-lookup"><span data-stu-id="c1258-130">You can use exponential backoff instead of retrying on failures.</span></span>

## <a name="backoff-example"></a><span data-ttu-id="c1258-131">Пример backoff</span><span class="sxs-lookup"><span data-stu-id="c1258-131">Backoff example</span></span>

<span data-ttu-id="c1258-132">Помимо обнаружения ограничений скорости, вы также можете выполнить экспоненциальный отсев.</span><span class="sxs-lookup"><span data-stu-id="c1258-132">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

<span data-ttu-id="c1258-133">В следующем коде показан пример экспоненциального отсевов:</span><span class="sxs-lookup"><span data-stu-id="c1258-133">The following code shows an example of exponential backoff:</span></span>

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

<span data-ttu-id="c1258-134">Можно также выполнить выполнение метода `System.Action` с помощью политики повторного выполнения, описанной в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="c1258-134">You can also perform a `System.Action` method execution with the retry policy described in this section.</span></span> <span data-ttu-id="c1258-135">В ссылаемой библиотеке также можно указать фиксированный интервал или механизм линейного отсевов.</span><span class="sxs-lookup"><span data-stu-id="c1258-135">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="c1258-136">Храните значение и стратегию в файле конфигурации для настройки и настройки значений во время запуска.</span><span class="sxs-lookup"><span data-stu-id="c1258-136">Store the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="c1258-137">Дополнительные сведения см. [в шаблонах повторного получения.](/azure/architecture/patterns/retry)</span><span class="sxs-lookup"><span data-stu-id="c1258-137">For more information, see [retry patterns](/azure/architecture/patterns/retry).</span></span>

<span data-ttu-id="c1258-138">Вы также можете обрабатывать ограничение скорости с помощью каждого бота в потоке.</span><span class="sxs-lookup"><span data-stu-id="c1258-138">You can also handle rate limit using the per bot per thread limit.</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="c1258-139">Ограничение на один бот на поток</span><span class="sxs-lookup"><span data-stu-id="c1258-139">Per bot per thread limit</span></span>

<span data-ttu-id="c1258-140">Ограничение для каждого бота в потоке управляет трафиком, который может создаваться ботом в одном разговоре.</span><span class="sxs-lookup"><span data-stu-id="c1258-140">The per bot per thread limit controls the traffic that a bot is allowed to generate in a single conversation.</span></span> <span data-ttu-id="c1258-141">Беседа 1:1 между ботом и пользователем, групповым чатом или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="c1258-141">A conversation is 1:1 between bot and user, a group chat, or a channel in a team.</span></span> <span data-ttu-id="c1258-142">Таким образом, если приложение отправляет по одному сообщению бота каждому пользователю, ограничение потока не затормажается.</span><span class="sxs-lookup"><span data-stu-id="c1258-142">So, if the application sends one bot message to each user, the thread limit does not throttle.</span></span>

>[!NOTE]
> * <span data-ttu-id="c1258-143">Ограничение потока в 3600 секунд и 1800 операций применяется только в том случае, если несколько сообщений бота отправляются одному пользователю.</span><span class="sxs-lookup"><span data-stu-id="c1258-143">The thread limit of 3600 seconds and 1800 operations applies only if multiple bot messages are sent to a single user.</span></span> 
> * <span data-ttu-id="c1258-144">Глобальное ограничение для каждого клиента — 30 запросов в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="c1258-144">The global limit per app per tenant is 30 Requests Per Second (RPS).</span></span> <span data-ttu-id="c1258-145">Таким образом, общее число сообщений бота в секунду не должно пересекать ограничение потока.</span><span class="sxs-lookup"><span data-stu-id="c1258-145">Hence, the total number of bot messages per second must not cross the thread limit.</span></span>
> * <span data-ttu-id="c1258-146">Разделение сообщений на уровне службы приводит к большему, чем ожидалось, RPS.</span><span class="sxs-lookup"><span data-stu-id="c1258-146">Message splitting at the service level results in higher than expected RPS.</span></span> <span data-ttu-id="c1258-147">Если вас беспокоит приближение к ограничениям, необходимо реализовать стратегию [обратного выхода.](#backoff-example)</span><span class="sxs-lookup"><span data-stu-id="c1258-147">If you are concerned about approaching the limits, you must implement the [backoff strategy](#backoff-example).</span></span> <span data-ttu-id="c1258-148">Значения, предоставляемые в этом разделе, являются только для оценки.</span><span class="sxs-lookup"><span data-stu-id="c1258-148">The values provided in this section are for estimation only.</span></span>

<span data-ttu-id="c1258-149">В следующей таблице содержится ограничение для каждого бота на поток:</span><span class="sxs-lookup"><span data-stu-id="c1258-149">The following table provides the per bot per thread limits:</span></span>

| <span data-ttu-id="c1258-150">Сценарий</span><span class="sxs-lookup"><span data-stu-id="c1258-150">Scenario</span></span> | <span data-ttu-id="c1258-151">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="c1258-151">Time period in seconds</span></span> | <span data-ttu-id="c1258-152">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="c1258-152">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1258-153">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-153">Send to conversation</span></span> | <span data-ttu-id="c1258-154">1</span><span class="sxs-lookup"><span data-stu-id="c1258-154">1</span></span> | <span data-ttu-id="c1258-155">7 </span><span class="sxs-lookup"><span data-stu-id="c1258-155">7</span></span> |
| <span data-ttu-id="c1258-156">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-156">Send to conversation</span></span> | <span data-ttu-id="c1258-157">2</span><span class="sxs-lookup"><span data-stu-id="c1258-157">2</span></span> | <span data-ttu-id="c1258-158">8 </span><span class="sxs-lookup"><span data-stu-id="c1258-158">8</span></span> |
| <span data-ttu-id="c1258-159">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-159">Send to conversation</span></span> | <span data-ttu-id="c1258-160">30</span><span class="sxs-lookup"><span data-stu-id="c1258-160">30</span></span> | <span data-ttu-id="c1258-161">60</span><span class="sxs-lookup"><span data-stu-id="c1258-161">60</span></span> |
| <span data-ttu-id="c1258-162">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-162">Send to conversation</span></span> | <span data-ttu-id="c1258-163">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-163">3600</span></span> | <span data-ttu-id="c1258-164">1800</span><span class="sxs-lookup"><span data-stu-id="c1258-164">1800</span></span> |
| <span data-ttu-id="c1258-165">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-165">Create conversation</span></span> | <span data-ttu-id="c1258-166">1</span><span class="sxs-lookup"><span data-stu-id="c1258-166">1</span></span> | <span data-ttu-id="c1258-167">7 </span><span class="sxs-lookup"><span data-stu-id="c1258-167">7</span></span> |
| <span data-ttu-id="c1258-168">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-168">Create conversation</span></span> | <span data-ttu-id="c1258-169">2</span><span class="sxs-lookup"><span data-stu-id="c1258-169">2</span></span> | <span data-ttu-id="c1258-170">8 </span><span class="sxs-lookup"><span data-stu-id="c1258-170">8</span></span> |
| <span data-ttu-id="c1258-171">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-171">Create conversation</span></span> | <span data-ttu-id="c1258-172">30</span><span class="sxs-lookup"><span data-stu-id="c1258-172">30</span></span> | <span data-ttu-id="c1258-173">60</span><span class="sxs-lookup"><span data-stu-id="c1258-173">60</span></span> |
| <span data-ttu-id="c1258-174">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-174">Create conversation</span></span> | <span data-ttu-id="c1258-175">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-175">3600</span></span> | <span data-ttu-id="c1258-176">1800</span><span class="sxs-lookup"><span data-stu-id="c1258-176">1800</span></span> |
| <span data-ttu-id="c1258-177">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-177">Get conversation members</span></span>| <span data-ttu-id="c1258-178">1</span><span class="sxs-lookup"><span data-stu-id="c1258-178">1</span></span> | <span data-ttu-id="c1258-179">14 </span><span class="sxs-lookup"><span data-stu-id="c1258-179">14</span></span> |
| <span data-ttu-id="c1258-180">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-180">Get conversation members</span></span>| <span data-ttu-id="c1258-181">2</span><span class="sxs-lookup"><span data-stu-id="c1258-181">2</span></span> | <span data-ttu-id="c1258-182">16 </span><span class="sxs-lookup"><span data-stu-id="c1258-182">16</span></span> |
| <span data-ttu-id="c1258-183">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-183">Get conversation members</span></span>| <span data-ttu-id="c1258-184">30</span><span class="sxs-lookup"><span data-stu-id="c1258-184">30</span></span> | <span data-ttu-id="c1258-185">120</span><span class="sxs-lookup"><span data-stu-id="c1258-185">120</span></span> |
| <span data-ttu-id="c1258-186">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-186">Get conversation members</span></span>| <span data-ttu-id="c1258-187">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-187">3600</span></span> | <span data-ttu-id="c1258-188">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-188">3600</span></span> |
| <span data-ttu-id="c1258-189">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-189">Get conversations</span></span> | <span data-ttu-id="c1258-190">1</span><span class="sxs-lookup"><span data-stu-id="c1258-190">1</span></span> | <span data-ttu-id="c1258-191">14 </span><span class="sxs-lookup"><span data-stu-id="c1258-191">14</span></span> |
| <span data-ttu-id="c1258-192">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-192">Get conversations</span></span> | <span data-ttu-id="c1258-193">2</span><span class="sxs-lookup"><span data-stu-id="c1258-193">2</span></span> | <span data-ttu-id="c1258-194">16 </span><span class="sxs-lookup"><span data-stu-id="c1258-194">16</span></span> |
| <span data-ttu-id="c1258-195">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-195">Get conversations</span></span> | <span data-ttu-id="c1258-196">30</span><span class="sxs-lookup"><span data-stu-id="c1258-196">30</span></span> | <span data-ttu-id="c1258-197">120</span><span class="sxs-lookup"><span data-stu-id="c1258-197">120</span></span> |
| <span data-ttu-id="c1258-198">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-198">Get conversations</span></span> | <span data-ttu-id="c1258-199">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-199">3600</span></span> | <span data-ttu-id="c1258-200">3600</span><span class="sxs-lookup"><span data-stu-id="c1258-200">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="c1258-201">Предыдущие версии и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API отстают.</span><span class="sxs-lookup"><span data-stu-id="c1258-201">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="c1258-202">Они отлаговываются до пяти запросов в минуту и возвращают не более 10 000 участников на каждую команду.</span><span class="sxs-lookup"><span data-stu-id="c1258-202">They are throttled to five requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="c1258-203">Чтобы обновить SDK bot Framework и код для использования последних конечных точек API с paginated, см. в рубрике Изменения API bot для членов команды и [чата.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="c1258-203">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="c1258-204">Вы также можете обрабатывать ограничение скорости с помощью ограничения потока для всех ботов.</span><span class="sxs-lookup"><span data-stu-id="c1258-204">You can also handle rate limit using the per thread limit for all bots.</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="c1258-205">Ограничение потока для всех ботов</span><span class="sxs-lookup"><span data-stu-id="c1258-205">Per thread limit for all bots</span></span>

<span data-ttu-id="c1258-206">Ограничение потока для всех ботов контролирует трафик, который всем ботам разрешено создавать в одном диалоге.</span><span class="sxs-lookup"><span data-stu-id="c1258-206">The per thread limit for all bots controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="c1258-207">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="c1258-207">A conversation here is 1:1 between bot and user, a group chat, or a channel in a team.</span></span>

<span data-ttu-id="c1258-208">В следующей таблице содержится ограничение потока для всех ботов:</span><span class="sxs-lookup"><span data-stu-id="c1258-208">The following table provides the per thread limit for all bots:</span></span>

| <span data-ttu-id="c1258-209">Сценарий</span><span class="sxs-lookup"><span data-stu-id="c1258-209">Scenario</span></span> | <span data-ttu-id="c1258-210">Период времени в секундах</span><span class="sxs-lookup"><span data-stu-id="c1258-210">Time period in seconds</span></span> | <span data-ttu-id="c1258-211">Максимально допустимые операции</span><span class="sxs-lookup"><span data-stu-id="c1258-211">Maximum allowed operations</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c1258-212">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-212">Send to conversation</span></span> | <span data-ttu-id="c1258-213">1</span><span class="sxs-lookup"><span data-stu-id="c1258-213">1</span></span> | <span data-ttu-id="c1258-214">14 </span><span class="sxs-lookup"><span data-stu-id="c1258-214">14</span></span> |
| <span data-ttu-id="c1258-215">Отправка в беседу</span><span class="sxs-lookup"><span data-stu-id="c1258-215">Send to conversation</span></span> | <span data-ttu-id="c1258-216">2</span><span class="sxs-lookup"><span data-stu-id="c1258-216">2</span></span> | <span data-ttu-id="c1258-217">16 </span><span class="sxs-lookup"><span data-stu-id="c1258-217">16</span></span> |
| <span data-ttu-id="c1258-218">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-218">Create conversation</span></span> | <span data-ttu-id="c1258-219">1</span><span class="sxs-lookup"><span data-stu-id="c1258-219">1</span></span> | <span data-ttu-id="c1258-220">14 </span><span class="sxs-lookup"><span data-stu-id="c1258-220">14</span></span> |
| <span data-ttu-id="c1258-221">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-221">Create conversation</span></span> | <span data-ttu-id="c1258-222">2</span><span class="sxs-lookup"><span data-stu-id="c1258-222">2</span></span> | <span data-ttu-id="c1258-223">16 </span><span class="sxs-lookup"><span data-stu-id="c1258-223">16</span></span> |
| <span data-ttu-id="c1258-224">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-224">Create conversation</span></span>| <span data-ttu-id="c1258-225">1</span><span class="sxs-lookup"><span data-stu-id="c1258-225">1</span></span> | <span data-ttu-id="c1258-226">14 </span><span class="sxs-lookup"><span data-stu-id="c1258-226">14</span></span> |
| <span data-ttu-id="c1258-227">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-227">Create conversation</span></span>| <span data-ttu-id="c1258-228">2</span><span class="sxs-lookup"><span data-stu-id="c1258-228">2</span></span> | <span data-ttu-id="c1258-229">16 </span><span class="sxs-lookup"><span data-stu-id="c1258-229">16</span></span> |
| <span data-ttu-id="c1258-230">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-230">Get conversation members</span></span>| <span data-ttu-id="c1258-231">1</span><span class="sxs-lookup"><span data-stu-id="c1258-231">1</span></span> | <span data-ttu-id="c1258-232">28</span><span class="sxs-lookup"><span data-stu-id="c1258-232">28</span></span> |
| <span data-ttu-id="c1258-233">Получить участников беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-233">Get conversation members</span></span>| <span data-ttu-id="c1258-234">2</span><span class="sxs-lookup"><span data-stu-id="c1258-234">2</span></span> | <span data-ttu-id="c1258-235">32</span><span class="sxs-lookup"><span data-stu-id="c1258-235">32</span></span> |
| <span data-ttu-id="c1258-236">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-236">Get conversations</span></span> | <span data-ttu-id="c1258-237">1</span><span class="sxs-lookup"><span data-stu-id="c1258-237">1</span></span> | <span data-ttu-id="c1258-238">28</span><span class="sxs-lookup"><span data-stu-id="c1258-238">28</span></span> |
| <span data-ttu-id="c1258-239">Получать беседы</span><span class="sxs-lookup"><span data-stu-id="c1258-239">Get conversations</span></span> | <span data-ttu-id="c1258-240">2</span><span class="sxs-lookup"><span data-stu-id="c1258-240">2</span></span> | <span data-ttu-id="c1258-241">32</span><span class="sxs-lookup"><span data-stu-id="c1258-241">32</span></span> |

## <a name="next-step"></a><span data-ttu-id="c1258-242">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="c1258-242">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c1258-243">Боты для звонков и собраний</span><span class="sxs-lookup"><span data-stu-id="c1258-243">Calls and meetings bots</span></span>](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)

