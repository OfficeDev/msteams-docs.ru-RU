---
title: Использование внешних поставщиков OAuth
description: В этом модуле вы узнаете, как выполнять проверку подлинности с помощью внешних поставщиков OAuth и как добавить ее во внешний браузер
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 8a7d89bbe3c6109e52a4d22f4bc26eace7acc5d1
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142278"
---
# <a name="use-external-oauth-providers"></a>Использование внешних поставщиков OAuth

Вы можете поддерживать внешних или сторонних поставщиков OAuth, таких как Google, GitHub, LinkedIn и Facebook с помощью обновленного API `authenticate()`:

```JavaScript
function authenticate(authenticateParameters?: AuthenticateParameters)
``` 

Для поддержки внешних поставщиков OAuth в API `authenticate()` добавляются следующие данные.

* Параметр `isExternal`
* Два значения заполнителей в существующем параметре `url`

В следующей таблице приводится список параметров API `authenticate()` и функций, а также их описания:

| Параметр| Описание|
| --- | --- |
|`isExternal` | Тип параметра — логический. Он указывает, что окно аутентификации открывается во внешнем браузере.|
|`failureCallback`| Функция вызывается в случае сбоя проверки подлинности, а всплывающее всплывающее окно аутентификации указывает причину сбоя.|
|`height` |Предпочтительная высота всплывающего окна. Значение можно игнорировать, если он находится за пределами допустимых границ.|
|`successCallback`| Функция будет вызвана, если проверка подлинности будет успешной, а результат возвращен из всплывающего окна аутентификации. Код аутентификации — это результат.|
|`url`  <br>|URL-адрес стороннего сервера приложений для всплывающего окна проверки подлинности со следующими двумя заполнителями параметров:</br> <br> - `oauthRedirectMethod`: передача заполнителя в `{}`. Этот заполнитель заменяется прямой ссылкой или веб-страницей платформой Teams, которая сообщает серверу приложений о том, что вызов идет с мобильной платформы.</br> <br> - `authId`: этот заполнитель заменяется UUID. Сервер приложений использует его для обслуживания сеанса.| 
|`width`|Предпочтительная ширина всплывающего окна. Значение можно игнорировать, если он находится за пределами допустимых границ.|

Дополнительные сведения о параметрах см. в [интерфейсе параметров проверки подлинности](/javascript/api/@microsoft/teams-js/microsoftteams.authentication.authenticateparameters?view=msteams-client-js-latest&preserve-view=true).

## <a name="add-authentication-to-external-browsers"></a>Добавление проверки подлинности во внешние браузеры

> [!NOTE]
> * В настоящее время можно добавить проверку подлинности во внешние браузеры только для вкладок на мобильных устройствах. 
> * Используйте бета-версию JS SDK для использования функций. Бета-версии доступны через [NPM](https://www.npmjs.com/package/@microsoft/teams-js/v/1.12.0-beta.2).

На следующем изображении обеспечивается поток для добавления проверки подлинности во внешние браузеры:

 :::image type="content" source="../../../assets/images/tabs/tabs-authenticate-OAuth.PNG" alt-text="authenticate-OAuth" border="true":::

**Добавление проверки подлинности во внешние браузеры**

1. 1. Инициация внешнего процесса аутентификации.

   Стороннее приложение вызывает функцию SDK `microsoftTeams.authentication.authenticate` со значение true для `isExternal` для инициации внешнего процесса аутентификации. 

   Переданное значение `url` содержит заполнители для `{authId}` и `{oauthRedirectMethod}`.  


    ```JavaScript
    microsoftTeams.authentication.authenticate({
       url: 'https://3p.app.server/auth?oauthRedirectMethod={oauthRedirectMethod}&authId={authId}',
       isExternal: true,
       successCallback: function (result) {
       //sucess 
       } failureCallback: function (reason) {
       //failure 
        }
    });
    ```

2. 2. Ссылка Teams во внешнем браузере.

   Клиенты Teams открывают URL-адрес во внешнем браузере после замены `oauthRedirectMethod` и `authId` подходящими значениями. 

   #### <a name="example"></a>Пример

   ```http
    https://3p.app.server/auth?oauthRedirectMethod=deeplink&authId=1234567890 
   ```

3. 3. Ответ сервера стороннего приложения.

   Сервер стороннего приложения `url` получает и сохраняет следующие два параметра запроса:

   | Параметр | Описание|
   | --- | --- |
   | `oauthRedirectMethod` |Указывает, как стороннее приложение должно отправлять ответ на запрос проверки подлинности обратно в Teams с одним из двух значений: deeplink (прямая ссылка) или page (страница).|
   |`authId` | ИД запроса request-id, созданный Teams для этого конкретного запроса на проверку подлинности, который необходимо отправить обратно в Teams с помощью deeplink.|

    > [!TIP]
    > Стороннее приложение может маршалировать `authId`, `oauthRedirectMethod` в параметре запроса OAuth `state` при создании URL-адреса входа для OAuthProvider. Параметр `state` содержит переданные `authId` и `oauthRedirectMethod`, когда OAuthProvider перенаправляет обратно на сторонний сервер, а стороннее приложение использует значения для отправки ответа на проверку подлинности обратно в Teams, как описано в **6. Ответ сервера стороннего приложения на запрос Teams**. 

4. 4. Перенаправление сервера стороннего приложения на указанный `url`.

   Сервер стороннего приложения перенаправляет на страницу аутентификации поставщиков OAuth во внешнем браузере. `redirect_uri` является выделенным маршрутом на сервере стороннего приложения. Вы можете зарегистрировать `redirect_uri` в консоли разработчика поставщиков OAuth как статический, параметры должны быть отправлены через объект state. 

   #### <a name="example"></a>Пример

    ```http
    https://accounts.google.com/o/oauth2/v2/auth?redirect_uri=https://3p.app.server/authredirect&state={"authId":"…","oauthRedirectMethod":"…"}&client_id=…    &response_type=code&access_type=offline&scope= … 
    ```

5. 5. Вход во внешний браузер.

   Пользователь выполняет вход во внешнем браузере. Поставщики OAuth перенаправляются обратно на `redirect_uri` с кодом аутентификации и объектом state.

6. Сервер приложений 3P проверяет и отвечает на Teams.

   Сервер стороннего приложения обрабатывает ответ и проверяет `oauthRedirectMethod`, который возвращается внешним поставщиком OAuth в объекте состояния, чтобы определить, должен ли ответ возвращаться через прямую ссылку обратного вызова проверки безопасности или через веб-страницу, которая вызывает `notifySuccess()`.

      ```JavaScript
      const state = JSON.parse(req.query.state)
      if (state.oauthRedirectMethod === 'deeplink') {
         return res.redirect('msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}')
      }
      else {
      // continue redirecting to a web-page that will call notifySuccess() – usually this method is used in Teams-Web
      …
      ```

7. 7. Создание прямой ссылки сторонним приложением.

   Стороннее приложение создает прямую ссылку для мобильного приложения Teams в следующем формате и отправляет код аутентификации с кодом сеанса обратно в Teams.

   ```JavaScript
   return res.redirect(`msteams://teams.microsoft.com/l/auth-callback?authId=${state.authId}&code=${req.query.code}`)
   ```

 8. Teams вызывает обратный вызов успеха и отправляет результат.

    Teams делает успешный вызов и отправляет результат (код аутентификации) в стороннее приложение. Стороннее приложение получает код при успешном вызове и использует код для получения маркера, а затем сведений о пользователе и обновления пользовательского интерфейса.

      ```JavaScript
      successCallback: function (result) { 
      … 
      } 
      ```

## <a name="see-also"></a>См. также

* [Настройка поставщиков удостоверений](../../../concepts/authentication/configure-identity-provider.md)
* [Проверка подлинности Microsoft Teams для вкладок](auth-flow-tab.md)
