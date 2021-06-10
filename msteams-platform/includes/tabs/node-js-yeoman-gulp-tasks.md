## <a name="create-the-app-package"></a><span data-ttu-id="d5f44-101">Создание пакета приложений</span><span class="sxs-lookup"><span data-stu-id="d5f44-101">Create the app package</span></span>

<span data-ttu-id="d5f44-102">Для проверки вкладки в Teams вам потребуется пакет Teams.</span><span class="sxs-lookup"><span data-stu-id="d5f44-102">You'll need an app package to test your tab in Teams.</span></span> <span data-ttu-id="d5f44-103">Это папка zip, которая содержит следующие необходимые файлы:</span><span class="sxs-lookup"><span data-stu-id="d5f44-103">It's a zip folder that contains the following required files:</span></span>

- <span data-ttu-id="d5f44-104">Значок **полного цвета** размером 192 x 192 пикселя.</span><span class="sxs-lookup"><span data-stu-id="d5f44-104">A **full color icon** measuring 192 x 192 pixels.</span></span>
- <span data-ttu-id="d5f44-105">Прозрачный **значок контура** размером 32 x 32 пикселя.</span><span class="sxs-lookup"><span data-stu-id="d5f44-105">A **transparent outline icon** measuring 32 x 32 pixels.</span></span>
- <span data-ttu-id="d5f44-106">Файл **manifest.js,** который указывает атрибуты приложения.</span><span class="sxs-lookup"><span data-stu-id="d5f44-106">A **manifest.json** file that specifies the attributes of your app.</span></span>

<span data-ttu-id="d5f44-107">Пакет создается с помощью задачи gulp, которая проверяет manifest.jsфайл и создает папку zip в `./package directory` .</span><span class="sxs-lookup"><span data-stu-id="d5f44-107">The package is created via a gulp task that validates the manifest.json file and generates the zip folder in the `./package directory`.</span></span> <span data-ttu-id="d5f44-108">В командную подсказку введите:</span><span class="sxs-lookup"><span data-stu-id="d5f44-108">In the command prompt enter:</span></span>

```bash
gulp manifest
```

## <a name="build-your-application"></a><span data-ttu-id="d5f44-109">Сборка приложения</span><span class="sxs-lookup"><span data-stu-id="d5f44-109">Build your application</span></span>

<span data-ttu-id="d5f44-110">Команда сборки перекладывания решения в *папку ./dist.*</span><span class="sxs-lookup"><span data-stu-id="d5f44-110">The build command transpiles your solution into the *./dist* folder.</span></span> <span data-ttu-id="d5f44-111">Далее введите:</span><span class="sxs-lookup"><span data-stu-id="d5f44-111">Next,enter:</span></span>

```bash
gulp build
```

## <a name="run-your-application-in-localhost"></a><span data-ttu-id="d5f44-112">Запустите приложение в localhost</span><span class="sxs-lookup"><span data-stu-id="d5f44-112">Run your application in localhost</span></span>

<span data-ttu-id="d5f44-113">Запустите локальный веб-сервер, введя следующие:</span><span class="sxs-lookup"><span data-stu-id="d5f44-113">Start a local web server by entering the following:</span></span>

```bash
gulp serve
```

<span data-ttu-id="d5f44-114">Введите `http://localhost:3007/<yourDefaultAppNameTab>/` в браузере и просмотр домашней страницы приложения:</span><span class="sxs-lookup"><span data-stu-id="d5f44-114">Enter `http://localhost:3007/<yourDefaultAppNameTab>/` in your browser and view your application's home page:</span></span>

![Снимок экрана домашней страницы](~/assets/images/tab-images/homePage.png)