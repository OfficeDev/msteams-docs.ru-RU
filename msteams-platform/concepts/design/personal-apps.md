---
title: Проектирование личного приложения
description: Узнайте, как реализовать рекомендации по проектированию, включая элементы пользовательского интерфейса, для разработки личного приложения с помощью комплекта пользовательского интерфейса Microsoft Teams.
author: heath-hamilton
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.openlocfilehash: 4646d47c5aa325291f060ea192dcc1705b414ac7
ms.sourcegitcommit: bd96080c78f25eb0a67ce176df5e255be348f7b1
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/14/2022
ms.locfileid: "68575798"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a>Проектирование личных приложений для Microsoft Teams

Личное приложение может быть ботом, закрытой рабочей областью или и тем, и другим.  Иногда он функционирует как место для создания или просмотра содержимого. В других случаях он позволяет пользователю просматривать все, что у него есть, если приложение настроено как вкладка в нескольких каналах.

Далее описано и показано, как люди могут добавлять личные приложения, использовать их и управлять ими в Teams. Это может помочь вам в создании приложения.

## <a name="microsoft-teams-ui-kit"></a>Комплект разработчика для пользовательского интерфейса Microsoft Teams

В комплекте разработчика для пользовательского интерфейса Microsoft Teams можно найти полные рекомендации по проектированию личных приложений, в том числе элементы, которые можно взять и изменить так, как нужно вам. В комплекте разработчика для пользовательского интерфейса также присутствуют такие важные темы, как специальные возможности, адаптивный размер, которые здесь не рассматриваются.

> [!div class="nextstepaction"]
> [Получить комплект разработчика для пользовательского интерфейса Microsoft Teams (Figma)](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a>Добавление личного приложения

Пользователи могут добавить личное приложение из магазина Teams или всплывающего окна приложения, щелкнув значок **Дополнительно** в левой части Teams (показано в следующем примере).

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="В примере показано, как добавить личное приложение из всплывающего меню приложения.":::

## <a name="use-a-personal-app-private-workspace"></a>Использование личного приложения (частная рабочая область)

В частной рабочей области пользователи могут просматривать значимое для них содержимое приложения в центральном расположении, не выходя из Teams.

(Примечание по реализации. Частная рабочая область основана на возможностях [*личной вкладки*](../../tabs/how-to/create-personal-tab.md).)

### <a name="anatomy-personal-app-private-workspace"></a>Структура: личное приложение (частная рабочая область)

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-component-anatomy.png" alt-text="В примере показана структура компонентов личной вкладки.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Атрибут приложения**: имя вашего приложения.|
|Б|**Вкладки**: обеспечивает навигацию для личного приложения.|
|В|**Дополнительное меню**: включает другие параметры и сведения о приложении.|
|D|**Основная навигация**: обеспечивает навигацию к другим основным функциям Teams вашего приложения.|

#### <a name="configure-and-add-multiple-actions-in-navbar"></a>**Настройка и добавление нескольких действий в NavBar**

Вы можете добавить несколько действий в верхнюю правую панель NavBar и создать меню переполнения для дополнительных действий в приложении.

>[!NOTE]
> В NavBar можно добавить не более пяти действий, включая меню переполнения.

:::image type="content" source="../../assets/images/overflow-menu-and-multiple-actionsoptions.png" alt-text="Снимок экрана — это пример, описывающий меню NavBar и Overflow.":::

Чтобы **настроить и добавить несколько действий в NavBar**, вызовите [API setNavBarMenu](/javascript/api/@microsoft/teams-js/microsoftteams.menus?view=msteams-client-js-1.12.1&preserve-view=true) . и добавьте свойство `displayMode enum` в `MenuItem`. Определяет `displayMode enum` , как меню отображается на панели Навигации. Значение по умолчанию равно `displayMode enum` `ifRoom`.

В зависимости от требований и пространства, доступных в NavBar, `displayMode enum` задайте один из следующих значений.

* Если есть место, задайте `ifRoom = 0` для размещения элемента в NavBar.
* Если места нет, `overflowOnly = 1`задайте значение, чтобы этот элемент всегда помещались в меню переполнения NavBar, но не в NavBar.

Ниже приведен пример настройки NavBar с помощью меню переполнения для нескольких действий.

```typescript
const menuItems = [item1, item2, item3, item4, item5]
microsoftTeams.menus.setNavBarMenu(menuItems, (id: string) => {
  output(`Clicked ${id}`)
  return true;
})
```

> [!NOTE]
> API `setNavBarMenu` не управляет кнопкой **"Обновить** ". Он отображается по умолчанию.

:::image type="content" source="../../assets/images/overflow-menu-and-multple-actions.png" alt-text="На снимке экрана показан пример навигации и несколько действий в меню переполнения.":::

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-tab-structural-anatomy.png" alt-text="В примере показана структура личной вкладки.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки**: обеспечивает навигацию для личного приложения.|
|1|**Веб-представление.** Отображает содержимое приложения.|

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="В этом примере показана структура компонентов личной вкладки.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Атрибут приложения**: логотип и имя приложения.|
|Б|**Вкладки**: обеспечивает навигацию для личного приложения.|
|В|**Всплывающее представление**: содержимое приложения перемещается из родительского окна в отдельное дочернее окно.|
|D|**Дополнительное меню**: включает другие параметры и сведения о приложении. (Вы также можете сделать **Параметры** вкладкой.)|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="В этом примере показана структура личной вкладки.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладки**: обеспечивает навигацию для личного приложения.|
|1|**iframe.** Отображает содержимое приложения.|

### <a name="design-with-ui-templates-and-advanced-components"></a>Разработка с помощью шаблонов пользовательского интерфейса и дополнительных компонентов

Используйте один из следующих шаблонов и компонентов Teams, чтобы спроектировать личную вкладку:

* [Список](../../concepts/design/design-teams-app-ui-templates.md#list). Списки могут отображать связанные элементы в формате, доступном для сканирования, и позволяют пользователям выполнять действия со всем списком или отдельными элементами.
* [Доска задач.](../../concepts/design/design-teams-app-ui-templates.md#task-board) Доска задач, иногда называемая канбан-доской или трассой, представляет собой набор карточек, часто используемых для отслеживания состояния рабочих элементов или билетов.
* [Панель мониторинга](../../concepts/design/design-teams-app-ui-templates.md#dashboard): панель мониторинга — это холст, содержащий несколько карточек, которые предоставляют обзор данных или содержимого.
* [Форма](../../concepts/design/design-teams-app-ui-templates.md#form). Формы предназначены для сбора, проверки и отправки данных пользовательского ввода в структурированном виде.
* [Пустое состояние](../../concepts/design/design-teams-app-ui-templates.md#empty-state). Шаблон пустого состояния можно использовать для различных сценариев, включая вход, первый запуск, сообщения об ошибках и т. д.
* [Навигация слева.](~/concepts/design/design-teams-app-advanced-ui-components.md#left-nav) Компонент навигации слева может помочь если личное приложение требует некоторой навигации. Как правило, навигация должна быть минимальной.

## <a name="use-a-personal-app-bot"></a>Использование личного приложения (бота)

Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on artboard). Users interact with the bot in a tab you specify.

### <a name="anatomy-personal-app-bot"></a>Структура: личное приложение (бот)

#### <a name="mobile"></a>Мобильная версия

:::image type="content" source="../../assets/images/personal-apps/mobile-personal-bot-anatomy.png" alt-text="В примере показана структура компонентов личного бота.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Точка входа бота**: точка входа для доступа пользователей к функции бота в личном приложении.|
|Б|**Кнопка "Назад"**: возвращает пользователей в личное рабочее пространство.|
|В|**Сообщение бота**: боты часто отправляют сообщения и уведомления в виде карточки (например, адаптивной карточки).|
|D|**Поле создания:** поле ввода для отправки сообщений боту.|

#### <a name="configure-back-button"></a>Настройка кнопки "Назад"

При нажатии кнопки "Назад" в приложении Teams вы перейти на платформу Teams, не переходя в приложение.

Чтобы перейти в приложение, настройте кнопку "Назад", чтобы при нажатии кнопки "Назад" можно было вернуться к предыдущим шагам и перейти к приложению.

Чтобы **настроить кнопку "Назад"**, вызовите API [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true) , который обрабатывает функции кнопки "Назад" в зависимости от одного из следующих условий:

* Если `registerBackButtonHandler` задано значение , `false`пакет SDK `navigateBack` для JavaScript вызывает API, а платформа Teams обрабатывает кнопку "Назад".
* Если `registerBackButtonHandler` задано `true`значение , приложение обрабатывает функции кнопки "Назад" (вы можете вернуться к предыдущим шагам и перейти к приложению), а платформа Teams не выполняет никаких дальнейших действий.

Ниже приведен пример настройки кнопки "Назад":

```typescript
microsoftTeams.registerBackButtonHandler(() => {
  const selectOption = registerBackReturn.options[registerBackReturn.selectedIndex].value
  var isHandled = false
  if (selectOption == 'true') 
    isHandled = true;
  output(`onBack isHandled ${isHandled}`)
  return isHandled;
})
```

#### <a name="desktop"></a>Версия для настольного компьютера

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="В примере показана структура компонента личного бота.":::

|Счетчик|Описание|
|----------|-----------|
|A|**Вкладка "Бот"**: например, включите вкладку **Чат** для доступа к беседам и уведомлениям бота.|
|Б|**Сообщение бота**: боты часто отправляют сообщения и уведомления в виде карточки (например, адаптивной карточки).|
|В|**Поле создания:** поле ввода для отправки сообщений боту.|

## <a name="manage-a-personal-tab"></a>Управление личной вкладкой

В левой части Teams пользователи могут щелкнуть личное приложение правой кнопкой мыши, чтобы закрепить, удалить или настроить другие параметры приложения.

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="В примере показаны параметры для управления личным приложением.":::

## <a name="best-practices"></a>Рекомендации

Используйте эти рекомендации для создания качественных приложений.

### <a name="tab-priority"></a>Приоритет вкладки

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a>Следует: показывать наиболее релевантный контент на первой вкладке

Благодаря гибкому размеру вкладки справа могут быть обрезаны или не видны.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="В примере показано личное приложение, отображающее наиболее релевантное содержимое на первой вкладке.":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a>Не следует: создавать дополнительное содержимое или метаданные

Как и в стандартном веб-приложении, навигация по вкладкам должна выполняться в порядке, который помогает понять основные функции приложения.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="В примере показано личное приложение с дополнительным содержимым или метаданными.":::

### <a name="tab-hierarchy"></a>Иерархия вкладок

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a>Следует: вкладки должны иметь одинаковую иерархию и представлять ключевые страницы приложения

Вкладки должны классифицировать основные функции и содержимое приложения. Благодаря гибкому размеру содержимое справа может быть обрезано или не видно.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="В примере показано личное приложение с вкладками одинаковой иерархии.":::

#### <a name="dont-include-different-levels-of-hierarchy"></a>Не следует: включать различные уровни иерархии

Содержимое должно развиваться в логическом порядке, который помогает пользователям понять его. Если у вас есть две тесно связанные вкладки, попробуйте объединить их в одну вкладку.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="В примере показано личное приложение с различными уровнями иерархии.":::

### <a name="first-run-experience"></a>Интерфейс при первом запуске

#### <a name="do-include-a-first-run-experience"></a>Следует: включить интерфейс при первом запуске

При первом использовании личного приложения должен отображаться как минимум экран приветствия. Для ботов опишите, что может делать ваш бот, и предоставьте быстрые действия, например кнопку входа.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="В примере показано, что следует делать при первом запуске личного приложения.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="В другом примере показано, что следует делать при первом запуске личного приложения.":::

#### <a name="dont-start-with-a-blank-screen"></a>Не следует: начинать с пустого экрана

Пользователи могут быть сбиты с толку, если при первом запуске приложения ничего не отображается.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="В примере показано, что не следует делать при первом запуске личного приложения.":::

### <a name="personalized-content"></a>Персонализированное содержимое

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a>Следует: агрегировать содержимое приложения, относящееся к пользователю

Будь то личная вкладка или бот, отображайте содержимое, связанное только с действиями пользователя в вашем приложении.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="В примере показано, что следует делать с личным приложением и персонализированным содержимым.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="В другом примере показано, что следует делать с личным приложением и персонализированным содержимым.":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a>Не следует: показывать нерелевантный или слишком широкий контент

В личном контексте не отображайте содержимое для команд, в которых пользователь не состоит. Содержимое личного бота должно быть ориентировано на отдельного человека, а не на группу.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="В примере показано, что не следует делать с личным приложением и персонализированным содержимым.":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="В другом примере показано, что не следует делать с личным приложением и персонализированным содержимым.":::

### <a name="complex-app-features"></a>Сложные функции приложения

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a>Следует: разрешить пользователям доступ к сложным функциям в браузере

Приложение должно сосредоточиться на основных задачах в Teams, но вы по-прежнему можете просматривать полное автономное приложение в браузере.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="В примере показано, как обрабатывать сложные функции приложения с помощью личного приложения.":::

#### <a name="dont-include-your-entire-app"></a>Не следует: включать все приложение

Если вы не создали приложение специально для Teams, возможно у вас есть функции, которые не имеют смысла в средстве совместной работы.

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="В примере показано, как не следует обрабатывать сложные функции приложения с помощью личного приложения.":::

## <a name="see-also"></a>Дополнительные ресурсы

Эти другие рекомендации по проектированию могут помочь в зависимости от области вашего личного приложения:

* [Проектирование вкладки](../../tabs/design/tabs.md)
* [Создание бота](../../bots/design/bots.md)
* [registerBackButtonHandler](/javascript/api/@microsoft/teams-js/pages.backstack?view=msteams-client-js-latest&preserve-view=true&branch=pr-en-us-6801&preserve-view=true)
* [Перечисление DisplayMode](/javascript/api/@microsoft/teams-js/menus.displaymode?view=msteams-client-js-latest&preserve-view=true)
