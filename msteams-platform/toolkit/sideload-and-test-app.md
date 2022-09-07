---
title: Загрузка и тестирование неопубликованного приложения в среде Teams
author: zyxiaoyuer
description: В этом модуле вы узнаете, как загрузить неопубликованное и протестировать приложение в другой среде.
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/03/2022
ms.openlocfilehash: ee1d3ee3a4f545a6c988c421fb18626a4a7276b7
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617332"
---
# <a name="sideload-and-test-app-in-teams-environment"></a>Загрузка и тестирование неопубликованного приложения в среде Teams

После добавления подключения API можно протестировать подключение API в локальной среде Teams Toolkit и развернуть приложение в облаке. В конвейере CI/CD после настройки на другой платформе необходимо создать субъект-службу Azure для подготовки и развертывания ресурсов.

В этом разделе вы узнаете,

* [Проверка подключения API в локальной среде](#test-api-connection-in-local-environment)
* [Развертывание приложения в Azure](#deploy-your-application-to-azure)
* [Подготовка и развертывание ресурсов CI/CD](#provision-and-deploy-cicd-resources)

## <a name="test-api-connection-in-local-environment"></a>Проверка подключения API в локальной среде

Ниже приведены инструкции по проверке подключения API в локальной среде Teams Toolkit.

 1. **Запуск установки npm**

    Выполните `npm install` в `bot` папке `api` или в папке, чтобы установить добавленные пакеты.

 2. **Добавление учетных данных API в параметры локального приложения**

    Набор средств Teams не запрашивает учетные данные, но оставляет заполнители в файле параметров локального приложения. Замените заполнители соответствующими учетными данными для доступа к API. Файл параметров локального приложения — `.env.teamsfx.local` это файл в папке `bot` `api` или папке.

 3. **Использование клиента API для выполнения запросов API**

    Импортируйте клиент API из исходного кода, для которого требуется доступ к API:

    ```BASH
    import { yourApiClient } from '{relative path to the generated file}'
    ```

 4. **Создание http-запросов к целевому API (с помощью Axios)**

    Созданный клиент API является клиентом Axios API. Используйте клиент Axios для выполнения запросов к API.

     > [!Note]
     > [Axios](https://www.npmjs.com/package/axios) — это популярный пакет nodejs, который помогает с http-запросами. Дополнительные сведения о том, как выполнять http-запросы, см. в примере документации [по Axios](https://axios-http.com/docs/example) , чтобы узнать, как выполнять http-запросы.

## <a name="deploy-your-application-to-azure"></a>Развертывание приложения в Azure

Чтобы развернуть приложение в Azure, необходимо добавить проверку подлинности в параметры приложения для соответствующей среды. Например, ваш API может иметь разные учетные данные для и `dev` `prod`. В зависимости от потребностей среды настройте Набор средств Teams.

Набор средств Teams настраивает локальную среду. Пример кода начальной загрузки содержит комментарии, которые сообщают, какие параметры приложения необходимо настроить. Дополнительные сведения о параметрах приложения см. в разделе ["Добавление параметров приложения"](https://github.com/OfficeDev/TeamsFx/wiki/%5BDocument%5D-Add-app-settings)

## <a name="provision-and-deploy-cicd-resources"></a>Подготовка и развертывание ресурсов CI/CD

Чтобы подготовить и развернуть ресурсы, предназначенные для Azure, внутри CI/CD, необходимо создать субъект-службу Azure для использования.

Выполните следующие действия, чтобы создать субъекты-службы Azure.

1. Зарегистрируйте приложение Microsoft Azure Active Directory (Azure AD) в одном клиенте.
2. Назначьте роль приложению Azure AD для доступа к подписке Azure. Роль `Contributor` рекомендуется.
3. Создайте новый секрет приложения Azure AD.

> [!TIP]
> Сохраните свой идентификатор клиента, идентификатор приложения (AZURE_SERVICE_PRINCIPAL_NAME) и секрет (AZURE_SERVICE_PRINCIPAL_PASSWORD) для использования в будущем.

Дополнительные сведения см. в [Руководстве по субъектам-службам Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Ниже приведены три способа создания субъектов-служб.

* [Портал Microsoft Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="see-also"></a>См. также

* [Публикация приложений Teams с помощью набора средств Teams](publish.md)
