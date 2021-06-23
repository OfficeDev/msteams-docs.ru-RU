---
title: Quickstart. Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams
author: surbhigupta
description: Руководство по созданию личной вкладки с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 220d1018f174fc935a10311723a730ebc74ccc33
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069199"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams

>[!NOTE]
>Этот quickstart следует шагам, описанным в приложении [Build Your First Microsoft Teams,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub.

В этом quickstart мы создам настраиваемую личную вкладку с помощью [Teams Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). Мы также загрузим приложение в Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Создание настраиваемой или статической вкладки**

Используйте клавиши со стрелками, чтобы выбрать статическую вкладку.

>[!IMPORTANT]
>Компонент пути *yourDefaultTabNameTab,* на который ссылается в этом quickstart,  это значение, которое вы ввели в генератор для имени вкладки по умолчанию плюс слово *Tab*.
>
>Например: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Создание личной вкладки

Чтобы добавить личную вкладку в это приложение, вы создайте страницу контента и обновим существующие файлы:

- В редакторе кода создайте новый HTML-файлpersonal.htm **l** и добавьте следующую разметку:

    ```html
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="UTF-8">
            <title>
                <!-- Todo: add your a title here -->
            </title>
            <meta name="viewport" content="width=device-width, initial-scale=1.0">
            <!-- inject:css -->
            <!-- endinject -->
        </head>
            <body>
                <h1>Personal Tab</h1>
                <p><img src="/assets/icon.png"></p>
                <p>This is your personal tab!</p>
            </body>
    </html>
    ```

- Сохраните **personal.html** в **веб-папке** приложения:

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Откройте **manifest.jsв** редакторе кода:

    ```bash
    ./src/manifest/manifest.json/
    ```

Добавьте следующее в пустой массив `staticTabs` () и `staticTabs":[]` добавьте следующий объект JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Не забудьте обновить компонент **пути "contentURL"** **yourDefaultTabNameTab** с фактическим именем вкладки.

- Сохраните обновленные **manifest.js.**

- Ваша страница контента должна быть подана в IFrame. Откройте **Tab.ts в** редакторе кода:

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Добавьте в список декораторов IFrame следующее:

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Обязательно сохраните обновленный **файл Tab.ts.** Код вкладки завершен.

## <a name="build-and-run-your-application"></a>Создание и запуск приложения

Откройте командную подсказку в каталоге проектов для выполнения следующих задач.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Чтобы просмотреть личную вкладку, перейдите к `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![снимок экрана личной вкладки](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS. Teams не позволяет локальному хостингу, поэтому необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который будет подвергать локальный порт URL-адресу, относящаяся к Интернету.

Чтобы протестировать расширение вкладки, вы будете использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение. Ngrok — это средство обратного прокси-программного обеспечения, которое создаст туннель для общедоступных конечных точек HTTPS локального веб-сервера. Веб-точки сервера будут доступны во время текущего сеанса на локальном компьютере. Когда машина отключена или заснул, служба больше не будет доступна.

В командной подсказке выйдите из localhost и введите следующее:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка была загружена в microsoft teams с помощью **ngrok** и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля.

## <a name="upload-your-application-to-teams"></a>Upload приложение для Teams

- Откройте Microsoft Teams клиента. Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)
- В панели **YourTeams** слева выберите меню рядом с командой, которую вы используете для тестирования вкладки, и `...` выберите команду **Manage.**
- На главной панели выберите **Приложения** из  панели вкладок и выберите Upload настраиваемого приложения, расположенного в нижнем правом углу страницы.
- Откройте каталог проектов, просмотрите **папку ./package,** выберите папку zip, щелкните правой кнопкой мыши и выберите **Открыть**. Вкладка будет загружена в Teams.

## <a name="view-your-personal-tabs"></a>Просмотр личных вкладок

В области navbar, расположенной слева от Teams, выберите меню и выберите приложение `...` из списка.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание личной вкладки с помощью ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
