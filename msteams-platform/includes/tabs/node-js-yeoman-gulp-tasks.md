## <a name="create-the-app-package"></a><span data-ttu-id="ad2dd-101">Создание пакета приложения</span><span class="sxs-lookup"><span data-stu-id="ad2dd-101">Create the app package</span></span>

<span data-ttu-id="ad2dd-102">Для тестирования вкладки в Teams необходим пакет приложения.</span><span class="sxs-lookup"><span data-stu-id="ad2dd-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="ad2dd-103">Это ZIP-папка, содержащая следующие обязательные файлы:</span><span class="sxs-lookup"><span data-stu-id="ad2dd-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="ad2dd-104">**Значок с полным цветом** , измеряющий 192 x 192 пикселей.</span><span class="sxs-lookup"><span data-stu-id="ad2dd-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="ad2dd-105">**Прозрачный значок структуры** , измеряющий 32 x 32 пикселей.</span><span class="sxs-lookup"><span data-stu-id="ad2dd-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="ad2dd-106">Файл **manifest. JSON** , задающий атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="ad2dd-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="ad2dd-107">Пакет создается с помощью задачи gulp, которая проверяет файл manifest. JSON и создает папку ZIP в файле `./package directory`.</span><span class="sxs-lookup"><span data-stu-id="ad2dd-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="ad2dd-108">В командной строки введите:</span><span class="sxs-lookup"><span data-stu-id="ad2dd-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="ad2dd-109">Создание приложения</span><span class="sxs-lookup"><span data-stu-id="ad2dd-109">Build your application</span></span>

<span data-ttu-id="ad2dd-110">Команда Build преобразует решение в папку *./dist.* .</span><span class="sxs-lookup"><span data-stu-id="ad2dd-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="ad2dd-111">Затем введите:</span><span class="sxs-lookup"><span data-stu-id="ad2dd-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="ad2dd-112">Запуск приложения на localhost</span><span class="sxs-lookup"><span data-stu-id="ad2dd-112">Run your application in localhost</span></span>

<span data-ttu-id="ad2dd-113">Запустите локальный веб-сервер, введя следующие команды:</span><span class="sxs-lookup"><span data-stu-id="ad2dd-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="ad2dd-114">Введите `http://localhost:3007/<yourDefaultAppNameTab>/` в браузере и просмотрите домашнюю страницу приложения:</span><span class="sxs-lookup"><span data-stu-id="ad2dd-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![снимок экрана: Домашняя страница](~/assets/images/tab-images/homePage.png)