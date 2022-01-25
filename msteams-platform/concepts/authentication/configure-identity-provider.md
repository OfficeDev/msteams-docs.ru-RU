---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает настройку поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: группы проверки подлинности Azure AD oauth identity provider
ms.openlocfilehash: 0e0b1e21bf3c2e877ddef790677ba2f4c227339e
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212337"
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
