---
title: Ограничение скорости
description: Ограничение скорости и лучшие практики в Microsoft Teams
keywords: ограничения скорости командных ботов
ms.openlocfilehash: 840737178234bcd6e2da1925b0031083717e2b91
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034685"
---
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a><span data-ttu-id="10fd2-104">Оптимизация бота: ограничение скорости и лучшие практики в Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="10fd2-104">Optimize your bot: rate limiting and best practices in Microsoft Teams</span></span>

<span data-ttu-id="10fd2-105">В общем принципе ваше приложение должно ограничить количество сообщений, которые оно публикует, в отдельном чате или разговоре по каналу.</span><span class="sxs-lookup"><span data-stu-id="10fd2-105">As a general principle, your application should limit the number of messages it posts to an individual chat or channel conversation.</span></span> <span data-ttu-id="10fd2-106">Это обеспечивает оптимальное впечатление, которое не будет "нежелательной почтой" для конечных пользователей.</span><span class="sxs-lookup"><span data-stu-id="10fd2-106">This ensures an optimal experience that doesn't feel “spammy” to your end users.</span></span>

<span data-ttu-id="10fd2-107">Чтобы защитить Microsoft Teams и ее пользователей, входящие запросы на ограничение скорости API для ботов.</span><span class="sxs-lookup"><span data-stu-id="10fd2-107">To protect Microsoft Teams and its users, the bot APIs rate-limit incoming requests.</span></span> <span data-ttu-id="10fd2-108">Приложения, которые преодолеют это ограничение, получают `HTTP 429 Too Many Requests` состояние ошибки.</span><span class="sxs-lookup"><span data-stu-id="10fd2-108">Apps that go over this limit receive an `HTTP 429 Too Many Requests` error status.</span></span> <span data-ttu-id="10fd2-109">Все запросы подчиняются одной политике ограничения скорости, включая отправку сообщений, список каналов и извлечение реестра.</span><span class="sxs-lookup"><span data-stu-id="10fd2-109">All requests are subject to the same rate-limiting policy, including sending messages, channel enumerations, and roster fetches.</span></span>

<span data-ttu-id="10fd2-110">Так как точные значения ограничений скорости могут изменяться, мы рекомендуем приложению реализовать соответствующее поведение при возврате `HTTP 429 Too Many Requests` API.</span><span class="sxs-lookup"><span data-stu-id="10fd2-110">Because the exact values of rate limits are subject to change, we recommend your application implement the appropriate backoff behavior when the API returns `HTTP 429 Too Many Requests`.</span></span>

## <a name="handling-rate-limits"></a><span data-ttu-id="10fd2-111">Ограничения скорости обработки</span><span class="sxs-lookup"><span data-stu-id="10fd2-111">Handling rate limits</span></span>

<span data-ttu-id="10fd2-112">При выдаче SDK-операции Bot Builder можно обрабатывать и `Microsoft.Rest.HttpOperationException` проверять код состояния.</span><span class="sxs-lookup"><span data-stu-id="10fd2-112">When issuing a Bot Builder SDK operation, you can handle `Microsoft.Rest.HttpOperationException` and check for the status code.</span></span>

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

## <a name="best-practices"></a><span data-ttu-id="10fd2-113">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="10fd2-113">Best practices</span></span>

<span data-ttu-id="10fd2-114">В общем, следует принять простые меры предосторожности, чтобы избежать получения `HTTP 429` ответов.</span><span class="sxs-lookup"><span data-stu-id="10fd2-114">In general, you should take simple precautions to avoid receiving `HTTP 429` responses.</span></span> <span data-ttu-id="10fd2-115">Например, не следует выдавать несколько запросов в один и тот же личный или каналный разговор.</span><span class="sxs-lookup"><span data-stu-id="10fd2-115">For instance, avoid issuing multiple requests to the same personal or channel conversation.</span></span> <span data-ttu-id="10fd2-116">Вместо этого рассмотрите пакетную обработку запросов API.</span><span class="sxs-lookup"><span data-stu-id="10fd2-116">Instead, consider batching the API requests.</span></span>

<span data-ttu-id="10fd2-117">Использование экспоненциального отработки со случайным испугом — это рекомендуемый способ обработки 429s.</span><span class="sxs-lookup"><span data-stu-id="10fd2-117">Using an exponential backoff with a random jitter is the recommended way to handle 429s.</span></span> <span data-ttu-id="10fd2-118">Это гарантирует, что в нескольких запросах не будут вводиться столкновения при повторном запросе.</span><span class="sxs-lookup"><span data-stu-id="10fd2-118">This ensures that multiple requests don't introduce collisions on retries.</span></span>

## <a name="example-detecting-transient-exceptions"></a><span data-ttu-id="10fd2-119">Пример: обнаружение временных исключений</span><span class="sxs-lookup"><span data-stu-id="10fd2-119">Example: detecting transient exceptions</span></span>

<span data-ttu-id="10fd2-120">Вот пример с использованием экспоненциального отработки с помощью блока обработки прикладных ошибок.</span><span class="sxs-lookup"><span data-stu-id="10fd2-120">Here is a sample using exponential backoff via the Transient Fault Handling Application Block.</span></span>

<span data-ttu-id="10fd2-121">Вы можете выполнять отработку и повторное выполнение с помощью [обработки временных ошибок.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29)</span><span class="sxs-lookup"><span data-stu-id="10fd2-121">You can perform backoff and retries using [Transient Fault Handling](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29).</span></span> <span data-ttu-id="10fd2-122">Инструкции по получению и установке пакета NuGet см. в странице [Добавление](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)блока приложений для обработки сбоя в решении.</span><span class="sxs-lookup"><span data-stu-id="10fd2-122">For guidelines on obtaining and installing the NuGet package, see [Adding the Transient Fault Handling Application Block to Your Solution](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)).</span></span> <span data-ttu-id="10fd2-123">*См. также* [переходную обработку с ошибками.](/azure/architecture/best-practices/transient-faults)</span><span class="sxs-lookup"><span data-stu-id="10fd2-123">*See also* [Transient fault handling](/azure/architecture/best-practices/transient-faults).</span></span>

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

## <a name="example-backoff"></a><span data-ttu-id="10fd2-124">Пример: отсев</span><span class="sxs-lookup"><span data-stu-id="10fd2-124">Example: backoff</span></span>

<span data-ttu-id="10fd2-125">Помимо обнаружения ограничений скорости, вы также можете выполнить экспоненциальный отсев.</span><span class="sxs-lookup"><span data-stu-id="10fd2-125">In addition to detecting rate limits, you can also perform an exponential backoff.</span></span>

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

<span data-ttu-id="10fd2-126">Вы также можете выполнить выполнение метода с описанным выше политикой `System.Action` повторного выполнения.</span><span class="sxs-lookup"><span data-stu-id="10fd2-126">You can also perform a `System.Action` method execution with the retry policy described above.</span></span> <span data-ttu-id="10fd2-127">В ссылаемой библиотеке также можно указать фиксированный интервал или механизм линейного отсевов.</span><span class="sxs-lookup"><span data-stu-id="10fd2-127">The referenced library also allows you to specify a fixed interval or a linear backoff mechanism.</span></span>

<span data-ttu-id="10fd2-128">Рекомендуется хранить значение и стратегию в файле конфигурации для настройки и настройки значений во время запуска.</span><span class="sxs-lookup"><span data-stu-id="10fd2-128">We recommend storing the value and strategy in a configuration file to fine-tune and tweak values at run time.</span></span>

<span data-ttu-id="10fd2-129">Дополнительные сведения можно получить в этом удобном [](/azure/architecture/patterns/retry)руководстве по различным шаблонам повторной проверки.</span><span class="sxs-lookup"><span data-stu-id="10fd2-129">For more information, check out this handy guide on various retry patterns: [Retry pattern](/azure/architecture/patterns/retry).</span></span>

## <a name="per-bot-per-thread-limit"></a><span data-ttu-id="10fd2-130">Ограничение на один бот на поток</span><span class="sxs-lookup"><span data-stu-id="10fd2-130">Per bot per thread limit</span></span>

>[!NOTE]
><span data-ttu-id="10fd2-131">Разделение сообщений на уровне службы приведет к большему, чем ожидалось, запросам в секунду (RPS).</span><span class="sxs-lookup"><span data-stu-id="10fd2-131">Message splitting at the service level will result in higher than expected requests per second (RPS).</span></span> <span data-ttu-id="10fd2-132">Если вас беспокоит приближение к ограничениям, необходимо реализовать описанную выше стратегию обратного выхода.</span><span class="sxs-lookup"><span data-stu-id="10fd2-132">If you're concerned about approaching the limits, you should implement the backoff strategy described above.</span></span> <span data-ttu-id="10fd2-133">Ниже приведены значения только для оценки.</span><span class="sxs-lookup"><span data-stu-id="10fd2-133">The values provided below are for estimation only.</span></span>

<span data-ttu-id="10fd2-134">Это ограничение контролирует трафик, который бот может создавать в одном разговоре.</span><span class="sxs-lookup"><span data-stu-id="10fd2-134">This limit controls the traffic that a bot is allowed to generate on a single conversation.</span></span> <span data-ttu-id="10fd2-135">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="10fd2-135">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="10fd2-136">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="10fd2-136">**Scenario**</span></span> | <span data-ttu-id="10fd2-137">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="10fd2-137">**Time-period (sec)**</span></span> | <span data-ttu-id="10fd2-138">**Max allowed operations**</span><span class="sxs-lookup"><span data-stu-id="10fd2-138">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10fd2-139">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-139">Send to Conversation</span></span> | <span data-ttu-id="10fd2-140">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-140">1</span></span> | <span data-ttu-id="10fd2-141">7 </span><span class="sxs-lookup"><span data-stu-id="10fd2-141">7</span></span> |
| <span data-ttu-id="10fd2-142">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-142">Send to Conversation</span></span> | <span data-ttu-id="10fd2-143">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-143">2</span></span> | <span data-ttu-id="10fd2-144">8 </span><span class="sxs-lookup"><span data-stu-id="10fd2-144">8</span></span> |
| <span data-ttu-id="10fd2-145">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-145">Send to Conversation</span></span> | <span data-ttu-id="10fd2-146">30</span><span class="sxs-lookup"><span data-stu-id="10fd2-146">30</span></span> | <span data-ttu-id="10fd2-147">60</span><span class="sxs-lookup"><span data-stu-id="10fd2-147">60</span></span> |
| <span data-ttu-id="10fd2-148">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-148">Send to Conversation</span></span> | <span data-ttu-id="10fd2-149">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-149">3600</span></span> | <span data-ttu-id="10fd2-150">1800</span><span class="sxs-lookup"><span data-stu-id="10fd2-150">1800</span></span> |
| <span data-ttu-id="10fd2-151">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-151">Create Conversation</span></span> | <span data-ttu-id="10fd2-152">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-152">1</span></span> | <span data-ttu-id="10fd2-153">7 </span><span class="sxs-lookup"><span data-stu-id="10fd2-153">7</span></span> |
| <span data-ttu-id="10fd2-154">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-154">Create Conversation</span></span> | <span data-ttu-id="10fd2-155">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-155">2</span></span> | <span data-ttu-id="10fd2-156">8 </span><span class="sxs-lookup"><span data-stu-id="10fd2-156">8</span></span> |
| <span data-ttu-id="10fd2-157">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-157">Create Conversation</span></span> | <span data-ttu-id="10fd2-158">30</span><span class="sxs-lookup"><span data-stu-id="10fd2-158">30</span></span> | <span data-ttu-id="10fd2-159">60</span><span class="sxs-lookup"><span data-stu-id="10fd2-159">60</span></span> |
| <span data-ttu-id="10fd2-160">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-160">Create Conversation</span></span> | <span data-ttu-id="10fd2-161">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-161">3600</span></span> | <span data-ttu-id="10fd2-162">1800</span><span class="sxs-lookup"><span data-stu-id="10fd2-162">1800</span></span> |
| <span data-ttu-id="10fd2-163">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-163">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-164">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-164">1</span></span> | <span data-ttu-id="10fd2-165">14 </span><span class="sxs-lookup"><span data-stu-id="10fd2-165">14</span></span> |
| <span data-ttu-id="10fd2-166">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-166">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-167">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-167">2</span></span> | <span data-ttu-id="10fd2-168">16 </span><span class="sxs-lookup"><span data-stu-id="10fd2-168">16</span></span> |
| <span data-ttu-id="10fd2-169">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-169">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-170">30</span><span class="sxs-lookup"><span data-stu-id="10fd2-170">30</span></span> | <span data-ttu-id="10fd2-171">120</span><span class="sxs-lookup"><span data-stu-id="10fd2-171">120</span></span> |
| <span data-ttu-id="10fd2-172">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-172">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-173">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-173">3600</span></span> | <span data-ttu-id="10fd2-174">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-174">3600</span></span> |
| <span data-ttu-id="10fd2-175">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-175">Get Conversations</span></span> | <span data-ttu-id="10fd2-176">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-176">1</span></span> | <span data-ttu-id="10fd2-177">14 </span><span class="sxs-lookup"><span data-stu-id="10fd2-177">14</span></span> |
| <span data-ttu-id="10fd2-178">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-178">Get Conversations</span></span> | <span data-ttu-id="10fd2-179">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-179">2</span></span> | <span data-ttu-id="10fd2-180">16 </span><span class="sxs-lookup"><span data-stu-id="10fd2-180">16</span></span> |
| <span data-ttu-id="10fd2-181">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-181">Get Conversations</span></span> | <span data-ttu-id="10fd2-182">30</span><span class="sxs-lookup"><span data-stu-id="10fd2-182">30</span></span> | <span data-ttu-id="10fd2-183">120</span><span class="sxs-lookup"><span data-stu-id="10fd2-183">120</span></span> |
| <span data-ttu-id="10fd2-184">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-184">Get Conversations</span></span> | <span data-ttu-id="10fd2-185">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-185">3600</span></span> | <span data-ttu-id="10fd2-186">3600</span><span class="sxs-lookup"><span data-stu-id="10fd2-186">3600</span></span> |

>[!NOTE]
> <span data-ttu-id="10fd2-187">Предыдущие версии и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API отстают.</span><span class="sxs-lookup"><span data-stu-id="10fd2-187">Previous versions of `TeamsInfo.getMembers` and `TeamsInfo.GetMembersAsync` APIs are being deprecated.</span></span> <span data-ttu-id="10fd2-188">Они будут перенастраиваться до 5 запросов в минуту и возвращать не более 10K членов каждой команды.</span><span class="sxs-lookup"><span data-stu-id="10fd2-188">They will be throttled to 5 requests per minute and return a maximum of 10K members per team.</span></span> <span data-ttu-id="10fd2-189">Чтобы обновить SDK bot Framework и код для использования последних конечных точек API с paginated, см. в рубрике Изменения API bot для членов команды и [чата.](../../resources/team-chat-member-api-changes.md)</span><span class="sxs-lookup"><span data-stu-id="10fd2-189">To update your Bot Framework SDK and the code to use the latest paginated API endpoints, see [Bot API changes for team and chat members](../../resources/team-chat-member-api-changes.md).</span></span>

## <a name="per-thread-limit-for-all-bots"></a><span data-ttu-id="10fd2-190">Ограничение потока для всех ботов</span><span class="sxs-lookup"><span data-stu-id="10fd2-190">Per thread limit for all bots</span></span>

<span data-ttu-id="10fd2-191">Это ограничение управляет трафиком, который все боты могут создавать в одном разговоре.</span><span class="sxs-lookup"><span data-stu-id="10fd2-191">This limit controls the traffic that all bots are allowed to generate across a single conversation.</span></span> <span data-ttu-id="10fd2-192">Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.</span><span class="sxs-lookup"><span data-stu-id="10fd2-192">A conversation here is 1:1 between bot and user, a group-chat, or a channel in a team.</span></span>

| <span data-ttu-id="10fd2-193">**Сценарий**</span><span class="sxs-lookup"><span data-stu-id="10fd2-193">**Scenario**</span></span> | <span data-ttu-id="10fd2-194">**Период времени (с)**</span><span class="sxs-lookup"><span data-stu-id="10fd2-194">**Time-period (sec)**</span></span> | <span data-ttu-id="10fd2-195">**Max allowed operations**</span><span class="sxs-lookup"><span data-stu-id="10fd2-195">**Max allowed operations**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="10fd2-196">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-196">Send to Conversation</span></span> | <span data-ttu-id="10fd2-197">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-197">1</span></span> | <span data-ttu-id="10fd2-198">14 </span><span class="sxs-lookup"><span data-stu-id="10fd2-198">14</span></span> |
| <span data-ttu-id="10fd2-199">Отправка в conversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-199">Send to Conversation</span></span> | <span data-ttu-id="10fd2-200">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-200">2</span></span> | <span data-ttu-id="10fd2-201">16 </span><span class="sxs-lookup"><span data-stu-id="10fd2-201">16</span></span> |
| <span data-ttu-id="10fd2-202">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-202">Create Conversation</span></span> | <span data-ttu-id="10fd2-203">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-203">1</span></span> | <span data-ttu-id="10fd2-204">14 </span><span class="sxs-lookup"><span data-stu-id="10fd2-204">14</span></span> |
| <span data-ttu-id="10fd2-205">Создание беседы</span><span class="sxs-lookup"><span data-stu-id="10fd2-205">Create Conversation</span></span> | <span data-ttu-id="10fd2-206">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-206">2</span></span> | <span data-ttu-id="10fd2-207">16 </span><span class="sxs-lookup"><span data-stu-id="10fd2-207">16</span></span> |
| <span data-ttu-id="10fd2-208">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-208">CreateConversation</span></span>| <span data-ttu-id="10fd2-209">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-209">1</span></span> | <span data-ttu-id="10fd2-210">14 </span><span class="sxs-lookup"><span data-stu-id="10fd2-210">14</span></span> |
| <span data-ttu-id="10fd2-211">CreateConversation</span><span class="sxs-lookup"><span data-stu-id="10fd2-211">CreateConversation</span></span>| <span data-ttu-id="10fd2-212">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-212">2</span></span> | <span data-ttu-id="10fd2-213">16 </span><span class="sxs-lookup"><span data-stu-id="10fd2-213">16</span></span> |
| <span data-ttu-id="10fd2-214">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-214">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-215">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-215">1</span></span> | <span data-ttu-id="10fd2-216">28</span><span class="sxs-lookup"><span data-stu-id="10fd2-216">28</span></span> |
| <span data-ttu-id="10fd2-217">Get Conversation Members</span><span class="sxs-lookup"><span data-stu-id="10fd2-217">Get Conversation Members</span></span>| <span data-ttu-id="10fd2-218">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-218">2</span></span> | <span data-ttu-id="10fd2-219">32</span><span class="sxs-lookup"><span data-stu-id="10fd2-219">32</span></span> |
| <span data-ttu-id="10fd2-220">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-220">Get Conversations</span></span> | <span data-ttu-id="10fd2-221">1</span><span class="sxs-lookup"><span data-stu-id="10fd2-221">1</span></span> | <span data-ttu-id="10fd2-222">28</span><span class="sxs-lookup"><span data-stu-id="10fd2-222">28</span></span> |
| <span data-ttu-id="10fd2-223">Get Conversations</span><span class="sxs-lookup"><span data-stu-id="10fd2-223">Get Conversations</span></span> | <span data-ttu-id="10fd2-224">2</span><span class="sxs-lookup"><span data-stu-id="10fd2-224">2</span></span> | <span data-ttu-id="10fd2-225">32</span><span class="sxs-lookup"><span data-stu-id="10fd2-225">32</span></span> |
