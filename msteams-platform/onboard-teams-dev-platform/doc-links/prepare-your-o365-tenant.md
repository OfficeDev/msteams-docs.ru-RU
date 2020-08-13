---
title: Подготовка среды разработки Teams
description: Настройка среды для приложений девелопи Teams
keywords: Настройка среды разработки Office 365 для клиентов Teams
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/12/2020
ms.locfileid: "46652140"
---
# <a name="prepare-your-development-environment"></a>Подготовка среды разработки

Если вы являетесь подписчиком Office 365, вы можете разрабатывать приложения для Microsoft Teams с одним из следующих [планов](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Бизнес базовый
* Бизнес премиум
* Корпоративный E1, E3 и т. д.
* Developer
* Образование, образование и образование

Microsoft Teams также будет доступен клиентам, которые подписываются на E4 до [выхода](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)из нее.

## <a name="just-need-a-development-environment"></a>Нужна среда разработки?

Если у вас в настоящее время нет учетной записи Office 365, вы можете зарегистрироваться для подписки на [программу Microsoft 365 для разработчиков](https://developer.microsoft.com/microsoft-365/dev-program) . Он *освободится* на 90 дней и будет обновляться до тех пор, пока вы его используете для разработки действий. Если у вас есть подписка на Visual Studio *Enterprise* или *Professional* , обе программы включают бесплатную [подписку](https://aka.ms/MyVisualStudioBenefits)на Microsoft 365 для разработчиков, действующую в течение всего срока действия вашей подписки на Visual Studio. *Ознакомьтесь* [со статьей Настройка подписки на Microsoft 365 для разработчиков](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Включение Microsoft Teams для Организации

Если для вашей организации не включена поддержка Microsoft Teams, сначала потребуется сделать это. Ознакомьтесь с подробными инструкциями по [обеспечению поддержки Teams в Организации](https://docs.microsoft.com/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включение пользовательских приложений Teams и включение специальной отправки приложений

Включите нестандартную загрузку приложений для клиента разработчика следующим образом:

1. Войдите в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора. 

2. Выберите **Показать все**  -->  **команды**. 

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/admin-center.png)

3. Перейдите к разделу политики установки **приложений Teams**  -->  **Setup Policies**  -->  **Global (по умолчанию на уровне Организации)**  

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Переключите флажок **Отправить настраиваемые приложения** в положение **вкл** .

Вот и все! Теперь тестовый клиент позволит разрешить нестандартную загрузку приложений.

> [!Note] 
> Поддержка загрузки неопубликованных приложений может занимать до 24 часов. Во время промежуточного режима вы можете использовать **отправку для \<your tenant> ** тестирования приложения.

![изображение меню переполнения приложения](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Для получения полной информации о том, как эти параметры взаимодействуют, *Ознакомьтесь*со статьей [Управление пользовательскими политиками и параметрами приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и [Управление политиками установки приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).