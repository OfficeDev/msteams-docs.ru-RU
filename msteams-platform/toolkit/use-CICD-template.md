---
title: Узнайте, как использовать шаблоны конвейеров CI/CD в GitHub, Azure DevOps и Jenkins для разработчиков Teams приложений
author: MuyangAmigo
description: Шаблоны CI/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 66560b1f228c32b0faf6569ff0ae536a81dc33c0
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073295"
---
# <a name="set-up-cicd-pipelines"></a>Настройка конвейеров CI/CD

TeamsFx помогает автоматизировать рабочий процесс разработки при создании Teams приложения. Ниже приведены средства и шаблоны, которые можно использовать для настройки конвейеров CI/CD, создания шаблонов рабочих процессов и настройки рабочего процесса CI/CD с GitHub, Azure DevOps, Jenkins и другими платформами. Чтобы подготовить и развернуть ресурсы, можно создать субъекты-службы Azure и опубликовать Teams с помощью портала Teams разработчика. Чтобы опубликовать Teams вручную, можно использовать портал разработчика [для Teams](https://dev.teams.microsoft.com/home).


|Средства и шаблоны | Описание |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub Действия, интегрируемые с TeamsFx CLI.|
|[Teams набор средств в Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Visual Studio Code, которое помогает разрабатывать приложения Teams, а также рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Средство командной строки, которое помогает разрабатывать приложения Teams, а также рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Шаблоны скриптов для автоматизации за пределами GitHub, Azure DevOps или Jenkins. |


## <a name="set-up-pipelines"></a>Настройка конвейеров

Конвейеры можно настроить на следующих платформах:

1. [Настройка конвейеров с помощью GitHub](#set-up-pipelines-with-github)
1. [Настройка конвейеров с помощью Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Настройка конвейеров с помощью Jenkins](#set-up-pipelines-with-jenkins)
1. [Настройка конвейеров для других платформ](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>Настройка конвейеров с помощью GitHub

Чтобы настроить конвейеры с GitHub ci/CD:

1. Создание шаблонов рабочих процессов.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.


## <a name="create-workflow-templates-with-github"></a>Создание шаблонов рабочих процессов с помощью GitHub

**Создание шаблонов рабочих процессов с помощью Teams набор средств в Visual Studio Code**

1. Создайте новый проект Teams с помощью Teams набор средств.
1. Выберите **Teams набор средств** на панели Visual Studio Code действий.
1. Выберите **"Добавить рабочие процессы CI/CD"**.
1. Выберите среду в командной строке.
1. Выберите **GitHub** в качестве поставщика CI/CD.
1. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision или Publish to Teams.
1. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
1. Следуйте файлам README, `.github/workflows` чтобы настроить рабочий процесс в GitHub.

**Создание шаблонов рабочих процессов с помощью CLI TeamsFx**

1. Введите `cd` Teams каталог проекта приложения.
2. Введите `teamsfx add cicd` команду, чтобы запустить интерактивный командный процесс.
3. Выберите среду в командной строке.
4. Выберите **GitHub** в качестве поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
8. Следуйте файлам README, `.github/workflows` чтобы настроить рабочий процесс в GitHub.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочих процессов, выполните ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-cicd-workflow"></a>Настройка рабочего процесса CI/CD

Вы можете изменить или удалить тестовые скрипты для настройки рабочего процесса CI/CD:

1. По умолчанию рабочий процесс CD активируется при выполнении новых фиксаций в ветви `main` .
1. При необходимости измените скрипты сборки.
1. Удалите тестовые скрипты по мере необходимости.

### <a name="set-up-pipelines-with-azure-devops"></a>Настройка конвейеров с помощью Azure DevOps

Чтобы настроить конвейеры с Azure DevOps ci/CD, с помощью этой команды:

1. Создание шаблонов рабочих процессов.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.


## <a name="create-workflow-templates-with-azure-devops"></a>Создание шаблонов рабочих процессов с помощью Azure DevOps

**Создание шаблонов рабочих процессов с помощью Teams набор средств в Visual Studio Code**

1. Создайте новый проект Teams с помощью Teams набор средств.
2. Выберите **Teams набор средств** на панели Visual Studio Code действий.
3. Выберите **"Добавить рабочие процессы CI/CD"**.
4. Выберите среду в командной строке.
5. Выберите **Azure DevOps** в качестве поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision и Publish для Teams.
7. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
8. Следуйте файлам README, `.azure/pipelines` чтобы настроить рабочий процесс в Azure DevOps.

**Создание шаблонов рабочих процессов с помощью CLI TeamsFx**

1. Введите `cd` Teams каталог проекта приложения.
2. Введите `teamsfx add cicd` команду, чтобы запустить интерактивный командный процесс.
3. Выберите среду в командной строке.
4. Выберите **Azure DevOps** в качестве поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
8. Следуйте файлам README, `.azure/pipelines` чтобы настроить рабочий процесс в Azure DevOps.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочих процессов, выполните ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

Ниже приведены изменения, которые можно внести в определение скрипта или рабочего процесса:

1. Используйте скрипт сборки npm или настройте способ сборки в коде автоматизации.
1. Используйте тестовый сценарий npm, который возвращает ноль для успешного выполнения, и измените тестовые команды.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Ниже приведены изменения, которые можно внести в определение скрипта или рабочего процесса:

1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает ноль для успешного выполнения, или измените тестовые команды.

### <a name="set-up-pipelines-with-jenkins"></a>Настройка конвейеров с помощью Jenkins

Чтобы настроить конвейеры с Jenkins для CI/CD, с помощью этой команды:

1. Создание шаблонов рабочих процессов.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.

## <a name="create-workflow-templates-with-jenkins"></a>Создание шаблонов рабочих процессов с помощью Jenkins

**Создание шаблонов рабочих процессов с помощью Teams набор средств в Visual Studio Code**

1. Создайте новый проект Teams с помощью Teams набор средств.
2. Выберите **Teams набор средств** на боковой Visual Studio Code панели.
3. Выберите **"Добавить рабочие процессы CI/CD"**.
4. Выберите среду в командной строке.
5. Выберите **Jenkins в качестве** поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
8. Следуйте файлам README, `.jenkins/pipelines` чтобы настроить рабочий процесс с помощью Jenkins.

**Создание шаблонов рабочих процессов с помощью CLI TeamsFx**

1. Введите `cd` Teams каталог проекта приложения.
2. Введите `teamsfx add cicd` команду, чтобы запустить интерактивный командный процесс.
3. Выберите среду в командной строке.
4. Выберите **Jenkins в качестве** поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих параметров: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, которые соответствуют вашим сценариям.
8. Следуйте файлам README, `.jenkins/pipelines` чтобы настроить рабочий процесс с помощью Jenkins.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочих процессов, выполните ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

Ниже приведены некоторые изменения, которые можно внести в проект:

1. Изменение способа активации потока CI. По умолчанию триггеры **pollSCM** используются при отправке нового изменения в **ветвь** разработки.
1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает ноль для успешного выполнения, или измените тестовые команды.


### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Чтобы настроить конвейер CD, выполните следующие действия.

1. Измените поток cd. По умолчанию используются триггеры `pollSCM` при отправке нового изменения в ветвь `main` .
1. При необходимости измените скрипты сборки.
1. Удалите тестовые скрипты, если у вас нет тестов.


### <a name="set-up-pipelines-for-other-platforms"></a>Настройка конвейеров для других платформ

Для создания и настройки конвейеров CI/CD на других платформах можно использовать стандартные примеры скриптов Bash.

* [Скрипты CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Скрипты CD](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Скрипты основаны на кроссплатформене средстве командной строки [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Вы можете установить его с помощью `npm install -g @microsoft/teamsfx-cli` документации [и](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) выполнить инструкции по настройке скриптов.

> [!NOTE]
>
> * Чтобы включить выполнение `@microsoft/teamsfx-cli` в режиме НЕПРЕРЫВНОЙ ИНТЕГРАЦИИ, включите `CI_ENABLED` .`export CI_ENABLED=true` В режиме НЕПРЕРЫВНОЙ ИНТЕГРАЦИИ `@microsoft/teamsfx-cli` удобно использовать CI/CD.
> * Чтобы включить `@microsoft/teamsfx-cli` выполнение в неинтерактивном режиме, задайте глобальную конфигурацию с помощью команды: `teamsfx config set -g interactive false`. В неинтерактивном режиме не `@microsoft/teamsfx-cli` запрашивает входные данные.

Убедитесь, что Azure Microsoft 365 учетные данные в переменных среды. Например, если вы используете GitHub в качестве репозитория исходного кода, см. раздел ["Секреты GitHub"](https://docs.github.com/en/actions/reference/encrypted-secrets).


## <a name="provision-and-deploy-resources"></a>Подготовка и развертывание ресурсов

Чтобы подготовить и развернуть ресурсы, предназначенные для Azure в CI/CD, необходимо создать субъект-службу Azure для использования.

Чтобы создать субъекты-службы Azure, выполните следующие действия.

1. Зарегистрируйте Microsoft Azure Active Directory (Azure AD) в одном клиенте.
2. Назначьте роль приложению Azure AD для доступа к подписке Azure. Рекомендуется `Contributor` использовать роль.
3. Создайте секрет приложения Azure AD.

> [!TIP]
> Сохраните идентификатор клиента, идентификатор приложения (AZURE_SERVICE_PRINCIPAL_NAME) и секрет (AZURE_SERVICE_PRINCIPAL_PASSWORD) для использования в будущем.

Дополнительные сведения см. в [руководстве по субъектам-службам Azure](/azure/active-directory/develop/howto-create-service-principal-portal). Ниже приведены три способа создания субъектов-служб.

* [Microsoft Azure портале](/azure/active-directory/develop/howto-create-service-principal-portal)
* [Windows PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Microsoft Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Публикация Teams с помощью портала Teams разработчика

При наличии изменений, связанных Teams файла манифеста приложения, можно обновить манифест и опубликовать Teams приложения.

Чтобы опубликовать Teams вручную, можно использовать портал разработчика [для Teams](https://dev.teams.microsoft.com/home).

Чтобы опубликовать приложение, выполните следующие действия:

1. Войдите на портал [разработчика Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
2. Импортируйте пакет приложения в ZIP-файле, выбрав .`App -> Import app -> Replace`
3. Выберите целевое приложение в списке приложений.
4. Опубликуйте приложение, выбрав .`Publish -> Publish to your org`

### <a name="see-also"></a>См. также

* [Краткое руководство по GitHub Actions](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Создание первого конвейера Azure DevOps конвейера](/azure/devops/pipelines/create-first-pipeline)
* [Создание первого конвейера Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Управление приложениями Microsoft Teams с помощью портала разработчика](/concepts/build-and-test/teams-developer-portal)
