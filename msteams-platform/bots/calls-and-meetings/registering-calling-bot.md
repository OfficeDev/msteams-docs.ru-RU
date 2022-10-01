---
title: Регистрация бота для звонков и собраний для Microsoft Teams
description: Узнайте, как зарегистрировать новый бот для аудио- и видеозвонков в Microsoft Teams, создать бот или добавить возможность вызова, добавить разрешения графа. Пример создания звонка, присоединения к собранию и передачи звонка.
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 3fe8d0adde45242738b8023c5478c24769561d1c
ms.sourcegitcommit: 53818e55dfe0dbdf874d578a40982f7db444f89b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/01/2022
ms.locfileid: "68319939"
---
# <a name="register-calls-and-meetings-bot-for-microsoft-teams"></a>Регистрация бота для звонков и собраний для Microsoft Teams

Бот, который участвует в аудио- или видеовызовах и виртуальных собраниях, — это обычный бот Microsoft Teams со следующими дополнительными функциями, используемыми для регистрации бота:

* Существует новая версия манифеста приложения Teams с двумя дополнительными параметрами `supportsCalling` и `supportsVideo`. Эти параметры включены в [схему манифеста для Microsoft Teams](../../resources/schema/manifest-schema.md).
* [Разрешения Microsoft Graph](./registering-calling-bot.md#add-graph-permissions) должны быть настроены для идентификатора приложения Microsoft бота.
* Для разрешений вызовов Graph и виртуальных собраний API требуется согласие администратора клиента.

## <a name="new-manifest-settings"></a>Новые параметры манифеста

Боты для вызовов и виртуальных собраний имеют следующие два дополнительных параметра в файле manifest.json, которые включают звук или видео для бота в Teams.

* `bots[0].supportsCalling`. If present and set to `true`, Teams allows your bot to participate in calls and online meetings.
* `bots[0].supportsVideo`. If present and set to `true`, Teams knows that your bot supports video.

Если вы хотите, чтобы среда IDE правильно проверяла схему manifest.json для вызовов и собраний для этих значений, вы можете изменить атрибут `$schema` следующим образом:

```json
"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
```

В следующем разделе вы можете создать новый бот или добавить возможности вызова к существующему боту.

## <a name="create-new-bot-or-add-calling-capabilities"></a>Создайте новый бот или добавьте возможности вызова

Сведения о создании ботов см. в [Создание бота для Teams](../how-to/create-a-bot-for-teams.md).

Чтобы создать новый бот для Teams:

1. Use this link to create a new bot, `https://dev.botframework.com/bots/new`. Alternately, if you select the **Create a bot** button in the Bot Framework portal, you create your bot in Microsoft Azure, for which you must have an Azure account.
1. Добавьте канал Teams.
1. Выберите вкладку **Вызов** на странице канала Teams. Выберите **Включить вызовы**, а затем обновите **Веб-перехватчик (для вызовов)** указав URL-адрес HTTPS, на который вы получаете входящие уведомления, например `https://contoso.com/teamsapp/api/calling`. Подробнее см. в статье [Настройка каналов](/bot-framework/portal-configure-channels).

    ![Настройка сведений о канале Teams](~/assets/images/calls-and-meetings/configure-msteams-channel.png)

В следующем разделе приведен список разрешений приложений, поддерживаемых для вызовов и виртуальных собраний.

## <a name="add-graph-permissions"></a>Предоставить разрешения Graph

Graph предоставляет детализированные разрешения для управления доступом приложений к ресурсам. Вы сами решаете, какие разрешения для Graph запрашивает приложение. API-интерфейсы вызовов Graph поддерживают разрешения приложений, которые используются приложениями, работающими без присутствия пользователя, выполнившего вход. Администратор клиента должен дать согласие на разрешения приложения.

### <a name="application-permissions-for-calls"></a>Разрешения приложения для вызовов

В следующей таблице приведен список разрешений приложений для вызовов:

|Разрешение    |Отображаемая строка   |Описание |Требуется согласие администратора |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| Calls.Initiate.All |Запуск исходящих индивидуальных вызовов из приложения в предварительной версии. |Позволяет приложению совершать исходящие звонки одному пользователю и передавать звонки пользователям из каталога вашей организации без необходимости входа пользователя.|Да|
| Calls.InitiateGroupCall.All |Инициируйте исходящие вызовы 1:1 и групповые вызовы из предварительной версии приложения. |Позволяет приложению выполнять исходящие звонки одному пользователю, нескольким пользователям, передавать звонки и добавлять участников на собрания в организации без необходимости входа пользователя.|Да|
| Calls.JoinGroupCall.All |Присоединяйтесь к групповым вызовам и собраниям в качестве предварительного просмотра приложения. |Позволяет приложению присоединяться к групповым звонкам и запланированным собраниям в организации без необходимости входа пользователя. Приложение присоединится к собраниям в клиенте с правами пользователя каталога.|Да|
| Calls.JoinGroupCallasGuest.All |Присоединяйтесь к групповым вызовам и собраниям в качестве гостевого предварительного просмотра. |Позволяет приложению анонимно присоединяться к групповым звонкам и запланированным собраниям в организации без необходимости входа пользователя. Приложение присоединено к собраниям в клиенте в качестве гостя.|Да|
| Calls.AccessMedia.All |Доступ к медиапотокам во время разговора в качестве предварительного просмотра приложения. |Позволяет приложению получить прямой доступ к потокам мультимедиа в ходе звонка без необходимости входа пользователя.|Да|

> [!IMPORTANT]
> Вы не можете использовать API доступа к мультимедиа для записи или иного сохранения мультимедийного содержимого вызовов или собраний, к которым обращается приложение, или для получения данных из этой записи или записи мультимедийного содержимого. Сначала необходимо вызвать [`updateRecordingStatus` API ](/graph/api/call-updaterecordingstatus), чтобы указать, что запись началась, и получить ответ об успешном завершении от этого API. Если приложение начинает записывать какое-либо собрание или вызов, оно должно завершить запись перед вызовом API `updateRecordingStatus`, чтобы указать, что запись завершена.

### <a name="application-permissions-for-online-meetings"></a>Разрешения приложений для виртуальных собраний

В следующей таблице представлен список разрешений приложений для виртуальных собраний:

|Разрешение    |Отображаемая строка   |Описание |Требуется согласие администратора |
|:-----------------------------|:-----------------------------------------|:-----------------|:-----------------|
| OnlineMeetings.Read.All |Чтение сведений о виртуальном собрании в предварительном просмотре приложения|Позволяет приложению считывать сведения о виртуальном собрании в организации без входа пользователя.|Да|
| OnlineMeetings.ReadWrite.All |Чтение и создание виртуальных собраний из предварительной версии приложения от имени пользователя|Позволяет приложению создавать виртуальные собрания в организации от имени пользователя без входа пользователя.|Да|

### <a name="assign-permissions"></a>Назначение разрешений

Если вы предпочитаете использовать конечную точку [Microsoft Azure Active Directory (Azure AD) V1](https://portal.azure.com) необходимо заранее настроить разрешения приложения для бота с помощью [портала Microsoft Azure](/azure/active-directory/develop/azure-ad-endpoint-comparison).

### <a name="get-tenant-administrator-consent"></a>Получить согласие администратора клиента

For apps using the Azure AD V1 endpoint, a tenant administrator can consent to the application permissions using the [Microsoft Azure portal](https://portal.azure.com) when your app is installed in their organization. Alternately, you can provide a sign-up experience in your app through which administrators can consent to the permissions you configured. Once administrator consent is recorded by Azure AD, your app can request tokens without having to request consent again.

You can rely on an administrator to grant the permissions your app needs at the [Microsoft Azure portal](https://portal.azure.com). A better option is to provide a sign-up experience for administrators by using the Azure AD V2 `/adminconsent` endpoint. For more information, see [instructions on constructing an Admin consent URL](/graph/auth-v2-service#3-get-administrator-consent).

> [!NOTE]
> Чтобы создать URL-адрес согласия администратора клиента, требуется настроенный URI перенаправления или URL-адрес ответа на [портале регистрации приложений](https://apps.dev.microsoft.com/). Чтобы добавить URL-адреса ответов для бота, войдите в систему регистрации бота, выберите **Дополнительные параметры** > **Редактировать манифест приложения**. Добавьте URL-адрес перенаправления в коллекцию `replyUrls`.

> [!IMPORTANT]
> Каждый раз, когда вы вносите изменения в разрешения приложения, вы также должны повторно получить согласие администратора. Изменения, внесенные на портале регистрации приложений, не отражаются до тех пор, пока согласие не будет повторно применено администратором клиента.

## <a name="code-sample"></a>Пример кода

| **Название примера** | **Описание** | **C#** |
|---------------|----------|--------|
| Вызов и собрание с ботом | Образец приложения демонстрирует, как бот может создавать вызовы, присоединяться к собраниям и перенаправлять вызовы. | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-calling-meeting/csharp) |
| События собрания в режиме реального времени |В примере приложения показано, как бот может получать события собраний в режиме реального времени.|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|

## <a name="step-by-step-guide"></a>Пошаговые инструкции

Следуйте [пошаговым инструкциям](../../sbs-calling-and-meeting.yml) чтобы настроить вызовы и собрания в боте.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Уведомления о входящих звонках](~/bots/calls-and-meetings/call-notifications.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Уведомления о входящих звонках](~/bots/calls-and-meetings/call-notifications.md)
* [Разработка ботов для вызовов и виртуальных собраний на компьютере](~/bots/calls-and-meetings/debugging-local-testing-calling-meeting-bots.md)
* [Просмотр разрешений приложения и предоставление согласия администратора](/MicrosoftTeams/app-permissions-admin-center).
* [Работа с API облачных коммуникаций в Microsoft Graph](/graph/api/resources/communications-api-overview)
