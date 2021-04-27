---
title: Quickstart. Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Руководство по созданию личной вкладки с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 30143fa3c84a68ae6c34176b252badaa4cef9613
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019554"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Quickstart. Создайте настраиваемую личную вкладку с Node.js и генератором Yeoman для Microsoft Teams

>[!NOTE]
>Этот quickstart следует шагам, описанным в приложении [Build Your First Microsoft Teams App Wiki,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub.

В этом quickstart мы создам настраиваемую личную вкладку с помощью генератора [Teams Yeoman.](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Мы также загрузим приложение в Team.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Хотите создать настраиваемую или статическую вкладку?**

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

Microsoft Teams — это полностью облачный продукт, который требует, чтобы содержимое вкладок было доступно в облаке с помощью конечных точек HTTPS. Команды не позволяют локальному размещению, поэтому необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который будет подвергать локальный порт URL-адресу, относящаяся к Интернету.

Чтобы протестировать расширение вкладки, вы будете использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение. Ngrok — это средство обратного прокси-программного обеспечения, которое создаст туннель для общедоступных конечных точек HTTPS локального веб-сервера. Веб-точки сервера будут доступны во время текущего сеанса на локальном компьютере. Когда машина отключена или заснул, служба больше не будет доступна.

В командной подсказке выйдите из localhost и введите следующее:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка была загружена в microsoft teams с помощью *ngrok* и успешно сохранена, ее можно просмотреть в Teams до окончания сеанса туннеля.

## <a name="upload-your-application-to-teams"></a>Отправка приложения в Teams

- Откройте клиент Microsoft Teams. Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)
- В панели *YourTeams* слева выберите меню рядом с командой, которую вы используете для тестирования вкладки, и `...` выберите команду **Manage.**
- На главной панели выберите **Приложения** из панели вкладок и выберите **Загрузите** пользовательское приложение, расположенное в нижнем правом углу страницы.
- Откройте каталог проектов, просмотрите **папку ./package,** выберите папку zip, щелкните правой кнопкой мыши и выберите **Открыть**. Вкладка будет загружена в Teams.

## <a name="view-your-personal-tabs"></a>Просмотр личных вкладок

В области navbar, расположенной слева от клиента Teams, выберите меню и выберите `...` приложение из списка.
