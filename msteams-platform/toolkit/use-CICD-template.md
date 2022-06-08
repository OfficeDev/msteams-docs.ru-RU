---
title: Узнайте, как использовать шаблоны конвейера CI/CD в GitHub, Azure DevOps и Jenkins для разработчиков приложений Teams.
author: MuyangAmigo
description: Шаблоны CI/CD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: c39ad23fe42fd9cfd97ae2fcf49390cf19fac4a2
ms.sourcegitcommit: ff31cbe4840191f004d8fc61dd4fd93d35fcaecb
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/07/2022
ms.locfileid: "65938935"
---
# <a name="set-up-cicd-pipelines"></a>Настройка конвейеров CI/CD

TeamsFx помогает автоматизировать рабочий процесс разработки при создании приложения Teams. Ниже приведены инструменты и шаблоны, которые можно использовать для настройки конвейеров CI/CD, создания шаблонов рабочих процессов и настройки рабочего процесса CI/CD с помощью GitHub, Azure DevOps, Jenkins и других платформ. Чтобы подготовить и развернуть ресурсы, вы можете создать субъекты-службы Azure и опубликовать приложение Teams с помощью портала разработчиков Teams. Чтобы опубликовать приложение Teams вручную, вы можете использовать [Портал разработчика для Teams](https://dev.teams.microsoft.com/home).

|Инструменты и шаблоны | Описание |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|Действие GitHub, которое интегрируется с TeamsFx CLI.|
|[Набор инструментов Teams в Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Расширение Visual Studio Code, помогающее разрабатывать приложения Teams и рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Инструмент командной строки, помогающий разрабатывать приложения Teams и рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) и [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Шаблоны скриптов для автоматизации за пределами GitHub, Azure DevOps или Jenkins. |

## <a name="set-up-pipelines"></a>Настройка конвейеров

Вы можете настроить конвейеры на следующих платформах:

1. [Настройка конвейеров с помощью GitHub](#set-up-pipelines-with-github)
1. [Настройка конвейеров с помощью Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Настройка конвейеров с помощью Jenkins](#set-up-pipelines-with-jenkins)
1. [Настройка конвейеров для других платформ](#set-up-pipelines-for-other-platforms)

## <a name="set-up-pipelines-with-github"></a>Настройка конвейеров с помощью GitHub

Чтобы настроить конвейеры с GitHub для CI/CD:

* Создание шаблонов рабочего процесса.

  * Visual Studio Code
  * TeamsFx CLI

* Настройка рабочего процесса CI/CD.

### <a name="create-workflow-templates"></a>Создание шаблонов рабочих процессов

С помощью GitHub можно создать следующие шаблоны рабочих процессов:

**Набор инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
1. **Щелкните значок** :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API"::: значка Набора средств Teams на панели навигации слева.
1. Выберите **Добавить рабочие процессы CI/CD.**.
1. Выберите среду из командной строки.
1. Выберите **GitHub** в качестве поставщика CI/CD.
1. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
1. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
1. Следуйте файлам README в разделе `.github/workflows`, чтобы настроить рабочий процесс в GitHub.

**TeamsFx CLI**

1. Войдите `cd` в каталог проекта приложения Teams.
2. Введите команду, `teamsfx add cicd`, чтобы запустить процесс интерактивной команды.
3. Выберите среду из командной строки.
4. Выберите **GitHub** в качестве поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.github/workflows`, чтобы настроить рабочий процесс в GitHub.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочего процесса, вы можете выполнить ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-cicd-workflow"></a>Настройка рабочего процесса CI/CD

Вы можете изменить или удалить сценарии тестирования, чтобы настроить рабочий процесс CI/CD:

1. По умолчанию рабочий процесс CD запускается, когда в ветку `main` вносятся новые фиксации.
1. При необходимости измените сценарии сборки.
1. При необходимости удалите тестовые сценарии.

## <a name="set-up-pipelines-with-azure-devops"></a>Настройка конвейеров с помощью Azure DevOps

Чтобы настроить конвейеры с помощью Azure DevOps для CI/CD:

* Создание шаблонов рабочего процесса.

  * Visual Studio Code
  * TeamsFx CLI

* Настройка рабочего процесса CI/CD.

### <a name="create-workflow-templates"></a>Создание шаблонов рабочих процессов

С помощью Azure DevOps можно создать следующие шаблоны рабочих процессов:

**Набор инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
2. **Щелкните значок** :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API"::: значка Набора средств Teams на панели навигации слева.
3. Выберите **Добавить рабочие процессы CI/CD.**.
4. Выберите среду из командной строки.
5. Выберите **Azure DevOps** в качестве поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision и Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.azure/pipelines`, чтобы настроить рабочий процесс в Azure DevOps.

**TeamsFx CLI**

1. Войдите `cd` в каталог проекта приложения Teams.
2. Введите команду, `teamsfx add cicd`, чтобы запустить процесс интерактивной команды.
3. Выберите среду из командной строки.
4. Выберите **Azure DevOps** в качестве поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.azure/pipelines`, чтобы настроить рабочий процесс в Azure DevOps.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочего процесса, вы можете выполнить ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

Для определения скрипта или рабочего процесса можно внести следующие изменения:

1. Используйте скрипт сборки npm или настройте способ сборки кода автоматизации.
1. Используйте тестовый скрипт npm, который возвращает null в случае успеха, и измените тестовые команды.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Для определения скрипта или рабочего процесса можно внести следующие изменения:

1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки кода автоматизации.
1. Убедитесь, что у вас есть тестовый скрипт npm, который возвращает null в случае успеха, или измените тестовые команды.

## <a name="set-up-pipelines-with-jenkins"></a>Настройка конвейеров с помощью Jenkins

Чтобы настроить конвейеры с Jenkins для CI/CD:

* Создание шаблонов рабочего процесса.

  * Visual Studio Code
  * TeamsFx CLI

* Настройка рабочего процесса CI/CD.

### <a name="create-workflow-templates"></a>Создание шаблонов рабочих процессов

С помощью Jenkins можно создать следующие шаблоны рабочих процессов:

**Набор инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
2. **Щелкните значок** :::image type="icon" source="../assets/images/teams-toolkit-v2/add-API/api-add-icon.png" alt-text="API"::: значка Набора средств Teams на панели навигации слева.
3. Выберите **Добавить рабочие процессы CI/CD.**.
4. Выберите среду из командной строки.
5. Выберите **Jenkins** в качестве поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.jenkins/pipelines`, чтобы настроить рабочий процесс с Jenkins.

**TeamsFx CLI**

1. Войдите `cd` в каталог проекта приложения Teams.
2. Введите команду, `teamsfx add cicd`, чтобы запустить процесс интерактивной команды.
3. Выберите среду из командной строки.
4. Выберите **Jenkins** в качестве поставщика CI/CD.
5. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.jenkins/pipelines`, чтобы настроить рабочий процесс с Jenkins.

> [!NOTE]
> Если вам нужно добавить дополнительные шаблоны рабочего процесса, вы можете выполнить ту же процедуру, чтобы создать шаблон рабочего процесса в Visual Studio Code или TeamsFx CLI.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

В проект можно внести следующие изменения:

1. Измените способ запуска потока CI. По умолчанию используются триггеры **pollSCM**, когда новое изменение помещается в ветку **dev**.
1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки кода автоматизации.
1. Убедитесь, что у вас есть тестовый скрипт npm, который возвращает null в случае успеха, или измените тестовые команды.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Выполните следующие шаги, чтобы настроить конвейер компакт-дисков:

1. Измените поток CD. По умолчанию используются триггеры `pollSCM`, когда новое изменение помещается в ветку `main`.
1. При необходимости измените сценарии сборки.
1. Удалите тестовые сценарии, если у вас нет тестов.

## <a name="set-up-pipelines-for-other-platforms"></a>Настройка конвейеров для других платформ

Вы можете следовать предопределенным перечисленным сценариям bash для создания и настройки конвейеров CI/CD на других платформах:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Скрипты основаны на кроссплатформенном инструменте командной строки TeamsFx [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Вы можете установить его `npm install -g @microsoft/teamsfx-cli` и следовать [документации](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), чтобы настроить скрипты.

> [!NOTE]
>
> * Чтобы включить `@microsoft/teamsfx-cli` работающий в режиме CI, включите `CI_ENABLED` с помощью `export CI_ENABLED=true`. В режиме CI `@microsoft/teamsfx-cli` подходит для CI/CD.
> * Чтобы `@microsoft/teamsfx-cli` работал в неинтерактивном режиме, установите глобальный config командой: `teamsfx config set -g interactive false`. В неинтерактивном режиме `@microsoft/teamsfx-cli` не требует ввода.

Обязательно настройте учетные данные Azure и Microsoft 365 в переменных среды безопасно. Например, если вы используете GitHub в качестве репозитория исходного кода, см. [секреты GitHub](https://docs.github.com/en/actions/reference/encrypted-secrets)

## <a name="provision-and-deploy-resources"></a>Подготовка и развертывание ресурсов

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

## <a name="publish-teams-app-using-teams-developer-portal"></a>Публикация приложения Teams с помощью портала разработчиков Teams

При наличии каких-либо изменений, связанных с файлом манифеста приложения Teams, вы можете обновить манифест и снова опубликовать приложение Teams. Чтобы опубликовать приложение Teams вручную, вы можете использовать [Портал разработчика для Teams](https://dev.teams.microsoft.com/home).

Выполните следующие шаги, чтобы опубликовать приложение:

1. Войдите на портал [разработчика для Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
2. Импортируйте пакет приложения в ZIP-файле и выберите .`App -> Import app -> Replace`
3. Выберите целевое приложение в списке приложений.
4. Опубликуйте приложение, выберите .`Publish -> Publish to your org`

### <a name="see-also"></a>Дополнительные ресурсы

* [Быстрый старт для действий GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Создайте свой первый конвейер Azure DevOps.](/azure/devops/pipelines/create-first-pipeline)
* [Создайте свой первый конвейер Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Управление приложениями Microsoft Teams с помощью портала разработчика](../concepts/build-and-test/teams-developer-portal.md)
