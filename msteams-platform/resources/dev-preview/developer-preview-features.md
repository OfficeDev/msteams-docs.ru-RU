---
title: Возможности общедоступной предварительной версии для разработчиков
description: Описание возможностей общедоступной предварительной версии для разработчиков Microsoft Teams
keywords: Функции teams Preview для разработчиков
ms.openlocfilehash: e607a6c65253a5fd94f8a805f1264a567bb8fd24
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819177"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="0cbc4-104">Возможности общедоступной предварительной версии для разработчиков для Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0cbc4-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="0cbc4-105">В предварительной версии для разработчиков включены следующие новые функции.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-105">The developer preview includes the following new features:</span></span>

## <a name="adaptive-cards-v12-support"></a><span data-ttu-id="0cbc4-106">Поддержка адаптивных картинок версии 1.2</span><span class="sxs-lookup"><span data-stu-id="0cbc4-106">Adaptive cards v1.2 support</span></span>

<span data-ttu-id="0cbc4-107">Поддержка [адаптивных карточек версии 1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) в Teams теперь доступна общественности.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-107">Support for [Adaptive cards v1.2](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0) in Teams is now available to the general public.</span></span> <span data-ttu-id="0cbc4-108">Однако [элементы мультимедиа в настоящее](https://adaptivecards.io/explorer/Media.html) время не поддерживаются в адаптивных картах версии 1.2 на платформе Teams.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-108">However, [Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="0cbc4-109">Единый вход (SSO)</span><span class="sxs-lookup"><span data-stu-id="0cbc4-109">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="0cbc4-110">Теперь вы можете [использовать единый вход для](~/tabs/how-to/authentication/auth-aad-sso.md) входа и проверки подлинности пользователя на настольных компьютерах и мобильных устройствах с помощью пакета SDK JavaScript для Teams на странице веб-контента.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-110">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="0cbc4-111">Одним из преимуществ является то, что пользователю никогда не приходится выполнять вход; и после согласия приложения с помощью своего профиля он будет автоматически входить на свою вкладку (втом числе мобильных устройств).</span><span class="sxs-lookup"><span data-stu-id="0cbc4-111">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="0cbc4-112">Наша предварительная версия для разработчиков доступна в версиях манифестов 1.5 и более поздних версиях.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-112">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="0cbc4-113">Наша текущая реализация может получить только ограниченный объем API Graph, но мы предоставляем обходное решение, чтобы получить дополнительные API Graph с помощью нашего существующего API аутентификации.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-113">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="0cbc4-114">Вызовы и боты собраний по сети</span><span class="sxs-lookup"><span data-stu-id="0cbc4-114">Calls and online meeting bots</span></span>

<span data-ttu-id="0cbc4-115">Добавление API [Microsoft Graph для звонков](/graph/api/resources/communications-api-overview?view=graph-rest-beta)и собраний по сети позволяет приложениям Microsoft Teams полнофункционально взаимодействовать с пользователями с помощью голоса и видео.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-115">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="0cbc4-116">Эти API позволяют добавлять новые функции приложения, такие как IVR, управление звонками и доступ к аудио- и /или видеопотокам в реальном времени для звонков и собраний, включая общий доступ к рабочему столу и приложениям.</span><span class="sxs-lookup"><span data-stu-id="0cbc4-116">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="0cbc4-117">Мы добавили новый раздел о том, как создавать и разрабатывать звонки и боты собраний по сети, начиная с [обзора.](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)</span><span class="sxs-lookup"><span data-stu-id="0cbc4-117">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>
