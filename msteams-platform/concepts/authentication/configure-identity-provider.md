---
title: Настройка поставщиков удостоверений OAuth 2.0
description: В этой статье описывается настройка поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
keywords: поставщик удостоверений AAD oauth для проверки подлинности teams
ms.openlocfilehash: b5ffd6c4c1edd2c4315ea1e31474a626de53aba1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014469"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Настройка приложения для использования Azure Active Directory в качестве поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов из неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с помощью Azure AD, выполните следующие действия:

1. Откройте портал [регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация". Найдите **раздел URI** перенаправления для приложения.

3. Убедитесь, что в  меню в меню "Интернет" выбран веб-сайт. Обновите URL-адрес конечной точки проверки подлинности. Для примеров приложений TypeScript/Node.js и C# на GitHub URL-адреса перенаправления будут иметь примерно такой вид:

    URL-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` фактический хост. Это может быть выделенный сайт размещения, например Azure, Glitch или туннель ngrok для localhost на вашем компьютере разработки, например `abcd1234.ngrok.io` . Возможно, у вас пока нет этих сведений, если вы еще не завершили или не развернетесь в приложении (или в примере приложения, упомянутом выше), но вы всегда можете вернуться на эту страницу, если эти сведения известны.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn** Следуйте инструкциям по [настройке приложения LinkedIn](https://developer.linkedin.com/docs/oauth2)

* **Google** Получение учетных данных клиента OAuth 2.0 из консоли [API Google](https://console.developers.google.com/)
