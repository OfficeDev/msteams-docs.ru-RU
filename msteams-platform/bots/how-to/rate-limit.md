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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Оптимизация бота: ограничение скорости и лучшие практики в Microsoft Teams

В общем принципе ваше приложение должно ограничить количество сообщений, которые оно публикует, в отдельном чате или разговоре по каналу. Это обеспечивает оптимальное впечатление, которое не будет "нежелательной почтой" для конечных пользователей.

Чтобы защитить Microsoft Teams и ее пользователей, входящие запросы на ограничение скорости API для ботов. Приложения, которые преодолеют это ограничение, получают `HTTP 429 Too Many Requests` состояние ошибки. Все запросы подчиняются одной политике ограничения скорости, включая отправку сообщений, список каналов и извлечение реестра.

Так как точные значения ограничений скорости могут изменяться, мы рекомендуем приложению реализовать соответствующее поведение при возврате `HTTP 429 Too Many Requests` API.

## <a name="handling-rate-limits"></a>Ограничения скорости обработки

При выдаче SDK-операции Bot Builder можно обрабатывать и `Microsoft.Rest.HttpOperationException` проверять код состояния.

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

## <a name="best-practices"></a>Рекомендации

В общем, следует принять простые меры предосторожности, чтобы избежать получения `HTTP 429` ответов. Например, не следует выдавать несколько запросов в один и тот же личный или каналный разговор. Вместо этого рассмотрите пакетную обработку запросов API.

Использование экспоненциального отработки со случайным испугом — это рекомендуемый способ обработки 429s. Это гарантирует, что в нескольких запросах не будут вводиться столкновения при повторном запросе.

## <a name="example-detecting-transient-exceptions"></a>Пример: обнаружение временных исключений

Вот пример с использованием экспоненциального отработки с помощью блока обработки прикладных ошибок.

Вы можете выполнять отработку и повторное выполнение с помощью [обработки временных ошибок.](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29) Инструкции по получению и установке пакета NuGet см. в странице [Добавление](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN)блока приложений для обработки сбоя в решении. *См. также* [переходную обработку с ошибками.](/azure/architecture/best-practices/transient-faults)

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

## <a name="example-backoff"></a>Пример: отсев

Помимо обнаружения ограничений скорости, вы также можете выполнить экспоненциальный отсев.

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

Вы также можете выполнить выполнение метода с описанным выше политикой `System.Action` повторного выполнения. В ссылаемой библиотеке также можно указать фиксированный интервал или механизм линейного отсевов.

Рекомендуется хранить значение и стратегию в файле конфигурации для настройки и настройки значений во время запуска.

Дополнительные сведения можно получить в этом удобном [](/azure/architecture/patterns/retry)руководстве по различным шаблонам повторной проверки.

## <a name="per-bot-per-thread-limit"></a>Ограничение на один бот на поток

>[!NOTE]
>Разделение сообщений на уровне службы приведет к большему, чем ожидалось, запросам в секунду (RPS). Если вас беспокоит приближение к ограничениям, необходимо реализовать описанную выше стратегию обратного выхода. Ниже приведены значения только для оценки.

Это ограничение контролирует трафик, который бот может создавать в одном разговоре. Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.

| **Сценарий** | **Период времени (с)** | **Max allowed operations** |
| --- | --- | --- |
| Отправка в conversation | 1 | 7  |
| Отправка в conversation | 2 | 8  |
| Отправка в conversation | 30 | 60 |
| Отправка в conversation | 3600 | 1800 |
| Создание беседы | 1 | 7  |
| Создание беседы | 2 | 8  |
| Создание беседы | 30 | 60 |
| Создание беседы | 3600 | 1800 |
| Get Conversation Members| 1 | 14  |
| Get Conversation Members| 2 | 16  |
| Get Conversation Members| 30 | 120 |
| Get Conversation Members| 3600 | 3600 |
| Get Conversations | 1 | 14  |
| Get Conversations | 2 | 16  |
| Get Conversations | 30 | 120 |
| Get Conversations | 3600 | 3600 |

>[!NOTE]
> Предыдущие версии и `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` API отстают. Они будут перенастраиваться до 5 запросов в минуту и возвращать не более 10K членов каждой команды. Чтобы обновить SDK bot Framework и код для использования последних конечных точек API с paginated, см. в рубрике Изменения API bot для членов команды и [чата.](../../resources/team-chat-member-api-changes.md)

## <a name="per-thread-limit-for-all-bots"></a>Ограничение потока для всех ботов

Это ограничение управляет трафиком, который все боты могут создавать в одном разговоре. Беседа здесь 1:1 между ботом и пользователем, групповой чат или канал в команде.

| **Сценарий** | **Период времени (с)** | **Max allowed operations** |
| --- | --- | --- |
| Отправка в conversation | 1 | 14  |
| Отправка в conversation | 2 | 16  |
| Создание беседы | 1 | 14  |
| Создание беседы | 2 | 16  |
| CreateConversation| 1 | 14  |
| CreateConversation| 2 | 16  |
| Get Conversation Members| 1 | 28 |
| Get Conversation Members| 2 | 32 |
| Get Conversations | 1 | 28 |
| Get Conversations | 2 | 32 |
