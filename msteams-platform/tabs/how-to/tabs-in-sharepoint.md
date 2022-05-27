---
title: Добавление вкладки Teams в SharePoint
author: surbhigupta
description: Узнайте, как развернуть существующую вкладку Teams в SharePoint в виде веб-части SharePoint Framework с помощью примеров кода.
keywords: разработка в SharePoint Framework вкладок Teams
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 54fd6858a115662e24944a692458bb3d4e8034a0
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757313"
---
# <a name="add-teams-tab-to-sharepoint"></a>Добавление вкладки Teams в SharePoint

Вы можете получить широкие возможности интеграции между Microsoft Teams и SharePoint, добавив вкладку Microsoft Teams в SharePoint в качестве веб-части SPFx. В этом документе описывается, как взять вкладку из примера приложения Microsoft Teams и использовать ее в SharePoint.

## <a name="rich-integration-between-teams-and-sharepoint"></a>Расширенная интеграция между Teams и SharePoint

В ноябрьском выпуске Teams и SharePoint Framework версии 1.7 разработчикам доступно две мощных возможности:

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
                        <h3>Вкладки Teams в SharePoint</h3>
                        <p>Создавайте разнообразные интерфейсы приложений в SharePoint, добавляя приложение Teams в SharePoint (рассмотрено в этой статье).</p>
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
                        <p>Добавьте свои веб-части SharePoint в Teams и позвольте SharePoint управлять размещением за вас.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Вкладки Teams в SharePoint

В SharePoint Framework версии 1.7 вы можете разместить свои вкладки Teams в SharePoint. Вкладки, размещенные в SharePoint, получают аналогичный **полностраничный** интерфейс, предоставляя все функции вкладок Teams и сохраняя контекст и удобство сайта SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework в Teams

Вы также можете реализовать свои вкладки Microsoft Teams с помощью SharePoint Framework. Веб-части SharePoint Framework размещаются в SharePoint, что избавляет от необходимости использования внешних служб, например Azure. Для разработчиков SharePoint это значительно упрощает процесс разработки вкладок Teams. Дополнительные сведения о SharePoint Framework в Teams см. в статье [Как использовать SharePoint Framework в Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Введение

Вкладка, используемая здесь, уже размещена в Azure, чтобы сосредоточиться на необходимых действиях по интеграции.

Пример используемого приложения — это приложение управления кадровым потенциалом. Оно управляет процессом найма кандидатов на открытые должности в команде. Создайте пример приложения Teams и загрузите его в Teams. Не создавайте реальное приложение для управления актерами.

### <a name="benefits-of-this-approach"></a>Преимущества этого подхода

* Охват пользователей SharePoint с помощью существующей вкладки Teams.
* Отправка манифеста приложения непосредственно в каталог приложений SharePoint. [Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются в SharePoint.
* Пользователи настраивают вкладку на странице аналогично другим веб-частям SharePoint.
* Ваша вкладка может получить доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как при запуске внутри Teams.

Чтобы добавить вкладку Teams в SharePoint, выполните следующие действия.

## <a name="1-test-the-sample-app"></a>1. Тестирование примера приложения

Скачайте [манифест примера приложения](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

1. Откройте Microsoft Teams.
1. Щелкните значок **Appstore** в левом нижнем углу боковой вкладки.
1. Выберите **Отправить пользовательское приложение** в левом нижнем углу. На следующем изображении показан соответствующий экран.  

    ![отправка пользовательского приложения](~/assets/images/tabs/tabs-in-sharepoint/upload-custom-app.png)

1. Файл для отправки находится в папке **Загрузки**. Он называется TalentMgmt-Azure.zip. На следующем изображении показан соответствующий экран.

    ![TalentMgmt в Azure](~/assets/images/tabs/tabs-in-sharepoint/talentmgmt-azure.png)

1. Вы можете увидеть экран установки или предоставления согласия для приложения управления кадровым потенциалом. Выберите команду, которую нужно установить.
1. Выберите **Установить** и начните экспериментировать с приложением.

## <a name="2-use-teams-tab-in-sharepoint"></a>2. Использование вкладки Teams в SharePoint

1. Отправьте и разверните пакет приложения Teams в каталоге приложений SharePoint, посетив страницу `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`. Например, `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`.

1. При появлении запроса включите параметр **Сделать это решение доступным для всех сайтов в организации**.
На следующем изображении показан соответствующий экран.

   ![Вкладки в представлении SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

1. На своем сайте создайте страницу. Для этого нажмите кнопку шестеренки в правом верхнем углу и выберите **Добавить страницу**.
На следующем изображении показан соответствующий экран.

   ![Представление SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

1. Вы можете просмотреть интерфейс разработки страниц SharePoint. Назовите свою страницу **Моя вкладка Teams**.

1. Откройте панель элементов веб-части, нажав кнопку `+`, и выберите вкладку Teams с именем **Отдел кадров Contoso**. Веб-части сортируются по алфавиту. Если это длинный список, его можно найти с помощью панели поиска. При этом на холсте создается веб-часть, содержащая вкладку Teams. На следующем изображении показано представление вкладки.

   ![Представление вкладки](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

1. Нажмите кнопку **Опубликовать** после завершения редактирования.

1. Выберите **Добавить страницу в навигацию**, чтобы получить быструю ссылку на страницу в панели навигации слева.
На следующем изображении показана вкладка в SharePoint.

   ![Изображение вкладки в SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="3-explore-app-pages-in-sharepoint"></a>3. Обзор страниц приложения в SharePoint

После публикации своей страницы вы можете изучить статью о [превращении приложения Teams в более комплексный интерфейс в SharePoint](/sharepoint/dev/spfx/web-parts/single-part-app-pages). При этом текущая страница преобразуется в страницу приложения, отображая обычный макет страницы SharePoint с полностраничным интерфейсом для вкладки Teams.

На следующем изображении показан комплексный интерфейс приложения Teams в SharePoint. ![Изображение вкладок в SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **SPFx** |
|-----------------|-----------------|----------|
| Веб-часть SPFx | Примеры веб-частей SPFx для вкладок, каналов и групп. | [Просмотр](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="see-also"></a>Дополнительные ресурсы

* [Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
* [Использование страниц приложений с одной веб-частью в SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
* [Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
