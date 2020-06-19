---
title: Ограничение скорости
description: Ограничения скорости и рекомендации в Microsoft Teams
keywords: ограничения скорости Боты Teams
ms.openlocfilehash: 9b244053d42aaddaf48c798e401438b614b0e1bd
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2020
ms.locfileid: "44801500"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="33b59-104">Оптимизация ограничения скорости и рекомендаций в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="33b59-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="33b59-105">Как правило, ваше приложение должно ограничивать количество сообщений, отправляемых в отдельный чат или беседу по каналу.</span><span class="sxs-lookup"><span data-stu-id="33b59-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="33b59-106">Это обеспечивает оптимальный интерфейс для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="33b59-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="33b59-107">Чтобы защитить Microsoft Teams и ее пользователей, API-интерфейсам Bot могут ограничивать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="33b59-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="33b59-108">Приложения, которые переходят по этому ограничению, получают `HTTP 429 Too Many Requests` состояние ошибки.</span><span class="sxs-lookup"><span data-stu-id="33b59-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="33b59-109">Все запросы распространяются на одну и ту же политику ограничения скорости, включая отправку сообщений, перечисление каналов и извлечение списков.</span><span class="sxs-lookup"><span data-stu-id="33b59-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="33b59-110">Так как точные значения пределов скорости могут измениться, мы рекомендуем, чтобы приложение выполняло соответствующее поведение при возврате API `HTTP 429 Too Many Requests` .</span><span class="sxs-lookup"><span data-stu-id="33b59-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="33b59-111">Пределы скорости обработки</span><span class="sxs-lookup"><span data-stu-id="33b59-111">Handling rate limits</span></span>

<span data-ttu-id="33b59-112">При выполнении операции с пакетом SDK построителя построителя можно обработать `Microsoft.Rest.HttpOperationException` код состояния и проверить его.</span><span class="sxs-lookup"><span data-stu-id="33b59-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="33b59-113">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="33b59-113">Best practices</span></span>

<span data-ttu-id="33b59-114">В общем случае следует принять простые меры предосторожности, чтобы не получать `HTTP 429` ответы.</span><span class="sxs-lookup"><span data-stu-id="33b59-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="33b59-115">Например, не выполняйте несколько запросов к одной беседе лично или каналу.</span><span class="sxs-lookup"><span data-stu-id="33b59-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="33b59-116">Вместо этого рассмотрите возможности пакетной обработки запросов API.</span><span class="sxs-lookup"><span data-stu-id="33b59-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="33b59-117">Использование экспоненциального отработки с случайной колебанием является рекомендуемым способом обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="33b59-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="33b59-118">Это гарантирует, что при повторе нескольких запросов не возникать конфликты.</span><span class="sxs-lookup"><span data-stu-id="33b59-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="33b59-119">Пример: Обнаружение временных исключений</span><span class="sxs-lookup"><span data-stu-id="33b59-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="33b59-120">Ниже приведен пример с использованием экспоненциального переработки через временный блок обработки сбоев.</span><span class="sxs-lookup"><span data-stu-id="33b59-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="33b59-121">Вы можете выполнять операции перегрузки и повторных попыток, используя [временную обработку сбоев](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="33b59-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="33b59-122">Рекомендации по получению и установке пакета NuGet приведены в статье [Добавление временного блока обработки сбоев в решение](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="33b59-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="33b59-123">*См. также* [временная обработка сбоев](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="33b59-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="33b59-124">Пример: отход</span><span class="sxs-lookup"><span data-stu-id="33b59-124">Example: backoff</span></span>

<span data-ttu-id="33b59-125">В дополнение к определению пределов скорости, можно также выполнить экспоненциальное переопределение.</span><span class="sxs-lookup"><span data-stu-id="33b59-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="33b59-126">Выполнение метода также можно выполнить `System.Action` с помощью политики повторных попыток, описанной выше.</span><span class="sxs-lookup"><span data-stu-id="33b59-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="33b59-127">Указанная библиотека также позволяет указать фиксированный интервал или линейный механизм отрезков.</span><span class="sxs-lookup"><span data-stu-id="33b59-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="33b59-128">Рекомендуется хранить значение и стратегию в файле конфигурации для точной настройки и корректировки значений во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="33b59-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="33b59-129">Дополнительную информацию вы узнаете в этом удобном руководстве по различным шаблонам повторных попыток: [шаблон повторов](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="33b59-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="33b59-130">Предельное число потоков для каждой ленты</span><span class="sxs-lookup"><span data-stu-id="33b59-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="33b59-131">Разбиение сообщений на уровне службы приведет к превышению ожидаемых запросов в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="33b59-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="33b59-132">Если вы беспокоитесь об этих пределах, необходимо реализовать стратегию отработки отказа, описанную выше.</span><span class="sxs-lookup"><span data-stu-id="33b59-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="33b59-133">Указанные ниже значения предназначены только для оценки.</span><span class="sxs-lookup"><span data-stu-id="33b59-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="33b59-134">Это предельное значение управляет трафиком, который может создаваться с помощью Bot в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="33b59-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="33b59-135">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="33b59-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="33b59-136">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="33b59-136">**Scenario**</span></span> | <span data-ttu-id="33b59-137">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="33b59-137">**Time-period (sec)**</span></span> | <span data-ttu-id="33b59-138">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="33b59-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33b59-139">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-139">Send to Conversation</span></span> | <span data-ttu-id="33b59-140">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-140">1</span></span> | <span data-ttu-id="33b59-141">7 </span><span class="sxs-lookup"><span data-stu-id="33b59-141">7</span></span> |
| <span data-ttu-id="33b59-142">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-142">Send to Conversation</span></span> | <span data-ttu-id="33b59-143">2</span><span class="sxs-lookup"><span data-stu-id="33b59-143">2</span></span> | <span data-ttu-id="33b59-144">8 </span><span class="sxs-lookup"><span data-stu-id="33b59-144">8</span></span> |
| <span data-ttu-id="33b59-145">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-145">Send to Conversation</span></span> | <span data-ttu-id="33b59-146">более</span><span class="sxs-lookup"><span data-stu-id="33b59-146">30</span></span> | <span data-ttu-id="33b59-147">60</span><span class="sxs-lookup"><span data-stu-id="33b59-147">60</span></span> |
| <span data-ttu-id="33b59-148">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-148">Send to Conversation</span></span> | <span data-ttu-id="33b59-149">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-149">3600</span></span> | <span data-ttu-id="33b59-150">1800</span><span class="sxs-lookup"><span data-stu-id="33b59-150">1800</span></span> |
| <span data-ttu-id="33b59-151">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-151">Create Conversation</span></span> | <span data-ttu-id="33b59-152">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-152">1</span></span> | <span data-ttu-id="33b59-153">7 </span><span class="sxs-lookup"><span data-stu-id="33b59-153">7</span></span> |
| <span data-ttu-id="33b59-154">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-154">Create Conversation</span></span> | <span data-ttu-id="33b59-155">2</span><span class="sxs-lookup"><span data-stu-id="33b59-155">2</span></span> | <span data-ttu-id="33b59-156">8 </span><span class="sxs-lookup"><span data-stu-id="33b59-156">8</span></span> |
| <span data-ttu-id="33b59-157">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-157">Create Conversation</span></span> | <span data-ttu-id="33b59-158">более</span><span class="sxs-lookup"><span data-stu-id="33b59-158">30</span></span> | <span data-ttu-id="33b59-159">60</span><span class="sxs-lookup"><span data-stu-id="33b59-159">60</span></span> |
| <span data-ttu-id="33b59-160">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-160">Create Conversation</span></span> | <span data-ttu-id="33b59-161">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-161">3600</span></span> | <span data-ttu-id="33b59-162">1800</span><span class="sxs-lookup"><span data-stu-id="33b59-162">1800</span></span> |
| <span data-ttu-id="33b59-163">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-163">Get Conversation Members</span></span>| <span data-ttu-id="33b59-164">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-164">1</span></span> | <span data-ttu-id="33b59-165">14 </span><span class="sxs-lookup"><span data-stu-id="33b59-165">14</span></span> |
| <span data-ttu-id="33b59-166">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-166">Get Conversation Members</span></span>| <span data-ttu-id="33b59-167">2</span><span class="sxs-lookup"><span data-stu-id="33b59-167">2</span></span> | <span data-ttu-id="33b59-168">16 </span><span class="sxs-lookup"><span data-stu-id="33b59-168">16</span></span> |
| <span data-ttu-id="33b59-169">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-169">Get Conversation Members</span></span>| <span data-ttu-id="33b59-170">более</span><span class="sxs-lookup"><span data-stu-id="33b59-170">30</span></span> | <span data-ttu-id="33b59-171">120</span><span class="sxs-lookup"><span data-stu-id="33b59-171">120</span></span> |
| <span data-ttu-id="33b59-172">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-172">Get Conversation Members</span></span>| <span data-ttu-id="33b59-173">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-173">3600</span></span> | <span data-ttu-id="33b59-174">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-174">3600</span></span> |
| <span data-ttu-id="33b59-175">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-175">Get Conversations</span></span> | <span data-ttu-id="33b59-176">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-176">1</span></span> | <span data-ttu-id="33b59-177">14 </span><span class="sxs-lookup"><span data-stu-id="33b59-177">14</span></span> |
| <span data-ttu-id="33b59-178">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-178">Get Conversations</span></span> | <span data-ttu-id="33b59-179">2</span><span class="sxs-lookup"><span data-stu-id="33b59-179">2</span></span> | <span data-ttu-id="33b59-180">16 </span><span class="sxs-lookup"><span data-stu-id="33b59-180">16</span></span> |
| <span data-ttu-id="33b59-181">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-181">Get Conversations</span></span> | <span data-ttu-id="33b59-182">более</span><span class="sxs-lookup"><span data-stu-id="33b59-182">30</span></span> | <span data-ttu-id="33b59-183">120</span><span class="sxs-lookup"><span data-stu-id="33b59-183">120</span></span> |
| <span data-ttu-id="33b59-184">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-184">Get Conversations</span></span> | <span data-ttu-id="33b59-185">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-185">3600</span></span> | <span data-ttu-id="33b59-186">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-186">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="33b59-187">Предельное количество потоков для всех Боты</span><span class="sxs-lookup"><span data-stu-id="33b59-187">Per thread limit for all bots</span></span>

<span data-ttu-id="33b59-188">Это значение управляет трафиком, в течение которого все боты могут создаваться в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="33b59-188">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="33b59-189">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="33b59-189">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="33b59-190">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="33b59-190">**Scenario**</span></span> | <span data-ttu-id="33b59-191">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="33b59-191">**Time-period (sec)**</span></span> | <span data-ttu-id="33b59-192">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="33b59-192">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33b59-193">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-193">Send to Conversation</span></span> | <span data-ttu-id="33b59-194">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-194">1</span></span> | <span data-ttu-id="33b59-195">14 </span><span class="sxs-lookup"><span data-stu-id="33b59-195">14</span></span> |
| <span data-ttu-id="33b59-196">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="33b59-196">Send to Conversation</span></span> | <span data-ttu-id="33b59-197">2</span><span class="sxs-lookup"><span data-stu-id="33b59-197">2</span></span> | <span data-ttu-id="33b59-198">16 </span><span class="sxs-lookup"><span data-stu-id="33b59-198">16</span></span> |
| <span data-ttu-id="33b59-199">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-199">Create Conversation</span></span> | <span data-ttu-id="33b59-200">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-200">1</span></span> | <span data-ttu-id="33b59-201">14 </span><span class="sxs-lookup"><span data-stu-id="33b59-201">14</span></span> |
| <span data-ttu-id="33b59-202">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-202">Create Conversation</span></span> | <span data-ttu-id="33b59-203">2</span><span class="sxs-lookup"><span data-stu-id="33b59-203">2</span></span> | <span data-ttu-id="33b59-204">16 </span><span class="sxs-lookup"><span data-stu-id="33b59-204">16</span></span> |
| <span data-ttu-id="33b59-205">креатеконверсатион</span><span class="sxs-lookup"><span data-stu-id="33b59-205">CreateConversation</span></span>| <span data-ttu-id="33b59-206">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-206">1</span></span> | <span data-ttu-id="33b59-207">14 </span><span class="sxs-lookup"><span data-stu-id="33b59-207">14</span></span> |
| <span data-ttu-id="33b59-208">креатеконверсатион</span><span class="sxs-lookup"><span data-stu-id="33b59-208">CreateConversation</span></span>| <span data-ttu-id="33b59-209">2</span><span class="sxs-lookup"><span data-stu-id="33b59-209">2</span></span> | <span data-ttu-id="33b59-210">16 </span><span class="sxs-lookup"><span data-stu-id="33b59-210">16</span></span> |
| <span data-ttu-id="33b59-211">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-211">Get Conversation Members</span></span>| <span data-ttu-id="33b59-212">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-212">1</span></span> | <span data-ttu-id="33b59-213">8</span><span class="sxs-lookup"><span data-stu-id="33b59-213">28</span></span> |
| <span data-ttu-id="33b59-214">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="33b59-214">Get Conversation Members</span></span>| <span data-ttu-id="33b59-215">2</span><span class="sxs-lookup"><span data-stu-id="33b59-215">2</span></span> | <span data-ttu-id="33b59-216">32</span><span class="sxs-lookup"><span data-stu-id="33b59-216">32</span></span> |
| <span data-ttu-id="33b59-217">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-217">Get Conversations</span></span> | <span data-ttu-id="33b59-218">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-218">1</span></span> | <span data-ttu-id="33b59-219">8</span><span class="sxs-lookup"><span data-stu-id="33b59-219">28</span></span> |
| <span data-ttu-id="33b59-220">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="33b59-220">Get Conversations</span></span> | <span data-ttu-id="33b59-221">2</span><span class="sxs-lookup"><span data-stu-id="33b59-221">2</span></span> | <span data-ttu-id="33b59-222">32</span><span class="sxs-lookup"><span data-stu-id="33b59-222">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="33b59-223">Предельное значение для ленты в центре обработки данных</span><span class="sxs-lookup"><span data-stu-id="33b59-223">Bot per data center limit</span></span>

<span data-ttu-id="33b59-224">Это значение управляет трафиком, который может создаваться с помощью Bot, во всех потоках в центре обработки данных (для нескольких клиентов).</span><span class="sxs-lookup"><span data-stu-id="33b59-224">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="33b59-225">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="33b59-225">**Time-period (sec)**</span></span> | <span data-ttu-id="33b59-226">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="33b59-226">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="33b59-227">1 </span><span class="sxs-lookup"><span data-stu-id="33b59-227">1</span></span> | <span data-ttu-id="33b59-228">двадцать</span><span class="sxs-lookup"><span data-stu-id="33b59-228">20</span></span> |
| <span data-ttu-id="33b59-229">1800</span><span class="sxs-lookup"><span data-stu-id="33b59-229">1800</span></span> | <span data-ttu-id="33b59-230">8000</span><span class="sxs-lookup"><span data-stu-id="33b59-230">8000</span></span> |
| <span data-ttu-id="33b59-231">3600</span><span class="sxs-lookup"><span data-stu-id="33b59-231">3600</span></span> | <span data-ttu-id="33b59-232">15000</span><span class="sxs-lookup"><span data-stu-id="33b59-232">15000</span></span> |
