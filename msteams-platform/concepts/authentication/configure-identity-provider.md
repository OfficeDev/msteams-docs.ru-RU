---
title: Настройка поставщиков удостоверений OAuth 2.0
description: Описывает настройку поставщиков удостоверений с фокусом на Azure AD
ms.topic: how-to
localization_priority: Normal
keywords: teams authentication AAD oauth identity provider
ms.openlocfilehash: ffcf376ea6c4f1a94d797413af22af867dbd5b53
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020858"
---
# <a name="configure-identity-providers"></a>Настройка поставщиков удостоверений

## <a name="configuring-an-application-to-use-azure-active-directory-as-an-identity-provider"></a>Настройка приложения для использования Azure Active Directory в качестве поставщика удостоверений

Поставщики удостоверений, поддерживающие OAuth 2.0, не будут проверку подлинности запросов от неизвестных приложений; приложения должны быть зарегистрированы заранее. Чтобы сделать это с Azure AD, выполните следующие действия:

1. Откройте [портал регистрации приложений.](https://ms.portal.azure.com/#blade/Microsoft_AAD_RegisteredApps/ApplicationsListBlade)

2. Выберите приложение, чтобы просмотреть его свойства, или нажмите кнопку "Новая регистрация". Найдите **раздел URI** перенаправления для приложения.

3. В меню отсев убедитесь, что **выбран** Веб. Обновите URL-адрес конечной точки проверки подлинности. В примере typeScript/Node.js и C# GitHub URL-адреса перенаправления будут похожи на такие:

    Url-адреса перенаправления: `https://<hostname>/bot-auth/simple-start`

Замените `<hostname>` фактическим хостом. Это может быть выделенный хостинг-сайт, например Azure, Glitch или туннель ngrok для localhost на компьютере разработки, например `abcd1234.ngrok.io` . Вы можете еще не иметь эту информацию, если вы еще не завершили или не выполнили хостинг приложения (или примера приложения, упомянутого выше), но вы всегда можете вернуться на эту страницу, когда эта информация будет известна.

## <a name="other-authentication-providers"></a>Другие поставщики проверки подлинности

* **LinkedIn** Следуйте инструкциям в [настройке приложения LinkedIn](/linkedin/talent/apply-with-linkedin)

* **Google** Получение учетных данных клиента OAuth 2.0 из [консоли API Google](https://console.developers.google.com/)
