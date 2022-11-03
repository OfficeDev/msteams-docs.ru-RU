---
title: Загрузка и тестирование неопубликованного приложения в среде Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете, как загружать и тестировать неопубликованное приложение в разных средах.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: 721b3a30bcc8c2fa49bb06491f4ab24bbeb844fd
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833004"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Загрузка и тестирование неопубликованного приложения в среде Teams

После добавления подключения API можно проверить подключение API в локальной среде Набора средств Teams и развернуть приложение в облаке. В конвейере CI/CD после настройки с другой платформой необходимо создать субъект-службу Azure для подготовки и развертывания ресурсов.

В этом разделе вы узнаете

* [Проверка подключения API в локальной среде](#test-api-connection-in-local-environment)
* [Развертывание приложения в Azure](#deploy-your-application-to-azure)
* [Подготовка и развертывание ресурсов CI/CD](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>Проверка подключения API в локальной среде

Следующие действия помогут проверить подключение API в локальной среде набора средств Teams.

 1. **Запуск установки npm**

    Выполните команду `npm install` в `bot` папке или `api` , чтобы установить добавленные пакеты.

 2. **Добавление учетных данных API в параметры локального приложения**

    Набор средств Teams не запрашивает учетные данные, но оставляет заполнители в файле параметров локального приложения. Замените заполнители соответствующими учетными данными для доступа к API. Файл параметров локального `.env.teamsfx.local` приложения — это файл в папке `bot` или `api` .

 3. **Использование клиента API для выполнения запросов API**

    Импортируйте клиент API из исходного кода, которому требуется доступ к API:

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Создание HTTP-запросов к целевому API (с помощью Axios)**

    Созданный клиент API является клиентом API Axios. Используйте клиент Axios для отправки запросов к API.

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) — это популярный пакет nodejs, который помогает выполнять HTTP-запросы. Дополнительные сведения о том, как выполнять HTTP-запросы, см. в [примере документации по Axios](https://axios-http.com/docs/example) , чтобы узнать, как создать http(s).

## <a name="deploy-your-application-to-azure"></a>Развертывание приложения в Azure

Чтобы развернуть приложение в Azure, необходимо добавить проверку подлинности в параметры приложения для соответствующей среды. Например, у API могут быть разные учетные данные для `dev` и `prod`. В зависимости от потребностей среды настройте Набор средств Teams.

Набор средств Teams настраивает локальную среду. Начальный пример кода содержит примечания, которые указывают, какие параметры приложения необходимо настроить. Дополнительные сведения о параметрах приложения см. в разделе [Добавление параметров приложения](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings).

## <a name="provision-and-deploy-cicd-resources"></a>Подготовка и развертывание ресурсов CI/CD

Чтобы подготовить и развернуть ресурсы, предназначенные для Azure, внутри CI/CD, необходимо создать субъект-службу Azure для использования.

Выполните следующие действия, чтобы создать субъекты-службы Azure.

1. Зарегистрируйте приложение Microsoft Azure Active Directory (Azure AD) в одном клиенте.
2. Assign a role to your Azure AD application to access your Azure subscription. The `Contributor` role is recommended.
3. Создайте новый секрет приложения Azure AD.

> [!TIP]
> Сохраните свой идентификатор клиента, идентификатор приложения (AZURE_SERVICE_PRINCIPAL_NAME) и секрет (AZURE_SERVICE_PRINCIPAL_PASSWORD) для использования в будущем.

Дополнительные сведения см. в [Руководстве по субъектам-службам Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Ниже приведены три способа создания субъектов-служб.

* [Портал Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>См. также

[Публикация приложений Teams с помощью набора средств Teams](publish.md)
