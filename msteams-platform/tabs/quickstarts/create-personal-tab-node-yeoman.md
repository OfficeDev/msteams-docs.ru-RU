---
title: 'Краткое руководство: Создание настраиваемой вкладки личных настроек с Node. js и генератором Yeoman для Microsoft Teams'
author: laujan
description: Руководство по созданию личных вкладок с генератором Yeoman для Microsoft Teams.
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675161"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Краткое руководство: Создание настраиваемой вкладки личных настроек с Node. js и генератором Yeoman для Microsoft Teams

>[!NOTE]
>Это руководство соответствует действиям, описанным в статье [Создание первого вики-сайта приложения Microsoft Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) , который находится в репозитории Microsoft OfficeDev GitHub.

В этом руководстве мы рассмотрим создание настраиваемой вкладки с помощью [генератора Yeoman Teams](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App). Мы также загружаем приложение в группу.

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Вы хотите создать настраиваемую или статическую вкладку?**

С помощью клавиш со стрелками выберите статическую вкладку.

>[!IMPORTANT]
>Компонент Path *йоурдефаулттабнаметаб*, указанный в этом кратком руководстве, — это значение, введенное в генератор для *имени вкладки по умолчанию* , а также для *вкладки*Word.
>
>Пример: дефаулттабнаме: *митаб* => */митабтаб/*

## <a name="create-your-personal-tab"></a>Создание вкладки "личные"

Чтобы добавить в это приложение вкладку Личные, вы создадите страницу контента и обновите существующие файлы:

- В редакторе кода создайте новый HTML-файл **Personal. HTML** и добавьте следующую разметку:

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

- Сохраните **личный. HTML** в **веб-** папке приложения:

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- Откройте **манифест. JSON** в редакторе кода.

```bash
./src/manifest/manifest.json/
```

Добавьте следующий код в пустой `staticTabs` массив (`staticTabs":[]`) и добавьте следующий объект JSON:

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

Не забудьте обновить компонент пути **"contentURL"** **йоурдефаулттабнаметаб** с именем текущей вкладки.

- Сохраните обновленный **манифест. JSON**.

- Страница контента должна обслуживаться в IFrame. Откройте **вкладку "TS"** в редакторе кода.

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- Добавьте следующие элементы в список декораторов IFrame:

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- Обязательно сохраните обновленный файл **TAB. TS** . Ваш код табуляции заполнен.

## <a name="build-and-run-your-application"></a>Построение и запуск приложения

Откройте командную строку в каталоге проекта, чтобы выполнить следующие задачи.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Чтобы просмотреть вкладку Личные, перейдите на страницу`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![снимок экрана: вкладка "личные"](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Установка безопасного туннеля для вкладки

Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладки было доступно из облака с использованием конечных точек HTTPS. В Teams не разрешается локальное размещение, поэтому необходимо либо опубликовать вкладку на общедоступном URL-адресе, либо использовать прокси-сервер, который будет предоставлять локальный порт URL-адресу, доступному для выхода в Интернет.

Чтобы протестировать расширение вкладки, вы будете использовать [ngrok](https://ngrok.com/docs), встроенный в это приложение. Ngrok — это программное средство обратного прокси-сервера, которое создает туннель для общедоступных конечных точек HTTPS на локальном веб-сервере. Конечные точки веб-сервера будут доступны в текущем сеансе на локальном компьютере. При завершении работы компьютера или переходе в спящий режим служба становится недоступной.

В командной строки выйдите из localhost и введите следующую команду:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После отправки вкладки в Microsoft Teams с помощью *ngrok*и успешного сохранения его можно просмотреть в Teams до завершения сеанса туннеля.

## <a name="upload-your-application-to-teams"></a>Отправка приложения в Teams

- Откройте клиент Microsoft Teams. Если вы используете [версию на основе веб-сайта](https://teams.microsoft.com) , вы можете проверить интерфейсный код с помощью [средств разработчика](~/tabs/how-to/developer-tools.md)в браузере.
- На панели *йоуртеамс* слева выберите `...` меню рядом с командой, которую вы используете для тестирования вкладки, и выберите пункт **Управление командой**.
- В главной панели выберите **приложения** из панели вкладок и нажмите кнопку **Отправить пользовательское приложение** , расположенное в правом нижнем углу страницы.
- Откройте каталог проекта, перейдите в папку **./паккаже** , выберите папку ZIP, щелкните правой кнопкой мыши и выберите команду **Открыть**. Вкладка будет загружена в Teams.

## <a name="view-your-personal-tabs"></a>Просмотр личных вкладок

В панели навигации, расположенной в левой части клиента Teams, выберите `...` меню и выберите приложение из списка.
