---
title: Функции в общедоступных Developer Preview
description: Сведения о функции в общедоступных веб-службах Microsoft Teams Developer Preview
ms.topic: reference
keywords: Функции предварительного просмотра teams для разработчиков
ms.openlocfilehash: 3275ef7ac0d4ba052f417f6e852f48e2fdf267f5
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014357"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="d51de-104">Функции в общедоступных Developer Preview Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="d51de-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="d51de-105">Предварительная версия для разработчиков включает следующие новые возможности:</span><span class="sxs-lookup"><span data-stu-id="d51de-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="d51de-106">Единый вход (SSO) для вкладок</span><span class="sxs-lookup"><span data-stu-id="d51de-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="d51de-107">Теперь вы можете использовать единый вход [(SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) для входа и проверки подлинности пользователя на настольных компьютерах и мобильных устройствах с помощью SDK JavaScript для Teams со страницы веб-контента.</span><span class="sxs-lookup"><span data-stu-id="d51de-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="d51de-108">Одно из преимуществ — это то, что пользователю никогда не нужно в это делать. и после того, как они согласились на использование своего профиля для приложения: они автоматически будут вошел на свою вкладку (включая мобильные устройства).</span><span class="sxs-lookup"><span data-stu-id="d51de-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="d51de-109">Предварительная версия для разработчиков доступна в версиях манифеста 1.5 и более больших версий.</span><span class="sxs-lookup"><span data-stu-id="d51de-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="d51de-110">Наша текущая реализация может получить только ограниченное количество API Graph, но мы предоставляем обходное решение для получения дополнительных API Graph с помощью существующего API проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="d51de-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="d51de-111">Звонки и боты собраний по сети</span><span class="sxs-lookup"><span data-stu-id="d51de-111">Calls and online meeting bots</span></span>

<span data-ttu-id="d51de-112">Благодаря добавлению [API Microsoft Graph](/graph/api/resources/communications-api-overview?view=graph-rest-beta)для звонков и собраний по сети приложения Microsoft Teams теперь могут взаимодействовать с пользователями с помощью голосовой и видеосвязи.</span><span class="sxs-lookup"><span data-stu-id="d51de-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="d51de-113">Эти API позволяют добавлять новые функции приложения, такие как интерактивный голосовой ответ (IVR), управление вызовами и доступ к аудио- и/или видеопотокам в режиме реального времени для звонков и собраний, включая общий доступ к рабочему столу и приложениям.</span><span class="sxs-lookup"><span data-stu-id="d51de-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="d51de-114">Мы добавили новый раздел о создании и разработке ботов для звонков и собраний по сети, начиная с [обзора.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d51de-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="d51de-115">Поддержка увеличения изображения</span><span class="sxs-lookup"><span data-stu-id="d51de-115">Image enlarge support</span></span>

<span data-ttu-id="d51de-116">Теперь боты могут указать, какие изображения, к которым разрешено использовать адаптивные карточки в Teams, могут увеличиваться.</span><span class="sxs-lookup"><span data-stu-id="d51de-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="d51de-117">Это удобно для таких сценариев, как совместное использование подробных пошагового визуального руководства с помощью ботов, которые в противном случае могут быть трудно читать пользователям.</span><span class="sxs-lookup"><span data-stu-id="d51de-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="d51de-118">Чтобы сделать изображение расширяемым, просто помечаем `allowExpand: true` его, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="d51de-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="d51de-119">Это приведет к тому, что веб-клиент Teams или настольный клиент будет отрисовки элемента при наведении курсор на изображение, чтобы пользователь может развернуть изображение.</span><span class="sxs-lookup"><span data-stu-id="d51de-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

