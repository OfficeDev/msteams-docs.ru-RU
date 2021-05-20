---
title: Отправить идентификатор клиента и идентификатор разговора в заготовки запроса бота
description: описывает, как отправить идентификатор клиента и идентификатор разговора на заготовки запроса бота.
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: 76f667453114ab202d43217b9a4c01a6d14cc1a8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565895"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a><span data-ttu-id="1b3e8-103">Отправить идентификатор клиента и идентификатор разговора в заготовки запроса бота</span><span class="sxs-lookup"><span data-stu-id="1b3e8-103">Send tenant ID and conversation ID to the request headers of the bot</span></span>

<span data-ttu-id="1b3e8-104">Текущие исходящие запросы боту не содержат в заголовке или URL никакой информации, которая помогает ботам маршрутить трафик без распаковки всей полезной нагрузки.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-104">The current outgoing requests to the bot do not contain in the header or URL any information that helps bots route the traffic without unpacking the entire payload.</span></span> <span data-ttu-id="1b3e8-105">Действия отправляются боту через URL-адрес, похожий на https://<your_domain>/api/messages.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-105">The activities are sent to the bot through a URL similar to https://<your_domain>/api/messages.</span></span> <span data-ttu-id="1b3e8-106">По поступали запросы на показ идентификатора разговора и идентификатора арендатора в заготовки.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-106">Requests are received to show the conversation ID and tenant ID in the headers.</span></span>

## <a name="request-header-fields"></a><span data-ttu-id="1b3e8-107">Запрос полей заголовка</span><span class="sxs-lookup"><span data-stu-id="1b3e8-107">Request header fields</span></span>

<span data-ttu-id="1b3e8-108">Ко всем запросам, отправленным ботам, добавляются два нестандартных поля заголовка запросов как для асинхронного потока, так и для синхронного потока.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-108">Two non-standard request header fields are added to all the requests sent to bots, for both asynchronous flow and synchronous flow.</span></span> <span data-ttu-id="1b3e8-109">В следующей таблице приведены поля заголовка запроса и их значения:</span><span class="sxs-lookup"><span data-stu-id="1b3e8-109">The following table provides the request header fields and their values:</span></span>

| <span data-ttu-id="1b3e8-110">Полевой ключ</span><span class="sxs-lookup"><span data-stu-id="1b3e8-110">Field key</span></span> | <span data-ttu-id="1b3e8-111">Значение</span><span class="sxs-lookup"><span data-stu-id="1b3e8-111">Value</span></span> |
|----------------|-----------------|
| <span data-ttu-id="1b3e8-112">x-ms-conversation-id</span><span class="sxs-lookup"><span data-stu-id="1b3e8-112">x-ms-conversation-id</span></span> | <span data-ttu-id="1b3e8-113">Идентификатор разговора, соответствующий активности запроса, если это применимо и подтверждено или проверено.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-113">The conversation ID corresponding to the request activity if applicable and confirmed or verified.</span></span> |
| <span data-ttu-id="1b3e8-114">x-ms-tenant-id</span><span class="sxs-lookup"><span data-stu-id="1b3e8-114">x-ms-tenant-id</span></span> | <span data-ttu-id="1b3e8-115">Идентификатор арендатора, соответствующий разговору в действии запроса.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-115">The tenant ID corresponding to the conversation in the request activity.</span></span> |

<span data-ttu-id="1b3e8-116">Если идентификатор клиента или идентификатора разговора не присутствует в действии или не был проверен на стороне службы, значение пусто.</span><span class="sxs-lookup"><span data-stu-id="1b3e8-116">If the tenant or conversation ID is not present in the activity or was not validated on the service side, the value is empty.</span></span>

![Запрос полей заголовка](~/assets/images/bots/requestheaderfields.png)
