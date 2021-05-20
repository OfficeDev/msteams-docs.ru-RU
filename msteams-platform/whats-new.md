---
title: Новые возможности
description: Описывает все новые функции разработчика в Microsoft Teams
ms.topic: reference
localization_priority: Normal
keywords: команды, что нового последнего
ms.openlocfilehash: aa78d187b3fa771c7e7f0fadfe1aa8f571203cb7
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566518"
---
# <a name="whats-new-for-developers-in-microsoft-teams"></a>Что нового для разработчиков в Microsoft Teams

Откройте для Microsoft Teams функции платформы, которые обычно доступны (GA) и в предварительном просмотре разработчика.

## <a name="ga-features"></a>Особенности GA

Microsoft Teams платформы, доступные всем разработчикам приложений.

<br>

<details>

<summary><b>2021</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|05/13/2021|Добавлена информация о mConnect и Skooler.|[Система управления обучением Moodle](resources/moodle-overview.md)
|05/10/2021| Манифест v1.10 выпущен.|[Схема манифеста](resources/schema/manifest-schema.md) |
|05/10/2021| Функция настройки приложения.| [Проектирование приложения Microsoft Teams для веб-Microsoft Teams](~/concepts/design/design-teams-app-overview.md#app-customization) |
|05/07/2021| Глубокие ссылки на аудио- и видеозвонки в чате. |[Прямые ссылки](concepts/build-and-test/deep-links.md#deep-linking-to-an-audio-or-audio-video-call) |
|04/30/2021|Новое руководство о том, как публиковать приложения в Teams магазине.|[Опубликуйте свое приложение в магазине Teams,](concepts/deploy-and-publish/appsource/publish.md) [Teams правила проверки магазина](concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) |
|04/29/2021 | Новое: Универсальные действия для адаптивных карт. | [Универсальные действия для адаптивных карточек](task-modules-and-cards/cards/universal-actions-for-adaptive-cards/overview.md) |
|03/18/2021|Примечание: Обновление до версии 4.10 или выше Bot Framework SDK, как мы начали с процесса амортизации для `TeamsInfo.getMembers` и `TeamsInfo.GetMembersAsync` . | [Изменения API-интерфейса Bot для участников группы или чата](resources/team-chat-member-api-changes.md) |
|03/05/2021|Примечание: Вкладки больше не будут иметь поля, окружающие их опыт. Разработчики вкладок должны просмотреть и обновить свои приложения. | [Удаление поля вкладок](resources/removing-tab-margins.md) |
|03/05/2021|Область установки по умолчанию и групповая возможность находится в предварительном просмотре разработчика.| [Область установки по умолчанию и возможности группы](concepts/deploy-and-publish/add-default-install-scope.md) |
|03/05/2021|Перезаказ личных вкладок приложения.|[Перезаказ вкладки чата в личных приложениях](tabs/how-to/create-tab-pages/content-page.md#reorder-static-personal-tabs)|
|03/04/2021|Информационная маскировка в адаптивных картах.| [Информационная маскировка в адаптивных картах](task-modules-and-cards/cards/cards-format.md#information-masking-in-adaptive-cards) |
|02/19/2021|Добавлены возможности определения местоположения. <br/> Информация о возможностях местоположения добавляется в обзор возможностей устройства, разрешения на использование родных устройств, возможности интеграции мультимедиа, а также файлы возможностей сканирования штрих-кодов.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройства , Интеграция](concepts/device-capabilities/native-device-permissions.md) [возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md), [Интеграция возможностей сканера или штрих-кода](concepts/device-capabilities/qr-barcode-scanner-capability.md), [Интеграция возможностей местоположения](concepts/device-capabilities/location-capability.md) |
|02/18/2021|Добавлена возможность сканирования штрих-кодов или штрих-кодов. <br/> Информация о возможностях сканирования штрих-кодов добавляется в обзор возможностей устройства, разрешения на работу с родными устройствами и интегрирует файлы возможностей мультимедиа.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройства , Интеграция](concepts/device-capabilities/native-device-permissions.md) [возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md), [Интеграция возможностей сканера или штрих-кода](concepts/device-capabilities/qr-barcode-scanner-capability.md) |
|02/09/2021|Добавлен обзор возможностей устройства. <br/> Информация о возможностях микрофона добавляется в разрешениях родных устройств и интегрирует файлы возможностей мультимедиа.|[Обзор](concepts/device-capabilities/device-capabilities-overview.md), [Запрос разрешений устройства](concepts/device-capabilities/native-device-permissions.md), Интеграция [возможностей мультимедиа](concepts/device-capabilities/mobile-camera-image-permissions.md)|

<br>

</details>

<br>

<details>
  
<summary><b>2020</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|11/30/2020|Интеграция платформы идентификации с Teams набор средств и Visual Studio Code для вкладок.|[Одноэтажная аутентификация с Teams набор средств и Visual Studio Code для вкладок](toolkit/visual-studio-code-tab-sso.md)|
|11/16/2020|Teams приложение манифест обновлен до версии 1.8.|[Справка: Схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|11/10/2020|Teams руководства по проектированию ботов.|[Рекомендации по проектированию ботов](bots/design/bots.md)|
|09/30/2020|Отправка и прием файлов ботам на мобильных устройствах теперь поддерживается.|[Отправка и получение файлов через бота](resources/bot-v3/bots-files.md)|
|09/22/2020|Новая информация для начала работы с Teams разработкой.|[Создайте свой первый Teams обзор приложения](build-your-first-app/build-first-app-overview.md)|
|09/18/2020|Поддержка приложений для Teams (Release Preview).|[Создание приложений для Teams встреч и](apps-in-teams-meetings/create-apps-for-teams-meetings.md) [приложений на Teams собраниях](apps-in-teams-meetings/teams-apps-in-meetings.md)|
|08/19/2020|Импорт Teams сообщения с microsoft Graph.|[Импорт сообщений из сторонних платформ в Teams с помощью Microsoft Graph](graph-api/import-messages/import-external-messages-to-teams.md)
| 08/12/2020 |Адаптивная поддержка карт в входящих webhook переехал в GA.|[Отправка адаптивных карточек с помощью входящего веб-перехватчика](~/webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook) |
|08/10/2020|Начать строить Teams приложения с Visual Studio набор средств.|[Создавайте приложения с помощью Microsoft Teams набор средств и Visual Studio Code](toolkit/visual-studio-overview.md) |
|08/06/2020|Поддержка проверки подлинности Tabs SSO.|[Разработка вкладки SSO Microsoft Teams](tabs/how-to/authentication/auth-aad-sso.md#develop-an-sso-microsoft-teams-tab) |
|07/27/2020 | Graph ботов и сообщений (Public Preview).|[Включить проактивную установку ботов и упреждающие обмен сообщениями в Teams с Microsoft Graph](graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages.md)|
| 07/22/2020 |Обновления возможностей мобильных устройств.|[Запрос разрешений на устройство для Microsoft Teams вкладки](concepts/device-capabilities/native-device-permissions.md) |
|07/20/2020|Teams Инструмент проверки приложений для отправки AppSource.|[Teams Инструмент проверки приложений](concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
|07/15/2020|Создайте виртуального помощника для Teams.|[Виртуальный помощник для Microsoft Teams](samples/virtual-assistant.md)|
|07/14/2020|Привокся в документацию по индикатору загрузки.|[Отображение родного индикатора загрузки](tabs/how-to/create-tab-pages/content-page.md#show-a-native-loading-indicator)
|07/01/2020|Начать строить Teams приложения с Visual Studio Code набор средств.|[Создавайте приложения с помощью Microsoft Teams набор средств и Visual Studio Code](toolkit/visual-studio-code-overview.md) |
|07/01/2020|Единый вкладок для вкладок GA для Teams веб- и настольных клиентов.|[Одноэтажный Sign-On (SSO)](tabs/how-to/authentication/auth-aad-sso.md)|
|06/05/2020| Схема манифеста обновлена до версии 1.7.| [Справка: Схема манифеста для Microsoft Teams](resources/schema/manifest-schema.md)|
|05/18/2020|Интегрируйте Power Virtual Agents с Teams.|[Интегрируйте Power Virtual Agents чат-бота с Microsoft Teams](bots/how-to/add-power-virtual-agents-bot-to-teams.md)|
|04/01/2020|Интеграция систем WFM с разъемом Shifts для Teams.|[Microsoft Teams Сдвиги разъемов WFM](samples/shifts-wfm-connectors.md)
| 03/24/2020 | Добавлена поддержка для извлечения одного участника беседы и дополнительная поддержка для извлечения участников страницы. | [Получите контекст Teams для вашего бота](~/bots/how-to/get-teams-context.md) |

<br>

</details>

<br>

<details>
  
<summary><b>2019</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
| 12/26/2019 | Параметр `replyToId` полезной нагрузки, отправленной боту, больше не зашифрован, что позволяет использовать это значение для построения глубоких ссылок на эти сообщения. Полезная нагрузка сообщения включает зашифрованные значения в `legacy.replyToId` параметре.  |
| 11/05/2019 | Единый знак на использование Teams JavaScript SDK. | [Единый вход](tabs/how-to/authentication/auth-aad-sso.md) |
| 10/31/2019 | Разговорные боты и документация расширения обмена сообщениями обновлены, чтобы отразить 4.6 Bot Framework SDK. Документация для v3 SDK доступна в разделе Ресурсы. | Вся документация по расширению бота и обмена сообщениями. |
| 10/31/2019 | Новая структура документации и рефакторинг основных статей. Пожалуйста, сообщите о любых мертвых ссылок или 404,5 GitHub выпуск. | Все из них! |
| 09/13/2019 | Бот запроса устанавливается из расширения обмена сообщениями на основе действий. | [Инициировать действия с расширением обмена сообщениями](resources/messaging-extension-v3/create-extensions.md#request-to-install-your-conversational-bot)
| 08/28/2019 | Поддержка частных каналов в вкладок и разъемах. | [Получение контекста для вкладки](tabs/how-to/access-teams-context.md#retrieving-context-in-private-channels) |
| 06/20/2019 | Поделитесь внешним веб-сайтом, с внешнего веб-сайта, в Teams канал. | [Поделиться с Teams](~/share-to-teams.md) |
| 05/25/2019 | Отвечайте сообщением бота из модуля задач. | [Ответить сообщением бота от модуля задач](resources/messaging-extension-v3/create-extensions.md#respond-with-an-adaptive-card-message-sent-from-a-bot) |
| 05/25/2019 | Боты в групповых чатах. | [Взаимодействие с ботом в групповом чате или канале](~/concepts/bots/bot-conversations/bots-conv-channel.md) |
| 05/20/2019 | Приложение проявляется локализации. | [Локализация приложений](~/publishing/apps-localization.md) |
| 05/20/2019 | Действия сообщения. | [Действия сообщений](resources/messaging-extension-v3/create-extensions.md#action-type-message-extensions) |
| 05/20/2019 | Ссылка разворачивается (пользовательские предварительные просмотры URL). | [Развертывание ссылки](messaging-extensions/how-to/link-unfurling.md)|
| 05/06/2019 | Программа сертификации приложений для магазинов приложений. | [Сертификация приложений](~/concepts/deploy-and-publish/appsource/post-publish/overview.md#complete-microsoft-365-certification) |
| 05/06/2019 | Шаблоны приложений теперь доступны. | [Шаблоны приложений](~/samples/app-templates.md) |
| 04/23/2019 | Расширения сообщений на основе действий теперь доступны. | [Расширение сообщений на основе действий](~/concepts/messaging-extensions/create-extensions.md) |
| 02/18/2019 | Создание глубоких ссылок на приватный чат не по доступно и доступно для разработчиков. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 01/23/2019 | Surfacing SKU и licenceType информации в контексте вкладки. | [Контекст вкладок](~/concepts/tabs/tabs-context.md) |

<br>

</details>

<br>

<details>

<summary><b>2018</b></summary>

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
| 11/12/2018 | Вкладки в групповом чате теперь доступны в выпущенной версии Teams, и был перемещен из предварительного просмотра разработчика. В рамках этой работы раздел вкладок был переработан для ясности.| [Настраиваемые вкладки](~/concepts/tabs/tabs-configurable.md) |
| 11/11/2018 | Начало работы для Узла JS и для .NET/C' было обновлено, чтобы использовать App Studio в Teams году, и был добавлен новый раздел о хостинге node на основе Teams приложений в Azure. | [Начать работу на платформе Microsoft Teams с C'/.NET и App Studio](~/get-started/get-started-dotnet-app-studio.md), [Начать работу на платформе Microsoft Teams с Узел JS и App Studio](~/get-started/get-started-nodejs-app-studio.md), Хост вашего узла Teams приложение в [Azure](~/get-started/get-started-nodejs-in-azure.md)|
| 11/09/2018 | Теперь вы можете создавать глубокие ссылки на частные чаты между пользователями. | [Глубокая ссылка на чат](concepts/build-and-test/deep-links.md#deep-linking-to-a-chat) |
| 11/08/2018 | SharePoint Framework 1.7 поставляется и с ним новая функция для использования Microsoft Teams в качестве SharePoint Framework веб-части. | [Вкладки в SharePoint](~/concepts/tabs/tabs-in-sharepoint.md) |
| 11/05/2018 | Функция **модуля задач** была выпущена. Модуль задач позволяет создавать модальные всплывающие окна в приложении Teams ботов и вкладок. Внутри всплывающего окна можно запустить свой собственный пользовательский html/JavaScript-код, показать виджет на `<iframe>` основе YouTube или Microsoft Stream или отобразить [адаптивную карту.](/adaptive-cards/) | [Модуль задачи Обзор](~/concepts/task-modules/task-modules-overview.md), [модуль задачи в вкладок](~/concepts/task-modules/task-modules-tabs.md),  [модуль задачи в ботах](~/concepts/task-modules/task-modules-bots.md) |
| 10/05/2018 | Информация о форматировании карт была обновлена и протестирована в настольных, iOS и Android клиентах для Teams. | [Карты](~/concepts/cards/cards.md), [Форматирование карт](~/concepts/cards/cards-format.md) |
| 09/24/2018 | API-версии звонков и онлайн-встреч для Microsoft Graph были выпущены в бета-версию, и Teams приложения теперь могут взаимодействовать с пользователями богатыми способами, используя голос и видео. | [Звонки и онлайн-встречи ботов](~/concepts/calls-and-meetings/registering-calling-bot.md), [в режиме реального времени концепции средств](~/concepts/calls-and-meetings/real-time-media-concepts.md)массовой информации , Регистрация [вызова бота](~/concepts/calls-and-meetings/registering-calling-bot.md), [отладка](~/concepts/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)и локальное тестирование , [Приложение-хостинг средств](~/concepts/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)массовой информации , Обработка [входящих уведомлений вызова](~/concepts/calls-and-meetings/call-notifications.md) |
| 09/11/2018 | Страницы конфигурации вкладок теперь значительно выше. | [Дизайн вкладок](tabs/design/tabs.md) |
| 08/15/2018 | Адаптивные карты теперь поддерживаются в Teams.|[Адаптивные действия карты в Teams](task-modules-and-cards/cards/cards-reference.md#adaptive-card) |
| 08/10/2018 | Поддержка клиентов DevTools.| [DevTools для Microsoft Teams рабочего стола](~/resources/dev-preview/developer-preview-tools.md)|
| 08/08/2018 | Расширения сообщений теперь поддерживают несколько команд. Эта функция была в предварительном просмотре разработчика, и теперь выпущена для всех пользователей.| [composeExtensions.commands](~/resources/schema/manifest-schema.md#composeextensionscommands)|
| 08/07/2018 | Конфигурация inline теперь поддерживается в Connectors. Документация коннекторов также была пересмотрена и расширена для ясности.| [Соединители](~/concepts/connectors/connectors.md)|
| 08/06/2018 | Теперь ваш бот может отправлять и получать файлы.| [Отправка и получение файлов через бота](~/bots/how-to/bots-filesv4.md)|
| 07/23/2018 | Информация о повторной сертификации приложений добавлена в раздел Издательский. |[Явные разрешения](resources/schema/manifest-schema.md#permissions)|
| 07/16/2018 | Больше места было выделено на страницу конфигурации вкладки. | [Страница конфигурации вкладок значительно выше](tabs/design/tabs.md)|
| 07/12/2018 | Информация о доступе гостей. | [Гостевой доступ в Microsoft Teams](/microsoftteams/guest-access#guest-access-overview)|
| 06/07/2018 | Добавлена информация Microsoft Teams каталога приложений для арендаторов. | [Опубликовать свое Microsoft Teams приложение](~/publishing/apps-publish.md)|
| 05/29/2018 | Адаптивные карты поддерживаются в Teams. | [Адаптивные действия карты в Teams](task-modules-and-cards/cards/cards-reference.md) |
| 04/17/2018 | replyToID был добавлен к полезной нагрузке для `Invoke` действий `MessageBack` и карт. Это особенно полезно, если вам нужно обновить сообщение о том, что действие карты пришли. | [Действия карты](~/concepts/cards/cards-actions.md)|
| 04/12/2018 | Добавлена эта тема для отслеживания изменений в Teams программирования и этого набора документации. | [Новые возможности](~/whats-new.md)|
| 04/10/2018 | Изменены URL-адреса аутентификации для последовательного использования идентификатора клиента на пути. | [Поток аутентификации для вкладок](~/concepts/authentication/auth-flow-tab.md), [AAD Tab аутентификации](~/concepts/authentication/auth-tab-AAD.md)|
| 04/06/2018 | Добавлены руководящие принципы проектирования для использования командного ящика. |[Командная коробка](~/resources/design/framework/command-box.md)|
| 04/02/2018 | Использование ботов для отправки уведомлений для вашего приложения. |[Боты только для уведомлений](~/concepts/bots/bots-notification-only.md)|
| 03/27/2018 | Расширенная документация для упреждающих сообщений. |[Начиная разговор](./concepts/bots/bot-conversations/bots-conv-proactive.md)|
| 03/15/2018 | Рефакторинг документации для карт. |[Карты](~/concepts/cards/cards.md), [Действия по картам](~/concepts/cards/cards-actions.md), [Форматирование карты](~/concepts/cards/cards-format.md), Ссылка на [карту](~/concepts/cards/cards-reference.md)|
| 03/03/2018 | Добавлена документация для Teams App Studio. |[Быстро разработать приложения с Teams App Studio](~/get-started/get-started-app-studio.md), [Используя библиотеку управления в App Studio](~/get-started/app-studio-component-library.md)|
| 02/27/2018 | Добавлен образец кода для демонстрации метода AsTeamsChannelAccounts(). |[Получите контекст для бота](~/concepts/bots/bots-context.md)|
| 02/05/2018 | Добавлены темы для начала использования C. |[Начало работы на платформе Microsoft Teams с использованием C#/.NET](./get-started/get-started-dotnet-app-studio.md)|

<br>

</details>

## <a name="developer-preview"></a>Developer preview

Предварительный просмотр разработчика — это общедоступная программа, которая обеспечивает ранний доступ к неизданным Teams функции платформы.  

| **Date** | **Примечания** | **Измененные темы** |
| -------- | --------- | ------------------ |
|03/05/2021| Вкладки больше не будут иметь поля, окружающие их опыт. Разработчики вкладок должны просмотреть и обновить свои приложения. | [Удаление поля вкладок](resources/removing-tab-margins.md) |

Для получения дополнительной информации, [смотрите предварительный просмотр публичного разработчика для Teams](~/resources/dev-preview/developer-preview-intro.md).

## <a name="teams-app-template-catalog"></a>Teams каталог шаблонов приложений

Наряду с новыми функциями, мы [также предоставляем готовые к производству Teams шаблоны](samples/app-templates.md) приложений, которые можно развернуть сразу или изменить с собой. Недавно добавленные шаблоны обозначены звездой.

## <a name="submit-your-feedback"></a>Отправить отзыв

Мы рекомендуем Teams задавать вопросы, подавать ошибки, отправлять запросы на функции и делать взносы. Вы можете отправить обратную связь через любой из [доступных каналов.](feedback.md)
