---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает настройку поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: проверка подлинности AAD поставщика удостоверений oauth
ms.openlocfilehash: cae2cc3d2feba8c17ad895864fd1b5995095f71b
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60887436"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Настройка приложения для использования Azure Active Directory поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с Azure AD, выполните следующие действия:

1. Откройте [портал регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Выберите приложение, чтобы просмотреть его свойства, или выберите кнопку "Новая регистрация". Найдите **раздел URI** перенаправления для приложения.

3. Выберите **Веб** из меню отсев. Обновите URL-адрес конечной точки проверки подлинности. В примере typeScript/Node.js C# и C# в GitHub URL-адреса перенаправления будут похожи на следующие:

    Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените фактическим хостом, который может быть выделенным хостинг-сайтом, таким как Azure, Glitch или туннель ngrok в localhost на компьютере разработки, например `<hostname>` `abcd1234.ngrok.io` . У вас может не быть этих сведений, если вы еще не завершили или не перенастроили приложение (или упомянутое выше примерное приложение), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn:** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)
