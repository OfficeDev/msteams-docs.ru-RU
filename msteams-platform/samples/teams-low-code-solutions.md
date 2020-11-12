---
title: Решения с нехваткой кодов для пользовательских приложений Teams
author: laujan
description: Сведения о доступных решениях Microsoft для Microsoft Teams и без кода
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 089e436d43819f9aabe3ceb47760f521b014d93f
ms.sourcegitcommit: f6029c8ff0c5315613a3efcd86777aa4cede39e6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/11/2020
ms.locfileid: "48995004"
---
# <a name="create-low-code-custom-apps-for-microsoft-teams"></a>Создание приложений с небольшим объемом кода для Microsoft Teams

[Microsoft Teams](/microsoftteams/platform) является расширяемым и адаптивным. Это означает, что у вас есть свобода создавать пользовательские приложения для Teams, которые удовлетворяют особым потребностям ваших пользователей. Несмотря на то, что вы можете создавать приложения "с нуля", с сегодняшней потребностью в быстрых решениях, можно использовать только те возможности, которые необходимы для создания элегантных приложений в сжатом промежутке времени.

Недорогие платформы кода предоставляют интуитивно понятный подход к разработке программного обеспечения и практически не требуют написания кода для создания приложений и процессов. Разработчики, работающие с сотрудниками, могут легко создавать пользовательские приложения и профессиональные разработчики, что экспоненциально ускоряет процесс разработки и развертывания приложений. Большинство непроизводительных платформ состоят из визуального интерфейса, соединителей для внутренних служб и встроенной системы управления жизненным циклом приложений для создания, отладки, развертывания и обслуживания приложений. Корпорация Майкрософт предоставляет несколько инновационных шлюзов для быстрого создания приложений, совместимых с Teams, с помощью атрибутов с небольшим кодом:

1. [Microsoft Power Platform](#teams-and-microsoft-power-platform)
1. [Шаблоны приложений Microsoft Teams](#teams-app-templates)

## <a name="teams-and-microsoft-power-platform"></a>Teams и Microsoft Power Platform

Microsoft Power Platform (/повер-платформ) сочетает в себе четыре надежные технологии Майкрософт на одной мощной платформе приложений. Power BI, Power Apps, Power Автоматизация (раньше) и виртуальные агенты энергопотребления позволяют создавать решения, автоматизировать процессы, анализировать данные и создавать виртуальные агенты в единой и интегрированной среде:

:::image type="content" source="../assets/images/power-platform-and-teams/ms-power-platform.png" alt-text="Службы Power Platform":::

### <a name="-teams-and-power-bi"></a>✔ Teams и Power BI

На [вкладке Power BI для Microsoft Teams](https://powerbi.microsoft.com/blog/announcing-new-power-bi-tab-for-microsoft-teams/) добавлена поддержка отчетов в рабочей области Teams и пользователи могут [совместно использовать интерактивное содержимое Power BI](/power-bi/collaborate-share/service-embed-report-microsoft-teams) , а также [совместно работать с другими](/power-bi/collaborate-share/service-collaborate-microsoft-teams) каналами и обсуждениями для групп. Вы можете создавать упакованное содержимое [приложения Power BI](/power-bi/collaborate-share/service-create-distribute-apps) с нуля и распространять его как приложение или можно [создать шаблонное приложение в Power BI](/connect-data/service-template-apps-create). Кроме того, вы можете использовать новое [приложение Power BI в Teams](https://go.microsoft.com/fwlink/?linkid=2143643) , чтобы обеспечить в Teams всю базовую среду Power BI Service.

### <a name="-teams-and-power-apps"></a>✔ Teams и Power Apps

С помощью [Power Apps](/powerapps/powerapps-overview)вы можете создавать бизнес-приложения, которые подключаются к бизнес-данным и приспособлены к потребностям вашей организации.  Приложения Power Apps позволяют широкому спектру сценариев приложений для решения бизнес-задач с помощью [приложений Canvas](/powerapps/maker/#canvas-apps). После построения приложение может быть экспортировано из портала Power Apps Maker и [встроенных в Microsoft Teams](/power-platform/admin/embed-app-teams).

Новое [приложение Power Apps](https://go.microsoft.com/fwlink/?linkid=2143374) в Teams предоставляет интегрированный интерфейс для разработчиков приложений для создания и редактирования приложений и рабочих процессов в Teams, а также для быстрой публикации и предоставления общего доступа к ним для всех пользователей в группе без необходимости переключаться между несколькими приложениями и службами.

### <a name="-teams-and-power-automate"></a>✔ Teams и Автоматизация управления питанием

С помощью [приложения "Автоматизация Power" в Teams](/power-automate/flows-teams)можно [создавать потоки для автоматизации повторяющихся рабочих задач](https://flow.microsoft.com/connectors/shared_teams/microsoft-teams/) непосредственно в среде Teams. Вы можете [инициировать потоки из любого сообщения в Microsoft Teams](/power-automate/trigger-flow-teams-message) и [использовать адаптивные карты в Power автоматизированной среде](/power-automate/create-adaptive-cards). Кроме того, вы можете создавать потоки для настройки и добавления дополнительных значений в Microsoft Teams из нового [приложения Power Apps](https://go.microsoft.com/fwlink/?linkid=2143539) в Teams.

### <a name="-teams-and-power-virtual-agents"></a>✔ Teams и виртуальные агенты управления питанием

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) — это решение с графическим интерфейсом, созданное на платформе Microsoft Power Framework и на клиенте Bot, которое позволяет каждому участнику группы создавать полнофункциональные, интерактивные чатботс, которые легко интегрируются с платформой Teams. Весь контент, созданный в виртуальном агенте, работает естественным образом в Microsoft Teams и Power Virtual Agents Боты участие пользователей в собственном холсте чата для Teams. Вы можете [интегрировать виртуальные агенты Power чатбот](/power-virtual-agents/publication-add-bot-to-microsoft-teams) в Teams через [портал виртуальных агентов](https://powervirtualagents.microsoft.com).

С помощью нового [приложения "виртуальные агенты Power](https://aka.ms/pva-teams-docs) " в Teams вы можете легко создавать, управлять и публиковать беседы Чатботс в Teams и делиться боты с другими людьми в Организации, чтобы они могли общаться и отвечать на них.

## <a name="teams-app-templates"></a>Шаблоны приложений Teams

:::image type="content" source="../assets/images/power-platform-and-teams/app-template-illustration.png" alt-text="Иллюстрация решения приложения":::

### <a name="-app-template-catalog"></a>Каталог шаблонов приложений ✔

[Шаблоны приложений](../samples/app-templates.md) — это готовые к работе приложения для Microsoft Teams, которые основаны на сообществах, Открытый источник и доступны на сайте GitHub. Каждый шаблон содержит подробные инструкции по развертыванию и установке этого приложения для вашей организации, предоставляя готовые к использованию приложение, которое можно установить и приступить к работе немедленно. Полный исходный код также доступен, поэтому вы можете изучить его подробно или разветвление кода и измените его в соответствии с вашими потребностями.

### <a name="-virtual-assistant-for-teams"></a>✔ Virtual Assistant для Teams

Virtual Assistant — это шаблон Microsoft Open-Source, который позволяет создавать надежное диалоговое решение, обеспечивая полный контроль над возможностями взаимодействия с пользователем, фирменной символикой и необходимыми данными. Вы можете настроить свой виртуальный помощник для [интеграции с средой Teams](https://microsoft.github.io/botframework-solutions/clients-and-channels/tutorials/enable-teams/1-intro). 

## <a name="additional-resources"></a>Дополнительные ресурсы

:::image type="content" source="../assets/images/power-platform-and-teams/blogs-and-resources.png" alt-text="Иллюстрация блогов и ресурсов":::

### <a name="-teams-shift-connectors"></a>✔Ные соединители Shift

Команды перемещаются в [соединители управления принудительными работами](../samples/shifts-wfm-connectors.md) — это готовые к использованию, интеграция с открытым кодом и сообщество, обеспечивающие единый интерфейс и быструю процедуру для цифрового преобразования сотрудников задействование с помощью команд Shift. Каждый соединитель предоставляет подробные инструкции по развертыванию и интеграции в Организации. Полный исходный код доступен в репозитории GitHub, где его можно исследовать подробно и/или подгонять в соответствии с конкретными потребностями.

### <a name="-power-platform-learn-modules"></a>Модули для изучения ✔ной платформы

|Тема|
|-----|
|**Power BI**|
|[Power BI для студии приложений](/learn/browse/?expanded=power-platform&products=power-bi&roles=maker)|
|[Power BI для разработчиков](/learn/browse/?expanded=power-platform&products=power-bi&roles=developer)|
|**Power Apps**|
|[Power Apps для App Maker](/learn/browse/?products=power-apps&roles=maker)|
|[Приложения для опытных разработчиков приложений](/learn/browse/?products=power-apps)|
|**Power Automate**|
|[Автоматизация управления питанием для студии приложений](/learn/browse/?expanded=power-platform&products=power-automate&roles=maker)|
|[Автоматизация управления для разработчиков](/learn/browse/?expanded=power-platform&products=power-automate&roles=developer)|
|**Виртуальные агенты Power**|
|[Виртуальные агенты управления питанием для разработчиков и лиц, принимающих приложения](/learn/browse/?products=power-virtual-agents&expanded=power-platform&roles=maker)

### <a name="-project-oakdale-preview"></a>✔ Оакдале Project (Предварительная версия)

[Project оакдале](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180
) — это новая платформа с недорогими данными, которая вскоре поступает в Microsoft Teams. Он позволит разработчикам создавать решения для платформы управления питанием в Teams непосредственно в Teams. Для получения дополнительных сведений *посетите* веб [-страницу Microsoft Project оакдале](https://powerapps.microsoft.com/blog/introducing-project-oakdale-a-new-low-code-data-platform-for-microsoft-teams) .

### <a name="-microsoft-blog-insights"></a>✔Ное представление блога Майкрософт

[Детальное представление о возможностях платформы данных в Project Оакдале](https://powerapps.microsoft.com/blog/a-closer-look-at-data-platform-capabilities-in-project-oakdale/)

[Объявление о платформе управления питанием и обновлениях Teams, чтобы помочь клиентам адаптироваться к удаленным работам](https://cloudblogs.microsoft.com/powerplatform/2020/05/19/announcing-power-platform-and-teams-updates-to-help-customers-adapt-to-remote-work/)

[Teams — это будущая работа с недостаточными функциями кода для расширения вашей цифровой рабочей области.](https://techcommunity.microsoft.com/t5/microsoft-teams-blog/teams-is-shaping-the-future-of-work-with-low-code-features-to/ba-p/1507180)

### <a name="-managing-power-platform-apps"></a>✔ Управление приложениями Power Platform

> [!div class="nextstepaction"]
> [Управление приложениями платформы энергопотребления Майкрософт в центре администрирования Microsoft Teams](/microsoftteams/manage-power-platform-apps)
