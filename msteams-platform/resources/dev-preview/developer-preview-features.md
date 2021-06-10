---
title: Функции в общедоступных Developer Preview
description: Сведения об особенностях в Microsoft Teams public Developer Preview
ms.topic: reference
localization_priority: Normal
keywords: Функции разработчика команд предварительного просмотра
ms.openlocfilehash: 84683420a5c61bb1eb493f8191bfbcbe97f6fb46
ms.sourcegitcommit: 60561c7cd189c9d6fa5e09e0f2b6c24476f2dff5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/06/2021
ms.locfileid: "52230906"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="13e82-104">Функции в общедоступных Developer Preview для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="13e82-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

> [!NOTE]
> <span data-ttu-id="13e82-105">Эта страница будет обесценяться в июне 2021 г.</span><span class="sxs-lookup"><span data-stu-id="13e82-105">This page will be deprecated in June 2021.</span></span> <span data-ttu-id="13e82-106">Сведения о функциях, доступных для предварительного просмотра разработчика, см. в выпуске [What's new?](~/whats-new.md)</span><span class="sxs-lookup"><span data-stu-id="13e82-106">For information on features available for developer preview, see [What's new?](~/whats-new.md)</span></span>

<span data-ttu-id="13e82-107">Предварительный просмотр разработчика включает следующие новые функции:</span><span class="sxs-lookup"><span data-stu-id="13e82-107">The developer preview includes the following new features:</span></span>

## <a name="app-customization"></a><span data-ttu-id="13e82-108">Настройка приложения</span><span class="sxs-lookup"><span data-stu-id="13e82-108">App customization</span></span>

<span data-ttu-id="13e82-109">Теперь можно определить выбранный набор свойств, которые администратор Teams настроить или ребрендировать в зависимости от необходимости организации.</span><span class="sxs-lookup"><span data-stu-id="13e82-109">You can now define a select set of properties, which a Teams admin can customize or rebrand based on their organization's need.</span></span> <span data-ttu-id="13e82-110">Дополнительные сведения см. в [функции настройки приложения.](~/concepts/design/design-teams-app-overview.md)</span><span class="sxs-lookup"><span data-stu-id="13e82-110">For more information, see [app customization feature](~/concepts/design/design-teams-app-overview.md).</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="13e82-111">Вкладки один вход (SSO)</span><span class="sxs-lookup"><span data-stu-id="13e82-111">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="13e82-112">Теперь вы можете использовать один вход [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) для входа и проверки подлинности пользователя на рабочем столе и мобильном телефоне с помощью Teams JavaScript SDK со страницы веб-контента.</span><span class="sxs-lookup"><span data-stu-id="13e82-112">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="13e82-113">Одним из преимуществ является то, что пользователю никогда не нужно вход; и после того, как они согласились на приложение с помощью своего профиля: они будут автоматически подписаны на вкладку (включая мобильный).</span><span class="sxs-lookup"><span data-stu-id="13e82-113">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="13e82-114">Предварительный просмотр разработчика доступен в манифестных версиях 1.5 и более.</span><span class="sxs-lookup"><span data-stu-id="13e82-114">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="13e82-115">Наша текущая реализация может получить ограниченное Graph API, однако мы предоставляем обходные пути для получения дополнительных API Graph с помощью существующего API проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="13e82-115">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="13e82-116">Вызовы и сетевые боты собраний</span><span class="sxs-lookup"><span data-stu-id="13e82-116">Calls and online meeting bots</span></span>

<span data-ttu-id="13e82-117">С добавлением [API Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true)microsoft для звонков и собраний в Интернете, Microsoft Teams приложения теперь могут взаимодействовать с пользователями с помощью голосовой связи и видео.</span><span class="sxs-lookup"><span data-stu-id="13e82-117">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta&preserve-view=true), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="13e82-118">Эти API позволяют добавлять новые функции приложения, такие как интерактивный голосовой ответ (IVR), управление вызовами и доступ к аудио- и/или видеопотокам в режиме реального времени для звонков и собраний, включая настольный компьютер и общий доступ к приложениям.</span><span class="sxs-lookup"><span data-stu-id="13e82-118">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="13e82-119">Добавлен новый раздел о создании и разработке ботов вызовов и сетевых собраний, начиная с [обзора.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="13e82-119">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>


## <a name="image-enlarge-support"></a><span data-ttu-id="13e82-120">Поддержка расширения изображения</span><span class="sxs-lookup"><span data-stu-id="13e82-120">Image enlarge support</span></span>

<span data-ttu-id="13e82-121">Теперь боты могут указывать, какие изображения, общие в адаптивных Teams, могут быть расширены.</span><span class="sxs-lookup"><span data-stu-id="13e82-121">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="13e82-122">Это полезно для таких сценариев, как обмен подробными пошаговими визуальными руководствами с помощью ботов, которые в противном случае могут быть трудно прочитать пользователям.</span><span class="sxs-lookup"><span data-stu-id="13e82-122">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="13e82-123">Чтобы сделать изображение расширяемым, просто пометить `allowExpand: true` его, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="13e82-123">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="13e82-124">Это приведет Teams веб-или настольного клиента к отрисовке элемента на наведении над изображением, чтобы позволить пользователю расширить изображение.</span><span class="sxs-lookup"><span data-stu-id="13e82-124">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>
