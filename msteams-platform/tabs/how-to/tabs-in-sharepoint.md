---
title: Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx
author: laujan
description: Развертывание существующей вкладки Teams в SharePoint в качестве веб-части SharePoint Framework.
keywords: Разработка sharepoint Framework для вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 2e5d1b01aa5f7566e25c7720d6a0539386226576
ms.sourcegitcommit: 6caf503de5544fb8b9c8c6bef8eff4ff5a46068c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/17/2021
ms.locfileid: "50270793"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx

## <a name="rich-integration-between-teams-and-sharepoint"></a>Интеграция Teams и SharePoint

В ноябрьских выпусках Teams и SharePoint Framework v. 1.7 У разработчиков есть две мощные возможности:

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
                        <p>Создайте богатые возможности приложений в SharePoint, введя приложение Teams в Sharepoint (эта статья).</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
<li>
    <a href="https://docs.microsoft.com/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab">
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
                        <p>Перенесите веб-части SharePoint в Teams и позвольте SharePoint управлять размещением.</p>
                    </div>
                </div>
            </div>
        </div>
    </a>
</li>
</ul>

### <a name="teams-tabs-in-sharepoint"></a>Вкладки Teams в SharePoint

В SharePoint Framework v.1.7 мы поддерживаем возможность разработчиков использовать свои вкладки Teams и проводить их в SharePoint. По мере того как вкладки, вкладки, которые были в SharePoint, получают аналогичную "полную страницу", выдавая все функции вкладок Teams, сохраняя контекст и знакомство с сайтом SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework в Teams

Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework. Для разработчиков SharePoint это значительно упрощает процесс разработки вкладок Teams, так как веб-части SharePoint Framework находятся в SharePoint без необходимости в внешних службах, таких как Azure. [Узнайте больше об использовании SharePoint Framework в Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Введение

В этих инструкциях объясняется, как можно получить вкладку из примера приложения Microsoft Teams и использовать ее в SharePoint. Мы будем использовать вкладку, которая уже есть в Azure, чтобы сосредоточиться на необходимых процессах интеграции.

Пример приложения, который мы используем, — это приложение управления одаренно. Он управляет процессом найма кандидатов на открытые позиции в команде. (Само приложение, несмотря на то, что оно выглядит хорошо, на самом деле ничего не делают. Мы хотим сосредоточиться на создании приложения Teams и его загрузке в Teams, а не на создании реального приложения для управления одаренными менеджерами.)

### <a name="benefits-of-this-approach"></a>Преимущества этого подхода

- Доступ к пользователям SharePoint с помощью существующей вкладки Teams
- Загрузите манифест приложения непосредственно в каталог приложений SharePoint. [Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются в SharePoint
- Конечные пользователи настраивают вкладку на странице так же, как и любые другие веб-части SharePoint
- Ваша вкладка может получить доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как и при запуске в Teams

## <a name="step-1-testing-the-sample-app"></a>Шаг 1. Тестирование примера приложения

Скачайте пример манифеста [**приложения**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip)здесь.

В Microsoft Teams щелкните значок Магазина в левом нижнем конце, а затем "Отправить пользовательское приложение" в левом нижнем. Отложенный файл будет расположен в папке "Загрузки"; он называется TalentMgmt-Azure.zip. Если все пройдет хорошо, вы увидите экран установки и согласия для приложения управления одарением. Выберите команду, в который вы хотите установить, и нажмите кнопку "Установить". Теперь вы можете поэкспериментировать с приложением.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Шаг 2. Использование вкладки Teams в SharePoint

Загрузите и развернете пакет приложения Teams в каталоге приложений SharePoint, посетив, `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx` например.

При запросе в включить "Сделать это решение доступным для всех сайтов в организации":

![Вкладки в представлении SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

Создайте новую страницу на своем сайте, нажав кнопку шестеренки в правом верхнем правом верхнем направлении и нажав кнопку "Добавить страницу":

![Представление SharePoint](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Вы увидите, как будет делиться страницами SharePoint. Назовите страницу "Моя вкладка Teams".

Откройте панели инструментов веб-части, нажав кнопку +, и выберите вкладку Teams (с именем "Contoso HR"). Веб-части сортироваться в алфавитном порядке; Если это длинный список, вы можете найти его с помощью панели поиска. В результате на холсте будет создаваться веб-часть, содержаная вкладку Teams:

![Представление "Вкладка"](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

После завершения редактирования нажмите кнопку "Опубликовать".

Может потребоваться нажать кнопку "Добавить страницу в навигацию", чтобы получить быструю ссылку на страницу в левой панели навигации:

![Вкладка в изображении Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Шаг 3. Изучение страниц приложений в SharePoint

После публикации страницы вы можете изучить, как сделать приложение Teams более полным [в SharePoint.](/sharepoint/dev/spfx/web-parts/single-part-app-pages) При этом текущая страница преобразуется в страницу приложения, где показан обычный макет страницы SharePoint с полно страницей для вкладки Teams:

![Изображение вкладок в Sharepoint](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="code-sample"></a>Пример кода
| **Имя примера** | **Описание** | **SPFx** |
|-----------------|-----------------|----------|
| Веб-часть SPFx | Примеры веб-части SPFx для вкладок, каналов и групп. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group/spfx)

## <a name="more-information"></a>Дополнительные сведения

- [Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Использование страницы одной части приложения в SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
