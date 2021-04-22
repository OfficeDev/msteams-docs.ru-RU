---
title: Отправка ID клиента и ИД беседы в заглавные главы запроса бота
description: описывает отправку ID клиента и ИД беседы в заглавные главы запроса бота.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922535"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="f9885-103">Отправка ID клиента и ИД беседы в заглавные главы запроса бота</span><span class="sxs-lookup"><span data-stu-id="f9885-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="f9885-104">Текущие исходяющие запросы на бот не содержат в загоне или URL-адресе никаких сведений, которые помогают ботам маршрутить трафик без распаковки всей полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="f9885-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="f9885-105">Действия отправляются боту по URL-адресу https://<your_domain>/api/messages.</span><span class="sxs-lookup"><span data-stu-id="f9885-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="f9885-106">Получены запросы, чтобы показать в заглавных загонах ИД беседы и ИД клиента.</span><span class="sxs-lookup"><span data-stu-id="f9885-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="f9885-107">Поля загона запроса</span><span class="sxs-lookup"><span data-stu-id="f9885-107">Request header fields</span></span>

<span data-ttu-id="f9885-108">Во все запросы, отправленные ботам, добавляются два нестандартных поля для загона запросов как для асинхронного потока, так и для синхронного потока.</span><span class="sxs-lookup"><span data-stu-id="f9885-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="f9885-109">В следующей таблице заглавные поля запроса и их значения.</span><span class="sxs-lookup"><span data-stu-id="f9885-109">The following table provides the request header fields and their values.</span></span>

| <span data-ttu-id="f9885-110">Ключ поля</span><span class="sxs-lookup"><span data-stu-id="f9885-110">Field key</span></span> | <span data-ttu-id="f9885-111">Значение</span><span class="sxs-lookup"><span data-stu-id="f9885-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="f9885-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="f9885-112">x-ms-conversation-id</span></span> | <span data-ttu-id="f9885-113">Документ беседы, соответствующий действию запроса, если он применим, подтвержден или проверен.</span><span class="sxs-lookup"><span data-stu-id="f9885-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="f9885-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="f9885-114">x-ms-tenant-id</span></span> | <span data-ttu-id="f9885-115">ID клиента, соответствующий диалогу в действии запроса.</span><span class="sxs-lookup"><span data-stu-id="f9885-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="f9885-116">Если в действии не присутствует или не проверяется на стороне службы, то значение пусто.</span><span class="sxs-lookup"><span data-stu-id="f9885-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![Поля загона запроса](~/assets/images/bots/requestheaderfields.png)
