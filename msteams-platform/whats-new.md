---
title: Новые возможности
description: Описание всех новых функций разработчика в Microsoft Teams
keywords: новые возможности teams
ms.openlocfilehash: da2378446f39ab8398cdc569987d14f5c6095330
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739044"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Новые возможности для разработчиков в Microsoft Teams

>[!TIP]
> Ознакомьтесь с шаблонами, готовыми к выпуску, в каталоге [**шаблонов приложений Teams.**](samples/app-templates.md) Каталог в алфавитном порядке, а самые новые добавления отмечены звездой **&#9734;.**

## <a name="change-log"></a>Журнал изменений

В журнале изменений перечислены изменения платформы Microsoft Teams и этого набора документов. Иногда записи могут использоваться для привлечь внимание к новой функции, которая просто интересна разработчикам Teams.

| **Дата** | **Примечания**. | **Измененные разделы** |
| -------- | --------- | ------------------ |
|11/30/2020|Новый: интеграция платформы удостоверений с teams набор средств и Visual Studio кода для вкладок|[Проверка подлинности с единым входом с помощью команд набор средств и Visual Studio кода для вкладок](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Манифест приложения Teams обновлен до версии 1.8|[Справка: схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Рекомендации по проектированию ботов Teams|[Рекомендации по проектированию ботов](bots/design/bots.md)|
|9/30/2020|Теперь поддерживается отправка и получение файлов ботам на мобильных устройствах.|[Отправка и получение файлов с помощью бота](resources/bot-v3/bots-files.md)|
|09/22/2020|Новое руководство по началу работы с Teams|[Создание первого обзора приложения Teams](build-your-first-app/build-first-app-overview.md)|
|9/18/2020|Поддержка приложений Teams для собраний (предварительная версия выпуска)|[Создание приложений для собраний Teams и](apps-in-teams-meetings/create-apps-for-teams-meetings.md) [приложений в собраниях Teams](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|8/19/2020|Импорт сообщений Teams с помощью Microsoft Graph|[Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |Поддержка адаптивных карточек при перемещении входящий веб-hook в ga.|[Отправка адаптивных карточек с помощью входящего веб-перехватчика](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Начало создания приложений Teams с помощью Visual Studio набор средств.|[Создание приложений с помощью microsoft Teams набор средств и Visual Studio кода](toolkit/visual-studio-overview.md) |
|08/06/2020|Поддержка проверки подлинности с SSO вкладок|[Разработка вкладки "SSO Microsoft Teams"](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Упреждающие боты и сообщения Graph (общедоступный предварительный просмотр)|[Включить упреждающие установки ботов и упреждающие сообщения в Teams с помощью Microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |Обновления возможностей мобильных устройств.|[Запрос разрешений устройства для вкладки Microsoft Teams](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Средство проверки приложений Teams для отправки в AppSource.|[Средство проверки приложений Teams](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Создание виртуального помощника для Teams|[Виртуальный помощник для Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Просмотр документации по индикатору загрузки|[Отображение индикатора загрузки](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Начало создания приложений Teams с помощью Visual Studio кода набор средств.|[Создание приложений с помощью microsoft Teams набор средств и Visual Studio кода](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Единый вход для вкладок GA для веб-клиентов Teams и классических клиентов|[Единый Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Схема манифеста обновлена до версии 1.7| [Справка: схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
| 05/20/2020 | Разрешения на согласие для определенных ресурсов с помощью API Microsoft Graph можно просмотреть для разработчиков. |[Согласие для определенных ресурсов (RSC) — Developer Preview](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Интеграция виртуальных агентов Power с Teams|[Интеграция бота чата power Virtual Agents с Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Интеграция систем WFM с соединитетелем Shifts для Teams|[Microsoft Teams сдвига соединители WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Добавлена поддержка получения одного участника беседы и дополнительная поддержка получения участников страницы. | [Получите контекст Teams для вашего бота](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | Параметр в полезной нагрузке, отправленной боту, больше не шифруется, что позволяет использовать это значение для создания глубоких ссылок на `replyToId` эти сообщения. В состав полезной нагрузки сообщения входят зашифрованные значения в параметре. `legacy.replyToId`.  |
| 11/5/2019 | Единый вход с помощью SDK JavaScript для Teams на странице веб-контента находится в предварительной версии разработчика. | [Единый вход](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Боты для бесед и документация по расширению обмена сообщениями обновлены для отражения SDK Bot Framework 4.6. Документация по V3 SDK доступна в разделе "Ресурсы". | Вся документация по ботам и расширениям сообщений. |
| 10/31/2019 | Новая структура документации и рефакторинг основных статей. Сообщайте о любых неудаваемых ссылках или сообщениях 404, создав проблему с GitHub. | Все из них! |
| 9/13/2019 | Бот запроса устанавливается из расширения обмена сообщениями на основе действий. | [Инициировать действия с расширениями обмена сообщениями](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Поддержка частных каналов на вкладке и соединители. | [Получить контекст для вкладки](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Поделиться внешним веб-сайтом с внешнего веб-сайта в канале Teams. | [Совместное участие в Teams](~/share-to-teams.md) |
| 05/25/2019 | Ответьте сообщением бота из модуля задачи. | [Ответ сообщением бота из модуля задачи](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Боты в групповых чатах. | [Взаимодействие с ботом в групповом чате или канале](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Локализация манифеста приложения. | [Локализация приложений](~/publishing/apps-localization.md) |
| 05/20/2019 | Действия с сообщениями. | [Действия с сообщениями](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Unfurling link (custom URL previews). | [Развернуть ссылку](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Программа сертификации приложений для приложений Магазина. | [Сертификация приложений](~/publishing/application-certification.md) |
| 05/06/2019 | Теперь доступны шаблоны приложений. | [Шаблоны приложений](~/samples/app-templates.md) |
| 04/23/2019 | Теперь доступны расширения обмена сообщениями на основе действий. | [Расширения сообщений на основе действий](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Создание прямых ссылок на приватный чат не является предварительным и доступным для разработчиков. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Просмотр сведений о SKU и licenceType в контексте вкладки. | [Контекст табули](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | Вкладки в групповом чате теперь доступны в выпущенной версии Teams и перемещены из предварительной версии для разработчиков. В рамках этой работы раздел вкладок был переработан для ясности.| [Настраиваемые вкладки](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Начало работы с Node JS и .NET/C# было обновлено для использования App Studio в Teams, а также добавлен новый раздел о размещении приложений Teams на основе узла в Azure. | Начало работы на платформе Microsoft Teams с [помощью C#/.NET](~/get-started/get-started-dotnet-app-studio.md)и App Studio, начало работы на платформе Microsoft Teams с [использованием Node JS](~/get-started/get-started-nodejs-app-studio.md)и App Studio, развяжите приложение [Node Teams в Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Теперь можно создавать глубокие ссылки на приватные чаты между пользователями. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 поставляется с новой функцией для использования вкладки Microsoft Teams в качестве веб-части SharePoint Framework. | [Вкладки в SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Функция "модуль задач" выпущена. Модуль задач позволяет создавать модальные всплывающие блоки в приложении Teams из ботов и вкладок. Во всплывающее представление можно запустить собственный код HTML или JavaScript, отобразить мини-приложения на основе youTube или Microsoft Stream или показать адаптивную `<iframe>` [карточку.](https://docs.microsoft.com/adaptive-cards/) | [Обзор модуля задач,](~/concepts/task-modules/task-modules-overview.md) [модуль задач на вкладке,](~/concepts/task-modules/task-modules-tabs.md)  [модуль задач в ботах](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Сведения о форматировании карточек были обновлены и протестированы в классических клиентах, клиентах iOS и Android для Teams. | [Карточки,](~/concepts/cards/cards.md) [форматирование карточек](~/concepts/cards/cards-format.md) |
| 09/24/2018 | API звонков и собраний по сети для Microsoft Graph были выпущены в бета-версии, и теперь приложения Teams могут взаимодействовать с пользователями с помощью голосовой и видеосвязи. | [Боты](~/concepts/calls-and-meetings/registering-calling-bot.md)для звонков и собраний по [сети,](~/concepts/calls-and-meetings/real-time-media-concepts.md)концепции мультимедиа в режиме реального [времени,](~/concepts/calls-and-meetings/registering-calling-bot.md)регистрация бота для звонков, [](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)отладка и локальное [тестирование,](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)мультимедиа с хостингом в приложении, обработка уведомлений о входящих [звонках](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Теперь страницы конфигурации вкладок значительно выше. | [Конструктор вкладок](tabs/design/tabs.md) |
| 08/15/2018 | Адаптивные карточки теперь поддерживаются в Teams.|[Действия адаптивной карточки в Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Поддержка клиентов для DevTools задокументирована для Developer Preview.| [DevTools для настольного клиента Microsoft Teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Расширения обмена сообщениями теперь поддерживают несколько команд. Эта функция была в Developer Preview и теперь выпущена для всех пользователей.| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | Теперь в соединителах поддерживается конфигурация во включении. Документация по соединитетелям также была изменена и расширена для ясности.| [Соединители](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Теперь бот может отправлять и получать файлы.| [Отправка и получение файлов с помощью бота](~/concepts/bots/bots-files.md)|
| 07/27/2018 | Предварительная версия для разработчиков теперь поддерживает несколько команд в расширениях обмена сообщениями. | [Расширения обмена сообщениями были расширены](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Сведения о повторной сертификации приложений добавлены в раздел "Публикация". |[Разрешения манифеста](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | В предварительной версии разработчика на странице конфигурации вкладок выделено больше места. | [Страница конфигурации вкладок значительно выше](tabs/design/tabs.md)|
| 07/12/2018 | Сведения о гостевом доступе. | [Гостевой доступ в Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Добавлены сведения о предварительном выпуске каталога приложений клиента Microsoft Teams. | [Публикация приложения Microsoft Teams](~/publishing/apps-publish.md)|
| 05/31/2018 | Предварительная версия teams для разработчиков (круг 3.6) была обновлена, включив возможность добавления ботов и вкладок в групповой чат. | [Функции предварительной версии,](~/resources/dev-preview/developer-preview-features.md) [схемы предварительной версии для разработчиков](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Адаптивные карточки теперь поддерживаются в Teams в действиях [адаптивных карт в Teams.](task-modules-and-cards/cards/cards-reference.md) |
| 05/29/2018 | Если вы используете предварительную версию [для](~/resources/dev-preview/developer-preview-intro.md)разработчиков, ваш бот сможет отправлять и получать файлы.| [Отправка и получение файлов с помощью бота](~/concepts/bots/bots-files.md), [функции в общедоступных Developer Preview для Microsoft Teams](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | ReplyToID был добавлен в полезной нагрузке для действий `Invoke` и `MessageBack` карт. Это особенно полезно, если вам нужно обновить сообщение, от которое поступило действие карточки. | [Действия с карточками](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Добавлен этот раздел для отслеживания изменений в интерфейсе программирования Teams и в этом наборе документации. | [Новые возможности](~/whats-new.md)|
| 04/10/2018 | Изменены URL-адреса проверки подлинности для согласованного использования ИД клиента в пути. | [Поток проверки подлинности для вкладок,](~/concepts/authentication/auth-flow-tab.md) [проверка подлинности вкладки AAD](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Добавлены рекомендации по проектированию для использования командного окна. |[Командная команда](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Использование ботов для отправки уведомлений для вашего приложения. |[Боты только для уведомлений](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Расширенная документация для упреждающего обмена сообщениями. |[Начиная разговор](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Рефакторатная документация для карточек. |[Карточки,](~/concepts/cards/cards.md) [действия с карточками,](~/concepts/cards/cards-actions.md) [форматирование карт,](~/concepts/cards/cards-format.md) [справочник по карточкам](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Добавлена документация для Teams App Studio. |[Быстрая разработка приложений с помощью Teams App Studio,](~/get-started/get-started-app-studio.md) [использование библиотеки управления в App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Добавлен пример кода для демонстрации метода AsTeamsChannelAccounts(). |[Получите контекст для бота](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Добавлены разделы для начала работы с C#. |[Начало работы на платформе Microsoft Teams с использованием C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Отправка вопросов, ошибок, запросов на функции и вкладов

Мы прослушиваем сообщество разработчиков по [нескольким каналам.](feedback.md)
