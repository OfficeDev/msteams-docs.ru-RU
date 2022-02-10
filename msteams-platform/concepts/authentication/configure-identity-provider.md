---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает, как настроить поставщиков удостоверений с упором на Microsoft Azure Active Directory (Azure AD)
ms.topic: how-to
ms.localizationpriority: medium
keywords: поставщик удостоверений Microsoft Azure Active Directory групп (Azure AD)
ms.openlocfilehash: 93622275a8bfc9007af751d8b9f6304a73450ec7
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/10/2022
ms.locfileid: "62517976"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-microsoft-azure-active-directory-azure-ad-as-an-identity-provider"></a>Настройка приложения для использования Microsoft Azure Active Directory (Azure AD) в качестве поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с Microsoft Azure Active Directory (Azure AD), выполните следующие действия:

1. Откройте портал [регистрации приложений](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade).

2. Выберите приложение, чтобы просмотреть его свойства, или выберите кнопку "Новая регистрация". Найдите **раздел URI перенаправления** для приложения.

3. Выберите **Веб** из меню отсев. Обновите URL-адрес конечной точки проверки подлинности. В примере typeScript/Node.js C# и C# в GitHub URL-адреса перенаправления будут похожи на следующие:

    Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` фактическим хостом, который может быть выделенным хостинг-сайтом, таким как Azure, Glitch или туннель ngrok в localhost `abcd1234.ngrok.io`на компьютере разработки, например . У вас может не быть этих сведений, если вы еще не завершили или не перенастроили приложение (или упомянутое выше примерное приложение), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn:** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google:** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)
