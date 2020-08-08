---
title: Новые возможности
description: Описание всех новых функций разработчика в Microsoft Teams
keywords: новые версии Teams
ms.openlocfilehash: 83fe01f5a34ae0d1f3f3f86699f47139bb630b3e
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587729"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Новые возможности для разработчиков в Microsoft Teams

>[!TIP]
> Ознакомьтесь с рабочими шаблонами, готовыми к работе, в [**каталоге шаблонов приложений Teams**](samples/app-templates.md). Каталог имеет алфавитный алфавит, а последние добавленные помечаются звездочкой **&#9734;**.

## <a name="change-log"></a>Журнал изменений

В журнале изменений перечисляются изменения платформы Microsoft Teams и этого набора документов. Иногда записи можно использовать для привлечения внимания к новой функции, которая представляет собой простой интерес для разработчиков Teams.

| **Date** | **Примечания** | **Измененные разделы** |
| -------- | --------- | ------------------ |
| 07/22/2020 |Обновления возможностей мобильных устройств.|[Запрос разрешений устройства для вкладки Microsoft Teams](~/tabs/how-to/native-device-permissions.md) |
|07/20/2020|Средство проверки приложений Teams для отправки AppSource.|[Средство проверки приложений Teams](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Создание виртуального помощника для Teams|[Виртуальный помощник для Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Отображение собственная документация по индикатору загрузки|[Индикатор загрузки машинного кода](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Приступите к созданию приложений Teams с помощью Visual Studio Code Toolkit.|[Создание приложений с помощью набора инструментов Microsoft Teams и кода Visual Studio](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Единый вход для вкладок "GA" для веб-клиентов Teams и настольных компьютеров|[Единый вход (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Схема манифеста обновлена до версии 1,7| [Ссылка: схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
| 05/20/2020 | Разрешения на согласие с определенными ресурсами с помощью API Microsoft Graph — в предварительной версии для разработчиков. |[Согласие для определенных ресурсов (RSC) — Предварительная версия для разработчиков](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Интеграция виртуальных агентов Power в Teams|[Интеграция виртуальных агентов Power чатбот с Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Интеграция систем WFM с соединителем смен для Teams|[Microsoft Teams смещается соединители WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Добавлена поддержка получения одного участника беседы и дополнительная поддержка извлечения элементов, на которых выполняется страница. | [Получите контекст Teams для вашего бота](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | `replyToId`Параметр в полезных данных, отправляемых на Bot, больше не шифруется, что позволяет использовать это значение для создания диплинкс к этим сообщениям. Полезные данные сообщений включают в себя зашифрованные значения в параметре. `legacy.replyToId`.  |
| 11/5/2019 | Единый вход с помощью пакета SDK для JavaScript в Teams на странице веб-контента находится в области предварительного просмотра для разработчиков. | [Единый вход](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Документация по расширению Боты и обмену сообщениями обновлена, чтобы отразить пакет SDK 4,6 Bot. Документация по пакету SDK v3 доступна в разделе Resources. | Документация по добавочному номеру ленты и почтовой службе. |
| 10/31/2019 | Новая структура документации и оптимизация кода основной статьи. Создайте отчет о недоставленных ссылках или 404, создав ошибку GitHub. | Все из них! |
| 9/13/2019 | На основе расширения обмена сообщениями на основе действий устанавливается Bot запросов. | [Запуск действий с расширениями обмена сообщениями](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Поддержка частных каналов в вкладках и соединителях. | [Получение контекста для вкладки](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Общий доступ к внешнему веб-сайту с внешнего веб-сайта в канал Teams. | [Предоставление общего доступа к Teams](~/share-to-teams.md) |
| 05/25/2019 | Ответ с сообщением Bot из модуля задачи. | [Ответ с сообщением Bot из модуля задач](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Боты в беседах групп. | [Взаимодействие с каналом "bot" в группе "чат" или "канал"](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Локализация манифеста приложения. | [Локализация приложений](~/publishing/apps-localization.md) |
| 05/20/2019 | Действия с сообщениями. | [Действия с сообщениями](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Link унфурлинг (пользовательский Просмотр URL-адресов). | [Развернуть ссылку](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Программа сертификации приложений для приложений Магазина. | [Сертификация приложений](~/publishing/application-certification.md) |
| 05/06/2019 | Шаблоны приложений теперь доступны. | [Шаблоны приложений](~/samples/app-templates.md) |
| 04/23/2019 | Теперь доступны расширения обмена сообщениями на основе действий. | [Расширения сообщений на основе действий](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Создание глубоких ссылок на частное чат — это недоступная Предварительная версия и доступная версия для разработчиков. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Отображение SKU и Лиценцетипе сведения в контексте Tab. | [Контекст вкладки](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | Вкладки группового чата теперь доступны в выпущенной версии Teams и были перемещены из области предварительного просмотра разработчика. В рамках этой работы раздел "вкладки" был изменен для ясности.| [Настраиваемые вкладки](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Начало работы с узлом JS и .NET/C# было обновлено для использования App Studio в Teams, а новый раздел добавлен в приложения Teams на базе узла для хостинга в Azure. | [Начало работы на платформе Microsoft Teams с C#/.нет и App Studio](~/get-started/get-started-dotnet-app-studio.md), Приступая к [работе на платформе Microsoft Teams с узлом JS и App Studio](~/get-started/get-started-nodejs-app-studio.md), [разместите приложение Teams в Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Теперь вы можете создавать глубокие ссылки на частные беседы между пользователями. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1,7 поставляется с новым компонентом для использования вкладки Microsoft Teams в качестве веб-части SharePoint Framework. | [Вкладки в SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Был выпущен компонент "модуль задач". Модуль задачи позволяет создавать Модальные всплывающие окна в приложении Teams, как с боты, так и с помощью вкладок. Во всплывающем окне можно запустить собственный код HTML/JavaScript, показать мини-приложение, `<iframe>` например YouTube или Microsoft Stream Stream, или отобразить [адаптивную карту](https://docs.microsoft.com/adaptive-cards/). | [Обзор модуля задачи](~/concepts/task-modules/task-modules-overview.md), [модуль задачи на вкладках](~/concepts/task-modules/task-modules-tabs.md), [модуль задачи в Боты](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Сведения о форматировании карточек обновлены и протестированы в клиентах для настольных ПК, iOS и Android для Teams. | [Карточки](~/concepts/cards/cards.md), [Форматирование карточек](~/concepts/cards/cards-format.md) |
| 09/24/2018 | Звонки и API собраний по сети для Microsoft Graph были выпущены для бета-версии, а приложения Teams теперь могут взаимодействовать с пользователями с помощью голосовых и видеоконференций. | [Звонки и собрания по сети Боты](~/concepts/calls-and-meetings/registering-calling-bot.md), [Основные понятия мультимедиа в реальном времени](~/concepts/calls-and-meetings/real-time-media-concepts.md), [регистрация абонентского робота](~/concepts/calls-and-meetings/registering-calling-bot.md), [Отладка и локальное тестирование](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md), работа с [размещенными в приложении носителями](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md), [обработка уведомлений о входящих вызовах](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Страницы настройки вкладок теперь имеют значительно больше времени. | [Конструктор вкладок](tabs/design/tabs.md) |
| 08/15/2018 | Адаптивные карты теперь поддерживаются в Teams.|[Действия адаптивной карточки в Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Поддержка клиентов для Девтулс была документирована для разработчиков в предварительной версии для разработчиков.| [Девтулс для настольного клиента Microsoft Teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Расширения обмена сообщениями теперь поддерживают несколько команд. Эта функция была в предварительной версии Developer, и теперь она выпущена для всех пользователей.| [Компосикстенсионс. Commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | Встроенная конфигурация теперь поддерживается в соединителях. Документация по соединителям также была пересмотрена и расширена для ясности.| [Соединители](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Теперь ваш Bot может отправлять и получать файлы.| [Отправка и получение файлов через Bot](~/concepts/bots/bots-files.md)|
| 07/27/2018 | Предварительная версия для разработчиков теперь поддерживает несколько команд в расширениях обмена сообщениями. | [Расширения для обмена сообщениями расширены](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Сведения о повторной сертификации приложений добавлены в раздел "публикация". |[Разрешения для манифеста](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | В предварительной версии для разработчиков на странице Настройка вкладки выделено больше места. | [Страница настройки вкладок значительно превышает высоту](tabs/design/tabs.md#configuration-page-height)|
| 07/12/2018 | Сведения о гостевом доступе. | [Гостевой доступ в Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Добавлены сведения о предварительном выпуске каталога приложений клиента Microsoft Teams. | [Публикация приложения Microsoft Teams](~/publishing/apps-publish.md)|
| 05/31/2018 | Бета-версия разработчиков Teams (Ring 3,6) была обновлена и добавлена возможность добавлять Боты и вкладки в групповой чат. | [Функции в предварительной версии для разработчиков](~/resources/dev-preview/developer-preview-features.md), [схема предварительной версии для разработчиков](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Адаптивные карты теперь поддерживаются в Teams в [действиях адаптивной карточки в Teams](task-modules-and-cards/cards/cards-reference.md). |
| 05/29/2018 | Если вы используете [Предварительный просмотр для разработчиков](~/resources/dev-preview/developer-preview-intro.md), пользователь Bot теперь может отправлять и получать файлы.| [Отправка и получение файлов через Bot](~/concepts/bots/bots-files.md), [функции в общедоступной предварительной версии для разработчиков Microsoft Teams](~/resources/dev-preview/developer-preview-features.md)|
| 04/17/2018 | в полезные данные для `Invoke` действий и карт добавлена реплитоид `MessageBack` . Это особенно полезно, если вам нужно обновить сообщение, из которого поступило действие карточки. | [Действия с картой](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Добавлена эта тема для отслеживания изменений в программном интерфейсе Teams и этом наборе документации. | [Новые возможности](~/whats-new.md)|
| 04/10/2018 | Изменены URL-адреса проверки подлинности для согласованного использования идентификатора клиента в пути. | [Процесс проверки](~/concepts/authentication/auth-flow-tab.md)подлинности вкладок [AAD](~/concepts/authentication/auth-tab-AAD.md) на вкладках|
| 04/06/2018 | Добавлены рекомендации по проектированию для использования поля "команда". |[Поле "команда"](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Использование боты для отправки уведомлений для вашего приложения. |[Боты только для уведомлений](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Расширенная документация для упреждающего обмена сообщениями. |[Начиная разговор](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Переструктурированная документация для карточек. |[Карточки](~/concepts/cards/cards.md), [действия карточек](~/concepts/cards/cards-actions.md), [Форматирование карточек](~/concepts/cards/cards-format.md), [Справочник по карточкам](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Добавлена документация для Teams Studio App Studio. |[Быстрая разработка приложений с помощью Team Studio App Studio](~/get-started/get-started-app-studio.md) [с помощью библиотеки элементов управления в App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Добавлен пример кода, демонстрирующий метод Астеамсчаннелаккаунтс (). |[Получение контекста для ленты](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Добавлены разделы, посвященные началу работы с C#. |[Начало работы на платформе Microsoft Teams с использованием C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Отправляйте свои вопросы, сообщения об ошибках, функции и публикации

Мы будем слушать сообщество разработчиков по [нескольким каналам](feedback.md).
