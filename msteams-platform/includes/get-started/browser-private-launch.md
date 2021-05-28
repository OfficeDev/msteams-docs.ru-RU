### <a name="optional-adjust-your-browser-launch-settings"></a><span data-ttu-id="366af-101">(Необязательный) Настройка параметров запуска браузера</span><span class="sxs-lookup"><span data-stu-id="366af-101">(Optional) Adjust your browser launch settings</span></span>

<span data-ttu-id="366af-102">При разработке Teams обычно запускать приложение в другом клиенте разработчика или с альтернативными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="366af-102">When developing a Teams app, it is common to run your app in an alternate developer tenant or with alternate credentials.</span></span>  <span data-ttu-id="366af-103">И Microsoft Edge, и Google Chrome предоставляют возможности для настройки параметров запуска для браузера.</span><span class="sxs-lookup"><span data-stu-id="366af-103">Both Microsoft Edge and Google Chrome provide facilities to adjust the launch settings for your browser.</span></span>  <span data-ttu-id="366af-104">Например, чтобы обновить проект для поддержки режима InPrivate (Microsoft Edge), откройте `.vscode/launch.json` файл в проекте.</span><span class="sxs-lookup"><span data-stu-id="366af-104">For example, to update the project to support InPrivate mode (Microsoft Edge), open the `.vscode/launch.json` file in your project.</span></span>  <span data-ttu-id="366af-105">Найми соответствующие параметры запуска и добавьте в каждый из них следующий блок:</span><span class="sxs-lookup"><span data-stu-id="366af-105">Look for the appropriate launch settings, and add the following block to each one:</span></span>

``` json
"runtimeArgs": [ "--inprivate" ]
```

<span data-ttu-id="366af-106">Например, параметр запуска для локального запуска выглядит так:</span><span class="sxs-lookup"><span data-stu-id="366af-106">For instance, the launch setting for running locally looks like this:</span></span>

``` json
{
   "name": "Start and Attach to Frontend (Edge)",
   "type": "pwa-msedge",
   "request": "launch",
   "url": "https://teams.microsoft.com/_#/l/app/${localTeamsAppId}?installAppPackage=true",
   "preLaunchTask": "Start Frontend",
   "postDebugTask": "Stop All Services",
   "presentation": {
         "group": "all",
         "hidden": true
   },
   "runtimeArgs": [ "--inprivate" ]
},
```

<span data-ttu-id="366af-107">Кроме того, можно настроить браузер для использования последнего известного профиля.</span><span class="sxs-lookup"><span data-stu-id="366af-107">Alternatively, you can configure your browser to use the last known profile.</span></span> <span data-ttu-id="366af-108">[Создайте новый профиль](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) в Microsoft Edge.</span><span class="sxs-lookup"><span data-stu-id="366af-108">[Create a new profile](https://support.microsoft.com/topic/sign-in-and-create-multiple-profiles-in-microsoft-edge-df94e622-2061-49ae-ad1d-6f0e43ce6435) in Microsoft Edge.</span></span>  <span data-ttu-id="366af-109">Затем настройть параметры, чтобы использовать последний известный профиль для новых ссылок:</span><span class="sxs-lookup"><span data-stu-id="366af-109">Then adjust the settings to use the last known profile for new links:</span></span>

- <span data-ttu-id="366af-110">В Microsoft Edge откройте `edge://settings/profiles/multiProfileSettings` .</span><span class="sxs-lookup"><span data-stu-id="366af-110">In Microsoft Edge, open `edge://settings/profiles/multiProfileSettings`.</span></span>
- <span data-ttu-id="366af-111">**Отключите автоматическое переключение профиля.**</span><span class="sxs-lookup"><span data-stu-id="366af-111">Turn off **Automatic profile switching**.</span></span>
- <span data-ttu-id="366af-112">Для профиля **по умолчанию для внешних ссылок** выберите **Last used (default).**</span><span class="sxs-lookup"><span data-stu-id="366af-112">For the **Default profile for external links**, select **Last used (default)**.</span></span>

<span data-ttu-id="366af-113">Убедитесь, что браузер открыт для правильного профиля перед отладки приложения.</span><span class="sxs-lookup"><span data-stu-id="366af-113">Ensure your browser is opened to the correct profile before debugging your app.</span></span>
