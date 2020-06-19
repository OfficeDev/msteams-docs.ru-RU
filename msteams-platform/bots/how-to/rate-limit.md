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
# <a name="optimize-your-bot-rate-limiting-and-best-practices-in-microsoft-teams"></a>Оптимизация ограничения скорости и рекомендаций в Microsoft Teams.

Как правило, ваше приложение должно ограничивать количество сообщений, отправляемых в отдельный чат или беседу по каналу. Это обеспечивает оптимальный интерфейс для конечных пользователей.

Чтобы защитить Microsoft Teams и ее пользователей, API-интерфейсам Bot могут ограничивать входящие запросы. Приложения, которые переходят по этому ограничению, получают `HTTP 429 Too Many Requests` состояние ошибки. Все запросы распространяются на одну и ту же политику ограничения скорости, включая отправку сообщений, перечисление каналов и извлечение списков.

Так как точные значения пределов скорости могут измениться, мы рекомендуем, чтобы приложение выполняло соответствующее поведение при возврате API `HTTP 429 Too Many Requests` .

## <a name="handling-rate-limits"></a>Пределы скорости обработки

При выполнении операции с пакетом SDK построителя построителя можно обработать `Microsoft.Rest.HttpOperationException` код состояния и проверить его.

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

В общем случае следует принять простые меры предосторожности, чтобы не получать `HTTP 429` ответы. Например, не выполняйте несколько запросов к одной беседе лично или каналу. Вместо этого рассмотрите возможности пакетной обработки запросов API.

Использование экспоненциального отработки с случайной колебанием является рекомендуемым способом обработки 429s. Это гарантирует, что при повторе нескольких запросов не возникать конфликты.

## <a name="example-detecting-transient-exceptions"></a>Пример: Обнаружение временных исключений

Ниже приведен пример с использованием экспоненциального переработки через временный блок обработки сбоев.

Вы можете выполнять операции перегрузки и повторных попыток, используя [временную обработку сбоев](/previous-versions/msp-n-p/hh675232%28v%3dpandp.10%29). Рекомендации по получению и установке пакета NuGet приведены в статье [Добавление временного блока обработки сбоев в решение](/previous-versions/msp-n-p/dn440719(v=pandp.60)?redirectedfrom=MSDN). *См. также* [временная обработка сбоев](/azure/architecture/best-practices/transient-faults).

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

## <a name="example-backoff"></a>Пример: отход

В дополнение к определению пределов скорости, можно также выполнить экспоненциальное переопределение.

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

Выполнение метода также можно выполнить `System.Action` с помощью политики повторных попыток, описанной выше. Указанная библиотека также позволяет указать фиксированный интервал или линейный механизм отрезков.

Рекомендуется хранить значение и стратегию в файле конфигурации для точной настройки и корректировки значений во время выполнения.

Дополнительную информацию вы узнаете в этом удобном руководстве по различным шаблонам повторных попыток: [шаблон повторов](/azure/architecture/patterns/retry).

## <a name="per-bot-per-thread-limit"></a>Предельное число потоков для каждой ленты

>[!NOTE]
>Разбиение сообщений на уровне службы приведет к превышению ожидаемых запросов в секунду (RPS). Если вы беспокоитесь об этих пределах, необходимо реализовать стратегию отработки отказа, описанную выше. Указанные ниже значения предназначены только для оценки.

Это предельное значение управляет трафиком, который может создаваться с помощью Bot в одной беседе. Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.

| **Сценарий** | **Период времени (с)** | **Максимальное число разрешенных операций** |
| --- | --- | --- |
| Отправить беседу | 1  | 7  |
| Отправить беседу | 2 | 8  |
| Отправить беседу | более | 60 |
| Отправить беседу | 3600 | 1800 |
| Создание беседы | 1  | 7  |
| Создание беседы | 2 | 8  |
| Создание беседы | более | 60 |
| Создание беседы | 3600 | 1800 |
| Получение участников беседы| 1  | 14  |
| Получение участников беседы| 2 | 16  |
| Получение участников беседы| более | 120 |
| Получение участников беседы| 3600 | 3600 |
| Получение бесед | 1  | 14  |
| Получение бесед | 2 | 16  |
| Получение бесед | более | 120 |
| Получение бесед | 3600 | 3600 |

## <a name="per-thread-limit-for-all-bots"></a>Предельное количество потоков для всех Боты

Это значение управляет трафиком, в течение которого все боты могут создаваться в одной беседе. Беседа — 1:1 между Bot и пользователем, группой-чат или каналом в команде.

| **Сценарий** | **Период времени (с)** | **Максимальное число разрешенных операций** |
| --- | --- | --- |
| Отправить беседу | 1  | 14  |
| Отправить беседу | 2 | 16  |
| Создание беседы | 1  | 14  |
| Создание беседы | 2 | 16  |
| креатеконверсатион| 1  | 14  |
| креатеконверсатион| 2 | 16  |
| Получение участников беседы| 1  | 8 |
| Получение участников беседы| 2 | 32 |
| Получение бесед | 1  | 8 |
| Получение бесед | 2 | 32 |

## <a name="bot-per-data-center-limit"></a>Предельное значение для ленты в центре обработки данных

Это значение управляет трафиком, который может создаваться с помощью Bot, во всех потоках в центре обработки данных (для нескольких клиентов).

|**Период времени (с)** | **Максимальное число разрешенных операций** |
| --- | --- |
| 1  | двадцать |
| 1800 | 8000 |
| 3600 | 15000 |
