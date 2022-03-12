---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает, как настроить поставщиков удостоверений с упором на Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
keywords: группы проверки подлинности Azure AD oauth identity provider
ms.openlocfilehash: ee99bf10f517eb928be0231a1188d2d5db74709d
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63452720"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-ad-as-an-identity-provider"></a>Настройка приложения для использования Azure AD в качестве поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с Azure AD, выполните следующие действия:

1. Откройте портал [регистрации приложений](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Выберите приложение, чтобы просмотреть его свойства, или выберите кнопку "Новая регистрация". Найдите **раздел URI перенаправления** для приложения.

3. Выберите **Веб** из меню отсев. Обновите URL-адрес конечной точки проверки подлинности. В примере typeScript/Node.js C# и C# в GitHub URL-адреса перенаправления будут похожи на следующие:

    Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` фактическим хостом, который может быть выделенным хостинг-сайтом, таким как Azure, Glitch или туннель ngrok в localhost `abcd1234.ngrok.io`на компьютере разработки, например . У вас может не быть этих сведений, если вы еще не завершили или не перенастроили приложение (или упомянутое выше примерное приложение), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn:** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)

* **Внешние поставщики OAuth из вкладок:** Дополнительные сведения см. в [дополнительных сведениях Об использовании внешних поставщиков OAuth](../../tabs/how-to/authentication/auth-oauth-provider.md)

## <a name="see-also"></a>См. также

* [Проверка подлинности пользователя в Microsoft Teams боте](../../resources/bot-v3/bot-authentication/auth-bot-AAD.md)
* [Поддержка единого входа (SSO) для вкладок](../../tabs/how-to/authentication/auth-aad-sso.md)
* [Проверка подлинности пользователя на вкладке Microsoft Teams](../../tabs/how-to/authentication/auth-tab-aad.md)
