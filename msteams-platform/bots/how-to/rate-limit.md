---
title: Ограничение скорости
description: Ограничения скорости и рекомендации в Microsoft Teams
keywords: ограничения скорости Боты Teams
ms.openlocfilehash: 145f65a7e17b833e11631dfc219d9f5732f43bc6
ms.sourcegitcommit: 6c692734a382865531a83b9ebd6f604212f484fc
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/02/2020
ms.locfileid: "42371767"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="d51c1-104">Оптимизация ограничения скорости и рекомендаций в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="d51c1-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="d51c1-105">Как правило, ваше приложение должно ограничивать количество сообщений, отправляемых в отдельный чат или беседу по каналу.</span><span class="sxs-lookup"><span data-stu-id="d51c1-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="d51c1-106">Это обеспечивает оптимальный интерфейс для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="d51c1-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="d51c1-107">Чтобы защитить Microsoft Teams и ее пользователей, API-интерфейсам Bot могут ограничивать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="d51c1-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="d51c1-108">Приложения, которые переходят по этому ограничению, получают состояние `HTTP 429 Too Many Requests` ошибки.</span><span class="sxs-lookup"><span data-stu-id="d51c1-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="d51c1-109">Все запросы распространяются на одну и ту же политику ограничения скорости, включая отправку сообщений, перечисление каналов и извлечение списков.</span><span class="sxs-lookup"><span data-stu-id="d51c1-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="d51c1-110">Так как точные значения пределов скорости могут измениться, мы рекомендуем, чтобы приложение выполняло соответствующее поведение при возврате `HTTP 429 Too Many Requests`API.</span><span class="sxs-lookup"><span data-stu-id="d51c1-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="d51c1-111">Пределы скорости обработки</span><span class="sxs-lookup"><span data-stu-id="d51c1-111">Handling rate limits</span></span>

<span data-ttu-id="d51c1-112">При выполнении операции с пакетом SDK построителя построителя `Microsoft.Rest.HttpOperationException` можно обработать код состояния и проверить его.</span><span class="sxs-lookup"><span data-stu-id="d51c1-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="d51c1-113">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="d51c1-113">Best practices</span></span>

<span data-ttu-id="d51c1-114">В общем случае следует принять простые меры предосторожности, чтобы не `HTTP 429` получать ответы.</span><span class="sxs-lookup"><span data-stu-id="d51c1-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="d51c1-115">Например, не выполняйте несколько запросов к одной беседе лично или каналу.</span><span class="sxs-lookup"><span data-stu-id="d51c1-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="d51c1-116">Вместо этого рассмотрите возможности пакетной обработки запросов API.</span><span class="sxs-lookup"><span data-stu-id="d51c1-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="d51c1-117">Использование экспоненциального отработки с случайной колебанием является рекомендуемым способом обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="d51c1-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="d51c1-118">Это гарантирует, что при повторе нескольких запросов не возникать конфликты.</span><span class="sxs-lookup"><span data-stu-id="d51c1-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="d51c1-119">Пример: Обнаружение временных исключений</span><span class="sxs-lookup"><span data-stu-id="d51c1-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="d51c1-120">Ниже приведен пример с использованием экспоненциального переработки через временный блок обработки сбоев.</span><span class="sxs-lookup"><span data-stu-id="d51c1-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="d51c1-121">Вы можете выполнять операции перегрузки и повторных попыток, используя [временную обработку сбоев](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span><span class="sxs-lookup"><span data-stu-id="d51c1-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="d51c1-122">Рекомендации по получению и установке пакета NuGet приведены в статье [Добавление временного блока обработки сбоев в решение](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN).</span><span class="sxs-lookup"><span data-stu-id="d51c1-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="d51c1-123">*См. также* [временная обработка сбоев](/azure/architecture/best-practices/transient-faults).</span><span class="sxs-lookup"><span data-stu-id="d51c1-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="d51c1-124">Пример: отход</span><span class="sxs-lookup"><span data-stu-id="d51c1-124">Example: backoff</span></span>

<span data-ttu-id="d51c1-125">В дополнение к определению пределов скорости, можно также выполнить экспоненциальное переопределение.</span><span class="sxs-lookup"><span data-stu-id="d51c1-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="d51c1-126">Выполнение `System.Action` метода также можно выполнить с помощью политики повторных попыток, описанной выше.</span><span class="sxs-lookup"><span data-stu-id="d51c1-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="d51c1-127">Указанная библиотека также позволяет указать фиксированный интервал или линейный механизм отрезков.</span><span class="sxs-lookup"><span data-stu-id="d51c1-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="d51c1-128">Рекомендуется хранить значение и стратегию в файле конфигурации для точной настройки и корректировки значений во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="d51c1-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="d51c1-129">Дополнительную информацию вы узнаете в этом удобном руководстве по различным шаблонам повторных попыток: [шаблон повторов](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="d51c1-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="d51c1-130">Предельное число потоков для каждой ленты</span><span class="sxs-lookup"><span data-stu-id="d51c1-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="d51c1-131">Разбиение сообщений на уровне службы приведет к превышению ожидаемых запросов в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="d51c1-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="d51c1-132">Если вы беспокоитесь об этих пределах, необходимо реализовать стратегию отработки отказа, описанную выше.</span><span class="sxs-lookup"><span data-stu-id="d51c1-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="d51c1-133">Указанные ниже значения предназначены только для оценки.</span><span class="sxs-lookup"><span data-stu-id="d51c1-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="d51c1-134">Это предельное значение управляет трафиком, который может создаваться с помощью Bot в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="d51c1-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="d51c1-135">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="d51c1-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="d51c1-136">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="d51c1-136">**Scenario**</span></span> | <span data-ttu-id="d51c1-137">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="d51c1-137">**Time-period (sec)**</span></span> | <span data-ttu-id="d51c1-138">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="d51c1-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
|| <span data-ttu-id="d51c1-139">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-139">1</span></span> | <span data-ttu-id="d51c1-140">см</span><span class="sxs-lookup"><span data-stu-id="d51c1-140">7</span></span> |
| <span data-ttu-id="d51c1-141">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="d51c1-141">Send to Conversation</span></span> | <span data-ttu-id="d51c1-142">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-142">2</span></span> | <span data-ttu-id="d51c1-143">8,5</span><span class="sxs-lookup"><span data-stu-id="d51c1-143">8</span></span> |
| <span data-ttu-id="d51c1-144">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="d51c1-144">Send to Conversation</span></span> | <span data-ttu-id="d51c1-145">более</span><span class="sxs-lookup"><span data-stu-id="d51c1-145">30</span></span> | <span data-ttu-id="d51c1-146">60</span><span class="sxs-lookup"><span data-stu-id="d51c1-146">60</span></span> |
| <span data-ttu-id="d51c1-147">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="d51c1-147">Send to Conversation</span></span> | <span data-ttu-id="d51c1-148">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-148">3600</span></span> | <span data-ttu-id="d51c1-149">1800</span><span class="sxs-lookup"><span data-stu-id="d51c1-149">1800</span></span> |
| <span data-ttu-id="d51c1-150">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-150">Create Conversation</span></span> | <span data-ttu-id="d51c1-151">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-151">1</span></span> | <span data-ttu-id="d51c1-152">см</span><span class="sxs-lookup"><span data-stu-id="d51c1-152">7</span></span> |
| <span data-ttu-id="d51c1-153">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-153">Create Conversation</span></span> | <span data-ttu-id="d51c1-154">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-154">2</span></span> | <span data-ttu-id="d51c1-155">8,5</span><span class="sxs-lookup"><span data-stu-id="d51c1-155">8</span></span> |
| <span data-ttu-id="d51c1-156">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-156">Create Conversation</span></span> | <span data-ttu-id="d51c1-157">более</span><span class="sxs-lookup"><span data-stu-id="d51c1-157">30</span></span> | <span data-ttu-id="d51c1-158">60</span><span class="sxs-lookup"><span data-stu-id="d51c1-158">60</span></span> |
| <span data-ttu-id="d51c1-159">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-159">Create Conversation</span></span> | <span data-ttu-id="d51c1-160">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-160">3600</span></span> | <span data-ttu-id="d51c1-161">1800</span><span class="sxs-lookup"><span data-stu-id="d51c1-161">1800</span></span> |
| <span data-ttu-id="d51c1-162">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-162">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-163">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-163">1</span></span> | <span data-ttu-id="d51c1-164">14 </span><span class="sxs-lookup"><span data-stu-id="d51c1-164">14</span></span> |
| <span data-ttu-id="d51c1-165">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-165">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-166">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-166">2</span></span> | <span data-ttu-id="d51c1-167">16 </span><span class="sxs-lookup"><span data-stu-id="d51c1-167">16</span></span> |
| <span data-ttu-id="d51c1-168">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-168">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-169">более</span><span class="sxs-lookup"><span data-stu-id="d51c1-169">30</span></span> | <span data-ttu-id="d51c1-170">120</span><span class="sxs-lookup"><span data-stu-id="d51c1-170">120</span></span> |
| <span data-ttu-id="d51c1-171">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-171">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-172">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-172">3600</span></span> | <span data-ttu-id="d51c1-173">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-173">3600</span></span> |
| <span data-ttu-id="d51c1-174">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-174">Get Conversations</span></span> | <span data-ttu-id="d51c1-175">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-175">1</span></span> | <span data-ttu-id="d51c1-176">14 </span><span class="sxs-lookup"><span data-stu-id="d51c1-176">14</span></span> |
| <span data-ttu-id="d51c1-177">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-177">Get Conversations</span></span> | <span data-ttu-id="d51c1-178">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-178">2</span></span> | <span data-ttu-id="d51c1-179">16 </span><span class="sxs-lookup"><span data-stu-id="d51c1-179">16</span></span> |
| <span data-ttu-id="d51c1-180">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-180">Get Conversations</span></span> | <span data-ttu-id="d51c1-181">более</span><span class="sxs-lookup"><span data-stu-id="d51c1-181">30</span></span> | <span data-ttu-id="d51c1-182">120</span><span class="sxs-lookup"><span data-stu-id="d51c1-182">120</span></span> |
| <span data-ttu-id="d51c1-183">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-183">Get Conversations</span></span> | <span data-ttu-id="d51c1-184">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-184">3600</span></span> | <span data-ttu-id="d51c1-185">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-185">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="d51c1-186">Предельное количество потоков для всех Боты</span><span class="sxs-lookup"><span data-stu-id="d51c1-186">Per thread limit for all bots</span></span>

<span data-ttu-id="d51c1-187">Это значение управляет трафиком, в течение которого все боты могут создаваться в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="d51c1-187">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="d51c1-188">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="d51c1-188">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="d51c1-189">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="d51c1-189">**Scenario**</span></span> | <span data-ttu-id="d51c1-190">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="d51c1-190">**Time-period (sec)**</span></span> | <span data-ttu-id="d51c1-191">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="d51c1-191">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d51c1-192">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="d51c1-192">Send to Conversation</span></span> | <span data-ttu-id="d51c1-193">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-193">1</span></span> | <span data-ttu-id="d51c1-194">14 </span><span class="sxs-lookup"><span data-stu-id="d51c1-194">14</span></span> |
| <span data-ttu-id="d51c1-195">Отправить беседу</span><span class="sxs-lookup"><span data-stu-id="d51c1-195">Send to Conversation</span></span> | <span data-ttu-id="d51c1-196">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-196">2</span></span> | <span data-ttu-id="d51c1-197">16 </span><span class="sxs-lookup"><span data-stu-id="d51c1-197">16</span></span> |
| <span data-ttu-id="d51c1-198">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-198">Create Conversation</span></span> | <span data-ttu-id="d51c1-199">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-199">1</span></span> | <span data-ttu-id="d51c1-200">14 </span><span class="sxs-lookup"><span data-stu-id="d51c1-200">14</span></span> |
| <span data-ttu-id="d51c1-201">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-201">Create Conversation</span></span> | <span data-ttu-id="d51c1-202">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-202">2</span></span> | <span data-ttu-id="d51c1-203">16 </span><span class="sxs-lookup"><span data-stu-id="d51c1-203">16</span></span> |
| <span data-ttu-id="d51c1-204">креатеконверсатион</span><span class="sxs-lookup"><span data-stu-id="d51c1-204">CreateConversation</span></span>| <span data-ttu-id="d51c1-205">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-205">1</span></span> | <span data-ttu-id="d51c1-206">14 </span><span class="sxs-lookup"><span data-stu-id="d51c1-206">14</span></span> |
| <span data-ttu-id="d51c1-207">креатеконверсатион</span><span class="sxs-lookup"><span data-stu-id="d51c1-207">CreateConversation</span></span>| <span data-ttu-id="d51c1-208">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-208">2</span></span> | <span data-ttu-id="d51c1-209">16 </span><span class="sxs-lookup"><span data-stu-id="d51c1-209">16</span></span> |
| <span data-ttu-id="d51c1-210">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-210">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-211">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-211">1</span></span> | <span data-ttu-id="d51c1-212">8</span><span class="sxs-lookup"><span data-stu-id="d51c1-212">28</span></span> |
| <span data-ttu-id="d51c1-213">Получение участников беседы</span><span class="sxs-lookup"><span data-stu-id="d51c1-213">Get Conversation Members</span></span>| <span data-ttu-id="d51c1-214">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-214">2</span></span> | <span data-ttu-id="d51c1-215">32</span><span class="sxs-lookup"><span data-stu-id="d51c1-215">32</span></span> |
| <span data-ttu-id="d51c1-216">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-216">Get Conversations</span></span> | <span data-ttu-id="d51c1-217">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-217">1</span></span> | <span data-ttu-id="d51c1-218">8</span><span class="sxs-lookup"><span data-stu-id="d51c1-218">28</span></span> |
| <span data-ttu-id="d51c1-219">Получение бесед</span><span class="sxs-lookup"><span data-stu-id="d51c1-219">Get Conversations</span></span> | <span data-ttu-id="d51c1-220">2</span><span class="sxs-lookup"><span data-stu-id="d51c1-220">2</span></span> | <span data-ttu-id="d51c1-221">32</span><span class="sxs-lookup"><span data-stu-id="d51c1-221">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="d51c1-222">Предельное значение для ленты в центре обработки данных</span><span class="sxs-lookup"><span data-stu-id="d51c1-222">Bot per data center limit</span></span>

<span data-ttu-id="d51c1-223">Это значение управляет трафиком, который может создаваться с помощью Bot, во всех потоках в центре обработки данных (для нескольких клиентов).</span><span class="sxs-lookup"><span data-stu-id="d51c1-223">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="d51c1-224">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="d51c1-224">**Time-period (sec)**</span></span> | <span data-ttu-id="d51c1-225">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="d51c1-225">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="d51c1-226">1,1</span><span class="sxs-lookup"><span data-stu-id="d51c1-226">1</span></span> | <span data-ttu-id="d51c1-227">двадцать</span><span class="sxs-lookup"><span data-stu-id="d51c1-227">20</span></span> |
| <span data-ttu-id="d51c1-228">1800</span><span class="sxs-lookup"><span data-stu-id="d51c1-228">1800</span></span> | <span data-ttu-id="d51c1-229">8000</span><span class="sxs-lookup"><span data-stu-id="d51c1-229">8000</span></span> |
| <span data-ttu-id="d51c1-230">3600</span><span class="sxs-lookup"><span data-stu-id="d51c1-230">3600</span></span> | <span data-ttu-id="d51c1-231">15000</span><span class="sxs-lookup"><span data-stu-id="d51c1-231">15000</span></span> |
