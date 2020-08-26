---
title: Возможности в общедоступной предварительной версии для разработчиков
description: Сведения о функциях в общедоступной предварительной версии Microsoft Teams
keywords: функции разработчиков Team Preview
ms.openlocfilehash: 773e0334bddf45b7b86d31329b99607f3b70c534
ms.sourcegitcommit: 52732714105fac07c331cd31e370a9685f45d3e1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/25/2020
ms.locfileid: "46874844"
---
# <a name="features-in-the-public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="0210c-104">Функции общедоступной предварительной версии для разработчиков Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0210c-104">Features in the Public Developer Preview for Microsoft Teams</span></span>

<span data-ttu-id="0210c-105">Предварительная версия для разработчиков содержит следующие новые функции:</span><span class="sxs-lookup"><span data-stu-id="0210c-105">The developer preview includes the following new features:</span></span>

## <a name="tabs-single-sign-on-sso"></a><span data-ttu-id="0210c-106">Вкладки с единым входом (SSO)</span><span class="sxs-lookup"><span data-stu-id="0210c-106">Tabs single sign-on (SSO)</span></span>

<span data-ttu-id="0210c-107">Теперь вы можете использовать [единый вход (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) для входа и проверки подлинности пользователя на настольных компьютерах и мобильных устройств с помощью SDK TEAMs SDK на странице веб-содержимого.</span><span class="sxs-lookup"><span data-stu-id="0210c-107">You can now use [single sign-on (SSO)](~/tabs/how-to/authentication/auth-aad-sso.md) to login and authenticate a user on desktop and mobile using the Teams JavaScript SDK from a web content page.</span></span> <span data-ttu-id="0210c-108">Одним из преимуществ является то, что пользователь не может войти в систему; и после того, как они будут отправлены в приложение с помощью своего профиля: они будут автоматически входить на свои вкладки (в том числе на мобильные устройства).</span><span class="sxs-lookup"><span data-stu-id="0210c-108">One of the benefits is that a user never has to sign-in; and once they've consented to the app using their profile: they will automatically be signed-in to their tab (including mobile).</span></span>

<span data-ttu-id="0210c-109">Предварительная версия для разработчиков доступна в версиях манифестов 1,5 и выше.</span><span class="sxs-lookup"><span data-stu-id="0210c-109">Our developer preview is available in manifest versions 1.5 and greater.</span></span> <span data-ttu-id="0210c-110">Наша текущая реализация может только получить ограниченный объем API Graph, но мы предоставляем обходной путь для получения дополнительных API Graph, использующих существующий API проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="0210c-110">Our current implementation can only get a limited amount of Graph APIs, however we provide a workaround to get additional Graph APIs using our existing authentication API.</span></span>

## <a name="calls-and-online-meeting-bots"></a><span data-ttu-id="0210c-111">Звонки и собрания по сети Боты</span><span class="sxs-lookup"><span data-stu-id="0210c-111">Calls and online meeting bots</span></span>

<span data-ttu-id="0210c-112">С добавлением [API Microsoft Graph для звонков и собраний по сети](/graph/api/resources/communications-api-overview?view=graph-rest-beta)приложения Microsoft Teams теперь могут взаимодействовать с пользователями с помощью голосовых и видеоконференций.</span><span class="sxs-lookup"><span data-stu-id="0210c-112">With the addition of [Microsoft Graph APIs for calls and online meetings](/graph/api/resources/communications-api-overview?view=graph-rest-beta), Microsoft Teams apps can now interact with users in rich ways using voice and video.</span></span> <span data-ttu-id="0210c-113">Эти API позволяют добавлять новые функции приложения, такие как интерактивный голосовой отклик (IVR), контроль звонков и доступ к потокам аудио-и видеоданных в режиме реального времени для звонков и собраний, в том числе для общего доступа к рабочему столу и приложениям.</span><span class="sxs-lookup"><span data-stu-id="0210c-113">These APIs allow you to add new app features such as interactive voice response (IVR), call control, and access to real-time audio and/or video streams for calls and meetings, including desktop and app sharing.</span></span>

<span data-ttu-id="0210c-114">Мы добавили новый раздел о том, как создавать и разрабатывать звонки и собрания по сети Боты, начиная с [обзора](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0210c-114">We've added a new section on how to create and develop calls and online meetings bots, starting with the [overview](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span>

## <a name="image-enlarge-support"></a><span data-ttu-id="0210c-115">Поддержка увеличения изображения</span><span class="sxs-lookup"><span data-stu-id="0210c-115">Image enlarge support</span></span>

<span data-ttu-id="0210c-116">Теперь в боты можно указать, какие изображения, используемые в функциях адаптивных карт в Teams, могут быть увеличены.</span><span class="sxs-lookup"><span data-stu-id="0210c-116">It is now possible for bots to indicate which images shared in Adaptive Cards in Teams are allowed to be enlarged.</span></span> <span data-ttu-id="0210c-117">Это полезно для таких сценариев, как совместное использование подробных визуальных руководств с помощью Боты, которые могут быть трудно читать для пользователей в ином случае.</span><span class="sxs-lookup"><span data-stu-id="0210c-117">This is useful for scenarios like sharing detailed step-by-step visual guides via bots which might be hard to read for users otherwise.</span></span> <span data-ttu-id="0210c-118">Чтобы сделать изображение расширяемым, пометьте его `allowExpand: true` как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="0210c-118">To make an image expandable, just flag it `allowExpand: true` as shown below.</span></span>

```json
    {
      "type": "Image",
      "url": "https://picsum.photos/200/200?image=110",
      "msTeams": {
        "allowExpand": true
      }
    }
```
<span data-ttu-id="0210c-119">Это приведет к тому, что веб-клиент Teams или настольный клиент будет отображать элемент, находящийся на изображении, чтобы разрешить пользователю развернуть изображение.</span><span class="sxs-lookup"><span data-stu-id="0210c-119">This will cause Teams web/desktop client to render an element on hover over the image to allow the user to expand the image.</span></span>

