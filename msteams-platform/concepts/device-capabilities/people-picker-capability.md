---
title: Интеграция возможностей выборщика людей
author: Rajeshwari-v
description: Использование SDK Teams JavaScript для интеграции возможностей выборщика людей
keywords: управлением выборщика людей
ms.topic: conceptual
localization_priority: Normal
ms.author: surbhigupta
ms.openlocfilehash: 8399eeb1a088e4b60c466d51c223b9405ebf1711
ms.sourcegitcommit: 059d22c436ee9b07a61561ff71e03e1c23ff40b8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/30/2021
ms.locfileid: "53211643"
---
# <a name="integrate-people-picker-capability"></a><span data-ttu-id="22eed-104">Интеграция возможностей выборщика людей</span><span class="sxs-lookup"><span data-stu-id="22eed-104">Integrate People Picker capability</span></span> 

<span data-ttu-id="22eed-105">Выбор людей — это управление для поиска и выбора людей.</span><span class="sxs-lookup"><span data-stu-id="22eed-105">People Picker is a control to search and select people.</span></span> <span data-ttu-id="22eed-106">Это родной потенциал, доступный в Teams платформе.</span><span class="sxs-lookup"><span data-stu-id="22eed-106">This is a native capability available in Teams platform.</span></span> <span data-ttu-id="22eed-107">Вы можете интегрировать Teams управления входными данными пользователей с веб-приложениями.</span><span class="sxs-lookup"><span data-stu-id="22eed-107">You can integrate Teams native People Picker input control with your web apps.</span></span> <span data-ttu-id="22eed-108">Можно выбрать между одним или несколькими выборами и конфигурациями, например ограничением поиска в чате, каналах или во всей организации.</span><span class="sxs-lookup"><span data-stu-id="22eed-108">You can select between single or multi selection, and configurations, such as limiting search within a chat, channels, or across the entire organization.</span></span>

<span data-ttu-id="22eed-109">Вы можете использовать [Microsoft Teams JavaScript клиента SDK,](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)который предоставляет API для интеграции возможностей выборщика людей `selectPeople` в вашем веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-109">You can use [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true), which provides `selectPeople` API to integrate the People Picker capability within your web app.</span></span> 

## <a name="advantages-of-integrating-people-picker-capability"></a><span data-ttu-id="22eed-110">Преимущества интеграции возможностей выборщика людей</span><span class="sxs-lookup"><span data-stu-id="22eed-110">Advantages of integrating People Picker capability</span></span>

* <span data-ttu-id="22eed-111">Управление выборщиком людей работает во всех Teams, таких как модуль задач, чат, канал, вкладка собраний и личное приложение.</span><span class="sxs-lookup"><span data-stu-id="22eed-111">The People Picker control works in all of Teams surfaces, such as task module, a chat, channel, meeting tab, and personal app.</span></span>
* <span data-ttu-id="22eed-112">Этот контроль позволяет искать и выбирать пользователей в чате, канале или всей организации.</span><span class="sxs-lookup"><span data-stu-id="22eed-112">This control allows you to search for and select users within a chat, channel, or the entire organization.</span></span>
*  <span data-ttu-id="22eed-113">Возможность выборки людей помогает в сценариях, связанных с назначением задач, тегами, уведомлением пользователя.</span><span class="sxs-lookup"><span data-stu-id="22eed-113">The People Picker capability helps with scenarios involving task assignment, tagging, notifying a user.</span></span> 
* <span data-ttu-id="22eed-114">Этот легкодоступный контроль можно использовать в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-114">You can use this readily available control in your web app.</span></span> <span data-ttu-id="22eed-115">Это значительно экономит усилия и время для создания такого управления самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="22eed-115">It saves the effort and time significantly to build such a control on your own.</span></span>

<span data-ttu-id="22eed-116">Необходимо вызвать `selectPeople` API для интеграции управления выборщиком людей в Teams приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-116">You must call the `selectPeople` API to integrate People Picker control in your Teams app.</span></span> <span data-ttu-id="22eed-117">Для эффективной интеграции необходимо иметь представление о фрагменте кода для [вызова](#code-snippet) API.</span><span class="sxs-lookup"><span data-stu-id="22eed-117">For effective integration, you must have an understanding of [code snippet](#code-snippet) for calling the API.</span></span> <span data-ttu-id="22eed-118">Важно ознакомиться с ошибками [ответа API](#error-handling) для обработки ошибок в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-118">It is important to familiarize yourself with the [API response errors](#error-handling) to handle the errors in your web app.</span></span>

> [!NOTE] 
> <span data-ttu-id="22eed-119">В настоящее время Microsoft Teams поддержка возможностей выборщика людей доступна только для мобильных клиентов.</span><span class="sxs-lookup"><span data-stu-id="22eed-119">Currently, Microsoft Teams support for People Picker capability is available for mobile clients only.</span></span>

## <a name="selectpeople-api"></a><span data-ttu-id="22eed-120">`selectPeople` API</span><span class="sxs-lookup"><span data-stu-id="22eed-120">`selectPeople` API</span></span> 

<span data-ttu-id="22eed-121">`selectPeople`API позволяет добавлять Teams в `People Picker input control` веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="22eed-121">`selectPeople` API enables you to add Teams native `People Picker input control` to your web apps.</span></span>  
<span data-ttu-id="22eed-122">Описание API следующим образом:</span><span class="sxs-lookup"><span data-stu-id="22eed-122">The API description is as follows:</span></span>

| <span data-ttu-id="22eed-123">API</span><span class="sxs-lookup"><span data-stu-id="22eed-123">API</span></span>      | <span data-ttu-id="22eed-124">Описание</span><span class="sxs-lookup"><span data-stu-id="22eed-124">Description</span></span>  |
| --- | --- |
|<span data-ttu-id="22eed-125">**selectPeople**</span><span class="sxs-lookup"><span data-stu-id="22eed-125">**selectPeople**</span></span>|<span data-ttu-id="22eed-126">Запускает выбор людей и позволяет пользователю искать и выбирать одного или несколько человек из списка.</span><span class="sxs-lookup"><span data-stu-id="22eed-126">Launches a People Picker and allows the user to search and select one or more people from the list.</span></span><br/><br/><span data-ttu-id="22eed-127">Этот API возвращает ID, имя и адрес электронной почты выбранных пользователей в вызываемом веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-127">This API returns the ID, name and email address of selected users to the calling web app.</span></span><br/><br/><span data-ttu-id="22eed-128">В случае личного приложения управление выполняет поиск по всей организации.</span><span class="sxs-lookup"><span data-stu-id="22eed-128">In case of a personal app, the control searches across the organization.</span></span> <span data-ttu-id="22eed-129">Если приложение добавляется в чат или канал, контекст поиска настраивается в зависимости от сценария.</span><span class="sxs-lookup"><span data-stu-id="22eed-129">If the app is added to a chat or channel, then the search context is configured depending on the scenario.</span></span> <span data-ttu-id="22eed-130">Поиск ограничен членами этого чата, канала или доступен в организации.</span><span class="sxs-lookup"><span data-stu-id="22eed-130">The search is restricted within the members of that chat, channel, or made available across the organization.</span></span>|

<span data-ttu-id="22eed-131">API `selectPeople` поставляется вместе со следующими конфигурациями ввода:</span><span class="sxs-lookup"><span data-stu-id="22eed-131">The `selectPeople` API comes along with following input configurations:</span></span>

|<span data-ttu-id="22eed-132">Параметр Конфигурация</span><span class="sxs-lookup"><span data-stu-id="22eed-132">Configuration parameter</span></span>|<span data-ttu-id="22eed-133">Тип</span><span class="sxs-lookup"><span data-stu-id="22eed-133">Type</span></span>|<span data-ttu-id="22eed-134">Описание</span><span class="sxs-lookup"><span data-stu-id="22eed-134">Description</span></span>| <span data-ttu-id="22eed-135">Значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="22eed-135">Default value</span></span>|
|-----|------|--------------|------|
|`title`| <span data-ttu-id="22eed-136">String</span><span class="sxs-lookup"><span data-stu-id="22eed-136">String</span></span>| <span data-ttu-id="22eed-137">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="22eed-137">It is an optional parameter.</span></span> <span data-ttu-id="22eed-138">Он задает название для управления выборщиком людей.</span><span class="sxs-lookup"><span data-stu-id="22eed-138">It sets title for the People Picker control.</span></span> | <span data-ttu-id="22eed-139">Выбор людей</span><span class="sxs-lookup"><span data-stu-id="22eed-139">Select people</span></span>|
|`setSelected`|<span data-ttu-id="22eed-140">String</span><span class="sxs-lookup"><span data-stu-id="22eed-140">String</span></span>| <span data-ttu-id="22eed-141">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="22eed-141">It is an optional parameter.</span></span> <span data-ttu-id="22eed-142">Необходимо передать AAD-ID людей, которые будут предварительно отбираться.</span><span class="sxs-lookup"><span data-stu-id="22eed-142">You must pass AAD IDs of the people to be preselected.</span></span> <span data-ttu-id="22eed-143">Этот параметр предварительно отбирает людей при запуске управления выборщиком людей.</span><span class="sxs-lookup"><span data-stu-id="22eed-143">This parameter preselects people while launching the People Picker control.</span></span> <span data-ttu-id="22eed-144">В случае единого выбора только первый допустимый пользователь будет предварительно заселяться, игнорируя остальные.</span><span class="sxs-lookup"><span data-stu-id="22eed-144">In case of single selection, only the first valid user is prepopulated ignoring the rest.</span></span> |<span data-ttu-id="22eed-145">Null</span><span class="sxs-lookup"><span data-stu-id="22eed-145">Null</span></span>| 
|`openOrgWideSearchInChatOrChannel`|<span data-ttu-id="22eed-146">Логический</span><span class="sxs-lookup"><span data-stu-id="22eed-146">Boolean</span></span> | <span data-ttu-id="22eed-147">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="22eed-147">It is an optional parameter.</span></span> <span data-ttu-id="22eed-148">Если установлено, что это верно, он запускает выбор людей в широкой области организации, даже если приложение добавлено в чат или канал.</span><span class="sxs-lookup"><span data-stu-id="22eed-148">When it is set to true, it launches the People Picker in organization wide scope even if the app is added to a chat or channel.</span></span> |<span data-ttu-id="22eed-149">Неверно</span><span class="sxs-lookup"><span data-stu-id="22eed-149">False</span></span>|
|`singleSelect`|<span data-ttu-id="22eed-150">Логический</span><span class="sxs-lookup"><span data-stu-id="22eed-150">Boolean</span></span>|<span data-ttu-id="22eed-151">Это необязательный параметр.</span><span class="sxs-lookup"><span data-stu-id="22eed-151">It is an optional parameter.</span></span> <span data-ttu-id="22eed-152">Когда установлено, что это верно, запускается выборщик людей, ограничивающий выбор только для одного пользователя.</span><span class="sxs-lookup"><span data-stu-id="22eed-152">When it is set to true, it launches the People Picker restricting the selection to one user only.</span></span> |<span data-ttu-id="22eed-153">Неверно</span><span class="sxs-lookup"><span data-stu-id="22eed-153">False</span></span>|

<span data-ttu-id="22eed-154">На следующем изображении показана возможность выборки людей в примере веб-приложения:</span><span class="sxs-lookup"><span data-stu-id="22eed-154">The following image depicts the experience of People Picker capability in a sample web app:</span></span>

![Опыт работы веб-приложения с возможностями выборщика людей](../../assets/images/tabs/people-picker-control-capability.png)

### <a name="code-snippet"></a><span data-ttu-id="22eed-156">Фрагмент кода</span><span class="sxs-lookup"><span data-stu-id="22eed-156">Code snippet</span></span>

<span data-ttu-id="22eed-157">**Вызов `selectPeople` API** для выбора людей из списка:</span><span class="sxs-lookup"><span data-stu-id="22eed-157">**Calling `selectPeople` API** to select people from a list:</span></span>

```javascript
 microsoftTeams.people.selectPeople((error: microsoftTeams.SdkError, people: microsoftTeams.people.PeoplePickerResult[]) => 
 {
    if (error) 
    {
        if (error.message) 
           {
             alert(" ErrorCode: " + error.errorCode + error.message);
           }
            else 
            {
              alert(" ErrorCode: " + error.errorCode);
            }
      }
    if (people)
     {
            output(" People length: " + people.length + " " + JSON.stringify(people));
      }
  });
```

## <a name="error-handling"></a><span data-ttu-id="22eed-158">Обработка ошибок</span><span class="sxs-lookup"><span data-stu-id="22eed-158">Error handling</span></span>

<span data-ttu-id="22eed-159">Необходимо обеспечить надлежащее обработку ошибок в веб-приложении.</span><span class="sxs-lookup"><span data-stu-id="22eed-159">You must ensure to handle the errors appropriately in your web app.</span></span> <span data-ttu-id="22eed-160">В следующей таблице перечислены коды ошибок и условия, при которых создаются ошибки:</span><span class="sxs-lookup"><span data-stu-id="22eed-160">The following table lists the error codes and the conditions under which the errors are generated:</span></span> 

|<span data-ttu-id="22eed-161">Код ошибки</span><span class="sxs-lookup"><span data-stu-id="22eed-161">Error code</span></span> |  <span data-ttu-id="22eed-162">Имя ошибки</span><span class="sxs-lookup"><span data-stu-id="22eed-162">Error name</span></span>     | <span data-ttu-id="22eed-163">Condition</span><span class="sxs-lookup"><span data-stu-id="22eed-163">Condition</span></span>|
| --------- | --------------- | -------- |
| <span data-ttu-id="22eed-164">**100**</span><span class="sxs-lookup"><span data-stu-id="22eed-164">**100**</span></span> | <span data-ttu-id="22eed-165">NOT_SUPPORTED_ON_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="22eed-165">NOT_SUPPORTED_ON_PLATFORM</span></span> | <span data-ttu-id="22eed-166">API не поддерживается на текущей платформе.</span><span class="sxs-lookup"><span data-stu-id="22eed-166">API is not supported on the current platform.</span></span>|
| <span data-ttu-id="22eed-167">**500**</span><span class="sxs-lookup"><span data-stu-id="22eed-167">**500**</span></span> | <span data-ttu-id="22eed-168">INTERNAL_ERROR</span><span class="sxs-lookup"><span data-stu-id="22eed-168">INTERNAL_ERROR</span></span> | <span data-ttu-id="22eed-169">Внутренняя ошибка встречается при запуске выборщика людей.</span><span class="sxs-lookup"><span data-stu-id="22eed-169">Internal error is encountered while launching People Picker.</span></span>|
| <span data-ttu-id="22eed-170">**4000**</span><span class="sxs-lookup"><span data-stu-id="22eed-170">**4000**</span></span> | <span data-ttu-id="22eed-171">INVALID_ARGUMENTS</span><span class="sxs-lookup"><span data-stu-id="22eed-171">INVALID_ARGUMENTS</span></span> | <span data-ttu-id="22eed-172">API вызывается с неправильными или недостаточными обязательными аргументами.</span><span class="sxs-lookup"><span data-stu-id="22eed-172">API is invoked with wrong or insufficient mandatory arguments.</span></span>|
| <span data-ttu-id="22eed-173">**8000**</span><span class="sxs-lookup"><span data-stu-id="22eed-173">**8000**</span></span> | <span data-ttu-id="22eed-174">USER_ABORT</span><span class="sxs-lookup"><span data-stu-id="22eed-174">USER_ABORT</span></span> |<span data-ttu-id="22eed-175">Пользователь отменил операцию.</span><span class="sxs-lookup"><span data-stu-id="22eed-175">User cancelled the operation.</span></span>|
| <span data-ttu-id="22eed-176">**9000**</span><span class="sxs-lookup"><span data-stu-id="22eed-176">**9000**</span></span> | <span data-ttu-id="22eed-177">OLD_PLATFORM</span><span class="sxs-lookup"><span data-stu-id="22eed-177">OLD_PLATFORM</span></span> | <span data-ttu-id="22eed-178">Пользователь находится на старой сборке платформы, где нет реализации API.</span><span class="sxs-lookup"><span data-stu-id="22eed-178">User is on old platform build where implementation of the API is not present.</span></span>  <span data-ttu-id="22eed-179">Обновление сборки устраняет проблему.</span><span class="sxs-lookup"><span data-stu-id="22eed-179">Upgrading the build resolves the issue.</span></span>|

## <a name="see-also"></a><span data-ttu-id="22eed-180">См. также</span><span class="sxs-lookup"><span data-stu-id="22eed-180">See also</span></span>

* [<span data-ttu-id="22eed-181">Интеграция возможностей мультимедиа в Teams</span><span class="sxs-lookup"><span data-stu-id="22eed-181">Integrate media capabilities in Teams</span></span>](mobile-camera-image-permissions.md)
* [<span data-ttu-id="22eed-182">Интеграция QR-кода или возможности сканера штрихкодов в Teams</span><span class="sxs-lookup"><span data-stu-id="22eed-182">Integrate QR code or barcode scanner capability in Teams</span></span>](qr-barcode-scanner-capability.md)
* [<span data-ttu-id="22eed-183">Интеграция возможностей расположения в Teams</span><span class="sxs-lookup"><span data-stu-id="22eed-183">Integrate location capabilities in Teams</span></span>](location-capability.md)
