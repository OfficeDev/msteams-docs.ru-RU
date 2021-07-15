---
title: Новые возможности
description: Описывает все новые возможности разработчика в Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: команды, новые возможности
ms.openlocfilehash: 00b100ad634c1155446ab0b908c13b6b6eb3038c
ms.sourcegitcommit: e327c9766dfa05abb468cdc71319e3cba7c6c79f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/14/2021
ms.locfileid: "53428711"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Что нового для разработчиков в Microsoft Teams

Откройте Microsoft Teams платформы, которые обычно доступны (GA) и в предварительном просмотре разработчика.

## <a name="ga-features"></a>Функции GA

Microsoft Teams платформы, доступные всем разработчикам приложений.

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|07/08/2021|Доступность приложения для собраний доступна на мобильных устройствах. Мобильные клиенты поддерживают приложения во время собрания. |[Расширяемость приложения для собраний](apps-in-teams-meetings/meeting-app-extensibility.md)|
|06/28/2021|Интеграция возможностей выборщика людей.|[Интеграция функции "Выбор людей"](concepts/device-capabilities/people-picker-capability.md)|  
|06/25/2021| Введено пошаговое руководство по отправке активных сообщений. | [Пошаговое руководство по отправке упреждающих сообщений](sbs-send-proactive.yml) |
|06/09/2021| Представление сцены для изображений в адаптивных картах с `allowExpand` атрибутом. | [Представление сцены для изображений в адаптивных картах](~/task-modules-and-cards/cards/cards-format.md) |
|05/31/2021| Вкладки для беседы. | [Начало и продолжение бесед о контенте в вкладке](~/tabs/how-to/conversational-tabs.md) |
|05/24/2021| Обновленные Teams руководства по разработке приложений с мобильными шаблонами и другими.|[Проектирование Teams приложения](~/concepts/design/design-teams-app-overview.md)
|05/13/2021| Добавлены сведения о mConnect и Skooler.|[Система управления обучением Moodle](resources/moodle-overview.md)
|05/10/2021| Манифест v1.10 выпущен.|[Схема манифеста](resources/schema/manifest-schema.md) |
|05/10/2021| Новая функция настройки приложения.| [Включить оргии для настройки приложения](concepts/design/enable-app-customization.md) |
|05/07/2021| Глубокие ссылки для аудио- и видеозвонков в чате. |[Прямые ссылки](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|Новые рекомендации по публикации приложений в Teams магазине.|[Публикация приложения в Teams и](concepts/deploy-and-publish/appsource/publish.md)Teams для [хранения](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | Универсальные действия для адаптивных карт. | [Универсальные действия для адаптивных карточек](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|04/29/2021 | Пользовательские представления. | [Пользовательские просмотры](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/User-Specific-Views.md) |
|04/29/2021 | Последовательное рабочий процесс. | [Последовательные рабочие процессы](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Sequential-Workflows.md) |
|04/29/2021 | На сегодняшний день карты. | [Актуальные карточки](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/Up-To-Date-Views.md) |
|04/08/2021| Функция настройки приложения.|[Обзор приложений команд разработки,](concepts/design/enable-app-customization.md) [обзор студии](concepts/build-and-test/app-studio-overview.md#connectors)приложений и [схема манифеста](resources/schema/manifest-schema-dev-preview.md) |
|03/18/2021|Примечание. Обновление до версии 4.10 или выше SDK Bot Framework, как мы начали с процесса амортизации для `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` . | [Изменения API-интерфейса Bot для участников группы или чата](resources/team-chat-member-api-changes.md) |
|03/05/2021|Примечание. У вкладок больше не будет поля, связанные с их опытом. Разработчики вкладок должны просмотреть и обновить свои приложения. | [Удаление полей вкладок](resources/removing-tab-margins.md) |
|03/05/2021|По умолчанию устанавливается область и возможности группы.| [Возможности установки по умолчанию и группы](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|Reorder personal app tabs.|[Reorder the chat tab in personal apps](tabs/how-to/create-personal-tab.md#reorder-static-personal-tabs)|
|03/04/2021|Маскировка сведений в адаптивных картах.| [Маскировка сведений в адаптивных картах](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|Добавлены возможности расположения. <br/> Сведения о возможностях расположения добавляются в обзор возможностей устройства, разрешения родных устройств, интеграцию возможностей мультимедиа, а также файлы возможностей сканера QR или штрихкода.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей](concepts/device-capabilities/mobile-camera-image-permissions.md)мультимедиа , [Интеграция QR](concepts/device-capabilities/qr-barcode-scanner-capability.md)или возможности сканера штрихкодов , [Интеграция возможностей расположения](concepts/device-capabilities/location-capability.md) |
|02/18/2021|Добавлена возможность сканера QR или штрихкода. <br/> Сведения о возможностях сканера QR или штрихкодов добавляются в обзор возможностей устройства, разрешения на личные устройства и интеграцию файлов возможностей мультимедиа.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md), [Интеграция QR или сканер штрихкодов](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|Добавлен обзор возможностей устройства. <br/> Сведения о возможностях микрофона добавляются в разрешения на родном устройстве и интегрируют файлы возможностей мультимедиа.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройств](concepts/device-capabilities/native-device-permissions.md), [Интеграция возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|11/30/2020|Интеграция платформы удостоверений с Teams набор средств и Visual Studio Code для вкладок.|[Проверка подлинности с одним входом с Teams набор средств и Visual Studio Code для вкладок](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teams манифеста приложения, обновленного до версии 1.8.|[Справка: схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Teams руководства по разработке ботов.|[Рекомендации по проектированию ботов](bots/design/bots.md)|
|09/30/2020|Теперь поддерживается отправка и получение файлов ботам на мобильных устройствах.|[Отправка и получение файлов через бот](resources/bot-v3/bots-files.md)|
|09/22/2020|Новые сведения для начала работы с Teams разработкой.|[Создание первого обзора Teams приложения](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|Поддержка приложений для собраний Teams (Предварительная версия выпуска).|[Создание приложений для Teams собраний](apps-in-teams-meetings/create-apps-for-teams-meetings.md) и [приложений в Teams собраниях](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|Импорт Teams с помощью Microsoft Graph.|[Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
|08/12/2020 |Поддержка адаптивных карт в входящий веб-сайт перенесена в ga.|[Отправка адаптивных карточек с помощью входящего веб-перехватчика](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Начало создания Teams приложений с помощью Visual Studio набор средств.|[Создание приложений с помощью Microsoft Teams набор средств и Visual Studio Code](toolkit/visual-studio-overview.md) |
|08/06/2020|Поддержка проверки подлинности tabs SSO.|[Разработка вкладки SSO Microsoft Teams](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph активных ботов и сообщений (Public Preview).|[Включить активную установку ботов и активный обмен сообщениями в Teams с microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
|07/22/2020 |Обновления возможностей мобильных устройств.|[Запрос разрешений устройства для вкладки Microsoft Teams](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Teams Средство проверки приложений для отправки appSource.|[Teams Средство проверки приложений](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|Создание виртуального помощника для Teams.|[Виртуальный помощник для Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Наружная документация по индикатору нагрузки.|[Отображение индикатора загрузки](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Начало создания Teams приложений с помощью Visual Studio Code набор средств.|[Создание приложений с помощью Microsoft Teams набор средств и Visual Studio Code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Один вход для вкладок GA для Teams и настольных клиентов.|[Единый Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Схема манифеста обновлена до версии 1.7.| [Справка: схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|05/18/2020|Интеграция Power Virtual Agents с Teams.|[Интеграция Power Virtual Agents чат-бота с Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Интеграция систем WFM с соединитетелем Shifts для Teams.|[Microsoft Teams Сдвиг соединители WFM](samples/shifts-wfm-connectors.md)
|03/24/2020 | Добавлена поддержка для получения одного участника беседы и дополнительная поддержка для получения страниц участников. | [Получите контекст Teams для вашего бота](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
| 12/26/2019 | Параметр полезной нагрузки, отправленной боту, больше не шифруется, что позволяет использовать это значение для создания глубоких ссылок `replyToId` на эти сообщения. Полезной нагрузки сообщения включают зашифрованные значения в параметре `legacy.replyToId` .  |
| 11/05/2019 | Один вход с помощью Teams JavaScript SDK. | [Единый вход](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Разговорные боты и документация по расширению обмена сообщениями обновлены с учетом SDK 4.6 Bot Framework. Документация по SDK v3 доступна в разделе Ресурсы. | Вся документация по расширению ботов и сообщений. |
| 10/31/2019 | Новая структура документации и рефакторинг основных статей. Пожалуйста, сообщайте о каких-либо мертвых ссылках или 404's, создав GitHub проблемы. | Все из них! |
| 09/13/2019 | Бот запроса устанавливается из расширения обмена сообщениями на основе действий. | [Инициировать действия с расширениями обмена сообщениями](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | Поддержка частных каналов на вкладке и соединители. | [Получение контекста для вкладки](tabs/how-to/access-teams-context.md#retrieve-context-in-private-channels) |
| 06/20/2019 | Поделитесь внешним веб-сайтом с внешнего веб-сайта в Teams канал. | [Поделиться с Teams](~/share-to-teams.md) |
| 05/25/2019 | Ответьте сообщением бота из модуля задач. | [Отвечать сообщением бота из модуля задач](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Боты в групповых чатах. | [Взаимодействие с ботом в групповом чате или канале](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Локализация манифеста приложений. | [Локализация приложений](~/publishing/apps-localization.md) |
| 05/20/2019 | Действия сообщения. | [Действия сообщений](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Разгрузка ссылок (пользовательские предварительные просмотры URL-адресов). | [Развертывание ссылки](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Программа сертификации приложений для приложений магазина. | [Сертификация приложений](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | Шаблоны приложений теперь доступны. | [Шаблоны приложений](~/samples/app-templates.md) |
| 04/23/2019 | Расширения обмена сообщениями на основе действий теперь доступны. | [Расширения сообщений на основе действий](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Создание глубоких ссылок на частный чат. | [Глубокая связь с чатом](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Сведения о SKU и licenceType в контексте вкладки. | [Tab Context](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
| 11/12/2018 | Вкладки в групповом чате теперь доступны в выпущенной версии Teams. В рамках этой работы раздел вкладок был переработан для ясности.| [Настраиваемые вкладки](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Начало работы для Node JS и для .NET/C# было обновлено, чтобы использовать App Studio в Teams, и был добавлен новый раздел о размещении приложений node Teams Azure. | Начало работы на платформе Microsoft Teams с [C#/.NET](~/get-started/get-started-dotnet-app-studio.md)и App Studio , начало работы на платформе Microsoft Teams с [Node JS](~/get-started/get-started-nodejs-app-studio.md)и App Studio , хост ваше приложение Teams узла в [Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Теперь можно создавать глубокие ссылки на частные чаты между пользователями. | [Глубокая связь с чатом](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 отгружена и вместе с ней новая функция для использования вкладки Microsoft Teams в качестве SharePoint Framework веб-части. | [Вкладки в SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Была **выпущена** функция модуля задач. Модуль задач позволяет создавать в приложении модальные всплывающие Teams, как из ботов, так и из вкладок. В всплывающее всплывающее представление можно запустить собственный пользовательский код HTML/JavaScript, показать виджет на основе, например видео YouTube или Microsoft Stream, или отобразить `<iframe>` [адаптивную карту.](/adaptive-cards/) | [Обзор модуля задач,](~/concepts/task-modules/task-modules-overview.md) [модуль задач в вкладке,](~/concepts/task-modules/task-modules-tabs.md)  [модуль задач в ботах](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Информация по форматированию для карт была обновлена и протестирована в клиентах для настольных компьютеров, iOS и Android для Teams. | [Форматирование](~/concepts/cards/cards.md) [карт, карт](~/concepts/cards/cards-format.md) |
| 09/24/2018 | API вызовов и онлайн-собраний для Microsoft Graph были выпущены в бета-версии, и Teams приложения теперь могут взаимодействовать с пользователями с помощью голосовой связи и видео. | [Вызовы](~/concepts/calls-and-meetings/registering-calling-bot.md)и [онлайн-боты](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md) [собраний,](~/concepts/calls-and-meetings/real-time-media-concepts.md)концепции мультимедиа в режиме реального [времени,](~/concepts/calls-and-meetings/registering-calling-bot.md)регистрация бота [вызова,](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)отладка и локальное тестирование, средства массовой информации с хостингом приложений, обработка входящих уведомлений о [вызове](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Страницы конфигурации вкладок теперь значительно выше. | [Дизайн вкладок](tabs/design/tabs.md) |
| 08/15/2018 | Адаптивные карты теперь поддерживаются в Teams.|[Действия адаптивной карты в Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Поддержка клиентов для DevTools.| [DevTools для Microsoft Teams настольного клиента](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Расширения обмена сообщениями теперь поддерживают несколько команд. | [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | Конфигурация inline теперь поддерживается в соединители. Документация соединители также была пересмотрена и расширена для ясности.| [Соединители](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Теперь бот может отправлять и получать файлы.| [Отправка и получение файлов через бот](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | Сведения о повторной сертификации приложений добавлены в раздел Публикация. |[Разрешения манифеста](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | На странице конфигурации вкладок выделено больше места. | [Страница конфигурации вкладок значительно выше](tabs/design/tabs.md)|
| 07/12/2018 | Сведения о гостевом доступе. | [Гостевой доступ в Microsoft Teams](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Добавлены Microsoft Teams каталога приложений клиента. | [Публикация приложения Microsoft Teams](~/publishing/apps-publish.md)|
| 05/29/2018 | Адаптивные карты поддерживаются в Teams. | [Действия адаптивной карты в Teams](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | ReplyToID был добавлен в полезной нагрузке для действий `Invoke` и `MessageBack` карт. Это особенно полезно, если необходимо обновить сообщение, из которое пришло действие карты. | [Действия карточек](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Добавлена эта тема для отслеживания изменений в интерфейсе Teams программирования и этом наборе документации. | [Новые возможности](~/whats-new.md)|
| 04/10/2018 | Изменены URL-адреса проверки подлинности, чтобы последовательно использовать идентификацию клиента в пути. | [Поток проверки подлинности для вкладок](~/concepts/authentication/auth-flow-tab.md), [проверка подлинности AAD Tab](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Добавлены рекомендации по разработке для использования командного окна. |[Командный окне](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Использование ботов для отправки уведомлений для приложения. |[Боты только для уведомлений](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Расширенная документация для активного обмена сообщениями. |[Начиная разговор](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Refactored documentation for cards. |[Карточки,](~/concepts/cards/cards.md) [действия карт,](~/concepts/cards/cards-actions.md) [форматирование карт,](~/concepts/cards/cards-format.md) [справочная карточка](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Добавлена документация Teams App Studio. |[Быстро разработайте приложения с Teams App Studio](~/get-started/get-started-app-studio.md), Используя библиотеку управления в App [Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Добавлен пример кода для демонстрации метода AsTeamsChannelAccounts(). |[Получите контекст для бота](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Добавлены темы для начала использования C#. |[Начало работы на платформе Microsoft Teams с использованием C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>Developer preview

Предварительная версия разработчика — это публичная программа, которая предоставляет ранний доступ к Teams функциям платформы.  

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|06/23/2021| API сведений о собраниях и событиях Teams в режиме реального времени. | [Создание приложений для собраний Teams](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-details-api) |
|06/21/2021|Удалить поведение для личного приложения с ботом | [Удалить обновления поведения в личных приложениях с помощью ботов](bots/how-to/conversations/subscribe-to-conversation-events.md#uninstall-behavior-for-personal-app-with-bot)|
|06/16/2021| Согласие для чатов с определенными ресурсами. |[Согласие, определенное для ресурсов,](graph-api/rsc/resource-specific-consent.md) [тестирование разрешений](graph-api/rsc/test-resource-specific-consent.md) на согласие, определенное ресурсами, в Teams|  
|05/26/2021|Создание вкладок с использованием адаптивных карточек|[Вкладки сборки](tabs/how-to/build-adaptive-card-tabs.md)|
|05/25/2021| Обновленные Teams набор средств [для Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) и [Visual Studio](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit&ssr=false#overview). | [Начало разработки Teams приложения](~/get-started/prerequisites.md) |
|05/25/2021| Новый портал разработчиков для Teams для управления вашими Teams приложениями. | [Портал разработчиков Teams](concepts/build-and-test/teams-developer-portal.md) |
|05/25/2021| Функция Custom Together Mode совмещает участников в одну виртуальную сцену и помещает их видеопотоки в заранее. | [Настраиваемые сцены режима "Вместе"](~/apps-in-teams-meetings/teams-together-mode.md) |
|05/24/2021|Ботам можно включить получение всех сообщений канала с помощью согласия на использование ресурсов (RSC).|[Получение всех сообщений с помощью RSC,](~/bots/how-to/conversations/channel-messages-with-rsc.md)обзор бесед [ботов,](~/bots/how-to/conversations/conversation-basics.md)разговоров каналов и групп [и](~/bots/how-to/conversations/channel-and-group-conversations.md)схемы манифеста [предварительного просмотра разработчика](~/resources/schema/manifest-schema-dev-preview.md) |
|05/21/2021|Вкладки связывают разгрузку и представление сцены|[Вкладки связывают разгрузку и представление сцены](tabs/tabs-link-unfurling.md) |
|03/05/2021| У вкладок больше не будет поля, связанные с их опытом. Разработчики вкладок должны просмотреть и обновить свои приложения. | [Удаление полей вкладок](resources/removing-tab-margins.md) |

Дополнительные сведения см. в [обзоре предварительного просмотра общедоступных разработчиков для Teams](~/resources/dev-preview/developer-preview-intro.md).

## <a name="teams-app-template-catalog"></a>Teams каталог шаблонов приложений

Наряду с новыми функциями, мы также предоставляем готовые к [Teams](samples/app-templates.md) шаблоны приложений, которые можно развернуть сразу или изменить в ваших потребностях. Новые добавленные шаблоны указываются звездой ☆.

## <a name="submit-your-feedback"></a>Отправка отзывов

Мы рекомендуем Teams разработчикам задавать вопросы, отправлять ошибки, отправлять запросы на функции и делать вклады. Вы можете отправить отзывы по любому из [доступных каналов.](feedback.md)
