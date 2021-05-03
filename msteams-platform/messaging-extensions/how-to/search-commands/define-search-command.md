---
title: Определение команд поиска расширения обмена сообщениями
author: clearab
description: Определение команд поиска расширения обмена сообщениями для Microsoft Teams приложений.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 19f1fdf7bd4efdbb0de11d1abad341ec24bc27bd
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696809"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="59385-103">Определение команд поиска расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="59385-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="59385-104">Команды поиска расширения обмена сообщениями позволяют пользователям искать внешние системы и вставлять результаты этого поиска в сообщение в виде карточки.</span><span class="sxs-lookup"><span data-stu-id="59385-104">Messaging extension search commands allow users to search external systems and insert the results of that search into a message in the form of a card.</span></span> <span data-ttu-id="59385-105">В этом документе приводятся руководства по выбору расположения ссылок команды поиска и добавлению команды поиска в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="59385-105">This document guides you on how to select  search command invoke locations, and add the search command to your app manifest.</span></span>

> [!NOTE]
> <span data-ttu-id="59385-106">Ограничение размера карты результатов — 28 КБ.</span><span class="sxs-lookup"><span data-stu-id="59385-106">The result card size limit is 28 KB.</span></span> <span data-ttu-id="59385-107">Карта не отправляется, если ее размер превышает 28 КБ.</span><span class="sxs-lookup"><span data-stu-id="59385-107">The card is not sent if its size exceeds 28 KB.</span></span>

## <a name="select-search-command-invoke-locations"></a><span data-ttu-id="59385-108">Выберите расположения команд поиска, вызываемой</span><span class="sxs-lookup"><span data-stu-id="59385-108">Select search command invoke locations</span></span>

<span data-ttu-id="59385-109">Команда поиска вызывается из любого из следующих местоположений:</span><span class="sxs-lookup"><span data-stu-id="59385-109">The search command is invoked from any one or both of the following locations:</span></span>

* <span data-ttu-id="59385-110">Область составить сообщение. Кнопки в нижней части области составить сообщение.</span><span class="sxs-lookup"><span data-stu-id="59385-110">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="59385-111">Командная шкатулка: @mentioning в командном окне.</span><span class="sxs-lookup"><span data-stu-id="59385-111">Command box: By @mentioning in the command box.</span></span>

<span data-ttu-id="59385-112">При вызове команды поиска из области составить сообщение пользователь отправляет результаты в беседу.</span><span class="sxs-lookup"><span data-stu-id="59385-112">When search command is invoked from the compose message area, the user sends the results to the conversation.</span></span> <span data-ttu-id="59385-113">Когда он вызывается из командного окна, пользователь взаимодействует с результативной картой или копирует ее для использования в другом месте.</span><span class="sxs-lookup"><span data-stu-id="59385-113">When it is invoked from the command box, the user interacts with the resulting card, or copies it for use elsewhere.</span></span>

<span data-ttu-id="59385-114">На следующем изображении отображаются расположения ссылок команды поиска:</span><span class="sxs-lookup"><span data-stu-id="59385-114">The following image displays the invoke locations of the search command:</span></span>

![Команда поиска вызывает расположения](~/assets/images/messaging-extension/search-command-invoke-locations.png)

## <a name="add-the-search-command-to-your-app-manifest"></a><span data-ttu-id="59385-116">Добавление команды поиска в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="59385-116">Add the search command to your app manifest</span></span>

<span data-ttu-id="59385-117">Чтобы добавить команду поиска в манифест приложения, необходимо добавить новый объект на верхний уровень `composeExtension` манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="59385-117">To add the search command to your app manifest, you must add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="59385-118">Вы можете добавить команду поиска либо с помощью App Studio, либо вручную.</span><span class="sxs-lookup"><span data-stu-id="59385-118">You can add the search command either with the help of App Studio, or manually.</span></span>

### <a name="create-a-search-command-using-app-studio"></a><span data-ttu-id="59385-119">Создание команды поиска с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="59385-119">Create a search command using App Studio</span></span>

<span data-ttu-id="59385-120">Обязательным условием для создания команды поиска является то, что вы уже должны создать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="59385-120">The prerequisite to create a search command is that you must already have created a messaging extension.</span></span> <span data-ttu-id="59385-121">Сведения о создании расширения обмена сообщениями см. в сообщении о создании расширения [обмена сообщениями.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="59385-121">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="59385-122">**Создание команды поиска**</span><span class="sxs-lookup"><span data-stu-id="59385-122">**To create a search command**</span></span>

1. <span data-ttu-id="59385-123">Откройте **App Studio** Microsoft Teams клиента и выберите вкладку Редактор **Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="59385-123">Open **App Studio** from the Microsoft Teams client, and select the **Manifest Editor** tab.</span></span>
1.  <span data-ttu-id="59385-124">Если вы уже создали пакет приложений в **App Studio,** выберите из списка.</span><span class="sxs-lookup"><span data-stu-id="59385-124">If you already created your app package in **App Studio**, select from the list.</span></span> <span data-ttu-id="59385-125">Если вы не создали пакет приложений, импортировать существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="59385-125">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="59385-126">После импорта пакета приложений выберите **расширения обмена сообщениями** в статье **Capabilities.**</span><span class="sxs-lookup"><span data-stu-id="59385-126">After importing app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="59385-127">Вы получите всплывающее окно, чтобы настроить расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="59385-127">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="59385-128">Выберите **Настройка в** окне, чтобы включить расширение обмена сообщениями в приложение.</span><span class="sxs-lookup"><span data-stu-id="59385-128">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="59385-129">На следующем изображении отображается страница расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="59385-129">The following image displays the messaging extension set up page:</span></span> 

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>

1. <span data-ttu-id="59385-130">Для создания расширения обмена сообщениями необходим зарегистрированный бот Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="59385-130">To create the messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="59385-131">Можно использовать существующий бот или создать новый бот.</span><span class="sxs-lookup"><span data-stu-id="59385-131">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="59385-132">Выберите **создание нового варианта бота,** назови имя нового бота и выберите **Create**.</span><span class="sxs-lookup"><span data-stu-id="59385-132">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="59385-133">На следующем изображении отображается создание бота для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="59385-133">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="59385-134">Выберите **Добавить** в **разделе Команда** страницы расширения обмена сообщениями, чтобы включить команды, которые решают поведение расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="59385-134">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="59385-135">На следующем изображении отображается добавление команд для расширения обмена сообщениями:</span><span class="sxs-lookup"><span data-stu-id="59385-135">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>
1. <span data-ttu-id="59385-136">Выберите **Разрешить пользователям запрашивать у службы сведения и вставить их в сообщение.**</span><span class="sxs-lookup"><span data-stu-id="59385-136">Select **Allow users to query your service for information and insert that into a message**.</span></span> <span data-ttu-id="59385-137">На следующем изображении отображается выбор параметров команды поиска:</span><span class="sxs-lookup"><span data-stu-id="59385-137">The following image displays the search command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-parameter-selection.png" alt="search command parameter selection" width="500"/>

1. <span data-ttu-id="59385-138">Добавление **командного и** **заголовок**.</span><span class="sxs-lookup"><span data-stu-id="59385-138">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="59385-139">Выберите расположение, на котором должна вызываться команда поиска.</span><span class="sxs-lookup"><span data-stu-id="59385-139">Select the location from where your search command must be invoked.</span></span> <span data-ttu-id="59385-140">Выбор сообщения **в** настоящее время не изменяет поведение команды поиска.</span><span class="sxs-lookup"><span data-stu-id="59385-140">Selecting **message** does not currently alter the behavior of your search command.</span></span> <span data-ttu-id="59385-141">На следующем изображении отображается расположение вызова команды поиска:</span><span class="sxs-lookup"><span data-stu-id="59385-141">The following image displays the search command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/search-command-invoke-location-selection.png" alt="search command invoke location selection]" width="500"/>

1. <span data-ttu-id="59385-142">Добавьте параметр поиска и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="59385-142">Add your search parameter and select **Save**.</span></span>

### <a name="create-a-search-command-manually"></a><span data-ttu-id="59385-143">Создание команды поиска вручную</span><span class="sxs-lookup"><span data-stu-id="59385-143">Create a search command manually</span></span> 

<span data-ttu-id="59385-144">Чтобы вручную добавить команду поиска расширения обмена сообщениями в манифест приложения, необходимо добавить в массив объектов следующие `composeExtension.commands` параметры:</span><span class="sxs-lookup"><span data-stu-id="59385-144">To manually add your messaging extension search command to your app manifest, you must add the following parameters to your `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="59385-145">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="59385-145">Property name</span></span> | <span data-ttu-id="59385-146">Назначение</span><span class="sxs-lookup"><span data-stu-id="59385-146">Purpose</span></span> | <span data-ttu-id="59385-147">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="59385-147">Required?</span></span> | <span data-ttu-id="59385-148">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="59385-148">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="59385-149">Это свойство — уникальный ID, который назначается команде поиска.</span><span class="sxs-lookup"><span data-stu-id="59385-149">This property is an unique ID that you assign to search command.</span></span> <span data-ttu-id="59385-150">Запрос пользователя включает этот ID.</span><span class="sxs-lookup"><span data-stu-id="59385-150">The user request includes this ID.</span></span> | <span data-ttu-id="59385-151">Да</span><span class="sxs-lookup"><span data-stu-id="59385-151">Yes</span></span> | <span data-ttu-id="59385-152">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-152">1.0</span></span> |
| `title` | <span data-ttu-id="59385-153">Это свойство — командное имя.</span><span class="sxs-lookup"><span data-stu-id="59385-153">This property is a command name.</span></span> <span data-ttu-id="59385-154">Это значение отображается в пользовательском интерфейсе (пользовательском интерфейсе).</span><span class="sxs-lookup"><span data-stu-id="59385-154">This value appears in the user interface (UI).</span></span> | <span data-ttu-id="59385-155">Да</span><span class="sxs-lookup"><span data-stu-id="59385-155">Yes</span></span> | <span data-ttu-id="59385-156">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-156">1.0</span></span> |
| `description` | <span data-ttu-id="59385-157">Это свойство — текст справки, указывающий, что делает эта команда.</span><span class="sxs-lookup"><span data-stu-id="59385-157">This property is a help text indicating what this command does.</span></span> <span data-ttu-id="59385-158">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="59385-158">This value appears in the UI.</span></span> | <span data-ttu-id="59385-159">Да</span><span class="sxs-lookup"><span data-stu-id="59385-159">Yes</span></span> | <span data-ttu-id="59385-160">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-160">1.0</span></span> |
| `type` | <span data-ttu-id="59385-161">Это свойство должно быть `query` .</span><span class="sxs-lookup"><span data-stu-id="59385-161">This property must be a `query`.</span></span> | <span data-ttu-id="59385-162">Нет</span><span class="sxs-lookup"><span data-stu-id="59385-162">No</span></span> | <span data-ttu-id="59385-163">1.4</span><span class="sxs-lookup"><span data-stu-id="59385-163">1.4</span></span> |
|`initialRun` | <span data-ttu-id="59385-164">Если это свойство заданной для **true,** это указывает на то, что эта команда должна быть выполнена, как только пользователь выберет эту команду в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="59385-164">If this property is set to **true**, it indicates this command should be executed as soon as the user selects this command in the UI.</span></span> | <span data-ttu-id="59385-165">Нет</span><span class="sxs-lookup"><span data-stu-id="59385-165">No</span></span> | <span data-ttu-id="59385-166">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-166">1.0</span></span> |
| `context` | <span data-ttu-id="59385-167">Это свойство — необязательный массив значений, определяя контекст, в котором доступно действие поиска.</span><span class="sxs-lookup"><span data-stu-id="59385-167">This property is an optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="59385-168">Возможные значения — `message`, `compose` и `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="59385-168">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="59385-169">Значение по умолчанию: `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="59385-169">The default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="59385-170">Нет</span><span class="sxs-lookup"><span data-stu-id="59385-170">No</span></span> | <span data-ttu-id="59385-171">1.5</span><span class="sxs-lookup"><span data-stu-id="59385-171">1.5</span></span> |

<span data-ttu-id="59385-172">Необходимо добавить сведения о параметре поиска, который определяет текст, видимый пользователю в Teams клиенте.</span><span class="sxs-lookup"><span data-stu-id="59385-172">You must add the details of the search parameter, that defines the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="59385-173">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="59385-173">Property name</span></span> | <span data-ttu-id="59385-174">Назначение</span><span class="sxs-lookup"><span data-stu-id="59385-174">Purpose</span></span> | <span data-ttu-id="59385-175">Требуется?</span><span class="sxs-lookup"><span data-stu-id="59385-175">Is required?</span></span> | <span data-ttu-id="59385-176">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="59385-176">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="59385-177">Это свойство определяет статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="59385-177">This property defines a static list of parameters for the command.</span></span> | <span data-ttu-id="59385-178">Нет</span><span class="sxs-lookup"><span data-stu-id="59385-178">No</span></span> | <span data-ttu-id="59385-179">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-179">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="59385-180">Это свойство описывает имя параметра.</span><span class="sxs-lookup"><span data-stu-id="59385-180">This property describes the name of the parameter.</span></span> <span data-ttu-id="59385-181">Это отправляется в службу в запросе пользователя.</span><span class="sxs-lookup"><span data-stu-id="59385-181">This is sent to your service in the user request.</span></span> | <span data-ttu-id="59385-182">Да</span><span class="sxs-lookup"><span data-stu-id="59385-182">Yes</span></span> | <span data-ttu-id="59385-183">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-183">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="59385-184">Это свойство описывает цели параметра или пример необходимого значения.</span><span class="sxs-lookup"><span data-stu-id="59385-184">This property describes the parameter’s purposes or example of the value that must be provided.</span></span> <span data-ttu-id="59385-185">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="59385-185">This value appears in the UI.</span></span> | <span data-ttu-id="59385-186">Да</span><span class="sxs-lookup"><span data-stu-id="59385-186">Yes</span></span> | <span data-ttu-id="59385-187">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-187">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="59385-188">Это свойство — короткое удобное название параметра или метка.</span><span class="sxs-lookup"><span data-stu-id="59385-188">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="59385-189">Да</span><span class="sxs-lookup"><span data-stu-id="59385-189">Yes</span></span> | <span data-ttu-id="59385-190">1.0</span><span class="sxs-lookup"><span data-stu-id="59385-190">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="59385-191">Это свойство задалось типу требуемого ввода.</span><span class="sxs-lookup"><span data-stu-id="59385-191">This property is set to the type of the input required.</span></span> <span data-ttu-id="59385-192">Возможные `text` значения: `textarea` , , , , `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="59385-192">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="59385-193">По умолчанию `text` установлено значение .</span><span class="sxs-lookup"><span data-stu-id="59385-193">Default is set to `text`.</span></span> | <span data-ttu-id="59385-194">Нет</span><span class="sxs-lookup"><span data-stu-id="59385-194">No</span></span> | <span data-ttu-id="59385-195">1.4</span><span class="sxs-lookup"><span data-stu-id="59385-195">1.4</span></span> |

#### <a name="example"></a><span data-ttu-id="59385-196">Пример</span><span class="sxs-lookup"><span data-stu-id="59385-196">Example</span></span>

<span data-ttu-id="59385-197">В следующем разделе приводится пример простого манифеста приложения объекта, определяющий `composeExtensions` команду поиска:</span><span class="sxs-lookup"><span data-stu-id="59385-197">Following section is an example of the simple app manifest of the `composeExtensions` object defining a search command:</span></span> 

```json
{
...
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [{
          "id": "searchCmd",
          "description": "Search Bing for information on the web",
          "title": "Search",
          "initialRun": true,
          "parameters": [{
            "name": "searchKeyword",
            "description": "Enter your search keywords",
            "title": "Keywords"
          }]
        }
      ]
    }
  ],
...
}
```
<span data-ttu-id="59385-198">Полный манифест приложения см. в [схеме манифеста Приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="59385-198">For the complete app manifest, see [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="59385-199">Пример кода</span><span class="sxs-lookup"><span data-stu-id="59385-199">Code sample</span></span>

| <span data-ttu-id="59385-200">Имя образца</span><span class="sxs-lookup"><span data-stu-id="59385-200">Sample Name</span></span>           | <span data-ttu-id="59385-201">Описание</span><span class="sxs-lookup"><span data-stu-id="59385-201">Description</span></span> | <span data-ttu-id="59385-202">.NET</span><span class="sxs-lookup"><span data-stu-id="59385-202">.NET</span></span>    | <span data-ttu-id="59385-203">Node.js</span><span class="sxs-lookup"><span data-stu-id="59385-203">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="59385-204">Teams расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="59385-204">Teams messaging extension action</span></span>| <span data-ttu-id="59385-205">Описывает, как определить команды действий, создать модуль задач и реагировать на отправку действия модуля задач.</span><span class="sxs-lookup"><span data-stu-id="59385-205">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="59385-206">View</span><span class="sxs-lookup"><span data-stu-id="59385-206">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="59385-207">View</span><span class="sxs-lookup"><span data-stu-id="59385-207">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="59385-208">Teams расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="59385-208">Teams messaging extension search</span></span>   |  <span data-ttu-id="59385-209">Описывает, как определить команды поиска и реагировать на поиски.</span><span class="sxs-lookup"><span data-stu-id="59385-209">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="59385-210">View</span><span class="sxs-lookup"><span data-stu-id="59385-210">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="59385-211">View</span><span class="sxs-lookup"><span data-stu-id="59385-211">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="59385-212">Следующий шаг</span><span class="sxs-lookup"><span data-stu-id="59385-212">Next step</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="59385-213">[Откликайся на команды поиска.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="59385-213">[Respond to the search commands](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

