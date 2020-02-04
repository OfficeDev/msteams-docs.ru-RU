---
title: Ограничение скорости
description: Ограничения скорости и рекомендации в Microsoft Teams
keywords: ограничения скорости Боты Teams
ms.openlocfilehash: 4e9efab539ec7817d259fd6c149c438ba02e3ce5
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675293"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="0b49d-104">Оптимизация ограничения скорости и рекомендаций в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="0b49d-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="0b49d-105">Как правило, ваше приложение должно ограничивать количество сообщений, отправляемых в отдельный чат или беседу по каналу.</span><span class="sxs-lookup"><span data-stu-id="0b49d-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="0b49d-106">Это обеспечивает оптимальный интерфейс для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="0b49d-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="0b49d-107">Чтобы защитить Microsoft Teams и ее пользователей, API-интерфейсам Bot могут ограничивать входящие запросы.</span><span class="sxs-lookup"><span data-stu-id="0b49d-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="0b49d-108">Приложения, которые переходят по этому ограничению, получают состояние `HTTP 429 Too Many Requests` ошибки.</span><span class="sxs-lookup"><span data-stu-id="0b49d-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="0b49d-109">Все запросы распространяются на одну и ту же политику ограничения скорости, включая отправку сообщений, перечисление каналов и извлечение списков.</span><span class="sxs-lookup"><span data-stu-id="0b49d-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="0b49d-110">Так как точные значения пределов скорости могут измениться, мы рекомендуем, чтобы приложение выполняло соответствующее поведение при возврате `HTTP 429 Too Many Requests`API.</span><span class="sxs-lookup"><span data-stu-id="0b49d-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="0b49d-111">Пределы скорости обработки</span><span class="sxs-lookup"><span data-stu-id="0b49d-111">Handling rate limits</span></span>

<span data-ttu-id="0b49d-112">При выполнении операции с пакетом SDK построителя построителя `Microsoft.Rest.HttpOperationException` можно обработать код состояния и проверить его.</span><span class="sxs-lookup"><span data-stu-id="0b49d-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="0b49d-113">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="0b49d-113">Best practices</span></span>

<span data-ttu-id="0b49d-114">В общем случае следует принять простые меры предосторожности, чтобы не `HTTP 429` получать ответы.</span><span class="sxs-lookup"><span data-stu-id="0b49d-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="0b49d-115">Например, не выполняйте несколько запросов к одной беседе лично или каналу.</span><span class="sxs-lookup"><span data-stu-id="0b49d-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="0b49d-116">Вместо этого рассмотрите возможности пакетной обработки запросов API.</span><span class="sxs-lookup"><span data-stu-id="0b49d-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="0b49d-117">Использование экспоненциального отработки с случайной колебанием является рекомендуемым способом обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="0b49d-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="0b49d-118">Это гарантирует, что при повторе нескольких запросов не возникать конфликты.</span><span class="sxs-lookup"><span data-stu-id="0b49d-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="0b49d-119">Пример: Обнаружение временных исключений</span><span class="sxs-lookup"><span data-stu-id="0b49d-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="0b49d-120">Ниже приведен пример с использованием экспоненциального переработки через временный блок обработки сбоев.</span><span class="sxs-lookup"><span data-stu-id="0b49d-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="0b49d-121">Вы можете выполнять операции перегрузки и повторных попыток, используя [временные библиотеки обработки ошибок](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span><span class="sxs-lookup"><span data-stu-id="0b49d-121">You can perform backoff and retries using [Transient Fault Handling libraries](/previous-versions/msp-n-p/hh680901(v=pandp.50)).</span></span> <span data-ttu-id="0b49d-122">Рекомендации по получению и установке пакета NuGet приведены в статье [Добавление временного блока обработки сбоев в решение](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span><span class="sxs-lookup"><span data-stu-id="0b49d-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/hh680891(v=pandp.50))</span></span>

```csharp
public class BotSdkTransientExceptionDetectionStrategy : ITransientErrorDetectionStrategy
{
    // List of error codes to retry on
    List<int> transientErrorStatusCodes = new List<int>() { 429 };

    public bool IsTransient(Exception ex)
    {
        var httpOperationException = ex as HttpOperationException;
        if (httpOperationException != null)
        {
            return httpOperationException.Response != null &&
                    transientErrorStatusCodes.Contains((int) httpOperationException.Response.StatusCode);
        }

        return false;
    }
}
```

## <a name="example-backoff"></a><span data-ttu-id="0b49d-123">Пример: отход</span><span class="sxs-lookup"><span data-stu-id="0b49d-123">Example: backoff</span></span>

<span data-ttu-id="0b49d-124">В дополнение к определению пределов скорости, можно также выполнить экспоненциальное переопределение.</span><span class="sxs-lookup"><span data-stu-id="0b49d-124">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

```csharp
/**
* The first parameter specifies the number of retries before failing the operation.
* The second parameter specifies the minimum and maximum backoff time respectively.
* The last parameter is used to add a randomized  +/- 20% delta to avoid numerous clients retrying simultaneously.
*/
var exponentialBackoffRetryStrategy = new ExponentialBackoff(3, TimeSpan.FromSeconds(2),
                        TimeSpan.FromSeconds(20), TimeSpan.FromSeconds(1));


// Define the Retry Policy
var retryPolicy = new RetryPolicy(new BotSdkTransientExceptionDetectionStrategy(), fixedIntervalRetryStrategy);

//Execute any bot sdk action
await retryPolicy.ExecuteAsync(() => connector.Conversations.ReplyToActivityAsync((Activity)reply)).ConfigureAwait(false);
```

<span data-ttu-id="0b49d-125">Выполнение `System.Action` метода также можно выполнить с помощью политики повторных попыток, описанной выше.</span><span class="sxs-lookup"><span data-stu-id="0b49d-125">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="0b49d-126">Указанная библиотека также позволяет указать фиксированный интервал или линейный механизм отрезков.</span><span class="sxs-lookup"><span data-stu-id="0b49d-126">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="0b49d-127">Рекомендуется хранить значение и стратегию в файле конфигурации для точной настройки и корректировки значений во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="0b49d-127">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="0b49d-128">Дополнительную информацию вы узнаете в этом удобном руководстве по различным шаблонам повторных попыток: [шаблон повторов](/azure/architecture/patterns/retry).</span><span class="sxs-lookup"><span data-stu-id="0b49d-128">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="0b49d-129">Предельное число потоков для каждой ленты</span><span class="sxs-lookup"><span data-stu-id="0b49d-129">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="0b49d-130">Разбиение сообщений на уровне службы приведет к превышению ожидаемых запросов в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="0b49d-130">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="0b49d-131">Если вы беспокоитесь об этих пределах, необходимо реализовать стратегию отработки отказа, описанную выше.</span><span class="sxs-lookup"><span data-stu-id="0b49d-131">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="0b49d-132">Указанные ниже значения предназначены только для оценки.</span><span class="sxs-lookup"><span data-stu-id="0b49d-132">The values provided below are for estimation only.</span></span>

<span data-ttu-id="0b49d-133">Это предельное значение управляет трафиком, который может создаваться с помощью Bot в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="0b49d-133">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="0b49d-134">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="0b49d-134">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="0b49d-135">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="0b49d-135">**Scenario**</span></span> | <span data-ttu-id="0b49d-136">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="0b49d-136">**Time-period (sec)**</span></span> | <span data-ttu-id="0b49d-137">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="0b49d-137">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49d-138">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-138">NewMessage</span></span> | <span data-ttu-id="0b49d-139">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-139">1</span></span> | <span data-ttu-id="0b49d-140">7 </span><span class="sxs-lookup"><span data-stu-id="0b49d-140">7</span></span> |
| <span data-ttu-id="0b49d-141">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-141">NewMessage</span></span> | <span data-ttu-id="0b49d-142">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-142">2</span></span> | <span data-ttu-id="0b49d-143">8 </span><span class="sxs-lookup"><span data-stu-id="0b49d-143">8</span></span> |
| <span data-ttu-id="0b49d-144">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-144">NewMessage</span></span> | <span data-ttu-id="0b49d-145">более</span><span class="sxs-lookup"><span data-stu-id="0b49d-145">30</span></span> | <span data-ttu-id="0b49d-146">60</span><span class="sxs-lookup"><span data-stu-id="0b49d-146">60</span></span> |
| <span data-ttu-id="0b49d-147">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-147">NewMessage</span></span> | <span data-ttu-id="0b49d-148">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-148">3600</span></span> | <span data-ttu-id="0b49d-149">1800</span><span class="sxs-lookup"><span data-stu-id="0b49d-149">1800</span></span> |
| <span data-ttu-id="0b49d-150">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-150">UpdateMessage</span></span> | <span data-ttu-id="0b49d-151">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-151">1</span></span> | <span data-ttu-id="0b49d-152">7 </span><span class="sxs-lookup"><span data-stu-id="0b49d-152">7</span></span> |
| <span data-ttu-id="0b49d-153">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-153">UpdateMessage</span></span> | <span data-ttu-id="0b49d-154">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-154">2</span></span> | <span data-ttu-id="0b49d-155">8 </span><span class="sxs-lookup"><span data-stu-id="0b49d-155">8</span></span> |
| <span data-ttu-id="0b49d-156">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-156">UpdateMessage</span></span> | <span data-ttu-id="0b49d-157">более</span><span class="sxs-lookup"><span data-stu-id="0b49d-157">30</span></span> | <span data-ttu-id="0b49d-158">60</span><span class="sxs-lookup"><span data-stu-id="0b49d-158">60</span></span> |
| <span data-ttu-id="0b49d-159">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-159">UpdateMessage</span></span> | <span data-ttu-id="0b49d-160">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-160">3600</span></span> | <span data-ttu-id="0b49d-161">1800</span><span class="sxs-lookup"><span data-stu-id="0b49d-161">1800</span></span> |
| <span data-ttu-id="0b49d-162">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-162">NewThread</span></span> | <span data-ttu-id="0b49d-163">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-163">1</span></span> | <span data-ttu-id="0b49d-164">7 </span><span class="sxs-lookup"><span data-stu-id="0b49d-164">7</span></span> |
| <span data-ttu-id="0b49d-165">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-165">NewThread</span></span> | <span data-ttu-id="0b49d-166">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-166">2</span></span> | <span data-ttu-id="0b49d-167">8 </span><span class="sxs-lookup"><span data-stu-id="0b49d-167">8</span></span> |
| <span data-ttu-id="0b49d-168">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-168">NewThread</span></span> | <span data-ttu-id="0b49d-169">более</span><span class="sxs-lookup"><span data-stu-id="0b49d-169">30</span></span> | <span data-ttu-id="0b49d-170">60</span><span class="sxs-lookup"><span data-stu-id="0b49d-170">60</span></span> |
| <span data-ttu-id="0b49d-171">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-171">NewThread</span></span> | <span data-ttu-id="0b49d-172">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-172">3600</span></span> | <span data-ttu-id="0b49d-173">1800</span><span class="sxs-lookup"><span data-stu-id="0b49d-173">1800</span></span> |
| <span data-ttu-id="0b49d-174">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-174">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-175">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-175">1</span></span> | <span data-ttu-id="0b49d-176">14 </span><span class="sxs-lookup"><span data-stu-id="0b49d-176">14</span></span> |
| <span data-ttu-id="0b49d-177">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-177">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-178">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-178">2</span></span> | <span data-ttu-id="0b49d-179">16 </span><span class="sxs-lookup"><span data-stu-id="0b49d-179">16</span></span> |
| <span data-ttu-id="0b49d-180">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-180">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-181">более</span><span class="sxs-lookup"><span data-stu-id="0b49d-181">30</span></span> | <span data-ttu-id="0b49d-182">120</span><span class="sxs-lookup"><span data-stu-id="0b49d-182">120</span></span> |
| <span data-ttu-id="0b49d-183">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-183">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-184">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-184">3600</span></span> | <span data-ttu-id="0b49d-185">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-185">3600</span></span> |
| <span data-ttu-id="0b49d-186">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-186">GetThread</span></span> | <span data-ttu-id="0b49d-187">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-187">1</span></span> | <span data-ttu-id="0b49d-188">14 </span><span class="sxs-lookup"><span data-stu-id="0b49d-188">14</span></span> |
| <span data-ttu-id="0b49d-189">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-189">GetThread</span></span> | <span data-ttu-id="0b49d-190">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-190">2</span></span> | <span data-ttu-id="0b49d-191">16 </span><span class="sxs-lookup"><span data-stu-id="0b49d-191">16</span></span> |
| <span data-ttu-id="0b49d-192">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-192">GetThread</span></span> | <span data-ttu-id="0b49d-193">более</span><span class="sxs-lookup"><span data-stu-id="0b49d-193">30</span></span> | <span data-ttu-id="0b49d-194">120</span><span class="sxs-lookup"><span data-stu-id="0b49d-194">120</span></span> |
| <span data-ttu-id="0b49d-195">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-195">GetThread</span></span> | <span data-ttu-id="0b49d-196">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-196">3600</span></span> | <span data-ttu-id="0b49d-197">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-197">3600</span></span> |

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="0b49d-198">Предельное количество потоков для всех Боты</span><span class="sxs-lookup"><span data-stu-id="0b49d-198">Per thread limit for all bots</span></span>

<span data-ttu-id="0b49d-199">Это значение управляет трафиком, в течение которого все боты могут создаваться в одной беседе.</span><span class="sxs-lookup"><span data-stu-id="0b49d-199">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="0b49d-200">Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.</span><span class="sxs-lookup"><span data-stu-id="0b49d-200">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="0b49d-201">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="0b49d-201">**Scenario**</span></span> | <span data-ttu-id="0b49d-202">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="0b49d-202">**Time-period (sec)**</span></span> | <span data-ttu-id="0b49d-203">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="0b49d-203">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0b49d-204">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-204">NewMessage</span></span> | <span data-ttu-id="0b49d-205">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-205">1</span></span> | <span data-ttu-id="0b49d-206">14 </span><span class="sxs-lookup"><span data-stu-id="0b49d-206">14</span></span> |
| <span data-ttu-id="0b49d-207">NewMessage</span><span class="sxs-lookup"><span data-stu-id="0b49d-207">NewMessage</span></span> | <span data-ttu-id="0b49d-208">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-208">2</span></span> | <span data-ttu-id="0b49d-209">16 </span><span class="sxs-lookup"><span data-stu-id="0b49d-209">16</span></span> |
| <span data-ttu-id="0b49d-210">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-210">UpdateMessage</span></span> | <span data-ttu-id="0b49d-211">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-211">1</span></span> | <span data-ttu-id="0b49d-212">14 </span><span class="sxs-lookup"><span data-stu-id="0b49d-212">14</span></span> |
| <span data-ttu-id="0b49d-213">упдатемессаже</span><span class="sxs-lookup"><span data-stu-id="0b49d-213">UpdateMessage</span></span> | <span data-ttu-id="0b49d-214">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-214">2</span></span> | <span data-ttu-id="0b49d-215">16 </span><span class="sxs-lookup"><span data-stu-id="0b49d-215">16</span></span> |
| <span data-ttu-id="0b49d-216">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-216">NewThread</span></span> | <span data-ttu-id="0b49d-217">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-217">1</span></span> | <span data-ttu-id="0b49d-218">14 </span><span class="sxs-lookup"><span data-stu-id="0b49d-218">14</span></span> |
| <span data-ttu-id="0b49d-219">невсреад</span><span class="sxs-lookup"><span data-stu-id="0b49d-219">NewThread</span></span> | <span data-ttu-id="0b49d-220">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-220">2</span></span> | <span data-ttu-id="0b49d-221">16 </span><span class="sxs-lookup"><span data-stu-id="0b49d-221">16</span></span> |
| <span data-ttu-id="0b49d-222">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-222">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-223">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-223">1</span></span> | <span data-ttu-id="0b49d-224">8</span><span class="sxs-lookup"><span data-stu-id="0b49d-224">28</span></span> |
| <span data-ttu-id="0b49d-225">жетсреадмемберс</span><span class="sxs-lookup"><span data-stu-id="0b49d-225">GetThreadMembers</span></span> | <span data-ttu-id="0b49d-226">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-226">2</span></span> | <span data-ttu-id="0b49d-227">32</span><span class="sxs-lookup"><span data-stu-id="0b49d-227">32</span></span> |
| <span data-ttu-id="0b49d-228">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-228">GetThread</span></span> | <span data-ttu-id="0b49d-229">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-229">1</span></span> | <span data-ttu-id="0b49d-230">8</span><span class="sxs-lookup"><span data-stu-id="0b49d-230">28</span></span> |
| <span data-ttu-id="0b49d-231">Поток</span><span class="sxs-lookup"><span data-stu-id="0b49d-231">GetThread</span></span> | <span data-ttu-id="0b49d-232">2 </span><span class="sxs-lookup"><span data-stu-id="0b49d-232">2</span></span> | <span data-ttu-id="0b49d-233">32</span><span class="sxs-lookup"><span data-stu-id="0b49d-233">32</span></span> |

## <a name="bot-per-data-center-limit"></a><span data-ttu-id="0b49d-234">Предельное значение для ленты в центре обработки данных</span><span class="sxs-lookup"><span data-stu-id="0b49d-234">Bot per data center limit</span></span>

<span data-ttu-id="0b49d-235">Это значение управляет трафиком, который может создаваться с помощью Bot, во всех потоках в центре обработки данных (для нескольких клиентов).</span><span class="sxs-lookup"><span data-stu-id="0b49d-235">This limit controls the traffic that a bot is allowed to generate across all threads in a data center (across multiple tenants).</span></span>

|<span data-ttu-id="0b49d-236">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="0b49d-236">**Time-period (sec)**</span></span> | <span data-ttu-id="0b49d-237">**Максимальное число разрешенных операций**</span><span class="sxs-lookup"><span data-stu-id="0b49d-237">**Max allowed operations**</span></span> |
| --- | --- |
| <span data-ttu-id="0b49d-238">1 </span><span class="sxs-lookup"><span data-stu-id="0b49d-238">1</span></span> | <span data-ttu-id="0b49d-239">двадцать</span><span class="sxs-lookup"><span data-stu-id="0b49d-239">20</span></span> |
| <span data-ttu-id="0b49d-240">1800</span><span class="sxs-lookup"><span data-stu-id="0b49d-240">1800</span></span> | <span data-ttu-id="0b49d-241">8000</span><span class="sxs-lookup"><span data-stu-id="0b49d-241">8000</span></span> |
| <span data-ttu-id="0b49d-242">3600</span><span class="sxs-lookup"><span data-stu-id="0b49d-242">3600</span></span> | <span data-ttu-id="0b49d-243">15000</span><span class="sxs-lookup"><span data-stu-id="0b49d-243">15000</span></span> |
