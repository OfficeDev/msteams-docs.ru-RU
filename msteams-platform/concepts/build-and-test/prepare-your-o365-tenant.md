---
title: Подготовка клиента Microsoft 365
description: Начало работы с Teams в Microsoft 365
keywords: Настройка отправки Microsoft 365 клиента Teams
ms.openlocfilehash: 67a0342a7e8605097eed53dd1b0bdf273d537c0e
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452767"
---
# <a name="prepare-your-microsoft-365-tenant"></a>Подготовка клиента Microsoft 365

Если вы являетесь подписчиком Microsoft 365, вы можете разрабатывать приложения для Microsoft Teams с одним из следующих [планов](https://products.office.com/business/compare-more-office-365-for-business-plans):

* Обычный
* Стандартный
* Корпоративный E1, E3 и т. д.
* Developer
* Образование, образование и образование

Microsoft Teams также будет доступен клиентам, которые подписываются на E4 до [выхода](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)из нее.

## <a name="just-need-a-development-environment"></a>Нужна среда разработки?

Если у вас в настоящее время нет учетной записи Microsoft 365, вы можете зарегистрироваться для подписки на [программу microsoft 365 для разработчиков](https://developer.microsoft.com/microsoft-365/dev-program) . Он *освободится* на 90 дней и будет обновляться до тех пор, пока вы его используете для разработки действий. Если у вас есть подписка на Visual Studio *Enterprise* или *Professional* , обе программы включают бесплатную [подписку](https://aka.ms/MyVisualStudioBenefits)на Microsoft 365 для разработчиков, действующую в течение всего срока действия вашей подписки на Visual Studio. *Ознакомьтесь* [со статьей Настройка подписки на Microsoft 365 для разработчиков](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).

## <a name="enable-microsoft-teams-for-your-organization"></a>Включение Microsoft Teams для Организации 

Если для вашей организации не включена поддержка Microsoft Teams, сначала потребуется сделать это. Ознакомьтесь с подробными инструкциями по [обеспечению поддержки Teams в Организации](/microsoftteams/enable-features-office-365).

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a>Включение пользовательских приложений Teams и включение специальной отправки приложений

Включите нестандартную загрузку приложений для клиента разработчика следующим образом:

1. Войдите в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора. 

2. Выберите **Показать все**  -->  **команды**. 

![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> Для отображения параметра "Teams" может потребоваться до 24 часов. Во время промежуточного приложения вы можете [отправить свое приложение в среду Teams](/microsoftteams/upload-custom-apps#validate) для тестирования и проверки.

3. Перейдите к разделу политики установки **приложений Teams**  -->  **Setup Policies**  -->  **Global (по умолчанию на уровне Организации)**  

![Включение представления Загрузка неопубликованных](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. Переключите флажок **Отправить настраиваемые приложения** в положение **вкл** .

Вот и все! Теперь тестовый клиент позволит разрешить нестандартную загрузку приложений.

> [!Note] 
> Поддержка загрузки неопубликованных приложений может занимать до 24 часов. Во время промежуточного режима вы можете использовать **отправку для \<your tenant> ** тестирования приложения.

![представление приложения упдлоад](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

Для получения полной информации о том, как эти параметры взаимодействуют, *Ознакомьтесь*со статьей [Управление пользовательскими политиками и параметрами приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) и [Управление политиками установки приложений в Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).
