---
title: Расширение возможностей приложений Teams в Microsoft 365 (предварительная версия)
description: Узнайте, как расширить приложения Teams в Microsoft 365 (в Teams, Outlook и Office в качестве узлов приложений).
ms.date: 10/10/2022
ms.topic: Conceptual
ms.custom: m365apps
ms.localizationpriority: medium
ms.openlocfilehash: 91586eefe21836118ed2f0a0071070ac2034bf76
ms.sourcegitcommit: 10debe0f01574a21aab54bfac692a4c8373263a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68789879"
---
# <a name="extend-teams-apps-across-microsoft-365"></a>Расширение приложений Teams в Microsoft 365

С помощью последних выпусков [клиентского пакета SDK javaScript для Microsoft Teams](../tabs/how-to/using-teams-client-sdk.md) (версии 2.0.0 и более поздних), [манифеста приложения Teams](../resources/schema/manifest-schema.md) (версии 1.13 и более поздних) и [набора средств Teams](../toolkit/visual-studio-code-overview.md) можно создавать и обновлять приложения Teams для запуска в других продуктах Microsoft 365 с высоким уровнем использования и публиковать их на коммерческой платформе Майкрософт ([Microsoft AppSource](https://appsource.microsoft.com/)) или в частном магазине приложений вашей организации.

Расширение приложения Teams в Microsoft 365 обеспечивает упрощенный способ доставки кроссплатформенных приложений для расширенной аудитории пользователей: из одной базы кода вы можете создавать приложения, адаптированные для Teams, Outlook и сред Office. Конечным пользователям не придется выходить из контекста своей работы, чтобы использовать ваше приложение, а администраторы получают преимущества от объединенного рабочего процесса управления и развертывания.

Платформа приложений Teams продолжает развиваться и целостно расширяться в экосистеме Microsoft 365. Ниже приведена текущая поддержка элементов платформы приложений Teams в Microsoft 365 (Teams, Outlook и Office в качестве узлов приложений):

| Функции приложений Teams| Элемент манифеста приложения | Поддержка Teams |Поддержка Outlook* | Поддержка Office* | Примечания |
|--|--|--|--|--|--|
| [**Личная область вкладок**](../tabs/what-are-tabs.md)    |`staticTabs`  | Интернет, настольные компьютеры, мобильные устройства | Интернет (целевой выпуск), настольный компьютер (бета-канал) | Web (Targeted Release), Desktop (Beta Channel), Mobile (Android)| Область канала и группы пока не поддерживается для Microsoft 365. См [. заметки](../tabs/how-to/using-teams-client-sdk.md#microsoft-365-support-running-teams-apps-in-office-and-outlook).
| [**Расширения сообщений, основанные**](../messaging-extensions/what-are-messaging-extensions.md) на поиске| `composeExtensions` | Интернет, настольные компьютеры, мобильные устройства| Интернет (целевой выпуск), настольный компьютер (бета-канал)| - |На основе действий пока не поддерживается для Microsoft 365. См [. заметки](extend-m365-teams-message-extension.md#troubleshooting). |
| Развертывание ссылки | `composeExtensions.messageHandlers` | Интернет, настольный компьютер | Интернет (целевой выпуск), настольный компьютер (бета-канал) | - | См. [заметки](extend-m365-teams-message-extension.md#link-unfurling) |
| [**Надстройки Office**](/office/dev/add-ins/develop/json-manifest-overview) (предварительная версия) | `extensions` | - | Интернет, настольный компьютер | - | Доступно только в версии [манифеста devPreview](../resources/schema/manifest-schema-dev-preview.md) . См [. заметки](#office-add-ins-preview).|

\*Для параметра [целевого выпуска Microsoft 365](/microsoft-365/admin/manage/release-options-in-office-365) и [Приложения Microsoft 365 регистрации канала обновления](/deployoffice/change-update-channels) требуется согласие администратора для всей организации или выбранных пользователей. Каналы обновления зависят от устройства и применяются только к установкам Office, работающим в Windows.

Рекомендации по манифесту приложения Teams и руководству по использованию версий ПАКЕТА SDK, а также дополнительные сведения о текущей поддержке возможностей платформы Teams в Microsoft 365 см. в [обзоре клиентского пакета SDK для JavaScript для Teams](../tabs/how-to/using-teams-client-sdk.md).

> [!NOTE]
> Мы приветствуем ваши отзывы и отчеты о проблемах, когда вы расширяете приложения Teams для работы в экосистеме Microsoft 365! Используйте регулярные [каналы сообщества разработчиков Microsoft Teams](/microsoftteams/platform/feedback) для отправки отзывов.

## <a name="personal-tabs-and-messaging-extensions-in-outlook-and-office"></a>Личные вкладки и расширения для обмена сообщениями в Outlook и Office

Обратитесь к пользователям, где они находятся, прямо в контексте их работы, расширив веб-приложение как [личное приложение Teams](extend-m365-teams-personal-tab.md) , которое также работает как в Outlook, так и в Office.

:::image type="content" source="images/outlook-office-teams-personal-tab.png" alt-text="На снимке экрана показан пример личной вкладки, работающей в Outlook, Office и Teams.":::

На мобильных устройствах можно протестировать и отладить личную вкладку Teams, запущенную в [приложении Office для Android](extend-m365-teams-personal-tab.md#office-app-for-android).

:::image type="content" source="images/office-mobile-personal-tab.png" alt-text="На снимке экрана показан пример личной вкладки, работающей в Office.":::

Вы также можете расширить [расширения сообщений Teams](extend-m365-teams-message-extension.md) на основе поиска для Outlook в Интернете и классических приложений Windows, позволяя клиентам искать результаты и делиться ими через область создания сообщений Outlook, а также клиенты Microsoft Teams.

:::image type="content" source="images/outlook-teams-messaging-ext.png" alt-text="На снимке экрана показан пример расширения сообщений, запущенного в Outlook и Teams.":::

[Распаковка ссылок](extend-m365-teams-message-extension.md#link-unfurling)  работает в Outlook Web и средах Windows так же, как в Microsoft Teams без каких-либо дополнительных работ, чем использование манифеста приложения Teams версии 1.13 или более поздней.

:::image type="content" source="images/outlook-teams-link-unfurling.png" alt-text="На снимке экрана показан пример распаковки ссылок в Outlook и Teams.":::

Создайте приложение с помощью последнего [манифеста приложения Teams](../resources/schema/manifest-schema.md) и [клиентского пакета SDK для JavaScript для Teams](../tabs/how-to/using-teams-client-sdk.md) , чтобы воспользоваться последним консолидированным процессом разработки приложений Microsoft 365. Затем упростите развертывание, установку и администрирование для ваших клиентов, расширяя возможности и возможности использования приложения.

## <a name="use-teams-app-manifest-across-microsoft-365"></a>Использование манифеста приложения Teams в Microsoft 365

С целью упрощения и оптимизации экосистемы разработчиков Microsoft 365 мы продолжаем расширять манифест приложения Teams в других областях Microsoft 365, используя следующее.

### <a name="office-add-ins-preview"></a>Надстройки Office (предварительная версия)

Теперь вы можете определять и развертывать надстройки Office в [предварительной версии](../resources/schema/manifest-schema-dev-preview.md) манифеста приложения Microsoft Teams для разработчиков. В настоящее время эта предварительная версия ограничена надстройками Outlook, работающими по подписке Office для Windows.

Дополнительные сведения см. в [Манифест Teams для надстроек Office (предварительная версия)](/office/dev/add-ins/develop/json-manifest-overview).

## <a name="microsoft-commercial-marketplace-submission"></a>Отправка коммерческой платформы Майкрософт

Присоединяйтесь к растущему числу рабочих приложений Teams в магазине [Microsoft Commercial Marketplace](https://appsource.microsoft.com/) (Microsoft AppSource) с расширенной поддержкой outlook и аудиторий предварительной версии Office (целевой выпуск). [Процесс отправки приложений для приложений Teams, включенных в Outlook и Office](../concepts/deploy-and-publish/appsource/publish.md), совпадает с процессом отправки приложений Для традиционных приложений Teams. Единственное отличие заключается в том, что вы будете использовать манифест приложения Teams [версии 1.13](../tabs/how-to/using-teams-client-sdk.md) в пакете приложения, который предоставляет поддержку приложений Teams, работающих в Microsoft 365.

После публикации приложения в качестве приложения Teams с поддержкой Microsoft 365 его можно будет обнаружить как устанавливаемое приложение в магазинах приложений Outlook и Office, а также в магазине Teams. При запуске в Outlook и Office ваше приложение использует те же разрешения, что и в Teams. Администраторы Teams могут [управлять доступом к приложениям Teams в Microsoft 365](/MicrosoftTeams/manage-third-party-teams-apps) для пользователей в своей организации.

Дополнительные сведения см. в статье [Публикация приложений Teams для Microsoft 365](publish.md).

## <a name="next-step"></a>Следующий этап

Настройте среду разработки для создания приложений Teams для Microsoft 365:

> [!div class="nextstepaction"]
> [Необходимые условия для установки](prerequisites.md)
