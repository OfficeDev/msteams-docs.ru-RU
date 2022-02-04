---
title: Поток покупок в приложении для монетизации приложений
description: Узнайте основные задачи и концепции, необходимые для реализации покупок в приложении и пробных функций в приложениях групп.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
localization_priority: Normal
ms.openlocfilehash: 455809e64a934384d28e00bdf721ae8c66cb7d19
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2022
ms.locfileid: "62363472"
---
# <a name="in-app-purchases"></a>Покупки в приложении

Microsoft Teams API, которые можно использовать для реализации покупок в приложении для обновления из бесплатных в платные Teams приложения. Покупка в приложении позволяет преобразовать пользователей из бесплатных в платные планы непосредственно из приложения.

> [!NOTE]
> Покупки в приложении для Teams приложений в настоящее время доступны только в [**предварительном просмотре разработчика**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

## <a name="implement-in-app-purchases"></a>Реализация покупок в приложении

Чтобы предложить пользователям приложения возможность покупки в приложении, убедитесь в следующем:

* Приложение построено на [Teams клиентской библиотеке SDK](https://github.com/OfficeDev/microsoft-teams-library-js).

* Приложение включено с помощью трансактабельного [предложения SaaS](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md).

* Приложение включено с [разрешениями RSC](#update-manifest).

* Приложение вызывается с [API`openPurchaseExperience`](#purchase-experience-api).

Возможность покупки в приложении может быть включена путем обновления файла **manifest.json** или включения предложений о покупке **в** приложении из раздела **Permissions** **портала разработчика**.

### <a name="update-manifest"></a>Манифест обновления

Чтобы включить возможность покупки в приложении, Teams файл **manifest.json** приложения, добавив разрешения RSC. Это позволяет пользователям приложения перейти на платную версию приложения и начать использовать новые функции. Обновление манифеста приложения:

```json

"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
             "name": "InAppPurchase.Allow.User",
             "type": "Delegated"
            }
        ]
}
```

### <a name="purchase-experience-api"></a>API опыта покупки

Чтобы вызвать покупку в приложении для приложения, вызывайте `openPurchaseExperience` API из вашего веб-приложения.

Ниже приводится пример вызова API из приложения:

```json
<body> 
<div> 
<div class="sectionTitle">openPurchaseExperience</div> 
<button onclick="openPurchaseExperience()">openPurchaseExperience</button> 
</div> 
</body> 
<script> 
   function openPurchaseExperience() {
      microsoftTeams.initialize();
      let callbackcalled = false;
      microsoftTeams.monetization.openPurchaseExperience((e) => {
      console.log("callback is being called");
      callbackcalled = true;  
      if (!!e && typeof e !== "string") {
            e = JSON.stringify(e);
            alert(e);
        }
        return;
      });
      console.log("after callback: ",callbackcalled);
    } 
</script> 
```

## <a name="end-user-in-app-purchasing-experience"></a>Опыт покупки в приложении для конечных пользователей

В следующем примере пользователи могут приобрести планы подписки для вымышленного приложения Teams *Contoso Tasks for Teams*:

1. В Teams **Store** найдите и выберите приложение.

1. В диалоговом окте "Сведения о приложении" **выберите Купить подписку** или **добавить для меня**. 

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Покупка подписки для выбранного приложения." border="true":::

    
1. **Добавить для меня** предлагает бесплатную пробную версию приложения, а затем **обновить** его до платной версии.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Обновление до подписки для выбранного приложения." border="true":::

1. В **диалоговом окте "Выбор плана подписки** " выберите план и выберите **checkout**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Выбор соответствующего плана подписки." border="true":::

1. Выполните транзакцию и **выберите Настройка для** настройки подписки.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Настройка подписки." border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Посадочная страница подписки." border="true":::


## <a name="see-also"></a>См. также

* [Включите предложение SaaS в Microsoft Teams приложение](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Создание предложения по программному обеспечению в качестве службы (SaaS)](include-saas-offer.md#create-your-saas-offer)