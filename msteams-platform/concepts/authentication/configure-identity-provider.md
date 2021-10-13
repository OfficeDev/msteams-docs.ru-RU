---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает настройку поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
ms.localizationpriority: medium
keywords: проверка подлинности AAD поставщика удостоверений oauth
ms.openlocfilehash: d14dc4811faae13535ad1029a8820c5904f44774
ms.sourcegitcommit: 37b1724bb0d2f1b087c356e0fd0ff80145671e22
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2021
ms.locfileid: "60291620"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Настройка приложения для использования Azure Active Directory поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с Azure AD, выполните следующие действия:

1. Откройте [портал регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация". Найдите **раздел URI** перенаправления для приложения.

3. В меню отсев убедитесь, что **выбран** Веб. Обновите URL-адрес конечной точки проверки подлинности. В примере typeScript/Node.js C# и C# в GitHub URL-адреса перенаправления будут похожи на такие:

    Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` фактическим хостом. Это может быть выделенный хостинг-сайт, например Azure, Glitch или туннель ngrok для localhost на компьютере разработки, например `abcd1234.ngrok.io` . У вас может не быть этих сведений, если вы еще не завершили или не выполнили хостинг приложения (или примера приложения, упомянутого выше), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn:** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)
