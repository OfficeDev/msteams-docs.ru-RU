---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
ms.localizationpriority: medium
keywords: Настройка Microsoft 365 клиента Teams загрузки
ms.openlocfilehash: 2b7da66460df12efd1e3c5bd45a9dfa6572e4b4c
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888155"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Microsoft 365 абоненты могут разрабатывать приложения для Microsoft Teams с одним из следующих планов:

* Базовый
* Стандартный
* Enterprise E1, E3 и E5
* Разработчик
* Education, Education Plus и Education E5

> [!NOTE]
> * Дополнительные сведения о Microsoft 365 подписках см. в [журнале plans](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams также доступен для клиентов, подписавших подписку на E4 до ее выхода на [пенсию.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Создание среды разработки

Если у вас нет Microsoft 365 учетной записи, необходимо подписаться на подписку [Microsoft 365 разработчика.](https://developer.microsoft.com/microsoft-365/dev-program) Подписка бесплатна в течение 90 дней и продолжает обновляться до тех пор, пока вы используете ее для разработки. Если у вас есть подписка Visual Studio Enterprise или Professional, обе программы включают бесплатную подписку Microsoft 365 [разработчика.](https://aka.ms/MyVisualStudioBenefits) Она активна до тех пор, пока Visual Studio подписка активна. Дополнительные сведения см. [в Microsoft 365 подписки разработчика.](/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-teams-for-your-organization"></a>Включить Teams для организации

Включить Teams для организации и дополнительные сведения см. в Teams [для вашей организации.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включите настраиваемые Teams приложения и включите настраиваемую загрузку приложений

**Включить настраиваемую загрузку или загрузку приложения для клиента разработчика**

1. Во входе [Центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.

2. Выберите **Показать все**  >  **Teams**.

    ![Меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > Для появления параметра Teams может занять **до 24** часов. За это время вы можете загрузить [настраиваемую Teams](/microsoftteams/upload-custom-apps#validate) среду для тестирования и проверки.

3. Перейдите **к Teams приложений** Установки  >  **политики**  >  **Глобальной**.

   ![Включайте представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Чтобы Upload **настраиваемые приложения на** **позицию On.**

5. Нажмите **Сохранить**. Клиент тестового клиента может разрешить настраиваемую загрузку приложений.

    > [!Note]
    > Для активной загрузки побок может занять до 24 часов. В промежуточном периоде вы можете использовать **отправку для \<your tenant>** тестирования приложения. Чтобы загрузить .zip пакета приложения, см. в [приложении upload custom apps.](/microsoftteams/upload-custom-apps#upload)

    ![Upload просмотра приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Полные сведения о взаимодействии этих параметров см. в приложении управление настраиваемой политикой и [настройками](/microsoftteams/teams-custom-app-policies-and-settings) в Teams и управление политиками установки [приложений в Teams.](/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"] 
> [Выбор параметров тестирования](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>См. также

[Добавление тестовых данных в Microsoft 365 тестовый клиент](~/concepts/build-and-test/test-data.md)
