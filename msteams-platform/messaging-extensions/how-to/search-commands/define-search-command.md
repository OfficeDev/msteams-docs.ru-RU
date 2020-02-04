---
title: Определение команд поиска для расширения обмена сообщениями
author: clearab
description: Определение команд поиска для расширения системы обмена сообщениями для приложений Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b6837fb8a131d8ce3e2bbd0c51c2861dbffda2bc
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675477"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="1f960-103">Определение команд поиска для расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1f960-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="1f960-104">Команды поиска для расширения системы обмена сообщениями позволяют пользователям искать внешние системы и вставлять результаты поиска в сообщения в виде карточки.</span><span class="sxs-lookup"><span data-stu-id="1f960-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="1f960-105">Выбор расположений вызова расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="1f960-105">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="1f960-106">Первое, что необходимо принять, — из чего можно запустить команду поиска (точнее, *вызвать*ее).</span><span class="sxs-lookup"><span data-stu-id="1f960-106">The first thing you need to decide is where your search command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="1f960-107">Команда поиска может быть вызвана из одного или обоих следующих расположений:</span><span class="sxs-lookup"><span data-stu-id="1f960-107">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="1f960-108">Кнопки в нижней части области "Создание сообщения"</span><span class="sxs-lookup"><span data-stu-id="1f960-108">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="1f960-109">По @mentioning в поле команды</span><span class="sxs-lookup"><span data-stu-id="1f960-109">By @mentioning in the command box</span></span>

<span data-ttu-id="1f960-110">При вызове из области "Создание сообщения" пользователь может отправлять результаты в беседу.</span><span class="sxs-lookup"><span data-stu-id="1f960-110">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="1f960-111">При вызове из поля команд пользователь может взаимодействовать с полученной картой или копировать его для использования в другом месте.</span><span class="sxs-lookup"><span data-stu-id="1f960-111">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="1f960-112">Добавление команды в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="1f960-112">Add the command to your app manifest</span></span>

<span data-ttu-id="1f960-113">Теперь, когда вы решили, как пользователи будут взаимодействовать с командой поиска, следует добавить его в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="1f960-113">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="1f960-114">Чтобы сделать это, добавьте новый `composeExtension` объект на верхний уровень манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="1f960-114">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="1f960-115">Это можно сделать с помощью App Studio или вручную.</span><span class="sxs-lookup"><span data-stu-id="1f960-115">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="1f960-116">Создание команды с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="1f960-116">Create a command using App Studio</span></span>

<span data-ttu-id="1f960-117">В следующих действиях предполагается, что вы уже [создали расширение системы обмена сообщениями](~/messaging-extensions/how-to/create-messaging-extension.md).</span><span class="sxs-lookup"><span data-stu-id="1f960-117">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="1f960-118">В клиенте Microsoft Teams откройте **app Studio** и выберите вкладку **редактор манифестов** .</span><span class="sxs-lookup"><span data-stu-id="1f960-118">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="1f960-119">Если вы уже создали пакет приложения в App Studio, выберите его из списка.</span><span class="sxs-lookup"><span data-stu-id="1f960-119">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="1f960-120">В противном случае вы можете импортировать существующий пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="1f960-120">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="1f960-121">Нажмите кнопку **Add (добавить** ) в разделе Command (Добавить).</span><span class="sxs-lookup"><span data-stu-id="1f960-121">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="1f960-122">Выберите **Разрешить пользователям запрашивать у службы сведения и вставлять их в сообщение**.</span><span class="sxs-lookup"><span data-stu-id="1f960-122">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
5. <span data-ttu-id="1f960-123">Добавьте **идентификатор команды** и **название**.</span><span class="sxs-lookup"><span data-stu-id="1f960-123">Add a **Command Id** and a **Title**.</span></span>
6. <span data-ttu-id="1f960-124">Выберите, откуда вы хотите запустить команду поиска.</span><span class="sxs-lookup"><span data-stu-id="1f960-124">Select where you want your search command to be triggered from.</span></span> <span data-ttu-id="1f960-125">В настоящее время выбор **сообщения** не изменяет поведение команды поиска.</span><span class="sxs-lookup"><span data-stu-id="1f960-125">Selecting **message** does not currently alter the behavior of your search command.</span></span>
7. <span data-ttu-id="1f960-126">Добавьте параметр поиска.</span><span class="sxs-lookup"><span data-stu-id="1f960-126">Add your search parameter.</span></span>
8. <span data-ttu-id="1f960-127">Щелкните Сохранить.</span><span class="sxs-lookup"><span data-stu-id="1f960-127">Click Save.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="1f960-128">Создание команды вручную</span><span class="sxs-lookup"><span data-stu-id="1f960-128">Manually create a command</span></span>

<span data-ttu-id="1f960-129">Чтобы вручную добавить команду поиска расширения обмена сообщениями в манифест приложения, необходимо добавить к `composeExtension.commands` массиву объектов следующие параметры.</span><span class="sxs-lookup"><span data-stu-id="1f960-129">To manually add your messaging extension search command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="1f960-130">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1f960-130">Property name</span></span> | <span data-ttu-id="1f960-131">Назначение</span><span class="sxs-lookup"><span data-stu-id="1f960-131">Purpose</span></span> | <span data-ttu-id="1f960-132">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="1f960-132">Required?</span></span> | <span data-ttu-id="1f960-133">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="1f960-133">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="1f960-134">Уникальный идентификатор, назначенный этой команде.</span><span class="sxs-lookup"><span data-stu-id="1f960-134">Unique ID that you assign to this command.</span></span> <span data-ttu-id="1f960-135">Запрос пользователя будет включать этот идентификатор.</span><span class="sxs-lookup"><span data-stu-id="1f960-135">The user request will include this ID.</span></span> | <span data-ttu-id="1f960-136">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-136">Yes</span></span> | <span data-ttu-id="1f960-137">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-137">1.0</span></span> |
| `title` | <span data-ttu-id="1f960-138">Имя команды.</span><span class="sxs-lookup"><span data-stu-id="1f960-138">Command name.</span></span> <span data-ttu-id="1f960-139">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1f960-139">This value appears in the UI.</span></span> | <span data-ttu-id="1f960-140">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-140">Yes</span></span> | <span data-ttu-id="1f960-141">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-141">1.0</span></span> |
| `description` | <span data-ttu-id="1f960-142">Текст справки, указывающий, что делает эта команда.</span><span class="sxs-lookup"><span data-stu-id="1f960-142">Help text indicating what this command does.</span></span> <span data-ttu-id="1f960-143">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1f960-143">This value appears in the UI.</span></span> | <span data-ttu-id="1f960-144">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-144">Yes</span></span> | <span data-ttu-id="1f960-145">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-145">1.0</span></span> |
| `type` | <span data-ttu-id="1f960-146">Необходимое значение — `query`.</span><span class="sxs-lookup"><span data-stu-id="1f960-146">Must be `query`</span></span> | <span data-ttu-id="1f960-147">Нет</span><span class="sxs-lookup"><span data-stu-id="1f960-147">No</span></span> | <span data-ttu-id="1f960-148">1.4</span><span class="sxs-lookup"><span data-stu-id="1f960-148">1.4</span></span> |
|`initialRun` | <span data-ttu-id="1f960-149">Если задано значение **true**, то эта команда должна выполняться сразу после того, как пользователь выберет эту команду в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1f960-149">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="1f960-150">Нет</span><span class="sxs-lookup"><span data-stu-id="1f960-150">No</span></span> | <span data-ttu-id="1f960-151">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-151">1.0</span></span> |
| `context` | <span data-ttu-id="1f960-152">Необязательный массив значений, определяющий контекст, в котором действие поиска доступно.</span><span class="sxs-lookup"><span data-stu-id="1f960-152">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="1f960-153">Возможные значения: `message`, `compose`, или `commandBox`.</span><span class="sxs-lookup"><span data-stu-id="1f960-153">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="1f960-154">Значение по умолчанию: `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="1f960-154">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="1f960-155">Нет</span><span class="sxs-lookup"><span data-stu-id="1f960-155">No</span></span> | <span data-ttu-id="1f960-156">1.5</span><span class="sxs-lookup"><span data-stu-id="1f960-156">1.5</span></span> |

<span data-ttu-id="1f960-157">Кроме того, необходимо добавить сведения о параметре Search, который будет определять текст, видимый для пользователя в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="1f960-157">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="1f960-158">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="1f960-158">Property name</span></span> | <span data-ttu-id="1f960-159">Назначение</span><span class="sxs-lookup"><span data-stu-id="1f960-159">Purpose</span></span> | <span data-ttu-id="1f960-160">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="1f960-160">Required?</span></span> | <span data-ttu-id="1f960-161">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="1f960-161">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="1f960-162">Статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="1f960-162">Static list of parameters for the command.</span></span> | <span data-ttu-id="1f960-163">Нет</span><span class="sxs-lookup"><span data-stu-id="1f960-163">No</span></span> | <span data-ttu-id="1f960-164">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-164">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="1f960-165">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="1f960-165">The name of the parameter.</span></span> <span data-ttu-id="1f960-166">Он отправляется службе по запросу пользователя.</span><span class="sxs-lookup"><span data-stu-id="1f960-166">This is sent to your service in the user request.</span></span> | <span data-ttu-id="1f960-167">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-167">Yes</span></span> | <span data-ttu-id="1f960-168">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-168">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="1f960-169">Описывает назначение этого параметра или пример значения, которое следует предоставить.</span><span class="sxs-lookup"><span data-stu-id="1f960-169">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="1f960-170">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="1f960-170">This value appears in the UI.</span></span> | <span data-ttu-id="1f960-171">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-171">Yes</span></span> | <span data-ttu-id="1f960-172">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-172">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="1f960-173">Краткий заголовком или меткой с понятным пользователем параметром.</span><span class="sxs-lookup"><span data-stu-id="1f960-173">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="1f960-174">Да</span><span class="sxs-lookup"><span data-stu-id="1f960-174">Yes</span></span> | <span data-ttu-id="1f960-175">1.0</span><span class="sxs-lookup"><span data-stu-id="1f960-175">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="1f960-176">Укажите требуемый тип ввода.</span><span class="sxs-lookup"><span data-stu-id="1f960-176">Set to the type of input required.</span></span> <span data-ttu-id="1f960-177">Возможные значения: `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span><span class="sxs-lookup"><span data-stu-id="1f960-177">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="1f960-178">Значение по умолчанию:`text`</span><span class="sxs-lookup"><span data-stu-id="1f960-178">Default is set to `text`</span></span> | <span data-ttu-id="1f960-179">Нет</span><span class="sxs-lookup"><span data-stu-id="1f960-179">No</span></span> | <span data-ttu-id="1f960-180">1.4</span><span class="sxs-lookup"><span data-stu-id="1f960-180">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="1f960-181">Пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="1f960-181">App manifest example</span></span>

<span data-ttu-id="1f960-182">Ниже приведен пример `composeExtensions` объекта, определяющего команду поиска.</span><span class="sxs-lookup"><span data-stu-id="1f960-182">The below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="1f960-183">Это не пример полного манифеста для полной схемы манифеста приложения: [схема манифеста приложения](~/resources/schema/manifest-schema.md).</span><span class="sxs-lookup"><span data-stu-id="1f960-183">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="1f960-184">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1f960-184">Next steps</span></span>

<span data-ttu-id="1f960-185">Теперь, когда вы добавили команду поиска, вам потребуется [обработать запрос поиска](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span><span class="sxs-lookup"><span data-stu-id="1f960-185">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]