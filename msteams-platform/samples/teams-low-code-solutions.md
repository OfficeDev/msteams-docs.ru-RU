---
title: Создание пользовательских приложений с минимальным объемом программирования для Microsoft Teams
author: surbhigupta
description: Узнайте о доступных решениях Майкрософт с минимальным или нулевым объемом программирования на основе Teams для Microsoft Power Platform.
ms.localizationpriority: medium
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 74dd4eb094c31510319932ec96cbb0db34a1fca5
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503314"
---
# <a name="create-low-code-custom-apps-for-teams"></a>Создание пользовательских приложений с низким кодом для Teams

Microsoft Teams является расширяемой и адаптивной средой. Это означает, что вы можете создавать пользовательские приложения для Teams, чтобы удовлетворить потребности пользователей. Пользовательские приложения с минимальным объемом программирования экономят время, быстро обеспечивают решение и закрывают ту же нишу пользовательского спроса, что и приложения, созданные с нуля. В этом документе представлен обзор Microsoft Power Platform, чат-бота Power Virtual Agents и Виртуального помощника.

Платформы для создания приложений с минимальным объемом программирования предоставляют интуитивно понятный подход к разработке программного обеспечения с минимальным или нулевым объемом программирования для создания приложений и процессов. Они позволяют разработчикам без опыта легко создавать пользовательские приложения с минимальным или нулевым объемом программирования, а профессиональным разработчикам — быстро разрабатывать и развертывать приложения. Эти платформы состоят из визуального интерфейса, соединителей с серверными службами и встроенной системы управления жизненным циклом приложений для создания, отладки, развертывания и обслуживания приложений. Microsoft Power Platform — новаторский портал для быстрой сборки Teams-совместимых приложений с минимальным или нулевым объемом программирования.

## <a name="teams-and-microsoft-power-platform"></a>Teams и Microsoft Power Platform

Microsoft Power Platform объединяет четыре богатые возможностями технологии Майкрософт: Power BI, Power Apps, Power Automate (ранее Microsoft Flow) и Power Virtual Agents в одной мощной платформе приложений. Эти технологии позволяют создавать решения, автоматизировать процессы, анализировать данные и разрабатывать виртуальные агенты в единой и интегрированной среде:

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Службы Power Platform":::

> [!NOTE]
> Не следует использовать Microsoft Power Platform для создания приложений, предназначенных для публикации в магазине приложений Teams. Приложения Microsoft Power Platform можно публиковать только в магазине приложений организации.

### <a name="-teams-and-power-bi"></a>✔ Teams и Power BI

[Вкладка Power BI для Microsoft Teams](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) добавляет поддержку отчетов в рабочую область Teams и позволяет пользователям [делиться интерактивным содержимым Power BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams) и [сотрудничать с другими пользователями в каналах и чатах Teams](/power-bi/collaborate-share/service-collaborate-microsoft-teams). Вы можете создать упакованное содержимое [Power BI](/power-bi/collaborate-share/service-create-distribute-apps) с нуля и распространить его как приложение или создать приложение-шаблон в [Power BI](/power-bi/connect-data/service-template-apps-create). Кроме того, новая возможность [Power BI в Teams](https://go.microsoft.com/fwlink/?linkid=2143643) позволяет перенести в Teams всю мощь служб Power BI и пользовательского взаимодействия.

### <a name="-teams-and-power-apps"></a>✔ Teams и Power Apps

[Power Apps](/powerapps/powerapps-overview) помогает создавать бизнес-приложения, которые подключаются к бизнес-данным и адаптированы к потребностям вашей организации.  Power Apps реализует широкий спектр сценариев приложений для решения бизнес-задач с помощью [приложений на основе холста](/powerapps/maker/#canvas-apps). После сборки вы можете экспортировать приложение с портала Power Apps Maker и [внедрить в Microsoft Teams](/power-platform/admin/embed-app-teams).

Новое [приложение Power Apps](https://go.microsoft.com/fwlink/?linkid=2143374) в Teams обеспечивает интегрированный интерфейс для разработчиков приложений, позволяющий создавать и изменять приложения и рабочие процессы в Teams. Они позволяют быстро публиковать приложения и делиться ими с участниками группы. Участники могут использовать приложения без переключения между несколькими приложениями и службами.

### <a name="-teams-and-power-automate"></a>✔ Teams и Power Automate

Вы можете [создавать потоки для автоматизации повторяющихся рабочих задач](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) непосредственно в среде Teams с помощью [приложения Power Automate в Teams](/power-automate/flows-teams). Вы можете [активировать поток из любого сообщения в Microsoft Teams](/power-automate/trigger-flow-teams-message) и использовать [адаптивные карточки в Power Automate](/power-automate/create-adaptive-cards). Кроме того, можно создавать потоки для настройки Microsoft Teams и обеспечения дополнительных услуг пользователю в новом приложении [Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) в Teams.

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams Power Virtual Agents

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) — это решение в виде интерактивного графического интерфейса на платформе Microsoft Power Platform и Bot Framework, не требующее программирования. Интерактивное решение графического интерфейса без необходимости создания программного кода позволяет каждому участнику вашей команды создавать многофункциональные чат-боты для бесед, легко интегрирующиеся с платформой Teams. Все содержимое, создаваемое в Power Virtual Agents, естественным образом выводится в Teams, а боты Power Virtual Agents взаимодействуют с пользователями на холсте собственного чата Teams. Вы можете [интегрировать чат-бот Power Virtual Agents](/power-virtual-agents/publication-add-bot-to-microsoft-teams) с Teams на портале [Power Virtual Agents](https://powervirtualagents.microsoft.com).

Используйте новое приложение [Power Virtual Agents](https://aka.ms/pva-teams-docs) в Teams, чтобы легко создавать и публиковать чат-боты для бесед, а также управлять ими в Teams. Вы можете поделиться ботами с другими пользователями в организации, чтобы общаться в чате и получать ответы на их вопросы.

### <a name="-virtual-assistant-for-teams"></a>Создание виртуального помощника для Teams

Виртуальный помощник — это шаблон Майкрософт с открытым исходным кодом, который позволяет создать надежное диалоговое решение, сохраняя полный контроль над взаимодействием с пользователем, фирменной символикой организации и необходимыми данными. Виртуальный помощник можно настроить для [интеграции в среду Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro).

### <a name="-power-platform-learn-modules"></a>✔ Модули Power Platform Learn

|  Статья  |  Ссылки  |
|:---------|:----------------------|
|Power BI|[Power BI для создателей приложений](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)</br>[Power BI для разработчиков](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|Power Apps|[Power Apps для создателей приложений](/learn/browse/?products=power-apps&roles=maker)</br>[Power Apps для разработчиков](/learn/browse/?products=power-apps)|
|Power Automate|[Power Automate для создателей приложений](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)</br>[Power Automate для разработчиков](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|Power Virtual Agents|[Power Virtual Agents для разработчиков и создателей приложений](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)|

### <a name="-project-oakdale-preview"></a>✔ Project (предварительная версия)

> [!NOTE]
> Project **Oakdale** переименован в **Dataverse для Teams**.

[Проект Oakdale](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) — это новая платформа данных с низким объемом программирования, которая скоро появится в Microsoft Teams. Она позволяет разработчикам создавать решения Teams Power Platform непосредственно в Teams. Дополнительные сведения о проекте можно найти в [блоге Microsoft Project Teams](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams) по ключевым словам "Проект Oakdale"

### <a name="-microsoft-blog-insights"></a>✔ Microsoft Blog Insights

[Подробный обзор возможностей платформы данных в проекте Oakdale](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Объявление об обновлении Power Platform и Teams, которые помогают пользователям адаптироваться к удаленной работе](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams определяет будущее работы благодаря возможностям создания приложений с минимальным уровнем программирования для совершенствования оцифрованной рабочей области](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Управление приложениями Power Platform

> [!div class="nextstepaction"]
> [Управление приложениями Power Platform в Центре администрирования Microsoft Teams](/microsoftteams/manage-power-platform-apps)

## <a name="see-also"></a>Дополнительные ресурсы

[Интеграция веб-приложений](~/samples/integrate-web-apps-overview.md)
