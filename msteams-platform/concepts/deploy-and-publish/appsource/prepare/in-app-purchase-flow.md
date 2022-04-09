---
title: Последовательность операций покупки из приложения для монетизации приложений
description: Узнайте основные задачи и концепции, необходимые для реализации покупок в приложении и пробных функций в приложениях Teams.
author: v-npaladugu
ms.author: surbhigupta
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 4f606363b62126731afcbc8b7f065951d8cd1a13
ms.sourcegitcommit: 61003a14e8a179e1268bbdbd9cf5e904c5259566
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/09/2022
ms.locfileid: "64736880"
---
# <a name="in-app-purchases"></a>Покупки из приложения

Microsoft Teams предоставляет API, которые можно использовать для реализации покупок в приложении, позволяющих пользователю перейти с бесплатной версии приложения Teams на платную. Покупка в приложении позволяет переключить пользователя с бесплатного на платный план пользования прямо в приложении.

> [!NOTE]
> Покупки в приложении для Teams в настоящее время доступны только в [**предварительной версии для разработчиков**](/microsoftteams/platform/resources/dev-preview/developer-preview-intro).

## <a name="implement-in-app-purchases"></a>Реализация покупок в приложении

Чтобы предложить пользователям возможность покупки в приложении, должны быть выполнены следующие условия.

* Приложение построено на [библиотеке SDK клиента Teams](https://github.com/OfficeDev/microsoft-teams-library-js).

* К приложению добавлено [предложение SaaS](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md), поддерживающее транзакции.

* В приложении включены [разрешения RSC](#update-manifest).

* Приложение вызывается через [API`openPurchaseExperience`](#purchase-experience-api).

Чтобы обеспечить возможность покупки в приложении, измените файл `manifest.json` или включите **Показывать предложение покупки в приложении** в разделе **Разрешения** **портала разработчика**.

### <a name="update-manifest"></a>Изменение манифеста

Чтобы включить возможность покупки в приложении, измените файл `manifest.json` приложения Teams, добавив разрешения RSC. Это позволяет пользователям перейти на платную версию приложения и начать использовать новые функции. Измените манифест приложения, выполнив следующие шаги.

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
}
```

### <a name="purchase-experience-api"></a>API покупки

Чтобы инициировать покупку в приложении для вашего веб-приложения, вызовите из него `openPurchaseExperience`API.

Ниже приводится пример вызова API из приложения.

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

## <a name="end-user-in-app-purchasing-experience"></a>Интерфейс покупки в приложении для конечных пользователей

В следующем примере пользователи могут приобрести планы подписки для вымышленного приложения Teams *Contoso Tasks for Teams*.

1. В Teams **Store** найдите и выберите приложение.

1. В диалоговом окне "Сведения о приложении" **выберите Купить подписку** или **Добавить для меня**.

    :::image type="content" source="~/assets/images/saas-offer/buysubscriptionplancontoso.png" alt-text="Покупка подписки для выбранного приложения." border="true":::

1. **Добавить для меня** предлагает установить бесплатную пробную версию приложения, а позже **обновить** его до платной версии.

    :::image type="content" source="~/assets/images/saas-offer/upgradeapp.png" alt-text="Обновление до подписки для выбранного приложения." lightbox="../../../../assets/images/saas-offer/upgradeapp.png" border="true":::

1. В диалоговом окне **Выбор плана подписки** выберите план и щелкните **Купить**.

    :::image type="content" source="~/assets/images/saas-offer/choosingsubscriptionplancontoso.png" alt-text="Выбор нужного плана подписки." lightbox="../../../../assets/images/saas-offer/choosingsubscriptionplancontoso.png" border="true":::

1. Завершите покупку и выберите **Настройка** для настройки подписки.

    :::image type="content" source="~/assets/images/saas-offer/saas-offer-configure-now.png" alt-text="Настройка подписки." lightbox="../../../../assets/images/saas-offer/saas-offer-configure-now.png" border="true":::

    :::image type="content" source="~/assets/images/saas-offer/getstarted.png" alt-text="Начальная страница подписки." lightbox="../../../../assets/images/saas-offer/getstarted.png" border="true":::

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Предварительное тестирование для приложений с монетизацией](~/concepts/deploy-and-publish/appsource/prepare/Test-preview-for-monetized-apps.md)

## <a name="see-also"></a>См. также

* [Включение предложения SaaS в приложение Microsoft Teams](~/concepts/deploy-and-publish/appsource/prepare/include-saas-offer.md)
* [Создание предложения по программному обеспечению в качестве службы (SaaS)](include-saas-offer.md#create-your-saas-offer)
