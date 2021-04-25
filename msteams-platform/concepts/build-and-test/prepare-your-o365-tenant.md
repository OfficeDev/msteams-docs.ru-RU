---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка отправки команд клиентов Microsoft 365
ms.openlocfilehash: 4fbe1dcc7ba202aff0b46c7fc50d9aebc0278c38
ms.sourcegitcommit: 7b4f383b506d4bc68a1b5641d6e0f404edbfbc6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/22/2021
ms.locfileid: "51946468"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Подписчики Microsoft 365 могут разрабатывать приложения для Microsoft Teams с одним из следующих планов:

* Обычный
* Стандартный
* Корпоративные E1, E3 и E5
* Developer
* Education, Education Plus и Education E5

> [!NOTE]
> * Дополнительные сведения о подписках на Microsoft 365 см. в [журнале plans.](https://products.office.com/business/compare-more-office-365-for-business-plans)
> * Teams также доступны для клиентов, подписавших подписку на E4 до ее выхода на [пенсию.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="create-your-development-environment"></a>Создание среды разработки

Если у вас нет учетной записи Microsoft 365, необходимо зарегистрироваться для подписки на программу разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Подписка бесплатна в течение 90 дней и продолжает обновляться до тех пор, пока вы используете ее для разработки. Если у вас есть подписка Visual Studio enterprise или Professional, обе программы [](https://aka.ms/MyVisualStudioBenefits)включают бесплатную подписку на разработчика Microsoft 365. Она активна до тех пор, пока Visual Studio подписка активна. Дополнительные сведения см. [в журнале Настройка подписки на разработчика Microsoft 365.](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-teams-for-your-organization"></a>Включить Teams для организации

Включить Teams для организации и дополнительные сведения см. в [дополнительных сведениях о](/microsoftteams/enable-features-office-365)том, как включить Teams для вашей организации.

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включить настраиваемые приложения Teams и включить настраиваемую загрузку приложений

**Включить настраиваемую загрузку или загрузку приложения для клиента разработчика**

1. Во входе [в центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.

2. Выберите **Показать все**  >  **команды.**

    ![Меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > Для появления параметра **Teams** может занять до 24 часов. В это время вы можете загрузить [свое настраиваемую](/microsoftteams/upload-custom-apps#validate) приложение в среду Teams для тестирования и проверки.

3. Перейдите в **Teams Apps**  >  **Setup Policies**  >  **Global.**

   ![Включайте представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Чтобы загрузить **настраиваемые приложения в** положение **On.**

5. Нажмите **Сохранить**. Клиент тестового клиента может разрешить настраиваемую загрузку приложений.

    > [!Note]
    > Для активной загрузки побок может занять до 24 часов. В промежуточном периоде вы можете использовать **отправку для \<your tenant>** тестирования приложения. Чтобы загрузить файл пакета .zip приложения, см. в [приложении upload custom apps.](/microsoftteams/upload-custom-apps#upload)

    ![Загрузка представления приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Полные сведения о взаимодействии этих параметров см. в сведениях об управлении настраиваемой политикой и настройками приложений [в Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и об управлении политиками установки приложений [в Teams.](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"] 
> [Выбор параметров тестирования](~/concepts/build-and-test/debug.md)

