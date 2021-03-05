---
title: Определение команд поиска расширения обмена сообщениями
author: clearab
description: Определение команд поиска расширения обмена сообщениями для приложений Microsoft Teams.
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 18bac3049fec8fead168c12f2832bfbbb72cf609
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449271"
---
# <a name="define-messaging-extension-search-commands"></a><span data-ttu-id="22767-103">Определение команд поиска расширения обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="22767-103">Define messaging extension search commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="22767-104">Команды поиска расширения обмена сообщениями позволяют пользователям искать внешние системы и вставлять результаты этого поиска в сообщение в виде карточки.</span><span class="sxs-lookup"><span data-stu-id="22767-104">Messaging extension search commands allow your users to search external systems and insert the results of that search into a message in the form of a card.</span></span>

> [!NOTE]
> <span data-ttu-id="22767-105">Ограничение размера карты результатов — 28 КБ.</span><span class="sxs-lookup"><span data-stu-id="22767-105">The result card size limit is 28 KB.</span></span> <span data-ttu-id="22767-106">Карта не отправляется, если ее размер превышает 28 КБ.</span><span class="sxs-lookup"><span data-stu-id="22767-106">The card is not sent if its size exceeds 28 KB.</span></span> 

## <a name="choose-messaging-extension-invoke-locations"></a><span data-ttu-id="22767-107">Выбор расположения ссылок на расширение обмена сообщениями</span><span class="sxs-lookup"><span data-stu-id="22767-107">Choose messaging extension invoke locations</span></span>

<span data-ttu-id="22767-108">Первое, что вам нужно решить, это откуда можно вызвать команду поиска (или, в частности, *вызвать).*</span><span class="sxs-lookup"><span data-stu-id="22767-108">The first thing you need to decide is where your search command can be triggered (or specifically, *invoked*) from.</span></span> <span data-ttu-id="22767-109">Команда поиска может вызываться из одного или обоих следующих местоположений:</span><span class="sxs-lookup"><span data-stu-id="22767-109">Your search command can be invoked from one or both of the following locations:</span></span>

* <span data-ttu-id="22767-110">Кнопки в нижней части области составить сообщение</span><span class="sxs-lookup"><span data-stu-id="22767-110">The buttons at the bottom of the compose message area</span></span>
* <span data-ttu-id="22767-111">По @mentioning в командном окне</span><span class="sxs-lookup"><span data-stu-id="22767-111">By @mentioning in the command box</span></span>

<span data-ttu-id="22767-112">При вызове из области составить сообщение у пользователя будет возможность отправки результатов в беседу.</span><span class="sxs-lookup"><span data-stu-id="22767-112">When invoked from the compose message area, your user will have the option of sending the results to the conversation.</span></span> <span data-ttu-id="22767-113">При вызове из командного окна пользователь может взаимодействовать с результативной картой или копировать ее для использования в другом месте.</span><span class="sxs-lookup"><span data-stu-id="22767-113">When invoked from the command box, the user can interact with the resulting card, or copy it for use elsewhere.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="22767-114">Добавление команды в манифест приложения</span><span class="sxs-lookup"><span data-stu-id="22767-114">Add the command to your app manifest</span></span>

<span data-ttu-id="22767-115">Теперь, когда вы решили, как пользователи будут взаимодействовать с командой поиска, пришло время добавить ее в манифест приложения.</span><span class="sxs-lookup"><span data-stu-id="22767-115">Now that you've decided how users will interact with your search command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="22767-116">Для этого вы добавите новый объект на верхний уровень `composeExtension` манифеста приложения JSON.</span><span class="sxs-lookup"><span data-stu-id="22767-116">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="22767-117">Это можно сделать либо с помощью App Studio, либо вручную.</span><span class="sxs-lookup"><span data-stu-id="22767-117">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="22767-118">Создание команды с помощью App Studio</span><span class="sxs-lookup"><span data-stu-id="22767-118">Create a command using App Studio</span></span>

<span data-ttu-id="22767-119">Обязательным условием для создания команды поиска является то, что необходимо уже создать расширение обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="22767-119">The prerequisite to create a search command is that you must already create a messaging extension.</span></span> <span data-ttu-id="22767-120">Сведения о создании расширения обмена сообщениями см. в сообщении о создании расширения [обмена сообщениями.](~/messaging-extensions/how-to/create-messaging-extension.md)</span><span class="sxs-lookup"><span data-stu-id="22767-120">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="22767-121">**Создание команды поиска**</span><span class="sxs-lookup"><span data-stu-id="22767-121">**To create a search command**</span></span>

1. <span data-ttu-id="22767-122">В клиенте Microsoft Teams откройте **App Studio** и выберите вкладку **Редактор Манифеста.**</span><span class="sxs-lookup"><span data-stu-id="22767-122">From the Microsoft Teams client, open **App Studio**, and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="22767-123">Если вы уже создали пакет приложений в **App Studio,** выберите его из списка.</span><span class="sxs-lookup"><span data-stu-id="22767-123">If you already created an app package in the **App Studio**, choose it from the list.</span></span> <span data-ttu-id="22767-124">Если вы не создали пакет приложений, импортировать существующий пакет.</span><span class="sxs-lookup"><span data-stu-id="22767-124">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="22767-125">После импорта пакета приложений выберите расширения **обмена** сообщениями в **статье Capabilities.**</span><span class="sxs-lookup"><span data-stu-id="22767-125">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span>
1. <span data-ttu-id="22767-126">Выберите **Добавить** в разделе **Команда** на странице расширения обмена сообщениями.</span><span class="sxs-lookup"><span data-stu-id="22767-126">Select **Add** in the **Command** section in the messaging extensions page.</span></span>
1. <span data-ttu-id="22767-127">Выберите **Разрешить пользователям запрашивать у службы сведения и вставить их в сообщение.**</span><span class="sxs-lookup"><span data-stu-id="22767-127">Choose **Allow users to query your service for information and insert that into a message**.</span></span>
1. <span data-ttu-id="22767-128">Добавление **командного и** **заголовок**.</span><span class="sxs-lookup"><span data-stu-id="22767-128">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="22767-129">Выберите расположение, в котором должна быть вызвана команда поиска.</span><span class="sxs-lookup"><span data-stu-id="22767-129">Select the location from where your search command must be triggered.</span></span> <span data-ttu-id="22767-130">Выбор сообщения **в** настоящее время не изменяет поведение команды поиска.</span><span class="sxs-lookup"><span data-stu-id="22767-130">Selecting **message** does not currently alter the behavior of your search command.</span></span>
1. <span data-ttu-id="22767-131">Добавьте параметр поиска и выберите **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="22767-131">Add your search parameter and select **Save**.</span></span>
 
### <a name="manually-create-a-command"></a><span data-ttu-id="22767-132">Вручную создайте команду</span><span class="sxs-lookup"><span data-stu-id="22767-132">Manually create a command</span></span>

<span data-ttu-id="22767-133">Чтобы вручную добавить команду поиска расширения обмена сообщениями в манифест приложения, необходимо добавить в массив объектов следующие `composeExtension.commands` параметры.</span><span class="sxs-lookup"><span data-stu-id="22767-133">To manually add your messaging extension search command to your app manifest, you'll need to add the following parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="22767-134">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22767-134">Property name</span></span> | <span data-ttu-id="22767-135">Назначение</span><span class="sxs-lookup"><span data-stu-id="22767-135">Purpose</span></span> | <span data-ttu-id="22767-136">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="22767-136">Required?</span></span> | <span data-ttu-id="22767-137">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="22767-137">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="22767-138">Уникальный ID, который вы назначаете этой команде.</span><span class="sxs-lookup"><span data-stu-id="22767-138">Unique ID that you assign to this command.</span></span> <span data-ttu-id="22767-139">Запрос пользователя будет включать этот ID.</span><span class="sxs-lookup"><span data-stu-id="22767-139">The user request will include this ID.</span></span> | <span data-ttu-id="22767-140">Да</span><span class="sxs-lookup"><span data-stu-id="22767-140">Yes</span></span> | <span data-ttu-id="22767-141">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-141">1.0</span></span> |
| `title` | <span data-ttu-id="22767-142">Имя команды.</span><span class="sxs-lookup"><span data-stu-id="22767-142">Command name.</span></span> <span data-ttu-id="22767-143">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="22767-143">This value appears in the UI.</span></span> | <span data-ttu-id="22767-144">Да</span><span class="sxs-lookup"><span data-stu-id="22767-144">Yes</span></span> | <span data-ttu-id="22767-145">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-145">1.0</span></span> |
| `description` | <span data-ttu-id="22767-146">Справка текста, указывающее, что делает эта команда.</span><span class="sxs-lookup"><span data-stu-id="22767-146">Help text indicating what this command does.</span></span> <span data-ttu-id="22767-147">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="22767-147">This value appears in the UI.</span></span> | <span data-ttu-id="22767-148">Да</span><span class="sxs-lookup"><span data-stu-id="22767-148">Yes</span></span> | <span data-ttu-id="22767-149">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-149">1.0</span></span> |
| `type` | <span data-ttu-id="22767-150">Необходимое значение — `query`.</span><span class="sxs-lookup"><span data-stu-id="22767-150">Must be `query`</span></span> | <span data-ttu-id="22767-151">Нет</span><span class="sxs-lookup"><span data-stu-id="22767-151">No</span></span> | <span data-ttu-id="22767-152">1.4</span><span class="sxs-lookup"><span data-stu-id="22767-152">1.4</span></span> |
|`initialRun` | <span data-ttu-id="22767-153">Если заданной **для true,** указывает, что эта команда должна быть выполнена, как только пользователь выберет эту команду в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="22767-153">If set to **true**, indicates this command should be executed as soon as the user chooses this command in the UI.</span></span> | <span data-ttu-id="22767-154">Нет</span><span class="sxs-lookup"><span data-stu-id="22767-154">No</span></span> | <span data-ttu-id="22767-155">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-155">1.0</span></span> |
| `context` | <span data-ttu-id="22767-156">Необязательный массив значений, определяя контекст, в котором доступно действие поиска.</span><span class="sxs-lookup"><span data-stu-id="22767-156">Optional array of values that defines the context the search action is available in.</span></span> <span data-ttu-id="22767-157">Возможные значения `message` , `compose` или `commandBox` .</span><span class="sxs-lookup"><span data-stu-id="22767-157">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="22767-158">Значение по умолчанию: `["compose", "commandBox"]`.</span><span class="sxs-lookup"><span data-stu-id="22767-158">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="22767-159">Нет</span><span class="sxs-lookup"><span data-stu-id="22767-159">No</span></span> | <span data-ttu-id="22767-160">1.5</span><span class="sxs-lookup"><span data-stu-id="22767-160">1.5</span></span> |

<span data-ttu-id="22767-161">Кроме того, необходимо добавить сведения о параметре поиска, который определит текст, видимый пользователю в клиенте Teams.</span><span class="sxs-lookup"><span data-stu-id="22767-161">You'll also need to add the details of the search parameter, which will define the text visible to your user in the Teams client.</span></span>

| <span data-ttu-id="22767-162">Имя свойства</span><span class="sxs-lookup"><span data-stu-id="22767-162">Property name</span></span> | <span data-ttu-id="22767-163">Назначение</span><span class="sxs-lookup"><span data-stu-id="22767-163">Purpose</span></span> | <span data-ttu-id="22767-164">Обязательный?</span><span class="sxs-lookup"><span data-stu-id="22767-164">Required?</span></span> | <span data-ttu-id="22767-165">Минимальная версия манифеста</span><span class="sxs-lookup"><span data-stu-id="22767-165">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="22767-166">Статический список параметров для команды.</span><span class="sxs-lookup"><span data-stu-id="22767-166">Static list of parameters for the command.</span></span> | <span data-ttu-id="22767-167">Нет</span><span class="sxs-lookup"><span data-stu-id="22767-167">No</span></span> | <span data-ttu-id="22767-168">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-168">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="22767-169">Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="22767-169">The name of the parameter.</span></span> <span data-ttu-id="22767-170">Это отправляется в службу в запросе пользователя.</span><span class="sxs-lookup"><span data-stu-id="22767-170">This is sent to your service in the user request.</span></span> | <span data-ttu-id="22767-171">Да</span><span class="sxs-lookup"><span data-stu-id="22767-171">Yes</span></span> | <span data-ttu-id="22767-172">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-172">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="22767-173">Описывает цели этого параметра или пример значения, которое должно быть предоставлено.</span><span class="sxs-lookup"><span data-stu-id="22767-173">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="22767-174">Это значение отображается в пользовательском интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="22767-174">This value appears in the UI.</span></span> | <span data-ttu-id="22767-175">Да</span><span class="sxs-lookup"><span data-stu-id="22767-175">Yes</span></span> | <span data-ttu-id="22767-176">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-176">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="22767-177">Краткое удобное название параметра или метка.</span><span class="sxs-lookup"><span data-stu-id="22767-177">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="22767-178">Да</span><span class="sxs-lookup"><span data-stu-id="22767-178">Yes</span></span> | <span data-ttu-id="22767-179">1.0</span><span class="sxs-lookup"><span data-stu-id="22767-179">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="22767-180">Задай тип необходимого ввода.</span><span class="sxs-lookup"><span data-stu-id="22767-180">Set to the type of input required.</span></span> <span data-ttu-id="22767-181">Возможные `text` значения: `textarea` , , , , `number` `date` `time` `toggle` .</span><span class="sxs-lookup"><span data-stu-id="22767-181">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="22767-182">По умолчанию установлено значение `text`</span><span class="sxs-lookup"><span data-stu-id="22767-182">Default is set to `text`</span></span> | <span data-ttu-id="22767-183">Нет</span><span class="sxs-lookup"><span data-stu-id="22767-183">No</span></span> | <span data-ttu-id="22767-184">1.4</span><span class="sxs-lookup"><span data-stu-id="22767-184">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="22767-185">Пример манифеста приложения</span><span class="sxs-lookup"><span data-stu-id="22767-185">App manifest example</span></span>

<span data-ttu-id="22767-186">Ниже приведен пример `composeExtensions` объекта, определяющий команду поиска.</span><span class="sxs-lookup"><span data-stu-id="22767-186">Below is an example of a `composeExtensions` object defining a search command.</span></span> <span data-ttu-id="22767-187">Это не пример полного манифеста, для полной схемы манифеста приложения см. схему манифеста [приложения.](~/resources/schema/manifest-schema.md)</span><span class="sxs-lookup"><span data-stu-id="22767-187">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="22767-188">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22767-188">Next steps</span></span>

<span data-ttu-id="22767-189">Теперь, когда вы добавили команду поиска, вам потребуется обрабатывать [запрос поиска.](~/messaging-extensions/how-to/search-commands/respond-to-search.md)</span><span class="sxs-lookup"><span data-stu-id="22767-189">Now that you've added your search command, you'll need to [handle the search request](~/messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
