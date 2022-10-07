---
title: Подключаемые модули Microsoft 365
description: В этой статье вы узнаете о подключаемых модулях Microsoft 365, о списке подключаемых модулей и метках, о Microsoft 365, взаимодействии с One Note и многом другом.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: Surbhigupta
ms.openlocfilehash: 56ba41598fb7d9e75aff92f240f7a3132988c1ec
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499309"
---
# <a name="microsoft-365-plugins"></a>Подключаемые модули Microsoft 365

Подключаемые модули Microsoft 365 обеспечивают интеграцию между веб-сайтом Moodle и Teams. Эти подключаемые модули упрощают для пользователей планирование, доставку и совместное использование контента курса. Подключаемые модули можно использовать независимо или в рамках партнерства в зависимости от требования.

## <a name="plugin-list-and-labels"></a>Список подключаемых модулей и метки

В следующей таблице перечислены подключаемые модули и метки GitHub, используемые с учетом требований.

<!--Old content of the table updated and revamped |Plugins to install |Description |GitHub label(s)|
|-----|-----|----|
|[**OpenID Connect**](#openid-connect)|Enable SSO for users who work using both Moodle and Microsoft Teams|auth_oidc|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) |Create Teams instances for each course in Moodle, and sync faculty as owners, and students as team members|• auth_oidc </br> • local_o365|
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Teams Theme**](#microsoft-365-teams-theme)| Remove Moodle blocks and extra chrome within the Moodle iframes for Teams, which applies while mapping courses to Teams instances | • auth_oidc </br> • local_o365 </br> • themeboost_o365teams |
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) </br> • [**Microsoft 365 Repository**](#microsoft-365-repository) |Leverage Microsoft 365 OneDrive content for file repositories to reduce storage needs in Moodle | • auth_oidc </br> * local_o365 </br> • repository_office 365|
|• [**OpenID Connect**](#openid-connect) </br> • [**OneNote**](#onenote-integration) </br> • [**OneNote Submissions**](#onenote-integration) </br> • [**OneNote Feedback**](#onenote-integration) | Enable OneNote to be used for assignment, submission and feedback |• auth_oidc </br> • local_onenote </br> • assignsubmission_onenote </br> • assignfeedback_onenote |  
|• [**OpenID Connect**](#openid-connect) </br> • [**Microsoft 365 integration**](#microsoft-365-integration) • [**Microsoft 365 Repository**](#microsoft-365-repository) </br> • [**Microsoft Block**](#microsoft-365-repository) | Enable 365 quick access blocks within Moodle with links to Microsoft 365 collaboration services and install links for Microsoft Office | • auth_oidc </br> • local_o365 </br> • repository_office365 </br> • block_microsoft |
|[**Teams Meeting**](#teams-meetings) | Enable Atto editor in Moodle to create Teams meeting links |atto_teamsmeeting |
|[**oEmbed Filter**](#oembed-filter) | Enable video links in Moodle | Filter_oembed| -->

|Устанавливаемые подключаемые модули |Описание |Метки GitHub|
|-----|-----|----|
|[**Подключение OpenID**](#openid-connect)|Включает единый вход для пользователей, которые работают одновременно в Moodle и Teams.|auth_oidc|
|[**Интеграция с Microsoft 365**](#microsoft-365-integration)|Создание экземпляров Teams для каждого курса в Moodle и синхронизация преподавателей в качестве владельцев, а учащихся — в качестве участников команд.|local_o365|
|[**Репозиторий Microsoft 365**](#microsoft-365-repository) |Поддерживает контент OneDrive в Microsoft 365 для репозиториев файлов, чтобы снизить требования хранилища в Moodle.| repository_office 365|
|[**Собрание Teams**](#teams-meetings) |Позволяет редактору Atto в Moodle создавать ссылки на собрания Teams.|atto_teamsmeeting |
|[**Тема Teams**](#microsoft-365-teams-theme)| Удалите блоки Moodle и дополнительный хром в iFrames Moodle для Teams, который применяется при сопоставлении курсов с экземплярами Teams.| themeboost_o365teams |
|[**OneNote**](#onenote-integration)| Включение OneNote для заданий, отправки и обратной связи.|local_onenote, assignsubmission_onenote и assignfeedback_onenote </br>|  
|[**Блок Microsoft**](#microsoft-block) | Позволяет Microsoft 365 быстро получать доступ к блокам в Moodle со ссылками на службы совместной работы Microsoft 365 и ссылками на установку Microsoft Office.|block_microsoft |
|[**Фильтр oEmbedr**](#oembed-filter) | Включение ссылок на видео в Moodle.|Filter_oembed|

Moodle LMS поддерживает следующие подключаемые модули.

## <a name="openid-connect"></a>OpenID Connect

Подключаемый модуль OpenID Connect позволяет пользователям проходить проверку подлинности на любом веб-сайте или в инструменте, который поддерживает необходимую спецификацию и единый вход с Microsoft Office 365. Подключаемый модуль OpenID Connect предоставляет учреждениям следующие варианты входа для удовлетворения их определенных требований.

* Пользователи могут ввести свои учетные данные Office 365, например адрес электронной почты и пароль, для прямого входа или войти с использованием полей имени пользователя и пароля Moodle, не входя в Office 365.
* Пользователи могут выбрать ссылку для входа через Office 365 или поставщика OpenID Connect на странице Moodle.

На следующем изображении показана страница входа OpenID Connect.

:::image type="content" source="../../assets/images/MoodleInstructions/openid-connect.png" alt-text="Вход в OpenID Connect":::

## <a name="microsoft-365-integration"></a>Интеграция с Microsoft 365

Интеграция с Microsoft 365 состоит из нескольких приложений с несколькими функциональными возможностями, что позволяет пользователям оставаться на связи и выполнять различные действия по мере необходимости. Подключаемый модуль позволяет администраторам проверить следующее.

* Проверка соответствующих функций интеграции.
* Синхронизация пользователей между Office 365 и Moodle.
* Настройка необходимых разрешений для пользователей.
* Настройка веб-сайта SharePoint для файлов курсов.

На следующем изображении показана страница настройки интеграции с Microsoft 365.

:::image type="content" source="../../assets/images/MoodleInstructions/365-integration.png" alt-text="Интеграция с Microsoft 365":::

### <a name="user-functions"></a>Функции пользователя

Благодаря интеграции с Microsoft 365 пользователи могут выполнять следующие действия.

* Проверка общего функционирования всех интеграций с подключаемыми модулями Microsoft 365.
* Отправка CSV-файла, который сопоставляет Moodle с пользователями Office 365.
* Проверка конфигурации разрешений Azure AD.

## <a name="microsoft-365-repository"></a>Репозиторий Microsoft 365

Подключаемый модуль репозитория Microsoft 365 позволяет пользователям хранить файлы курсов в OneDrive. Преподаватели могут добавлять файлы из раздела OneDrive с файлами курсов или из личного пространства в репозиторий.

Пользователь может применять репозиторий Microsoft 365 в качестве репозитория файлов для учреждения, сохраняя простую структуру данных Moodle. Подключаемый модуль репозитория Microsoft 365 предоставляет следующие возможности.

* Преподаватели могут хранить файлы курсов в OneDrive. Каждый курс содержит собственную папку, созданную в OneDrive, что позволяет преподавателям добавлять файлы из области OneDrive с файлами курсов или из личного пространства.  
* Добавление файлов в Moodle в виде копии или создание ссылки на файл. Связанный файл отображается в новом окне приложения или внедряется в веб-страницу.
* Отправка файлов в OneDrive или SharePoint с помощью средства выбора файлов Moodle.

На следующем изображении показан репозиторий файлов Microsoft 365.

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-365- repository.png" alt-text="Репозиторий M365" :::

## <a name="teams-meetings"></a>Собрания Teams

Подключаемый модуль собраний Teams позволяет пользователю создавать приглашения на собрания в календаре, заданиях, публикациях на форуме, а также в редакторе Atto при доступности.

После установки подключаемого модуля преподаватели и учащиеся могут создавать голосовые или видеособрания с помощью Moodle, для чего требуется учетная запись Microsoft 365 и разрешения Moodle.

>[!NOTE]
>Собрания Teams не отображаются в календаре Outlook или Teams, однако имена отдельных учащихся можно добавить в приглашение.

На следующем изображении показана страница входа в собрание Teams.

:::image type="content" source="../../assets/images/MoodleInstructions/teams-meeting.png" alt-text="Вход в собрание Teams":::

## <a name="microsoft-365-teams-theme"></a>Тема Teams в Microsoft 365

Подключаемый модуль темы Teams в Microsoft 365 предоставляет пользователям настраиваемый вид домашней страницы курса Moodle, который доступен для просмотра, когда пользователь обращается к своим курсам Moodle в Teams.

Подключаемый модуль темы предоставляет пользователям унифицированный расширенный интерфейс со следующими функциями.

* Адаптация к изменениям темы Microsoft Teams, например использование стандартной или темной темы и высокой контрастности.
* Фокус на действиях курса.
* Удаление блоков, структуры навигации и колонтитулов Moodle.
* Предоставление элементов пользовательского интерфейса Microsoft Teams.

На следующем изображении показана тема Teams, настроенная пользователем.

:::image type="content" source="../../assets/images/MoodleInstructions/teams-theme.png" alt-text="Тема Microsoft Teams":::

## <a name="onenote-integration"></a>Интеграция с OneNote

Подключаемый модуль интеграции с OneNote предоставляет пользователям возможность просматривать записные книжки, разделы и страницы, где отправляются задания, а преподаватели предоставляют необходимые отзывы о соответствующих заданиях в OneNote. OneNote также улучшает пользовательский интерфейс, добавляя функции помимо тестов и ссылок, расширяя возможности мобильных устройств с помощью цифровых перьев, фотографий или видео и совместной работы с группами.

Интеграция с OneNote облегчает доступ к репозиториям текстов, графических изображений и аудио. Подключаемый модуль предоставляет следующие преимущества.

* Доступен обзор записных книжек, разделов и страниц, на которых учащиеся работают над заданиями и предоставляют отзывы об этих заданиях в OneNote.
* Объединение цифрового скоросшивателя для заметок, заданий и отзывов с целью проверки и применения в качестве справочника.
* Расширение возможностей создания черновиков в дополнение к текстам и ссылкам, а также расширение использования мобильных устройств с помощью цифровых перьев, фотографий или видео и совместной работы с группами.
* Добавление страницы отправки и отзывов для каждого задания в учетной записи преподавателя. При сохранении в Moodle копия HTML и любые связанные изображения упаковываются в ZIP-файл.

> [!NOTE]
> События отправки или обратной связи запускают создание в OneNote с разделом для каждого курса, в котором зарегистрирован учащийся.

## <a name="microsoft-block"></a>Блок Microsoft

Подключаемый модуль блока Microsoft позволяет пользователю получать доступ к расположению SharePoint с файлами курса и просматривать курс в записной книжке OneNote для отправки, а также изменять настройки интеграции с Office 365. Администраторы могут настроить отображение блока на всех страницах курса.

Блок Microsoft улучшает взаимодействие с пользователем, предоставляя пользовательский интерфейс для изменения функций интеграции с Microsoft 365 и доступ к многочисленным ресурсам этой службы. Администраторы могут настроить блок для просмотра изменений так, чтобы он отображался на каждой странице курса. Блок позволяет пользователю выполнять следующие действия.

* Получение доступа к расположению SharePoint с файлами курса и записной книжке OneNote.
* Просмотр курса в записной книжке OneNote для отправки.
* Настройка синхронизации календаря Outlook.
* Управление подключением к Office 365.
* Настройка личных параметров интеграции с Office 365.

На следующем изображении показан пользовательский интерфейс блока Microsoft.

:::image type="content" source="../../assets/images/MoodleInstructions/microsoft-block-1.png" alt-text="Блок Microsoft":::

## <a name="oembed-filter"></a>Фильтр oEmbed

Подключаемый модуль фильтра oEmbed упрощает и улучшает пользовательский интерфейс, упрощая включение внешнего HTML-контента в Moodle. Ниже указаны преимущества фильтра oEmbed.

* Ускорение внедрения видео на страницу HTML.
* Поддержка внедрения нескольких поставщиков видеоконтента.
* Более быстрый способ копирования и внедрения кода из любой поддерживаемой службы.
* Поддержка внедрения видео без ключа API.

На следующем изображении показано добавление внешнего HTML-контента в Moodle.

:::image type="content" source="../../assets/images/MoodleInstructions/oEmbed-filter.png" alt-text="Страница фильтра oEmbed":::

## <a name="see-also"></a>См. также

* [Партнерские приложения для Moodle](../partner-apps-for-moodle.md)
* [Вопросы и ответы о Moodle](../faqs.md)
