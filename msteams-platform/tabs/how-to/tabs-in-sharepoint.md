---
title: Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx
author: laujan
description: Сведения о том, как развернуть существующую вкладку Teams в SharePoint в качестве веб-части SharePoint Framework.
keywords: разработка SharePoint Framework для вкладок Teams
ms.topic: conceptual
ms.author: ''
ms.openlocfilehash: b29cd29891779a69a0342f10d383792b3818590a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675402"
---
# <a name="adding-a-microsoft-teams-tab-in-sharepoint-as-an-spfx-web-part"></a>Добавление вкладки Microsoft Teams в SharePoint в качестве веб-части SPFx

> [!IMPORTANT]
> Эта функция в настоящее время находится на этапе тестирования и может быть изменена. Он не поддерживается для использования в рабочих средах. Отзывы и предложения по этой функции отправляйте с помощью [списка проблем в документации разработчиков SharePoint](https://github.com/SharePoint/sp-dev-docs/issues).

## <a name="rich-integration-between-teams-and-sharepoint"></a>Расширенная интеграция между Teams и SharePoint

С помощью выпуска Teams и SharePoint Framework в ноябре. 1,7 у разработчиков есть два мощных возможности:

<ul  class="panelContent cardsC">
<li>
    <a href="#introduction">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage bgdAccent1">
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/image084.png" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h3>Вкладки Teams в SharePoint</h3>
                        <p>Создайте полнофункциональные приложения в SharePoint, переведя приложение Teams в SharePoint (Эта статья).</p>
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
                            <img src="~/assets/images/tabs/tabs-in-sharepoint/SharePoint-web-part-exposed-as-a-Tab-in-Microsoft-Teams.png" />
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

В SharePoint Framework v. 1.7 мы теперь поддерживаем возможность разработчикам принимать свои вкладки Teams и размещать их в SharePoint. Как вкладки, размещенные в SharePoint, получают похожий вид "полная страница", предоставляя все функции вкладок Teams, сохраняя контекст и знакомство с сайтом SharePoint.

### <a name="sharepoint-framework-in-teams"></a>SharePoint Framework в Teams

Вы также можете реализовать вкладки Microsoft Teams с помощью SharePoint Framework. Для разработчиков SharePoint это значительно упрощает процесс разработки для вкладок Teams, так как веб-части SharePoint Framework размещаются в SharePoint без необходимости использования внешних служб, таких как Azure. [Узнайте больше об использовании SharePoint Framework в Teams.](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)

## <a name="introduction"></a>Введение

В этих инструкциях объясняется, как можно взять вкладку из примера приложения Microsoft Teams и использовать его в SharePoint. Мы будем использовать вкладку, которая уже размещена в Azure, чтобы сосредоточиться на необходимой работе по интеграции.

Пример приложения, который мы используем, является приложением для управления. Он управляет процессом найма кандидатов для открытых позиций в группе. (Само приложение, хотя оно отлично, не выполняет никаких действий. Мы хотим сосредоточиться на создании приложения Teams и его загрузке в Teams, но не создавать приложение для управления реальными специалистами.

### <a name="benefits-of-this-approach"></a>Преимущества этого подхода

- Доступ к пользователям SharePoint с помощью текущей вкладки групп
- Отправьте манифест приложения непосредственно в каталог приложений SharePoint. [Пакеты приложений Teams](~/concepts/build-and-test/apps-package.md) теперь поддерживаются в SharePoint
- Конечные пользователи настраивают вкладку на странице, как и любые другие веб-части SharePoint
- Вкладка может получать доступ к [контексту](~/tabs/how-to/access-teams-context.md) так же, как и при работе в Teams

## <a name="step-1-testing-the-sample-app"></a>Шаг 1: Тестирование примера приложения

Скачайте пример манифеста приложения [**отсюда**](https://github.com/MicrosoftDocs/msteams-docs/raw/master/msteams-platform/assets/downloads/TalentMgmt-Azure.zip).

В Microsoft Teams щелкните значок магазин в левом нижнем углу, а затем "Отправить настраиваемое приложение" в нижнем левом углу. Файл, который требуется отправить, будет размещен в папке "загрузки"; Он называется Талентмгмт-Азуре. zip. Если все правильно, вы увидите экран Установка/согласие для приложения управления. Выберите группу, в которую вы хотите установить, и нажмите кнопку установить. Теперь вы можете поэкспериментировать с приложением.

## <a name="step-2-using-the-teams-tab-in-sharepoint"></a>Шаг 2: Использование вкладки "команды" в SharePoint

Отправьте и разверните пакет приложения Teams в каталоге приложений SharePoint, посетив `https://YOUR_TENANT_NAME.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`, например,. `https://contoso.sharepoint.com/sites/apps/AppCatalog/Forms/AllItems.aspx`

При появлении соответствующего запроса включите параметр "сделать это решение доступным для всех сайтов в организации":

![](~/assets/images/tabs/tabs-in-sharepoint/image065.png)

На сайте создайте новую страницу, нажав кнопку шестеренки в верхнем правом углу, а затем "добавить страницу".

![](~/assets/images/tabs/tabs-in-sharepoint/image066.png)

Вы увидите процесс создания страниц SharePoint. Присвойте странице имя "Моя группа".

Откройте панель элементов веб-частей, нажав кнопку +, и выберите вкладку группы (с именем "Contoso HR"). Веб-части сортируются по алфавиту; Если это длинный список, его можно найти с помощью панели поиска. При этом на холсте, содержащем вкладку Teams, будет создана веб-часть:

![](~/assets/images/tabs/tabs-in-sharepoint/image071.png)

После завершения редактирования нажмите кнопку "опубликовать".

Можно нажать кнопку "добавить страницу в навигацию", чтобы получить краткую ссылку на страницу в левой панели навигации:

![](~/assets/images/tabs/tabs-in-sharepoint/image073.png)

## <a name="step-3-explore-app-pages-in-sharepoint"></a>Шаг 3: изучение страниц приложения в SharePoint

После публикации страницы вы можете изучить [возможности приложения Teams в среде SharePoint полностью](/sharepoint/dev/spfx/web-parts/single-part-app-pages). При этом текущая страница преобразуется в страницу приложения с обычным макетом страницы SharePoint с использованием полноэкранной среды для вкладки teams:

![](~/assets/images/tabs/tabs-in-sharepoint/image085.png)

## <a name="more-information"></a>Дополнительные сведения

- [Создание вкладки Microsoft Teams с помощью SharePoint Framework - Обучающий материал](/sharepoint/dev/spfx/web-parts/get-started/using-web-part-as-ms-teams-tab)
- [Использование страницы одной части приложения в SharePoint Online](/sharepoint/dev/spfx/web-parts/single-part-app-pages)
