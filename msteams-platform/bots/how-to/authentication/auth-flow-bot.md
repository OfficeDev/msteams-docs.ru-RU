---
title: Microsoft Teams Поток проверки подлинности для ботов
description: Описывает Microsoft Teams проверку подлинности в ботах с образцом кода.
keywords: боты потока проверки подлинности команд
ms.localizationpriority: medium
ms.topic: overview
ms.openlocfilehash: 9413a4a894ff7b67a2158f34c35bdfecd935b7a5
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887861"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Поток проверки подлинности для ботов в Microsoft Teams

OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является обязательным условием для работы с проверкой подлинности в Teams; [Вот хороший обзор,](https://aaronparecki.com/oauth-2-simplified/) который легче следовать, чем [формальные спецификации](https://oauth.net/2/). Поток проверки подлинности для вкладок и ботов немного отличается : вкладки очень похожи на веб-сайты, поэтому они могут напрямую использовать OAuth 2.0, в то время как боты не являются и должны делать несколько вещей по-другому, но основные понятия идентичны.

Пример GitHub репо [Microsoft Teams](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) проверки подлинности см. в примере, демонстрируемом потоком проверки подлинности для ботов с Node.js и типом гранта кода авторизации [OAuth 2.0.](https://oauth.net/2/grant-types/authorization-code/)

![Схема последовательности проверки подлинности ботов](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. Пользователь отправляет сообщение боту.
2. Бот определяет, нужно ли пользователю войти.
   В этом примере бот хранит маркер доступа в хранилище пользовательских данных. Он просит пользователя войти, если у него нет проверенного маркера для выбранного поставщика удостоверений. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Бот строит URL-адрес на стартовую страницу потока проверки подлинности и отправляет карточку пользователю с `signin` действием. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Как и другие потоки auth приложения в Teams, стартовая страница должна быть в домене, который в вашем списке, и в том же домене, что и страница перенаправления после `validDomains` входа.
    > [!IMPORTANT] 
    > Поток грантов кода авторизации OAuth 2.0 вызывает параметр в запросе на проверку подлинности, который содержит уникальный маркер сеанса для предотвращения атаки подделки запросов на `state` сайте. [](https://en.wikipedia.org/wiki/Cross-site_request_forgery) В примере используется случайно созданный GUID.
4. Когда пользователь выбирает кнопку *signin,* Teams открывает всплывающее окно и переходит на начните страницу.
   > [!NOTE]
   > Размер всплывающее окно можно контролировать с помощью параметров строки запроса ширины и высоты в URL-адресе. Например, если добавить ширину=600 и высоту=600, размер всплывающее окно — 600x600 пикселей. Фактический размер всплывающее окно зажат в процентах от основного Teams окна. Если окно Teams, всплывающее окно меньше указанных размеров.

5. На стартовой странице пользователь перенаправляется в конечную точку поставщика `authorize` удостоверений. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. На сайте поставщика пользователь в записи и предоставляет доступ к боту.
7. Поставщик принимает пользователя на страницу перенаправления OAuth бота с кодом авторизации.
8. Бот выкупает код авторизации маркера  доступа и предварительно связывает маркер с пользователем, который инициировал входной поток. Ниже мы называем это *временным маркером.*
    * В примере бот связывает значение параметра с идентификатором пользователя, который инициировал процесс регистрации, чтобы впоследствии он соедиировал его со значением, возвращенным поставщиком `state` `state` удостоверений. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT] 
      > Бот хранит маркер, который он получает от поставщика удостоверений, и связывает его с определенным пользователем, но он помечен как "ожидающий проверки". 
    * Временный маркер нельзя использовать без дополнительной проверки.
      1. **Проверка того, что получено от поставщика удостоверений.** Значение параметра `state` должно быть подтверждено в отношении того, что было сохранено ранее. 
      1. **Проверка того, что получено от Teams.** Для [проверки](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) подлинности выполняется двухшаговая проверка подлинности, чтобы убедиться, что пользователь, уполномочивший бота с поставщиком удостоверений, является тем же пользователем, который общается с ботом. Это [охраняет от атак man-in-the-middle](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) и [фишинга.](https://en.wikipedia.org/wiki/Phishing) Бот создает код проверки и сохраняет его, связанный с пользователем. Код проверки отправляется автоматически Teams, как описано ниже. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Вызов OAuth отрисовки страницы, которая вызывает `notifySuccess("<verification code>")` . ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams закрывает всплывающее окно и отправляет `<verification code>` отправленное обратно `notifySuccess()` в бот. Бот получает сообщение [вызова](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) с `name = signin/verifyState` .
11. Бот проверяет входящий код проверки на код проверки, хранимый с временным маркером пользователя. ([Просмотр кода](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Если они совпадают, бот отмечает маркер как проверенный и готовый к использованию. В противном случае поток auth не удается, и бот удаляет временный маркер.

    > [!NOTE]
    > При проблемах с проверкой подлинности на мобильных устройствах убедитесь, что SDK JavaScript обновляется до версии 1.4.1 или более поздней версии.

## <a name="code-sample"></a>Пример кода

Пример кода, показывающий процесс проверки подлинности бота:

| **Название примера** | **Описание** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams проверки подлинности | В этом примере демонстрируется проверка подлинности в Microsoft Teams приложениях. | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| Проверка подлинности ботов | В этом примере показано, как использовать проверку подлинности для бота, запущенного в Microsoft Teams | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [Просмотр](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>Дополнительные ресурсы

[Добавление проверки подлинности в Teams бота](add-authentication.md)
