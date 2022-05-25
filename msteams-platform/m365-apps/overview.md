---
title: Расширение возможностей приложений Teams в Microsoft 365 (предварительная версия)
description: Расширьте возможности приложений Teams на другие часто используемые области Microsoft 365.
ms.date: 05/24/2022
ms.topic: overview
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 9cc0d88d5f992aa596509a6206a26baa413bdcf1
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/25/2022
ms.locfileid: "65668146"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Расширение приложений Teams в Microsoft 365

В последних выпусках клиентского [пакета SDK Microsoft Teams JavaScript](../tabs/how-to/using-teams-client-sdk.md) (версия 2.0.0), [манифеста приложения Teams](../resources/schema/manifest-schema.md) (версия 1.13) и [набора средств Teams](../toolkit/visual-studio-code-overview.md) можно создавать и обновлять приложения Teams для запуска в других продуктах с высоким уровнем использования Microsoft 365 и публиковать их на коммерческой платформе Майкрософт ([ Microsoft AppSource](https://appsource.microsoft.com/)).

Расширение приложения Teams в Microsoft 365 обеспечивает упрощенный способ предоставления кроссплатформенных приложений для расширенной аудитории пользователей: из одной базы кода можно создавать интерфейсы приложений, адаптированные для сред Teams, Outlook и Office. Конечным пользователям не придется выходить из контекста своей работы, чтобы использовать ваше приложение, а администраторы получают преимущества от консолидированного рабочего процесса управления и развертывания.

Платформа Teams продолжает развиваться и расширяться целостно в Microsoft 365 экосистеме. Ниже приведена текущая поддержка элементов платформы Teams в Microsoft 365 (Teams, Outlook и Office в качестве узлов приложений):

|          | Элемент манифеста приложения | Teams поддержки |Outlook* | Office* | Примечания |
|--|--|--|--|--|--|
| [**Вкладки**](../tabs/what-are-tabs.md) (личная область)    |`staticTabs`  | Web, Desktop, Mobile | Веб (целевой выпуск), рабочий стол (бета-канал) | Интернет (целевой выпуск)| Область канала и группы пока не поддерживается для Microsoft 365. См. [примечания](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Расширения сообщений**](../messaging-extensions/what-are-messaging-extensions.md) (на основе поиска)| `composeExtensions` | Web, Desktop, Mobile| Веб (целевой выпуск), рабочий стол (бета-канал)| |На основе действий пока не поддерживается Microsoft 365. См. [примечания](extend-m365-teams-message-extension.md#preview-your-message-extension-in-outlook). |
| [**Graph соединителей**](/microsoftsearch/connectors-overview)| `graphConnector` | Web, Desktop, Mobile| Интернет, рабочий стол | Веб| Просмотр [заметок](#graph-connectors)
| [**Office надстроек**](/office/dev/add-ins/develop/json-manifest-overview) (предварительная версия) | `extensions` | | Интернет, рабочий стол  | | Доступно только в [версии манифеста devPreview](../resources/schema/manifest-schema-dev-preview.md) . См. [примечания](#office-add-ins-preview).|

\*Для [Microsoft 365 выпусков](/microsoft-365/admin/manage/release-options-in-office-365) и Приложения Microsoft 365 канала обновления требуется согласие [](/deployoffice/change-update-channels) администратора для всей организации или выбранных пользователей.

Рекомендации по манифесту Teams и управлению версиями пакета SDK, а также дополнительные сведения о текущей поддержке возможностей платформы Teams в Microsoft 365 см. в обзоре клиентского пакета [SDK Teams JavaScript](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Мы будем рады вашим отзывам и отчетам о проблемах при расширении Teams приложений для работы в Microsoft 365 экосистеме! Используйте обычные каналы [сообщества Microsoft Teams разработчиков для](/microsoftteams/platform/feedback) отправки отзывов.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Личные вкладки и расширения для обмена сообщениями в Outlook и Office

Свяжитесь с пользователями прямо в контексте их работы, расширив веб-приложение в качестве Teams личных вкладок, которое также работает как в Outlook, так и Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="Персональная вкладка, запущенная в Outlook, Office и Teams":::

Вы также можете расширить расширения сообщений Teams на основе поиска до Outlook в Интернете и Windows desktop, позволяя клиентам выполнять поиск и делиться результатами через область создания сообщений Outlook, а также Microsoft Teams клиентов.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="Расширение сообщений, работающее в Outlook и Teams":::

Создание приложения с использованием последней [Teams](../resources/schema/manifest-schema.md) и клиентского [пакета SDK Teams JavaScript](../tabs/how-to/using-teams-client-sdk.md) обеспечивает консолидированную разработку. Благодаря возможности оптимизировать развертывание, установку и администрирование для клиентов, вы можете расширить потенциальный охват и использование приложения.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Использование Teams приложения в Microsoft 365

Чтобы упростить и оптимизировать экосистему Microsoft 365 разработчиков, мы продолжаем расширять манифест приложения Teams в другие области Microsoft 365 следующим образом.

### <a name="graph-connectors"></a>Graph соединителей

С помощью соединителей Microsoft Graph ваша организация может индексировать сторонние данные, чтобы они отображались как Поиск (Майкрософт) результаты, расширяя типы источников контента, доступных для поиска, в приложениях Teams.
Дополнительные сведения см. в [Graph microsoft Поиск (Майкрософт)](/microsoftsearch/connectors-overview).

Чтобы приступить к работе с соединителями графов в приложениях Teams, ознакомьтесь с примером соединителей Teams [Toolkit Graph](https://aka.ms/teamsfx-graph-connector-sample) и справочником по схеме манифеста Microsoft Teams developer preview.[](../resources/schema/manifest-schema-dev-preview.md)

### <a name="office-add-ins-preview"></a>Office надстроек (предварительная версия)

Теперь вы можете определять и развертывать Office в предварительной версии манифеста Microsoft Teams [](../resources/schema/manifest-schema-dev-preview.md) разработчика. В настоящее время эта предварительная версия ограничена Outlook надстроек, работающих в подписке Office для Windows.

Дополнительные сведения см[. в Teams манифеста Office надстроек (предварительная версия)](/office/dev/add-ins/develop/json-manifest-overview).

## <a name="microsoft-appsource-submission"></a>Отправка Microsoft AppSource

Присоединяйтесь к постоянному числу рабочих приложений Teams в [Microsoft AppSource](https://appsource.microsoft.com/) Store с расширенной поддержкой Outlook и Office (целевой выпуск). Процесс отправки приложений Teams, включенных для [Outlook и Office](../concepts/deploy-and-publish/appsource/publish.md), совпадает с процессом отправки приложений Teams. Единственным отличием является использование манифеста приложения Teams версии [1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, что обеспечивает поддержку приложений Teams, которые выполняются в Microsoft 365.

После публикации в Microsoft 365 приложения с Teams приложение будет обнаруживаемым как устанавливаемое приложение из хранилищ Outlook и Приложение Office, а также Teams store. При запуске в Outlook и Office приложение использует те же разрешения, что и Teams. Teams администраторы могут управлять [доступом к Teams приложениям](/MicrosoftTeams/manage-third-party-teams-apps) в Microsoft 365 для пользователей в своей организации.

Дополнительные сведения см. в [статье Teams для Microsoft 365](publish.md).

## <a name="next-step"></a>Следующий этап

Настройка среды разработки для создания Teams приложений для Microsoft 365:

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)
