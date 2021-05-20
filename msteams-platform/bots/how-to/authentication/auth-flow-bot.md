---
title: Microsoft Teams Поток аутентификации для ботов
description: Описывает Microsoft Teams проверки подлинности у ботов
keywords: команды аутентификации поток ботов
localization_priority: Normal
ms.topic: overview
ms.openlocfilehash: f3bf73c105dc38e1cea515bfa7bb7d5324b02ce4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565907"
---
# <a name="authentication-flow-for-bots-in-microsoft-teams"></a>Поток аутентификации для ботов в Microsoft Teams

OAuth 2.0 — это открытый стандарт проверки подлинности и авторизации, используемый Azure Active Directory (Azure AD) и многими другими поставщиками удостоверений. Базовое понимание OAuth 2.0 является необходимым условием для работы с аутентификацией в Teams; [Вот хороший обзор, который](https://aaronparecki.com/oauth-2-simplified/) легче следовать, чем формальные [спецификации](https://oauth.net/2/). Поток аутентификации для вкладок и ботов немного отличается - вкладки очень похожи на веб-сайты, чтобы они могли использовать OAuth 2.0 непосредственно, в то время как боты не являются и должны делать несколько вещей по-разному, - но основные понятия идентичны.

Можно GitHub [репо Microsoft Teams authentication Sample для](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) примера, демонстрируя поток аутентификации для ботов с помощью Node.js и типа кода [авторизации OAuth 2.0.](https://oauth.net/2/grant-types/authorization-code/)

![Диаграмма последовательности аутентификации Bot](../../../assets/images/authentication/bot_auth_sequence_diagram.png)

1. Пользователь отправляет сообщение боту.
2. Бот определяет, нужно ли пользователю войти в программу.
   В этом примере бот хранит токен доступа в своем пользовательском хранимом данных. Он просит пользователя войти в сеть, если у него нет проверенного маркера для выбранного поставщика идентификационных данных. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/utils/AuthenticationUtils.ts#L58-L76))
3. Бот строит URL на начало страницы потока аутентификации и отправляет карту пользователю с `signin` действием. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L160-L190))</br>
    Как и другие потоки auth приложения в Teams, начало страницы должно быть в домене, который находится в вашем `validDomains` списке, и в том же домене, что и страница перенаправления после входа.
    > [!IMPORTANT] 
    > Поток разрешения OAuth 2.0 требует параметра в `state` запросе проверки подлинности, который содержит уникальный маркер сеанса для предотвращения атаки [подделки запроса на кросс-сайт.](https://en.wikipedia.org/wiki/Cross-site_request_forgery) В этом примере используется случайным образом созданный GUID.
4. Когда пользователь выбирает кнопку *signin,* Teams открывает всплывающее окно и переходит на старт-страницу.
   > [!NOTE]
   > Размер всплывающего окна можно контролировать с помощью параметров строки запроса ширины и высоты в URL.адресу. Например, если добавить ширину 500 и высоту 500, то размер всплывающего окна составляет 500х500 пикселей. Teams отображает всплывающее окно с данным размером пикселя, максимум, что в процентах от размера главного окна.

5. Начало страницы перенаправляет пользователя в конечную точку поставщика `authorize` идентификационных данных. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/public/html/auth-start.html#L51-L56))
6. На сайте провайдера пользователь ва-гнет и предоставляет доступ к боту.
7. Поставщик отвеляет пользователя на страницу OAuth бота с кодом авторизации.
8. Бот выкупает код авторизации маркера доступа и **предварительно связывает** токен с пользователем, инициировав тем самым поток ва-во. Ниже мы называем это временным *маркером*.
    * В этом примере бот связывает значение параметра с идентификатором пользователя, инициировавого `state` процесс вовся, чтобы впоследствии сопоставить его со `state` значением, возвращенным поставщиком идентификационных данных. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L70-L99))
      > [!IMPORTANT] 
      > Бот хранит токен, который он получает от поставщика идентификационных данных, и связывает его с конкретным пользователем, но он помечен как "до проверки". 
    * Предварительный токен не может быть использован без дополнительной проверки.
      1. **Проверить, что получено от поставщика идентификационных данных.** Значение параметра должно быть `state` подтверждено по отношению к тому, что было сохранено ранее. 
      1. **Проверить, что получено от Teams.** [Двухшаговая проверка подлинности](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) выполняется для того, чтобы пользователь, уполномочил бота с поставщиком идентификационных данных, был тем же пользователем, который общается с ботом. Это защищает от [атак «человек в середине» и](https://en.wikipedia.org/wiki/Man-in-the-middle_attack) [фишинга.](https://en.wikipedia.org/wiki/Phishing) Бот генерирует код проверки и хранит его, связанный с пользователем. Код проверки отправляется автоматически Teams описано ниже. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/AuthBot.ts#L100-L113))
9. Обратный вызов OAuth отображает страницу, которая вызывает `notifySuccess("<verification code>")` . [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/master/src/views/oauth-callback-success.hbs))
10. Teams закрывает всплывающее окно и отправляет `<verification code>` отправленное `notifySuccess()` обратно к боту. Бот получает сообщение [вызова](/bot-framework/dotnet/bot-builder-dotnet-activities#invoke) с `name = signin/verifyState` .
11. Бот проверяет входящий код проверки на код проверки, хранящийся с временным маркером пользователя. [(Посмотреть код](https://github.com/OfficeDev/microsoft-teams-sample-auth-node/blob/469952a26d618dbf884a3be53c7d921cc580b1e2/src/dialogs/BaseIdentityDialog.ts#L127-L140))
12. Если они совпадают, бот отмечает маркер как проверенный и готовый к использованию. В противном случае поток аута выходит из строя, и бот удаляет предварительный маркер.

    > [!NOTE]
    > Если у вас проблемы с аутентификацией на мобильном телефоне, убедитесь, что ваш JavaScript SDK обновляется до версии 1.4.1 или позже.

## <a name="code-sample"></a>Пример кода

Пример кода, показывающего процесс проверки подлинности бота:

| **Название образца** | **Описание** | **Node.js** | **.NET** | **Python** |
|-----------------|----------------|--------------|----------|-----------|
| Teams аутентификация | Этот пример демонстрирует аутентификацию в Microsoft Teams приложениях. | [View](https://github.com/OfficeDev/microsoft-teams-sample-auth-node) | | |
| Бот аутентификация | Этот образец demonstartes как использовать аутентификацию для бота runnning в Microsoft Teams | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth)

## <a name="see-also"></a>См. также

[Добавить аутентификацию к вашему Teams боту](add-authentication.md)
