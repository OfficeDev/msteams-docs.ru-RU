---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описание настройки поставщиков удостоверений с фокусом на Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: high
keywords: проверка подлинности Teams поставщиком удостоверений OAuth от Azure AD
ms.openlocfilehash: c21be68ef76568ea4c5bb534f329f725d599b1ac
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111803"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>Настройка приложения для использования Azure AD в качестве поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут выполнять проверку подлинности запросов из неизвестных приложений. Приложения должны быть зарегистрированы заранее. Чтобы сделать это с помощью Azure AD, выполните следующие действия:

1. Откройте [портал регистрации приложений](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация". Найдите раздел **URI перенаправления** для приложения.

3. Выберите в раскрывающемся меню **Интернет**. Обновите URL-адрес конечной точки проверки подлинности. Для примеров приложений TypeScript/Node.js и C# на GitHub URL-адреса перенаправления будут выглядеть примерно так:

    URL-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` на фактический узел, который может быть выделенным сайтом размещения, таким как Azure, Glitch или туннель ngrok для localhost на компьютере разработки, например,`abcd1234.ngrok.io`. Эти сведения могут не быть предоставлены, если вы еще не завершили установку приложения (или пример приложения, упомянутый выше) или не разместили его, но вы всегда можете вернуться на эту страницу, когда эта информация станет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **Linkedin:** Следуйте инструкциям по [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)

* **Внешние поставщики OAuth с вкладок:** Дополнительные сведения см. в разделе [Использование внешних поставщиков OAuth](../../tabs/how-to/authentication/auth-oauth-provider.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Проверка подлинности пользователя в боте Microsoft Teams](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [Поддержка единого входа (SSO) для вкладок](../../tabs/how-to/authentication/auth-aad-sso.md)
* [Проверка подлинности пользователя на вкладке Microsoft Teams](../../tabs/how-to/authentication/auth-tab-aad.md)
