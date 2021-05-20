---
title: 'Быстрый старт: Создайте пользовательскую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams'
author: laujan
description: Краткое руководство по созданию личной вкладке с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 88ad05aacaed69d695bc918e3e8a44ec18e560ae
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566611"
---
# <a name="create-a-custom-personal-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Создайте пользовательскую личную вкладку, Node.js и генератор Yeoman для Microsoft Teams

>[!NOTE]
>Этот быстрый старт следует шагам, изложенным [в приложении Microsoft Teams в вики,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub microsoft OfficeDev.

В этом quickstart мы будем ходить через создание пользовательских личных вкладку с [помощью Teams генератора Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). Мы также загрузим приложение в Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Создание настраиваемой или статической вкладки**

Используйте клавиши стрелки, чтобы выбрать статическую вкладку.

>[!IMPORTANT]
>Компонент пути *yourDefaultTabNameTab*, на который ссылается в этом quickstart, это значение, которое вы ввели в генератор *для имени вкладки по умолчанию* плюс слово *Tab*.
>
>Например: DefaultTabName: *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>Создайте свою личную вкладку

Чтобы добавить личную вкладку в это приложение, вы создадите страницу содержимого и обновит существующие файлы:

- В редакторе кода создайте новый HTML-файл, **personal.html** и добавьте следующую разметку:

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

- Сохранить **personal.html** в веб-папке **приложения:**

    ```bash
    ./src/app/web/<yourDefaultTabNameTab>/personal.html
    ```

- Откройте **manifest.jsв** редакторе кода:

    ```bash
    ./src/manifest/manifest.json/
    ```

Добавьте следующее в `staticTabs` пустой массив `staticTabs":[]` () и добавьте следующий объект JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Не забудьте обновить **компонент пути "contentURL"** **yourDefaultTabNameTab с** вашим фактическим именем вкладки.

- Сохраните обновленный **manifest.jsна**.

- Ваша страница содержимого должна быть подана в IFrame. Откройте **Tab.ts** в редакторе кода:

    ```bash
    ./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
    ```

- Добавьте следующее в список декораторов IFrame:

    ```typescript
     @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
    ```

- Убедитесь в том, чтобы сохранить **обновленный файл Tab.ts.** Код вкладки завершен.

## <a name="build-and-run-your-application"></a>Создание и запуск приложения

Откройте командный запрос в каталоге проекта для выполнения следующих задач.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Чтобы просмотреть вашу личную вкладку, перейдите на `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![личный скриншот вкладки](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля для вкладки

Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладок было доступно из облака с помощью конечных точек HTTPS. Teams не позволяет локального хостинга, поэтому, вам нужно либо опубликовать свою вкладку на общедоступный URL или использовать прокси, который будет подвергать ваш местный порт в интернет-адрес.

Чтобы проверить расширение вкладок, вы будете использовать [ngrok](https://ngrok.com/docs), который встроен в это приложение. Ngrok является обратным прокси программное обеспечение инструмент, который создаст туннель для локально работает веб-сервера общедоступных https конечных точек. Веб-конечные точки сервера будут доступны в течение текущего сеанса на локальной машине. Когда машина выключена или засыпает, служба больше не будет доступна.

В вашем командном запросе выйдите из локального хостинга и введите следующее:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После того, как вкладка была загружена в команды Майкрософт, **через ngrok,** и успешно сохранена, вы можете просмотреть ее в Teams до окончания сеанса туннеля.

## <a name="upload-your-application-to-teams"></a>Upload заявление в Teams

- Откройте Microsoft Teams клиента. Если вы [используете веб-версию,](https://teams.microsoft.com) вы можете проверить свой передний код с помощью инструментов [разработчика браузера.](~/tabs/how-to/developer-tools.md)
- В **панели YourTeams** слева выберите меню рядом с командой, `...` которую вы используете, чтобы протестировать вкладку и выбрать **команду Manage.**
- В основной панели **выберите Приложения** из панели **вкладок Upload выбрать специальное** приложение, расположенное в правом нижнем углу страницы.
- Откройте каталог проекта, просмотрите папку **./package,** выберите папку на молнии, нажмите правой кнопкой мыши и выберите **Open.** Ваша вкладка будет загружаться в Teams.

## <a name="view-your-personal-tabs"></a>Просмотр личных вкладок

В навигационной панели, расположенной слева от Teams, `...` выберите меню и выберите приложение из списка.

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание личной вкладки с помощью ASP.NETCore](~/tabs/quickstarts/create-personal-tab-dotnet-core.md)
