---
title: Добавление вкладки Teams в SharePoint
author: surbhigupta
description: Узнайте, как развернуть существующую вкладку Teams для SharePoint в качестве SharePoint Framework веб-части с помощью образцов кода.
keywords: teams tabs sharepoint framework development
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: ea5f5cc90e1451ab65a31205f4c83137163a36cc
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399228"
---
# <a name="add-teams-tab-to-sharepoint"></a>Добавление вкладки Teams в SharePoint

Вы можете получить богатый опыт интеграции между Microsoft Teams и SharePoint, добавив вкладку Microsoft Teams в SharePoint как SPFx веб-части. В этом документе вы можете узнать, как взять вкладку из Microsoft Teams и использовать ее в SharePoint.

## <a name="rich-integration-between-teams-and-sharepoint"></a>Насыщенная интеграция между Teams и SharePoint

С выпуском Teams и SharePoint Framework v.1.7 у разработчиков есть две мощные возможности:

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" alt="tab-in-sharepoint view"/>
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Teams вкладок в SharePoint</h3>
                        <p>Создайте богатые возможности приложения в SharePoint, введя Teams приложение в SharePoint (эта статья).</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" alt="web-part-exposed-as-a-tab" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>SharePoint Framework в Teams</h3>
                        <p>Принесите SharePoint веб-части в Teams и SharePoint управлять хостингом для вас.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Teams вкладки в SharePoint

С SharePoint Framework v.1.7 вы можете Teams вкладки SharePoint. Так как вкладки, SharePoint, получают аналогичный полный опыт страницы, подвергая все возможности вкладок Teams, сохраняя контекст и знакомство SharePoint сайта.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework в Teams

Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework. SharePoint Framework веб-части находятся в SharePoint без необходимости для внешних служб, таких как Azure. Для SharePoint разработчиков это значительно упрощает процесс разработки Teams вкладок. Дополнительные сведения о SharePoint Framework в Teams см. в SharePoint Framework в [Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Введение

Вкладка, используемая здесь, уже находится в Azure, чтобы сосредоточиться на требуемой работе по интеграции.

Используемая примерная приложение — приложение управления талантами. Он управляет процессом найма кандидатов на открытые позиции в команде. Создайте пример Teams и загрузите его в Teams. Не создавайте реальное приложение для управления талантами.

### <a name="benefits-of-this-approach"></a>Преимущества этого подхода

* Охватите SharePoint пользователями с помощью существующей Teams вкладки.
* Upload манифест приложения непосредственно в каталоге SharePoint приложения. [Teams пакеты приложений](~/concepts/build-and-test/apps-package.md) теперь поддерживаются SharePoint.
* Пользователи настраивают вкладку на странице так же, как и SharePoint веб-части.
* Ваша вкладка может получить доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как и при запуске Teams.

Чтобы добавить вкладку Teams в SharePoint, выполните следующие действия, чтобы добавить вкладку Teams в SharePoint:

## <a name="1-test-the-sample-app"></a>1. Проверка примера приложения

Скачайте [манифест примера приложения](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

1. Откройте Microsoft Teams.
1. Выберите **значок Appstore** в нижней левой части боковой вкладки.
1. Выберите **Upload настраиваемого приложения** в левом нижнем ок. На следующем изображении отображается соответствующий экран:  

    ![загрузка настраиваемой приложения](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. Файл для отправки находится в папке **Downloads** . Он называется TalentMgmt-Azure.zip. На следующем изображении отображается соответствующий экран:

    ![TalentMgmt в Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Вы можете увидеть экран установки или согласия для приложения управления талантами. Выберите команду, которая будет устанавливаться.
1. Выберите **установку** и начните экспериментировать с приложением.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Используйте вкладку Teams в SharePoint

1. Upload развертывание пакета Teams приложения в каталоге SharePoint приложения, посетив `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`. Например, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. При запросе **вделайте это решение доступным для всех сайтов в организации**.
На следующем изображении отображается соответствующий экран:

   ![Вкладки в представлении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. На сайте создайте новую страницу, выбрав кнопку передач в правом верхнем справа, а затем выберите **Добавить страницу**.
На следующем изображении отображается соответствующий экран:

   ![Представление Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Вы можете увидеть опыт SharePoint страниц. Назови страницу **My Teams Tab**.

1. Откройте инструментарий `+` веб-части, выбрав кнопку, и выберите вкладку Teams с именем **Hr Contoso**. Веб-части сортироваться в алфавитном порядке. Если это длинный список, его можно найти с помощью панели поиска. Это создает веб-часть на холсте, содержаще вкладку Teams. На следующем изображении отображается представление вкладки:

   ![Представление Tab](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Выберите **кнопку Публикация** после завершения редактирования.

1. Выберите **страницу Добавить в навигацию** , чтобы иметь быструю ссылку на страницу в левой панели навигации.
На следующем изображении отображается вкладка в Sharepoint:

   ![Вкладка в изображении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Изучите страницы приложений в SharePoint

После публикации страницы вы можете изучить возможность превращения [Teams](/sharepoint/dev/spfx/web-parts/single-part-app-pages) приложения в более полное SharePoint. Это преобразует текущую страницу в страницу приложения, демонстрируя SharePoint макет страницы с полным опытом страницы для вкладки Teams.

На следующем изображении отображается полное Teams приложения в SharePoint: ![Изображение вкладок в Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **SPFx** |
|-----------------|-----------------|----------|
| SPFx веб-части | SPFx веб-части для вкладок, каналов и групп. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Дополнительные ресурсы

* [Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [Использование страниц приложений с одной веб-частью в SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
