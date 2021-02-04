---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
ms.topic: how-to
keywords: Настройка отправки Teams для клиента Microsoft 365
ms.openlocfilehash: 50765271b93edd380d1c23672289b618baf1d346
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093945"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Если вы подписчик Microsoft 365, вы можете разрабатывать приложения для Microsoft Teams с помощью одного из следующих [планов:](https://products.office.com/business/compare-more-office-365-for-business-plans)

* Обычный
* Стандартный
* Корпоративные E1, E3 и E5
* Developer
* Education, Education Plus и Education E5

Microsoft Teams также будет доступен клиентам, которые подписаны на E4 до его выхода из [нее.](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)

## <a name="just-need-a-development-environment"></a>Нужна только среда разработки?

Если у вас нет учетной записи Microsoft 365, вы можете подписаться на программу для разработчиков [Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program) Он *бесплатный* в течение 90 дней и будет постоянно обновляться, пока вы используете его для разработки. Если у вас есть подписка Visual Studio *Корпоративная* или *Профессиональная,* обе программы включают бесплатную подписку разработчика Microsoft 365, активную в течение Visual Studio подписки. [](https://aka.ms/MyVisualStudioBenefits) *См.* ["Настройка подписки разработчика Microsoft 365".](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)

## <a name="enable-microsoft-teams-for-your-organization"></a>Включить Microsoft Teams для своей организации 

Если Microsoft Teams не включен для вашей организации, это необходимо сделать в первую очередь. Подробное руководство по введению [Teams для вашей организации.](/microsoftteams/enable-features-office-365)

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включите настраиваемые приложения Teams и включите отправку пользовательских приложений

Включите настраиваемую загрузку нео том же приложения для клиента разработчика следующим образом:

1. Войдите в [Центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора. 

2. Выберите **"Показать все**  -->  **команды"**. 

![Изображение меню Центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> Для появления параметра "Teams" может занять до 24 часов. Во время промежуточного действия вы можете [отправить пользовательское приложение в среду Teams](/microsoftteams/upload-custom-apps#validate) для тестирования и проверки.

3. Переход к **глобальным политикам установки** приложений Teams  -->    -->  **(по умолчанию для всей организации)**  

![включить представление неогрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Перенимите **отправку пользовательских приложений** в **положение "на месте".**

5. Выберите **"Сохранить",** чтобы сохранить изменения.

Вот и все! Теперь тестовый клиент разрешит загрузку неогрузки пользовательского приложения.

> [!Note] 
> Загрузка нео боков может занять до 24 часов. В это время вы можете использовать **отправку для \<your tenant>** тестирования приложения.

![представление приложения updload](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Полные сведения о взаимодействии этих параметров см. в подстройки *"Управление* настраиваемой политикой и настройками приложений в [Microsoft Teams"](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и "Управление политиками настройки приложений [в Microsoft Teams".](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)
