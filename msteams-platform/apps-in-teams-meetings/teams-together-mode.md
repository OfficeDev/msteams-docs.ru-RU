---
title: Настраиваемые сцены режима совместно
description: Работа с настраиваемой совместной сценой режима
ms.topic: conceptual
ms.openlocfilehash: b2a81d92724785acbcd198d6240eec7d8d510e1c
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949751"
---
# <a name="custom-together-mode-scenes-in-teams"></a><span data-ttu-id="1b7fd-103">Настраиваемые сцены режима совместно в Teams</span><span class="sxs-lookup"><span data-stu-id="1b7fd-103">Custom Together Mode scenes in Teams</span></span>

> [!NOTE]
> <span data-ttu-id="1b7fd-104">В настоящее время эта функция доступна только [для предварительного просмотра общедоступных](../resources/dev-preview/developer-preview-intro.md) разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-104">This feature is currently available in [public developer preview](../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="1b7fd-105">Настраиваемые сцены режима together в Microsoft Teams предоставляют иммерсивную и привлекаемую среду собраний, которая объединяет людей и побуждает их включить видео.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-105">Custom Together Mode scenes in Microsoft Teams provides an immersive and engaging meeting environment that brings people together and encourages them to turn on their video.</span></span> <span data-ttu-id="1b7fd-106">Она цифровым образом объединяет участников в одну виртуальную сцену и помещает их видеопотоки в заранее разработанные и исправленные создателем сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-106">It digitally combines participants into a single virtual scene and places their video streams in pre-determined seats designed and fixed by the scene creator.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/MGsNmYKgeTA]

<span data-ttu-id="1b7fd-107">Сцена в пользовательских сценах режима together — это артефакт, созданный разработчиком сцены с помощью студии Microsoft Scene.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-107">A scene in custom Together Mode scenes is an artifact created by the scene developer using the Microsoft Scene studio.</span></span> <span data-ttu-id="1b7fd-108">В зачатом параметре сцены участники обозначили места с видеопотоками, отрисовав их в этих местах.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-108">In a conceived scene setting, participants have designated seats with video streams rendered in those seats.</span></span>

> [!NOTE]
> <span data-ttu-id="1b7fd-109">Рекомендуется использовать только приложения для сцены, так как опыт приобретения для таких приложений является более плавным.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-109">Scene only apps are recommended as the acquisition experience for such apps is more seamless.</span></span>

<span data-ttu-id="1b7fd-110">Следующий процесс дает обзор для создания приложения только сцены:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-110">The following process gives an overview to create a scene only app:</span></span>

:::image type="content" source="../assets/images/apps-in-meetings/create-together-mode-scene-flow.png" alt-text="Создание приложения только для сцены" border="false":::

> [!NOTE]
> * <span data-ttu-id="1b7fd-112">Только приложение сцены по-прежнему является приложением в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-112">A scene only app is still an app in Microsoft Teams.</span></span> <span data-ttu-id="1b7fd-113">Студия Scene обрабатывает создание пакета приложений в фоновом режиме.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-113">The Scene studio handles the app package creation in the background.</span></span>
> * <span data-ttu-id="1b7fd-114">Несколько сцен в одном пакете приложений отображаются как единый список сцен для пользователей.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-114">Multiple scenes in a single app package appear as a flat list of scenes to users.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b7fd-115">Необходимые компоненты</span><span class="sxs-lookup"><span data-stu-id="1b7fd-115">Prerequisites</span></span>

<span data-ttu-id="1b7fd-116">Необходимо иметь базовое представление о следующих действиях, чтобы использовать настраиваемые сцены Режима совместной работы:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-116">You must have a basic understanding of the following to use custom Together Mode scenes:</span></span>

* <span data-ttu-id="1b7fd-117">Определение сцены и мест в сцене.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-117">Definition of scene and seats in a scene.</span></span>
* <span data-ttu-id="1b7fd-118">У вас есть учетная запись разработчика Майкрософт и ознакомьтесь с Microsoft Teams [портала разработчиков](../concepts/build-and-test/teams-developer-portal.md) и App Studio.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-118">Have a Microsoft Developer account and be familiar with the Microsoft Teams [Developer Portal](../concepts/build-and-test/teams-developer-portal.md) and App Studio.</span></span>
* <span data-ttu-id="1b7fd-119">[Концепция боковой загрузки приложений.](../concepts/deploy-and-publish/apps-upload.md)</span><span class="sxs-lookup"><span data-stu-id="1b7fd-119">[Concept of app sideloading](../concepts/deploy-and-publish/apps-upload.md).</span></span>
* <span data-ttu-id="1b7fd-120">Убедитесь, что администратор разрешил  Upload настраиваемого приложения и выбрать все фильтры в рамках политик установки приложений и собраний соответственно.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-120">Ensure that the Administrator has granted permission to **Upload a custom app** and to select all filters as part of App Setup and Meeting policies respectively.</span></span>

## <a name="best-practices"></a><span data-ttu-id="1b7fd-121">Рекомендации</span><span class="sxs-lookup"><span data-stu-id="1b7fd-121">Best practices</span></span>

<span data-ttu-id="1b7fd-122">Перед созданием сцены считайте, что ниже имеется бесшовный опыт создания сцены:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-122">Prior to building a scene, consider the following to have a seamless scene building experience:</span></span>

* <span data-ttu-id="1b7fd-123">Убедитесь, что все изображения находятся в формате PNG.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-123">Ensure that all images are in PNG format.</span></span>
* <span data-ttu-id="1b7fd-124">Убедитесь, что конечный пакет со всеми изображениями не должен превышать разрешение 1920x1080.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-124">Ensure that the final package with all the images put together must not exceed 1920x1080 resolution.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b7fd-125">Разрешение — это 10-е число.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-125">The resolution is an even number.</span></span> <span data-ttu-id="1b7fd-126">Это требование, чтобы сцены были успешно освещены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-126">This is a requirement for scenes to be lit up successfully.</span></span>

* <span data-ttu-id="1b7fd-127">Убедитесь, что максимальный размер сцены — 10 МБ.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-127">Ensure that the maximum scene size is 10 MB.</span></span>
* <span data-ttu-id="1b7fd-128">Убедитесь, что максимальный размер каждого изображения составляет 5 МБ.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-128">Ensure that the maximum size of each image is 5 MB.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="1b7fd-129">Сцена — это коллекция из нескольких изображений.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-129">A scene is a collection of multiple images.</span></span> <span data-ttu-id="1b7fd-130">Ограничение для каждого отдельного изображения.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-130">The limit is for each individual image.</span></span>
    > * <span data-ttu-id="1b7fd-131">Отдельное разрешение изображения также должно быть 10-м числом.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-131">The individual image resolution must also be an even number.</span></span>
  
* <span data-ttu-id="1b7fd-132">Убедитесь, **что прозрачный** почтовый ящик выбран, если изображение прозрачное.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-132">Ensure that the **Transparent** checkbox is selected if the image is transparent.</span></span> <span data-ttu-id="1b7fd-133">Этот контрольный ящик доступен на правой панели при выборе изображения.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-133">This checkbox is available on the right panel when an image is selected.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b7fd-134">Перекрывающиеся изображения должны быть помечены как **Прозрачные,** чтобы указать, что они перекрывают изображения в сцене.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-134">Overlapping images need to be marked as **Transparent** to indicate that they are overlapping images in the scene.</span></span>

## <a name="build-a-scene-using-the-scene-studio"></a><span data-ttu-id="1b7fd-135">Создание сцены с помощью студии Scene</span><span class="sxs-lookup"><span data-stu-id="1b7fd-135">Build a scene using the Scene studio</span></span>

<span data-ttu-id="1b7fd-136">В Microsoft есть студия Scene, которая позволяет создавать сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-136">Microsoft has a Scene studio that allows you to build scenes.</span></span> <span data-ttu-id="1b7fd-137">Он доступен на [сайте Scenes Editor - Teams портале разработчиков.](https://dev.teams.microsoft.com/scenes)</span><span class="sxs-lookup"><span data-stu-id="1b7fd-137">It is available on [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

> [!NOTE]
> <span data-ttu-id="1b7fd-138">Этот документ ссылается на студию Scene на портале Microsoft Teams разработчика.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-138">This document is referring to Scene studio in the Microsoft Teams Developer Portal.</span></span> <span data-ttu-id="1b7fd-139">Интерфейс и функциональные возможности в Конструкторе сцен App Studio одинаковы.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-139">The interface and functionalities are all the same in App Studio Scene Designer.</span></span>

<span data-ttu-id="1b7fd-140">Сцена в контексте студии Scene — это артефакт, содержащий следующее:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-140">A scene in the context of the Scene studio is an artifact that contains the following:</span></span>

* <span data-ttu-id="1b7fd-141">Места, зарезервированные для организатора собраний и презентаторов собраний.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-141">Seats reserved for meeting organizer and meeting presenters.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b7fd-142">Presenter не ссылаться на пользователя, который активно обмена.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-142">Presenter does not refer to the user who is actively sharing.</span></span> <span data-ttu-id="1b7fd-143">Это относится к [роли собрания](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span><span class="sxs-lookup"><span data-stu-id="1b7fd-143">It refers to the [meeting role](https://support.microsoft.com/en-us/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

* <span data-ttu-id="1b7fd-144">Место и изображение для каждого участника с регулируемой шириной и высотой.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-144">Seat and image for each participant with an adjustable width and height.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1b7fd-145">PNG — это единственный поддерживаемый формат.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-145">PNG is the only supported format.</span></span>

* <span data-ttu-id="1b7fd-146">XYZ координаты всех мест и изображений.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-146">XYZ coordinates of all the seats and images.</span></span>
* <span data-ttu-id="1b7fd-147">Коллекция изображений, замаскированных как одно изображение.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-147">Collection of images that are camouflaged as one image.</span></span>

<span data-ttu-id="1b7fd-148">Размеры сидений становятся холстом для отображения видеопотока участника.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-148">The seat dimensions become the canvas for rendering the participant video stream.</span></span> <span data-ttu-id="1b7fd-149">На следующем изображении показано каждое место, которое представлено в качестве аватара для создания сцен:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-149">The following image shows each seat represented as an avatar for building scenes:</span></span>

![Студия Scene](../assets/images/apps-in-meetings/scene-design-studio.png)

<span data-ttu-id="1b7fd-151">**Создание сцены с помощью студии Scene**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-151">**To build a scene using the Scene studio**</span></span>

1. <span data-ttu-id="1b7fd-152">Перейдите к редактору сцены [— Teams порталу разработчиков](https://dev.teams.microsoft.com/scenes).</span><span class="sxs-lookup"><span data-stu-id="1b7fd-152">Go to [Scenes Editor - Teams Developer Portal](https://dev.teams.microsoft.com/scenes).</span></span>

    >[!NOTE]
    > * <span data-ttu-id="1b7fd-153">Чтобы открыть студию Scene, можно перейти на главную страницу [портала Teams](https://dev.teams.microsoft.com/home) разработчика и выбрать Создать настраиваемые сцены **для собраний.**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-153">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home) and select **Create custom scenes for meetings**.</span></span>
    > * <span data-ttu-id="1b7fd-154">Чтобы открыть студию Scene, можно перейти на домашную  страницу портала [Teams](https://dev.teams.microsoft.com/home)разработчика, выбрать инструменты из левого раздела и выбрать студию **Scene** из раздела **Tools.**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-154">To open Scene studio, you can navigate to the home page of [Teams Developer Portal](https://dev.teams.microsoft.com/home), select **Tools** from the left hand section, and select **Scene studio** from the **Tools** section.</span></span>

1. <span data-ttu-id="1b7fd-155">На странице **Редактор сцены** выберите Создать **новую сцену.**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-155">In the **Scenes Editor** page, select **Create a new scene**.</span></span>

1. <span data-ttu-id="1b7fd-156">В поле **Сцена** введите имя сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-156">In the **Scene** box, enter a name for the scene.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="1b7fd-157">Вы можете выбрать **close** toggle между закрытием или открытием правой области.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-157">You can select **Close** to toggle between closing or reopening the right pane.</span></span>
    > * <span data-ttu-id="1b7fd-158">Вы можете увеличить или увеличить масштаб сцены с помощью панели масштабирования для лучшего представления сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-158">You can zoom in or zoom out of the scene using the zoom bar for a better view of the scene.</span></span>

1. <span data-ttu-id="1b7fd-159">Перетащите и сбросите изображение в среду, отображаемую на следующем изображении:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-159">Drag and drop the image into the environment as displayed in the following image:</span></span>

    >[!NOTE]
    > * <span data-ttu-id="1b7fd-160">Вы можете [ скачать ](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip)SampleScene.zip[SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) с изображениями.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-160">You can download the [SampleScene.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleScene.zip) and [SampleApp.zip](https://github.com/MicrosoftDocs/msteams-docs/tree/master/msteams-platform/apps-in-teams-meetings/SampleApp.zip) files with the images.</span></span>
    > * <span data-ttu-id="1b7fd-161">Кроме того, вы можете добавить фоновые изображения в сцену с помощью **Добавить изображения**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-161">Alternately, you can add background images to the scene using **Add images**.</span></span>

    ![Перетаскивать в сцену](../assets/images/apps-in-meetings/drag-and-drop-scene.png)

1. <span data-ttu-id="1b7fd-163">Выберите размещенное изображение.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-163">Select the image that you have placed.</span></span>

1. <span data-ttu-id="1b7fd-164">На правой области выберите выравнивание для изображения или используйте слайдер **Resize** для настройки размера изображения.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-164">From the right pane, select an alignment for the image or use the **Resize** slider to adjust the image size.</span></span>

    ![Выравнивание для изображений](../assets/images/apps-in-meetings/image-alignment.png)

1. <span data-ttu-id="1b7fd-166">Выберите область за пределами изображения.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-166">Select an area outside of the image.</span></span>

1. <span data-ttu-id="1b7fd-167">В верхнем правом углу выберите **Участники** под **слоями**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-167">In the upper-right corner, select **Participants** under **Layers**.</span></span>

1. <span data-ttu-id="1b7fd-168">Выберите число участников сцены из окна **Число** участников и выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-168">Select the number of participants for the scene from the **Number of participants** box, and select **Add**.</span></span>

    >[!NOTE]
    > * <span data-ttu-id="1b7fd-169">После отправки сцены места размещения аватара заменяются видеопотоками фактического участника.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-169">After the scene is shipped, the avatar placements are replaced with actual participant's video streams.</span></span>
    > * <span data-ttu-id="1b7fd-170">Вы можете перетаскивать изображения участников вокруг сцены и разместить их в нужном положении и повторно их использовать стрелку повторного использования.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-170">You can drag the participant images around the scene and place them in the required position and resize them using the resize arrow.</span></span>

1. <span data-ttu-id="1b7fd-171">Выберите любое изображение участника и выберите поле **Назначение** места для назначения места участнику.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-171">Select any participant image, and choose the **Assign Spot** check box to assign the spot to the participant.</span></span>

1. <span data-ttu-id="1b7fd-172">Выберите **роль организатора** собрания или **презентовщика** для участника.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-172">Select **Meeting Organizer** or **Presenter** role for the participant.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1b7fd-173">На собрании одному участнику должна быть назначена роль организатора собрания.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-173">In a meeting, one participant must be assigned the role of a meeting organizer.</span></span>

    ![Назначение места](../assets/images/apps-in-meetings/assign-spot.png)

1. <span data-ttu-id="1b7fd-175">Выберите **Сохранить** и выбрать **view в Teams,** чтобы быстро протестировать сцену в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-175">Select **Save** and select **View in Teams** to quickly test your scene in Microsoft Teams.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1b7fd-176">Чтобы удалить созданную сцену, выберите **удалить сцену на** верхней панели.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-176">To delete a scene you created, select **Delete scene** on the top bar.</span></span>

1. <span data-ttu-id="1b7fd-177">В **диалоговом окне Представление Teams** выберите **Предварительный просмотр в Teams**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-177">In the **View in Teams** dialog box, select **Preview in Teams**.</span></span>
1. <span data-ttu-id="1b7fd-178">В диалоговом окне, которое отображается, выберите **Добавить**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-178">In the dialog box that appears, select **Add**.</span></span>

    <span data-ttu-id="1b7fd-179">Сцену можно протестировать или получить доступ, создав тестовую встречу и запустив настраиваемые сцены режима together.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-179">The scene can be tested or accessed by creating a test meeting and launching custom Together Mode scenes.</span></span> <span data-ttu-id="1b7fd-180">Дополнительные сведения см. в [дополнительных сведениях о активации пользовательских сцен режима Together Mode.](#activate-custom-together-mode-scenes)</span><span class="sxs-lookup"><span data-stu-id="1b7fd-180">For more information, see [activate custom Together Mode scenes](#activate-custom-together-mode-scenes).</span></span>

    ![Запуск настраиваемой совместной сцены режима](../assets/images/apps-in-meetings/launchtogethermode.png)

    >[!NOTE]
    > * <span data-ttu-id="1b7fd-182">Выбор **предварительного** просмотра автоматически создает приложение Microsoft Teams, которое можно просмотреть на странице **Приложения** на портале Teams разработчика.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-182">Selecting **Preview** automatically creates a Microsoft Teams app that can be viewed in the **Apps** page in the Teams Developer Portal.</span></span>
    > * <span data-ttu-id="1b7fd-183">Выбор **предварительного** просмотра автоматически создает пакет приложений, который appmanifest.jsза кулисами.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-183">Selecting **Preview** automatically creates an app package that is appmanifest.json behind the scene.</span></span> <span data-ttu-id="1b7fd-184">Как уже говорилось ранее, это абстрактно, но вы можете получить доступ к автоматически созданному пакету приложений, переходя в **Приложения** из меню.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-184">As stated earlier, this is abstracted, but you can access the automatically created app package by navigating to **Apps** from the menu.</span></span>
    > * <span data-ttu-id="1b7fd-185">Затем сцену можно просмотреть в настраиваемой галерее "Вместе режим".</span><span class="sxs-lookup"><span data-stu-id="1b7fd-185">The scene can then be viewed in the custom Together Mode scenes gallery.</span></span>

1. <span data-ttu-id="1b7fd-186">Необязательно, вы можете выбрать **Share** из меню **Сохранить** выпадающим, чтобы создать ссылку для обмена, чтобы легко распространять сцены для других использовать.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-186">Optionally, you can select **Share** from the **Save** drop-down menu to create a shareable link to easily distribute your scenes for others to use.</span></span> <span data-ttu-id="1b7fd-187">Открытие этой ссылки устанавливает сцену для пользователя, и они могут приступить к ее использованию.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-187">Opening this link installs the scene for the user and they can start using it.</span></span>

1. <span data-ttu-id="1b7fd-188">После предварительного просмотра сцена может быть отправлена в качестве приложения для Teams, следуя шагам для отправки приложения.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-188">After preview, the scene can be shipped as an app to Teams by following the steps for app submission.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1b7fd-189">Этот шаг требует пакета приложений, который отличается от пакета сцены, для сцены, которая была разработана.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-189">This step requires the app package that is different from the scene package, for the scene that was designed.</span></span> <span data-ttu-id="1b7fd-190">Автоматически созданный пакет приложений можно найти в разделе **Приложения** в центре Teams разработчиков.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-190">The app package created automatically can be found in the **Apps** section in the Teams Developer Center.</span></span>

1. <span data-ttu-id="1b7fd-191">Необязательный пакет сцены можно получить, выбрав **экспорт** из меню **Сохранить** отсев.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-191">Optionally, the scene package can be retrieved by selecting **Export** from the **Save** drop-down menu.</span></span> <span data-ttu-id="1b7fd-192">Загружается .zip, то есть пакет сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-192">A .zip file, that is the scene package, is downloaded.</span></span>

    ![Экспорт сцены](../assets/images/apps-in-meetings/build-a-scene.png)

    >[!NOTE]
    > <span data-ttu-id="1b7fd-194">Пакет сцены состоит из scene.jsи активов PNG, используемых для создания сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-194">Scene package comprises of a scene.json and the PNG assets used to build a scene.</span></span> <span data-ttu-id="1b7fd-195">Пакет сцены можно просмотреть для включения других изменений, описанных в примере scene.jsв разделе этого документа.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-195">The scene package can be reviewed for incorporating other changes as described in the Sample scene.json section of this document.</span></span>

<span data-ttu-id="1b7fd-196">Более сложная сцена, которая использует Z-ось, демонстрируется в пошаговом примере начала работы.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-196">A more complex scene that leverages the Z-axis is demonstrated in the step-by-step getting started sample.</span></span>

## <a name="sample-scenejson"></a><span data-ttu-id="1b7fd-197">Пример scene.jsна</span><span class="sxs-lookup"><span data-stu-id="1b7fd-197">Sample scene.json</span></span>

<span data-ttu-id="1b7fd-198">Scene.jsвместе с изображениями указывают точное расположение сидений.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-198">Scene.json along with the images indicate the exact position of the seats.</span></span> <span data-ttu-id="1b7fd-199">Сцена состоит из изображений bitmap, спрайтов и прямоугольников для вложения видео участников.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-199">A scene consists of bitmap images, sprites, and rectangles to put participant videos in.</span></span> <span data-ttu-id="1b7fd-200">Эти спрайты и ящики участников определяются в системе координат мира с X-axis, указывающей направо, а Y-оси , указывающей вниз.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-200">These sprites and participant boxes are defined in a world coordinate system with the X-axis pointing to the right and the Y-axis pointing downwards.</span></span> <span data-ttu-id="1b7fd-201">Настраиваемые сцены режима "Вместе" поддерживают масштабирование текущих участников.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-201">Custom Together Mode scenes supports zooming in on the current participants.</span></span> <span data-ttu-id="1b7fd-202">Это полезно для небольших собраний в большой сцене.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-202">This is helpful for small meetings in a large scene.</span></span> <span data-ttu-id="1b7fd-203">Спрайт — это статическое изображение bitmap, которое находится в мире.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-203">A sprite is a static bitmap image positioned in the world.</span></span> <span data-ttu-id="1b7fd-204">Значение Z спрайта определяет положение спрайта.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-204">The Z value of the sprite determines the position of the sprite.</span></span> <span data-ttu-id="1b7fd-205">Отрисовка начинается с спрайта с наименьшим значением Z, поэтому более высокое значение Z означает, что оно ближе к камере.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-205">Rendering starts with the sprite with lowest Z value, so higher Z value means it is closer to the camera.</span></span> <span data-ttu-id="1b7fd-206">Каждый участник имеет свою собственную видео-ленту, которая сегментироваться таким образом, чтобы отрисовка только переднего плана.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-206">Each participant has its own video feed, which is segmented so that only the foreground is rendered.</span></span>

<span data-ttu-id="1b7fd-207">Ниже приводится scene.jsпример:</span><span class="sxs-lookup"><span data-stu-id="1b7fd-207">Following is the scene.json sample:</span></span>

```json
{
   "protocolVersion": "1.0",
   "id": "A",
   "autoZoom": true,
   "mirrorParticipants ": true,
   "extent":{
      "left":0.0,
      "top":0.0,
      "width":16.0,
      "height":9.0
   },
   "sprites":[
      {
         "filename":"background.png",
         "cx":8.0,
         "cy":4.5,
         "width":16.0,
         "height":9.0,
         "zOrder":0.0,
   "isAlpha":false
      },
      {
         "filename":"table.png",
         "cx":8.0,
         "cy":7.0,
         "width":12.0,
         "height":4.0,
         "zOrder":3.0,
   "isAlpha":true
      },
      {
         "filename":"row0.png",
         "cx":12.0,
         "cy":15.0,
         "width":8.0,
         "height":4.0,
         "zOrder":2.0,
   "isAlpha":true
      }

   ],
   "participants":[
      {
         "cx":5.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":0
      },
      {
         "cx":11.0,
         "cy":4.0,
         "width":4.0,
         "height":2.25,
         "zOrder":1.0,
         "seatingOrder":1
      }
   ]
}
```

<span data-ttu-id="1b7fd-208">Каждая сцена имеет уникальный ID и имя.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-208">Each scene has a unique ID and name.</span></span> <span data-ttu-id="1b7fd-209">В сцене JSON также содержатся сведения о всех активах, используемых для сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-209">The scene JSON also contains information on all the assets used for the scene.</span></span> <span data-ttu-id="1b7fd-210">Каждый актив содержит имя файла, ширину, высоту и положение на оси X и Y.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-210">Each asset contains a filename, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="1b7fd-211">Кроме того, каждое сиденье содержит ID места, ширину, высоту и положение на оси X и Y.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-211">Similarly, each seat contains a seat ID, width, height, and position on the X and Y-axis.</span></span> <span data-ttu-id="1b7fd-212">Порядок рассадки создается автоматически и может изменяться в зависимости от предпочтений.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-212">The seating order is generated automatically and can be altered as per preference.</span></span>

> [!NOTE]
> <span data-ttu-id="1b7fd-213">Номер заказа сидений соответствует порядку присоединения к вызову.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-213">Seating order number corresponds to the order of people joining the call.</span></span>

<span data-ttu-id="1b7fd-214">ZOrder представляет порядок размещения изображений и сидений вдоль оси Z.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-214">The zOrder represents the order of placing images and seats along the Z-axis.</span></span> <span data-ttu-id="1b7fd-215">Во многих случаях это дает ощущение глубины или раздела при необходимости.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-215">In many cases, it gives a sense of depth or partition if required.</span></span> <span data-ttu-id="1b7fd-216">Дополнительные сведения см. в примере пошаговая приступить к работе.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-216">For more information, see the step-by-step getting started sample.</span></span> <span data-ttu-id="1b7fd-217">Пример использует zOrder.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-217">The sample leverages the zOrder.</span></span>

<span data-ttu-id="1b7fd-218">Теперь, когда вы прошли через пример scene.js, вы можете активировать настраиваемые сцены режима together для вовлечения в сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-218">Now that you have gone through the sample scene.json, you can activate the custom Together Mode scenes to engage in scenes.</span></span>

## <a name="activate-custom-together-mode-scenes"></a><span data-ttu-id="1b7fd-219">Активация настраиваемой совместной сцены режима</span><span class="sxs-lookup"><span data-stu-id="1b7fd-219">Activate custom Together Mode scenes</span></span>

<span data-ttu-id="1b7fd-220">Сведения о том, как конечный пользователь работает со сценами в настраиваемом режиме Together Mode.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-220">Get end-to-end information of how an end user engages with scenes in custom Together Mode scenes.</span></span>

<span data-ttu-id="1b7fd-221">**Выбор сцен и активация настраиваемой совместной сцены режима**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-221">**To choose scenes and activate custom Together Mode scenes**</span></span>

1. <span data-ttu-id="1b7fd-222">Создание нового тестового собрания.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-222">Create a new test meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1b7fd-223">При выборе **предварительного** просмотра в студии Scene сцена устанавливается как приложение в Microsoft Teams.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-223">On selecting **Preview** in the Scene studio, the scene is installed as an app in Microsoft Teams.</span></span> <span data-ttu-id="1b7fd-224">Это модель для разработчика для тестирования и опробовки сцен из студии Scene.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-224">This is the model for a developer to test and try out scenes from the Scene studio.</span></span> <span data-ttu-id="1b7fd-225">После отправки сцены в качестве приложения пользователи видят эти сцены в галерее сцен.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-225">After a scene is shipped as an app, users see these scenes in the scene gallery.</span></span>

1. <span data-ttu-id="1b7fd-226">Из **выпадаемой** галереи в верхнем левом углу выберите **режим Together Mode**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-226">From the **Gallery** drop-down in the upper-left corner, select **Together Mode**.</span></span> <span data-ttu-id="1b7fd-227">Появляется диалоговое окно **Picker** и добавляется добавленная сцена.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-227">The **Picker** dialog box appears and the scene that is added is available.</span></span>

1. <span data-ttu-id="1b7fd-228">Выберите **сцену Изменения,** чтобы изменить сцену по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-228">Select **Change scene** to change the default scene.</span></span>

1. <span data-ttu-id="1b7fd-229">В **галерее Сцены** выберите сцену, используемую для собрания.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-229">From the **Scene Gallery**, select the scene you want to use for your meeting.</span></span>

1. <span data-ttu-id="1b7fd-230">Необязательно, организатор собрания и презентер могут изменить сцену **для всех участников** собрания.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-230">Optionally, the meeting organizer and presenter can **Change scene for all participants** in the meeting.</span></span>

    >[!NOTE]
    > <span data-ttu-id="1b7fd-231">В любой момент времени для собрания можно использовать только одну сцену.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-231">At any point in time, only one scene can be used homogeneously for the meeting.</span></span> <span data-ttu-id="1b7fd-232">Если презентер или организатор изменяет сцену, она изменяется для всех.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-232">If a presenter or organizer changes a scene, it  changes for all.</span></span> <span data-ttu-id="1b7fd-233">Включение или выход из настраиваемого режима совместной работы может быть засвидетельна отдельными участниками, но в то время как в настраиваемом режиме together mode все участники имеют ту же сцену.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-233">Switching in or out of custom Together Mode scenes is up to individual participants, but while in custom Together Mode scenes, all participants have the same scene.</span></span>

1. <span data-ttu-id="1b7fd-234">Нажмите **Применить**.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-234">Select **Apply**.</span></span> <span data-ttu-id="1b7fd-235">Teams устанавливает приложение для пользователя и применяет сцену.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-235">Teams installs the app for the user and applies the scene.</span></span>

## <a name="open-a-custom-together-mode-scenes-scene-package"></a><span data-ttu-id="1b7fd-236">Откройте настраиваемый пакет сцен в режиме "Вместе"</span><span class="sxs-lookup"><span data-stu-id="1b7fd-236">Open a custom Together Mode scenes Scene Package</span></span>

<span data-ttu-id="1b7fd-237">Вы можете поделиться пакетом сцены, который является .zip, извлеченным из студии Scene другим создателям для дальнейшего расширения сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-237">You can share the Scene Package that is a .zip file retrieved from the Scene studio to other creators to further enhance the scene.</span></span> <span data-ttu-id="1b7fd-238">Можно **использовать функцию Import a Scene.**</span><span class="sxs-lookup"><span data-stu-id="1b7fd-238">The **Import a Scene** functionality can be leveraged.</span></span> <span data-ttu-id="1b7fd-239">Этот инструмент помогает развернуть пакет сцены, чтобы создатель мог продолжить создание сцены.</span><span class="sxs-lookup"><span data-stu-id="1b7fd-239">This tool helps unwrap a scene package to let the creator continue building the scene.</span></span>

![Файл застежки-молнии сцены](../assets/images/apps-in-meetings/scene-zip-file.png)

## <a name="see-also"></a><span data-ttu-id="1b7fd-241">См. также</span><span class="sxs-lookup"><span data-stu-id="1b7fd-241">See also</span></span>

[<span data-ttu-id="1b7fd-242">Приложения для Teams собраний</span><span class="sxs-lookup"><span data-stu-id="1b7fd-242">Apps for Teams meetings</span></span>](teams-apps-in-meetings.md)
