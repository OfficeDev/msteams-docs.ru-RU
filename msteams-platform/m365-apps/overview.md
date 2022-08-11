---
title: Расширение возможностей приложений Teams в Microsoft 365 (предварительная версия)
description: Из этой статьи вы узнаете, как создавать, обновлять и расширять возможности приложений Teams, а также как создавать приложения, используемые в других областях с высоким уровнем использования в Microsoft 365.
ms.date: 05/24/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 208843d9d4c46d29b095ffaf7260f28889f8ed45
ms.sourcegitcommit: 209b9942c02b5affdd995348902114d3b9805c61
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/09/2022
ms.locfileid: "67288215"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Расширение приложений Teams в Microsoft 365

С помощью последних выпусков клиентского [пакета SDK JavaScript для Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) (версия 2.0.0), манифеста приложения [Teams](../resources/schema/manifest-schema.md) (версия 1.13) и [набора средств Teams](../toolkit/visual-studio-code-overview.md) можно создавать и обновлять приложения Teams для запуска в других высокопроизводительные продукты Microsoft 365 и публиковать их на коммерческой платформе Майкрософт ([коммерческая платформа Майкрософт](https://appsource.microsoft.com/)).

Расширение приложения Teams в Microsoft 365 обеспечивает упрощенный способ предоставления кроссплатформенных приложений для расширенной аудитории пользователей: с помощью одной базы кода можно создавать интерфейсы приложений, адаптированные для сред Teams, Outlook и Office. Конечным пользователям не придется выходить из контекста своей работы, чтобы использовать ваше приложение, а администраторы получают преимущества от консолидированного рабочего процесса управления и развертывания.

Платформа приложений Teams продолжает развиваться и расширяться целостно в экосистеме Microsoft 365. Ниже приведена текущая поддержка элементов платформы приложений Teams в Microsoft 365 (Teams, Outlook и Office в качестве узлов приложений):

|          | Элемент манифеста приложения | Поддержка Teams |Поддержка Outlook* | Поддержка Office* | Примечания |
|--|--|--|--|--|--|
| [**Вкладки**](../tabs/what-are-tabs.md) (личная область)    |`staticTabs`  | Web, Desktop, Mobile | Веб (целевой выпуск), рабочий стол (бета-канал) | Интернет (целевой выпуск)| Область канала и группы пока не поддерживается для Microsoft 365. См. [примечания](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Расширения сообщений**](../messaging-extensions/what-are-messaging-extensions.md) (на основе поиска)| `composeExtensions` | Web, Desktop, Mobile| Веб (целевой выпуск), рабочий стол (бета-канал)| - |На основе действий для Microsoft 365 пока не поддерживается. См. [примечания](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook). |
| [**Соединители графов**](/graph/connecting-external-content-connectors-overview)| `graphConnector` | Web, Desktop, Mobile| Интернет, рабочий стол | Веб| Просмотр [заметок](#graph-connectors)
| [**Надстройки Office**](/office/dev/add-ins/develop/json-manifest-overview) (предварительная версия) | `extensions` | - | Интернет, рабочий стол | - | Доступно только в [версии манифеста devPreview](../resources/schema/manifest-schema-dev-preview.md) . См. [примечания](#office-add-ins-preview).|

\*Для [параметра целевого выпуска Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) [Приложения Microsoft 365](/deployoffice/change-update-channels) регистрации канала обновления требуется согласие администратора для всей организации или выбранных пользователей. Каналы обновления относятся к конкретному устройству и применяются только к установкам Office, работающим в Windows.

Рекомендации по манифесту приложения Teams и управлению версиями пакета SDK, а также дополнительные сведения о текущей поддержке возможностей платформы Teams в Microsoft 365 см. в обзоре клиентского [пакета SDK для JavaScript для Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Мы будем рады вашим отзывам и отчетам о проблемах при расширении приложений Teams для работы в экосистеме Microsoft 365! Используйте обычные каналы [сообщества разработчиков Microsoft Teams](/microsoftteams/platform/feedback) для отправки отзывов.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Личные вкладки и расширения для обмена сообщениями в Outlook и Office

Свяжитесь с пользователями прямо в контексте их работы, расширив веб-приложение как приложение личной вкладки Teams, которое также работает как в Outlook, так и в Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Снимок экрана— пример, на котором показана вкладка &quot;Личные&quot;, работающее в Outlook, Office и Teams.":::

Вы также можете расширить расширения сообщений Teams на основе поиска на Outlook в Интернете и классическом компьютере Windows, позволяя клиентам выполнять поиск и делиться результатами через область создания сообщений Outlook, а также клиенты Microsoft Teams.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="На снимке экрана показан пример расширения сообщений, запущенного в Outlook и Teams.":::

Создание приложения с использованием последней версии манифеста [приложения Teams](../resources/schema/manifest-schema.md) и клиентского [пакета SDK JavaScript для Teams](../tabs/how-to/using-teams-client-sdk.md) обеспечивает консолидированную разработку. Благодаря возможности оптимизировать развертывание, установку и администрирование для клиентов, вы можете расширить потенциальный охват и использование приложения.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Использование манифеста приложения Teams в Microsoft 365

Чтобы упростить и оптимизировать экосистему разработчиков Microsoft 365, мы продолжаем расширять манифест приложения Teams в других областях Microsoft 365 следующим образом.

### <a name="graph-connectors"></a>Соединители графов

С помощью соединителей Microsoft Graph ваша организация может индексировать сторонние данные, чтобы они отображались в виде результатов поиска (Майкрософт), расширяя типы источников контента, доступных для поиска, в приложениях Teams.
Дополнительные сведения см. в [обзоре соединителей Microsoft Graph для Поиска (Майкрософт).](/microsoftsearch/connectors-overview)

Чтобы приступить к работе с соединителями графов в приложениях Teams, ознакомьтесь с примером соединителей [Teams Toolkit Graph](https://aka.ms/teamsfx-graph-connector-sample) и справочником по схеме манифеста предварительной версии [microsoft Teams Developer](../resources/schema/manifest-schema-dev-preview.md) .

### <a name="office-add-ins-preview"></a>Надстройки Office (предварительная версия)

Теперь вы можете определять и развертывать надстройки Office в [](../resources/schema/manifest-schema-dev-preview.md) предварительной версии манифеста приложения Microsoft Teams для разработчиков. В настоящее время эта предварительная версия доступна только для надстроек Outlook, работающих в подписке Office для Windows.

Дополнительные сведения см. в [Манифест Teams для надстроек Office (предварительная версия)](/office/dev/add-ins/develop/json-manifest-overview).

## <a name="microsoft-appsource-submission"></a>Отправка Microsoft AppSource

Присоединяйтесь к постоянному числу рабочих приложений Teams в [Microsoft AppSource](https://appsource.microsoft.com/) Store, расширяя поддержку аудиторий Outlook и Office (targeted Release). Процесс [отправки приложений Teams](../concepts/deploy-and-publish/appsource/publish.md) , включенных для Outlook и Office, такой же, как и для традиционных приложений Teams. Единственным отличием является использование манифеста приложения Teams версии [1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, в котором реализована поддержка приложений Teams, которые работают в Microsoft 365.

После публикации в виде приложения Teams с поддержкой Microsoft 365 ваше приложение будет обнаруживаться как устанавливаемое приложение из магазинов приложений Outlook и Office, а также в магазине Teams. При запуске в Outlook и Office ваше приложение использует те же разрешения, что и в Teams. Администраторы Teams могут [управлять доступом к приложениям Teams в Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) для пользователей в своей организации.

Дополнительные сведения см [. в статье "Публикация приложений Teams для Microsoft 365"](publish.md).

## <a name="next-step"></a>Следующий этап

Настройка среды разработки для создания приложений Teams для Microsoft 365:

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)
