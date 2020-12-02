---
title: Изменение порядка вкладок личных приложений
description: Изменение порядка статических вкладок личного приложения в личном приложении
keywords: Разработка вкладок Teams
ms.openlocfilehash: a8a7c3d23bac98ef1085a8f3443ca0fc92ae0a31
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/02/2020
ms.locfileid: "49554831"
---
# <a name="reorder-personal-app-tabs"></a><span data-ttu-id="bab44-104">Изменение порядка вкладок личных приложений</span><span class="sxs-lookup"><span data-stu-id="bab44-104">Reorder personal app tabs</span></span>

<span data-ttu-id="bab44-105">Начиная с манифеста версии 1,7 разработчики могут переупорядочивать все вкладки в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="bab44-105">Starting with manifest version 1.7 developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="bab44-106">В частности, разработчик может переместить вкладку "Chat Chat" (которая всегда устанавливается по умолчанию в первую позицию) в заголовке вкладки личного приложения.</span><span class="sxs-lookup"><span data-stu-id="bab44-106">In particular, a developer can move the “bot chat” tab (which has always defaulted to the first position) anywhere in the personal app tab header.</span></span> <span data-ttu-id="bab44-107">Мы объявили два зарезервированных ключевых слов Ентитид Tab: "беседы" и "About".</span><span class="sxs-lookup"><span data-stu-id="bab44-107">We’ve declared two reserved tab entityId keywords: “conversations” and “about”.</span></span>

## <a name="moving-the-chatconversation-tab"></a><span data-ttu-id="bab44-108">Перемещение вкладки "чат/беседа"</span><span class="sxs-lookup"><span data-stu-id="bab44-108">Moving the “Chat/Conversation” tab</span></span>

<span data-ttu-id="bab44-109">Если вы создаете робот с областью "Личное", он всегда будет отображаться в первой позиции вкладки личного приложения.</span><span class="sxs-lookup"><span data-stu-id="bab44-109">If you create a bot with a “personal” scope, it will always show up in the first tab position in a personal app.</span></span> <span data-ttu-id="bab44-110">Если вы хотите переместить его в другую позицию, необходимо добавить к манифесту статический объект вкладки с зарезервированным ключевым словом "беседы".</span><span class="sxs-lookup"><span data-stu-id="bab44-110">If you wish to move it to another position, you need to add a static tab object to your manifest with the reserved keyword “conversations”.</span></span> <span data-ttu-id="bab44-111">Когда вы добавляете вкладку "беседы" в массиве "Статиктабс", это место, где будет отображаться вкладка беседа в Интернете и на настольном компьютере.</span><span class="sxs-lookup"><span data-stu-id="bab44-111">Wherever you add the “conversations” tab in the “staticTabs” array, that’s where the conversation tab will appear on web and desktop.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

> [!NOTE]
> <span data-ttu-id="bab44-112">Обратите внимание, что это поведение не отображается на мобильном устройстве, так как личный чат уже имеет выделенное место в личном приложении.</span><span class="sxs-lookup"><span data-stu-id="bab44-112">Note that this behavior is not reflected on mobile since the personal bot chat already has a dedicated place within the personal app.</span></span>

## <a name="moving-the-about-tab"></a><span data-ttu-id="bab44-113">Перемещение вкладки "о программе"</span><span class="sxs-lookup"><span data-stu-id="bab44-113">Moving the “About” tab</span></span>

<span data-ttu-id="bab44-114">Вкладка "о программе" всегда по умолчанию отображается в конце строки заголовка вкладки личного приложения.</span><span class="sxs-lookup"><span data-stu-id="bab44-114">The “About” tab always defaults to the end of the personal app tab header bar.</span></span> <span data-ttu-id="bab44-115">Если вы хотите переместить его в другую позицию, необходимо использовать Ентитид "About".</span><span class="sxs-lookup"><span data-stu-id="bab44-115">If you wish to move it to another position, you need to use the “about” entityId.</span></span>

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
> [!NOTE]
> <span data-ttu-id="bab44-116">Обратите внимание, что вкладка "о программе" не отображается на мобильном устройстве.</span><span class="sxs-lookup"><span data-stu-id="bab44-116">Note that the about tab is not shown on mobile.</span></span>

## <a name="example-code"></a><span data-ttu-id="bab44-117">Пример кода</span><span class="sxs-lookup"><span data-stu-id="bab44-117">Example code</span></span>

```json
{
   "staticTabs":[
      {
         "entityId":"homeTab",
         "name":"Home",
         "contentUrl":"https://www.contoso.com",
         "websiteUrl":" https://www.contoso.com ",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"about",
         "scopes":[
            "personal"
         ]
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```
