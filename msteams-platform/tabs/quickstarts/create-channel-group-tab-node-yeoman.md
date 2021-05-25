---
title: Создание настраиваемой вкладки канала и группы с Node.js и генератором Yeoman для Microsoft Teams
author: laujan
description: Руководство quickstart по созданию вкладки канала и группы с генератором Yeoman для Microsoft Teams.
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 70b1dbe5a5abafa44ddbdf9045c55a33cf8fcb20
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630245"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>Создание настраиваемой вкладки канала и группы с Node.js и генератора Yeoman для Microsoft Teams

>[!NOTE]
>Этот quickstart следует шагам, описанным в приложении [Build Your First Microsoft Teams,](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) найденном в репозитории Microsoft OfficeDev GitHub.

В этом quickstart мы создам настраиваемый канал и вкладку группы с помощью [Teams Yeoman](https://github.com/OfficeDev/generator-teams/).

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**Хотите создать настраиваемую или статическую вкладку?**

Используйте клавиши стрелки для выбора настраиваемой вкладки.

**Какие области вы собираетесь использовать для вкладки?**

Вы можете выбрать группу и/или групповой чат

**Хотите, чтобы эта вкладка была доступна в SharePoint Online? (Y/n)** 

Выберите **n**.

>[!IMPORTANT]
>Компонент пути **yourDefaultTabNameTab,** на который ссылается в этом quickstart,  это значение, которое вы ввели в генератор для имени вкладки по умолчанию плюс слово **Tab**.
>
>Например: DefaultTabName: **MyTab**  =>  **/MyTabTab/**

В каталоге проектов перейдите к следующему:

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

Здесь вы найдете логику вкладки. Найдите метод и добавьте следующий тег и содержимое в `render()` `<div>` верхнюю часть `<PanelBody>` кода контейнера:

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

Обязательно сохраните обновленный файл.

## <a name="build-and-run-your-application"></a>Создание и запуск приложения

Откройте командную подсказку в каталоге проектов для выполнения следующих задач.

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

Чтобы просмотреть страницу конфигурации вкладок, перейдите к `https://localhost:3007/<yourDefaultAppNameTab>/config.html` . Должны отображаться следующие сведения:

![Скриншот страницы конфигурации](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>Создание безопасного туннеля на вкладке

Microsoft Teams является полностью облачным продуктом и требует, чтобы содержимое вкладки было доступно в облаке с помощью конечных точек HTTPS. Teams не позволяет локальному хостингу, поэтому необходимо либо опубликовать вкладку на общедоступный URL-адрес, либо использовать прокси-сервер, который будет подвергать локальный порт URL-адресу, относящаяся к Интернету.

Чтобы протестировать расширение вкладки, вы будете использовать [ngrok,](https://ngrok.com/docs)встроенный в это приложение. Ngrok — это средство обратного прокси-программного обеспечения, которое создаст туннель для общедоступных конечных точек HTTPS локального веб-сервера. Веб-точки сервера будут доступны во время текущего сеанса на локальном компьютере. Когда машина отключена или заснул, служба больше не будет доступна.

В командной подсказке выйдите из localhost и введите следующее:

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> После того как вкладка была загружена в группы Майкрософт и успешно сохранена, ее можно просмотреть в галерее вкладок, добавить ее в планку вкладок и взаимодействовать с ней до окончания сеанса туннеля ngrok. Если вы перезапустите сеанс ngrok, вам потребуется обновить приложение с новым URL-адресом.

## <a name="upload-your-application-to-teams"></a>Upload приложение для Teams

- Откройте Microsoft Teams клиента. Если вы используете [веб-версию,](https://teams.microsoft.com) вы можете проверить исходный код с помощью средств разработчика [браузера.](~/tabs/how-to/developer-tools.md)
- В панели *YourTeams* слева выберите меню рядом с командой, которую вы используете для тестирования вкладки, и `...` выберите команду **Manage.**
- На главной панели выберите **Приложения** из  панели вкладок и выберите Upload настраиваемого приложения, расположенного в нижнем правом углу страницы.
- Откройте каталог проектов, просмотрите **папку ./package,** выберите папку почтовый индекс пакета приложений и **откройте**. Вкладка будет загружена в Teams.
- Вернись в команду, выберите канал, в котором вы хотите отобразить вкладку, выберите ➕ из панели вкладок и выберите вкладку из галереи.
- Следуйте указаниям для добавления вкладки. Обратите внимание, что существует настраиваемый диалоговое окно конфигурации для вкладки канал/группа.
- Выберите **Сохранить,** и вкладка будет добавлена в вкладку канала.

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание настраиваемой вкладки канала и группы с помощью ASP.NETCore](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
