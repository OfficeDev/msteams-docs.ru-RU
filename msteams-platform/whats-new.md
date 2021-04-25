---
title: Новые возможности
description: Описание всех новых функций разработчика в Microsoft Teams
ms.topic: reference
keywords: команды, новые возможности
ms.openlocfilehash: 8d38c5a4f79b557209eedab6747517e689248874
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946461"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Новые возможности для разработчиков в Microsoft Teams

>[!TIP]
> Ознакомьтесь с примерами решений для общих сценариев команд в каталоге шаблонов [**приложений Teams!**](samples/app-templates.md) Каталог в алфавитном порядке, а самые новые дополнения помечены звездой ☆.

## <a name="change-log"></a>Журнал изменений

Журнал изменений содержит изменения в платформе Microsoft Teams и в этом наборе документов. Иногда записи могут использоваться для вызова внимания к новой функции, которая просто интересна разработчикам Teams.

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|04/08/2021| Функция настройки приложения теперь доступна в предварительном просмотре разработчика.|[Обзор приложений команд разработки,](concepts/design/design-teams-app-overview.md#app-customization) [обзор студии](concepts/build-and-test/app-studio-overview.md#connectors)приложений и [схема манифеста](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021|Примечание. Обновление до версии 4.10 или выше SDK Bot Framework, как мы начали с процесса амортизации для `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` . | [Изменения API-интерфейса Bot для участников группы или чата](resources/team-chat-member-api-changes.md) |
|03/05/2021|Примечание. У вкладок больше не будет поля, связанные с их опытом. Разработчики вкладок должны просмотреть и обновить свои приложения. | [Удаление полей вкладок](resources/removing-tab-margins.md) |
|03/05/2021|По умолчанию область установки и возможности групповой установки в предварительном просмотре разработчика.| [Возможности установки по умолчанию и группы](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|Переубор личных вкладок приложений|[Reorder the chat tab in personal apps](tabs/how-to/create-tab-pages/content-page.md#reorder-static-personal-tabs)|
|03/04/2021|Маскировка сведений в адаптивных картах находится в предварительном просмотре разработчика.| [Маскировка сведений в адаптивных картах](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|Новое. Добавлены возможности расположения. <br/> Обновление. Сведения о возможностях расположения добавляются в обзор возможностей устройства, разрешения на использование родных устройств, интеграцию возможностей мультимедиа и файлов сканера QR или штрих-кодов.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей](concepts/device-capabilities/mobile-camera-image-permissions.md)мультимедиа , [Интеграция QR](concepts/device-capabilities/qr-barcode-scanner-capability.md)или возможности сканера штрихкодов , [Интеграция возможностей расположения](concepts/device-capabilities/location-capability.md) |
|02/18/2021|Новое. Добавлена возможность сканера QR или штрихкода. <br/> Обновление. Сведения о возможностях сканера QR или штрихкодов добавляются в обзор возможностей устройства, разрешения на устройства и интеграцию файлов средств массовой информации.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md), [Интеграция QR или сканер штрихкодов](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|Новый: добавлен обзор возможностей устройств. <br/> Обновление. Сведения о возможностях микрофона добавляются в разрешения на родном устройстве и интегрируют файлы возможностей мультимедиа.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md)|
|11/30/2020|Новое: интеграция платформы удостоверений с teams набор средств и Visual Studio кода для вкладок|[Проверка подлинности с помощью единого набор средств и Visual Studio для вкладок](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Манифест приложения Teams, обновленный до версии 1.8|[Справка. Схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Рекомендации по разработке ботов teams|[Рекомендации по проектированию ботов](bots/design/bots.md)|
|9/30/2020|Теперь поддерживается отправка и получение файлов ботам на мобильных устройствах.|[Отправка и получение файлов через бот](resources/bot-v3/bots-files.md)|
|09/22/2020|Новое руководство "Начало работы с командами"|[Создание первого обзора приложения Teams](build-your-first-app/build-first-app-overview.md)|
|9/18/2020|Поддержка приложений in-meeting Teams (Предварительная версия выпуска)|[Создание приложений для собраний teams и](apps-in-teams-meetings/create-apps-for-teams-meetings.md) [приложений в собраниях Teams](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|8/19/2020|Сообщения import Teams с помощью Microsoft Graph|[Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |Поддержка адаптивных карт в входящий веб-сайт перенесена в ga.|[Отправка адаптивных карточек с помощью входящего веб-перехватчика](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Начало создания приложений Teams с помощью Visual Studio набор средств.|[Создание приложений с помощью кода Microsoft Teams набор средств и Visual Studio](toolkit/visual-studio-overview.md) |
|08/06/2020|Поддержка проверки подлинности tabs SSO|[Разработка вкладки SSO Microsoft Teams](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph proactive bots and messages (Public Preview)|[Включить активную установку ботов и активную передачу сообщений в Teams с Microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |Обновления возможностей мобильных устройств.|[Запрос разрешений на устройства для вкладки Microsoft Teams](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Teams App Validation Tool for AppSource submissions.|[Средство проверки приложений Teams](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)
|07/15/2020|Создание виртуального помощника для Teams|[Виртуальный помощник для Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Наружная документация по индикатору загрузки|[Отображение индикатора загрузки](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Начало создания приложений Teams с помощью Visual Studio кода набор средств.|[Создание приложений с помощью кода Microsoft Teams набор средств и Visual Studio](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Единый вход для вкладок GA для веб-и настольных клиентов Teams|[Единый Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Схема манифеста обновлена до версии 1.7| [Справка. Схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
| 05/20/2020 | Разрешения на согласие с использованием API Microsoft Graph в предварительном просмотре разработчика. |[Согласие на определенные ресурсы (RSC) — Developer Preview](graph-api/rsc/resource-specific-consent.md) |
|5/18/2020|Интеграция виртуальных агентов Power с teams|[Интеграция чат-бота виртуальных агентов Power с Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Интеграция систем WFM с соединитетелем Shifts для teams|[Microsoft Teams переносит соединители WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Добавлена поддержка для получения одного участника беседы и дополнительная поддержка для получения страниц участников. | [Получите контекст Teams для вашего бота](~/bots/how-to/get-teams-context.md)
| 12/26/2019 | Параметр полезной нагрузки, отправленной боту, больше не шифруется, что позволяет использовать это значение для создания глубоких ссылок `replyToId` на эти сообщения. Полезной нагрузки сообщения включают зашифрованные значения в параметре. `legacy.replyToId`.  |
| 11/5/2019 | Один вход с использованием команд JavaScript SDK на странице веб-контента находится в предварительном просмотре разработчика. | [Единый вход](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Разговорные боты и документация по расширению обмена сообщениями обновлены с учетом SDK 4.6 Bot Framework. Документация по SDK v3 доступна в разделе Ресурсы. | Вся документация по расширению ботов и сообщений. |
| 10/31/2019 | Новая структура документации и рефакторинг основных статей. Пожалуйста, сообщайте о любых мертвых ссылках или 404-х, создав проблему GitHub. | Все из них! |
| 9/13/2019 | Бот запроса устанавливается из расширения обмена сообщениями на основе действий. | [Инициировать действия с расширениями обмена сообщениями](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 8/28/2019 | Поддержка частных каналов на вкладке и соединители. | [Получение контекста для вкладки](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Поделитесь внешним веб-сайтом с внешнего веб-сайта в канал Teams. | [Share to Teams](~/share-to-teams.md) |
| 05/25/2019 | Ответьте сообщением бота из модуля задач. | [Отвечать сообщением бота из модуля задач](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Боты в групповых чатах. | [Взаимодействие с ботом в групповом чате или канале](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Локализация манифеста приложений. | [Локализация приложений](~/publishing/apps-localization.md) |
| 05/20/2019 | Действия сообщения. | [Действия сообщений](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Разгрузка ссылок (пользовательские предварительные просмотры URL-адресов). | [Развертывание ссылки](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Программа сертификации приложений для приложений магазина. | [Сертификация приложений](~/publishing/application-certification.md) |
| 05/06/2019 | Шаблоны приложений теперь доступны. | [Шаблоны приложений](~/samples/app-templates.md) |
| 04/23/2019 | Расширения обмена сообщениями на основе действий теперь доступны. | [Расширения сообщений на основе действий](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Создание глубоких ссылок на частный чат не является предварительным и доступным для разработчика. | [Глубокая связь с чатом](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Сведения о SKU и licenceType в контексте вкладки. | [Tab Context](~/concepts/tabs/tabs-context.md) |
| 11/12/2018 | Вкладки в групповом чате теперь доступны в выпущенной версии Teams и перенесены из предварительного просмотра разработчика. В рамках этой работы раздел вкладок был переработан для ясности.| [Настраиваемые вкладки](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Начало работы для Node JS и для .NET/C# было обновлено для использования App Studio в Teams, и добавлен новый раздел о размещении приложений Node Teams в Azure. | Начало работы на платформе Microsoft Teams с [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)и App Studio, начало работы на платформе Microsoft Teams с [node JS и App Studio,](~/get-started/get-started-nodejs-app-studio.md)хост ваше приложение [Node Teams](~/get-started/get-started-nodejs-in-azure.md) в Azure|
| 11/09/2018 | Теперь можно создавать глубокие ссылки на частные чаты между пользователями. | [Глубокая связь с чатом](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 отгрузила и вместе с ней новую функцию для использования вкладки Microsoft Teams в качестве веб-части SharePoint Framework. | [Вкладки в SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Была выпущена функция "Модуль задач". Модуль задач позволяет создавать модальные всплывающие опытом в приложении Teams как из ботов, так и из вкладок. В всплывающее всплывающее представление можно запустить собственный пользовательский код HTML/JavaScript, показать виджет на основе, например видео YouTube или Microsoft Stream, или отобразить `<iframe>` [адаптивную карту.](https://docs.microsoft.com/adaptive-cards/) | [Обзор модуля задач,](~/concepts/task-modules/task-modules-overview.md) [модуль задач в вкладке,](~/concepts/task-modules/task-modules-tabs.md)  [модуль задач в ботах](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Информация по форматированию для карт была обновлена и протестирована на настольных компьютерах, клиентах iOS и Android для Teams. | [Форматирование](~/concepts/cards/cards.md) [карт, карт](~/concepts/cards/cards-format.md) |
| 09/24/2018 | API вызовов и онлайн-собраний для Microsoft Graph были выпущены в бета-версии, и теперь приложения Teams могут взаимодействовать с пользователями с помощью голосовой и видеосвязи. | [Вызовы](~/concepts/calls-and-meetings/registering-calling-bot.md)и [онлайн-боты](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md) [собраний,](~/concepts/calls-and-meetings/real-time-media-concepts.md)концепции мультимедиа в режиме реального [времени,](~/concepts/calls-and-meetings/registering-calling-bot.md)регистрация бота [вызова,](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)отладка и локальное тестирование, средства массовой информации с хостингом приложений, обработка входящих уведомлений о [вызове](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Страницы конфигурации вкладок теперь значительно выше. | [Дизайн вкладок](tabs/design/tabs.md) |
| 08/15/2018 | Адаптивные карты теперь поддерживаются в Teams.|[Действия адаптивной карты в Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Поддержка клиентов для DevTools была задокументирована для Developer Preview.| [DevTools для настольного клиента Microsoft Teams](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Расширения обмена сообщениями теперь поддерживают несколько команд. Эта функция находится в Developer Preview и теперь выпущена для всех пользователей.| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | Конфигурация inline теперь поддерживается в соединители. Документация соединители также была пересмотрена и расширена для ясности.| [Соединители](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Теперь бот может отправлять и получать файлы.| [Отправка и получение файлов через бот](~/concepts/bots/bots-files.md)|
| 07/27/2018 | Предварительный просмотр разработчика теперь поддерживает несколько команд в расширениях обмена сообщениями. | [Расширения обмена сообщениями были расширены](~/resources/dev-preview/developer-preview-features.md)|
| 07/23/2018 | Сведения о повторной сертификации приложений добавлены в раздел Публикация. |[Разрешения манифеста](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | В предварительном просмотре разработчика на страницу конфигурации вкладок выделено больше места. | [Страница конфигурации вкладок значительно выше](tabs/design/tabs.md)|
| 07/12/2018 | Сведения о гостевом доступе. | [Гостевой доступ в Microsoft Teams](https://docs.microsoft.com/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Добавлены сведения о предварительном выпуске каталога приложений клиента Microsoft Teams. | [Публикация приложения Microsoft Teams](~/publishing/apps-publish.md)|
| 05/31/2018 | Предварительный просмотр разработчика Teams (кольцо 3.6) был обновлен, чтобы включить возможность добавления ботов и вкладок в групповой чат. | [Функции в предварительном просмотре разработчика](~/resources/dev-preview/developer-preview-features.md), [схема предварительного просмотра разработчика](~/resources/schema/manifest-schema-dev-preview.md)|
| 05/29/2018 | Адаптивные карты теперь поддерживаются в Teams в [действиях адаптивных карт в Teams.](task-modules-and-cards/cards/cards-reference.md) |
| 05/29/2018 | Если вы используете предварительный [просмотр разработчика,](~/resources/dev-preview/developer-preview-intro.md)ваш бот теперь может отправлять и получать файлы.| [Отправка и получение файлов через бот](~/concepts/bots/bots-files.md), [функции](~/resources/dev-preview/developer-preview-features.md) в Developer Preview для Microsoft Teams|
| 04/17/2018 | ReplyToID был добавлен в полезной нагрузке для действий `Invoke` и `MessageBack` карт. Это особенно полезно, если необходимо обновить сообщение, из которое пришло действие карты. | [Действия карты](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Добавлена эта тема для отслеживания изменений в интерфейсе программирования Teams и наборе документации. | [Новые возможности](~/whats-new.md)|
| 04/10/2018 | Изменены URL-адреса проверки подлинности, чтобы последовательно использовать идентификацию клиента в пути. | [Поток проверки подлинности для вкладок](~/concepts/authentication/auth-flow-tab.md), [проверка подлинности AAD Tab](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Добавлены рекомендации по разработке для использования командного окна. |[Командный окне](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Использование ботов для отправки уведомлений для приложения. |[Боты только для уведомлений](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Расширенная документация для активного обмена сообщениями. |[Начиная разговор](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Refactored documentation for cards. |[Карточки,](~/concepts/cards/cards.md) [действия карт,](~/concepts/cards/cards-actions.md) [форматирование карт,](~/concepts/cards/cards-format.md) [справочная карточка](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Добавлена документация для Teams App Studio. |[Быстро разработайте приложения в Teams App Studio,](~/get-started/get-started-app-studio.md)используя библиотеку управления [в App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Добавлен пример кода для демонстрации метода AsTeamsChannelAccounts(). |[Получите контекст для бота](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Добавлены темы для начала использования C#. |[Начало работы на платформе Microsoft Teams с использованием C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

## <a name="submit-your-questions-bugs-feature-requests-and-contributions"></a>Отправка вопросов, ошибок, запросов на функции и взносов

Мы слушаем сообщество разработчиков по [нескольким каналам.](feedback.md)
