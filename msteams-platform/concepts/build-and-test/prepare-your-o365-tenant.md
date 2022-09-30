---
title: Подготовка клиента Microsoft 365
description: В этом модуле вы узнаете, как приступить к работе с Teams в Microsoft 365 и создать среду разработки.
ms.topic: how-to
ms.localizationpriority: medium
ms.openlocfilehash: c5ebc7d36f73978e1cd954c7be8d7ac3595ba68e
ms.sourcegitcommit: edfe85e312c73e34aa795922c4b7eb0647528d48
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/30/2022
ms.locfileid: "68243586"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Подписчики Microsoft 365 могут разрабатывать приложения для Microsoft Teams с помощью одного из следующих планов:

* Базовый
* Стандартный
* Корпоративный E1, E3 и E5
* Developer
* Education, Education Plus и Education E5

> [!NOTE]
>
> * Подробнее о подписках на Microsoft 365 см. в [Планах](https://products.office.com/business/compare-more-office-365-for-business-plans).
> * Teams также доступна для клиентов, которые подписались на E4 до его [прекращения](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).

## <a name="create-your-development-environment"></a>Подготовка среды разработки

Если у вас нет учетной записи Microsoft 365, вы должны подписаться на программу [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program). Подписка бесплатна в течение 90 дней и продлевается, пока вы используете ее для разработки. Если у вас есть подписка на Visual Studio Enterprise или Professional, то она включает бесплатную [подписку для разработчиков](https://aka.ms/MyVisualStudioBenefits) Microsoft 365. Она активна до тех пор, пока активна подписка на Visual Studio. Подробнее см. в статье [Настройка подписки разработчика Microsoft 365](/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-teams-for-your-organization"></a>Включите Teams для организации

Включите Teams для организации. Дополнительные сведения см. в разделе [Включение Teams для организации](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включите пользовательские приложения Teams и загрузку пользовательских приложений.

Чтобы включить индивидуальную загрузку или загрузку неопубликованных приложений для клиента разработчика, выполните следующее.

1. Войдите в [Центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) со своими учетными данными администратора.

2. Выберите **Показать все** > **Teams**.

    ![Меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > Может потребоваться до 24 часов для появления пункта **Teams**. Можно [отправить пользовательское приложение в среду Teams](/microsoftteams/upload-custom-apps#validate) для тестирования и проверки.

3. Перейдите к **глобальным политикам** > **установки приложений** >  Teams **.**

   ![Включите представление загрузки неопубликованного приложения](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Установите переключатель **Загрузка неопубликованных приложений** в положение **Включено**.

5. Нажмите кнопку **Сохранить**. Тестовый клиент может разрешить загрузку неопубликованных приложений.

    > [!Note]
    > Активация неопубликованной загрузки может занять до 24 часов. А пока вы можете использовать **загрузку для \<your tenant>**, чтобы протестировать приложение. Чтобы загрузить ZIP-файл пакета приложения, см. [Загрузка пользовательских приложений](/microsoftteams/upload-custom-apps#upload).

    ![Добавить представление приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Полные сведения о том, как взаимодействуют эти параметры, см. в статье [Управление пользовательскими политиками и параметрами приложений в Teams](/microsoftteams/teams-custom-app-policies-and-settings) и [Управление политиками настройки приложений в Teams](/microsoftteams/teams-app-setup-policies).

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Выбор параметров тестирования](~/concepts/build-and-test/debug.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Добавьте тестовые данные в тестовый клиент Microsoft 365](~/concepts/build-and-test/test-data.md).
* [Microsoft 365 Multi-Geo](/microsoft-365/enterprise/microsoft-365-multi-geo?view=o365-worldwide&preserve-view=true)
