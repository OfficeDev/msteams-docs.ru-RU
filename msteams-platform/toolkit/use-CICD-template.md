---
title: Поддержка ci или CD для Teams разработчиков приложений
author: MuyangAmigo
description: Шаблоны CICD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: b8a6506707626a80cabc9c730eef6fe11160e386
ms.sourcegitcommit: 7cccec0b2512f4e9366eb7c88998c5181a52681d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059070"
---
# <a name="cicd-guide"></a>Руководство по CI/CD

TeamsFx помогает автоматизировать рабочий процесс разработки при создании Teams приложения. Документ предоставляет инструменты и шаблоны для начала работы с настройкой конвейеров ci или CD с GitHub, Azure Devops и Jenkins.

|Инструменты и шаблоны|Описание| 
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|GitHub действия, которые интегрируются с TeamsFx CLI.|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) и [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub или CD-шаблоны для Teams приложения. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) и [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Шаблоны ci Или CD Jenkins для Teams приложения.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) и [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Шаблоны скриптов для автоматизации за пределами GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Шаблоны рабочего процесса ci или CD в GitHub

**Включить рабочий процесс ci или CD** для автоматизации Teams разработки приложений в GitHub:

1. Создание папки под `.github/workflows`
1. Скопируйте один из следующих файлов шаблона:
    * [github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) для рабочего процесса CI.
    * [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) для рабочего процесса CD.
1. Настройка процессов, подходящих для сценариев.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

Выполните следующие действия, чтобы адаптировать рабочий процесс для проекта:

1. Измените поток CI. 
1. Используйте сценарий сборки npm или настройте способ создания проекта в коде автоматизации.
1. Используйте тестовый сценарий npm, который возвращает нулевой для успеха, и измените команды тестирования.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Выполните следующие действия по настройке рабочего процесса CD:

1. По умолчанию запускается рабочий процесс CD, когда в филиале будут сделаны новые `main` коммиты.
1. Создание GitHub [для среды](https://docs.github.com/en/actions/reference/encrypted-secrets) для удержания основных учетных данных служб Azure и учетных данных учетных записей M365. Дополнительные сведения см. [в GitHub Действия.](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md)
1. При необходимости измените сценарии сборки.
1. Удалите тестовые скрипты по мере необходимости.

> [!NOTE]
> Этап предоставления не входит в шаблон CD, так как обычно выполняется только один раз. Можно выполнить предоставление в Teams набор средств, TeamsFx CLI или с помощью отдельного рабочего процесса. Убедитесь в том, что после предварительной фиксации. Результаты подготовка откладываются в `.fx` папку.

### <a name="github-secrets"></a>Секреты Github

В следующей таблице перечислены все секреты, необходимые для создания среды в GitHub:

1. Выберите **Настройки**.
1. Перейдите в **раздел Environments.**
1. Выберите **новую среду.**
1. Введите имя для среды. Имя среды по умолчанию, предоставленное в шаблоне, `test_environment` является . 
1. Выберите **Настройка среды.**
1. Выберите **Добавить секрет**.

В следующей таблице перечислены все секреты, необходимые для создания среды:

|Имя|Описание|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|Основное имя службы Azure, используемого для предоставления ресурсов.|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Пароль директора службы Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|M365_ACCOUNT_NAME|Учетная запись M365 для создания и публикации Teams приложения.|
|M365_ACCOUNT_PASSWORD|Пароль учетной записи M365.|
|M365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Дополнительные сведения см. в том, как найти [ваш ID клиента M365.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|


> [!NOTE]
> В настоящее время принцип службы Azure используется в рабочего процессах CI/CD. Дополнительные сведения см. в [дополнительных сведениях о создании принципов службы Azure.](#create-azure-service-principals)

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Настройка конвейеров ci или CD с помощью Azure DevOps

Вы можете настроить автоматические конвейеры в Azure DevOps и сделать ссылку на скрипты.

Выполните следующие действия, чтобы приступить к работе:

* [Скрипты CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Настройка конвейера CI

1. Добавьте [ci Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) в Azure DevOps репозиторий и сделайте необходимые настройки, как вы можете сделать вывод из комментариев в файле скрипта.
1. Выполните [действия по созданию Azure DevOps pipeline для CI.](/azure/devops/pipelines/create-first-pipeline)
Вот сценарий общих сценариев конвейера ci:

```yml
trigger:
- dev 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  inputs:
    filePath: './others-script-ci-template.sh'
```

Ниже приводится изменение, которое можно внести для определения скрипта или рабочего процесса:

1. Измените поток CI. По умолчанию мы отодвигаем новый коммит в `dev` ветвь.
1. Измените способ установки узла и npm.
1. Используйте сценарий сборки npm или настройте способ сборки в коде автоматизации.
1. Используйте тестовый сценарий npm, который возвращает нулевой для успеха, и измените команды тестирования.

### <a name="set-up-cd-pipeline"></a>Настройка конвейера CD

1. Добавьте [cd-скрипты](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) в Azure DevOps репозиторий и сделайте необходимые настройки, как вы можете сделать вывод из комментариев в файле скрипта.
1. Создайте Azure DevOps конвейера для компакт-диска. Дополнительные сведения см. в [создании первого конвейера.](/azure/devops/pipelines/create-first-pipeline) Определение Конвейера можно сослаться на следующее определение примера для CI Pipeline.
1. Добавьте необходимые переменные [по Определению](/azure/devops/pipelines/process/variables)переменных и при необходимости сделайте их секретами.

```yml
trigger:
- main 

pool:
  vmImage: ubuntu-latest

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '14.17.0'
    checkLatest: true
  
- task: Bash@3
  env:
    SP_NAME: $(AZURE_SERVICE_PRINCIPAL_NAME)
    SP_PASSWORD: $(AZURE_SERVICE_PRINCIPAL_PASSWORD)
    TENANT_ID: $(AZURE_TENANT_ID)
    AZURE_SUBSCRIPTION_ID: $(AZURE_SUBSCRIPTION_ID)
    M365_ACCOUNT_NAME: $(M365_ACCOUNT_NAME)
    M365_ACCOUNT_PASSWORD: $(M365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Ниже приводится изменение, которое можно внести для определения скрипта или рабочего процесса:

1. Как запускается поток CD. По умолчанию это происходит, когда в главную ветвь будут сделаны новые **коммиты.**
1. Измените способ установки узла и npm.
1. Измените имя среды, по умолчанию его **постановка**.
1. Убедитесь, что у вас есть сценарий сборки npm или настройка способа сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает нулевой для успеха и/или измените команды тестирования.

### <a name="pipeline-variables-for-azure-devops"></a>Переменные конвейера для Azure DevOps

Выполните следующие действия для создания переменных Pipeline в Azure DevOps:

1. На странице редактирования конвейера выберите **Переменные** и выберите **новую переменную.**
1. Введите имя или пару значений для переменной.
1. Чтобы при необходимости засекретить это **значение,** загляйте в почтовый ящик.
1. Выберите **ОК** для создания переменной.

|Имя|Описание|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|Основное имя службы Azure, используемого для предоставления ресурсов.|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Пароль директора службы Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|M365_ACCOUNT_NAME|Учетная запись M365 для создания и публикации Teams App.|
|M365_ACCOUNT_PASSWORD|Пароль учетной записи M365.|
|M365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Узнайте больше о том, как найти [ваш ID клиента M365](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Шаблоны конвейера CI или CD в Дженкинсе

Чтобы добавить эти шаблоны в репозиторий, вы осквите версии [jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) и  [jenkins-cd-template. Jenkinsfile,](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) который будет расположен в репозитории по филиалу.

Кроме того, необходимо создать ci или CD-конвейеры в Дженкинсе, которые указывают на конкретный **Jenkinsfile** соответственно.

Выполните следующие действия, чтобы проверить, как подключить Jenkins к различным платформам SCM:

1. [Дженкинс с GitHub](https://www.jenkins.io/solutions/github/)
2. [Дженкинс с Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Дженкинс с GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins with Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Настройка конвейера CI

Ниже приводится ряд изменений, которые можно внести для адаптации проекта:

1. Переименуй файл шаблона в **Jenkinsfile** и поместите его под целевую ветвь, например **ветвь разработчика.**
1. Измените, как запускается поток CI. Мы по умолчанию используем триггеры **pollSCM** при нажатии нового изменения в **ветвь разработчиков.**
1. Убедитесь, что у вас есть сценарий сборки npm или настройка способа сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает нулевой для успеха и/или измените команды тестирования.

### <a name="customize-cd-pipeline"></a>Настройка конвейера CD

Выполните следующие действия по настройке конвейера CD:

1. Переименуй файл шаблона в **Jenkinsfile** и поместите его под целевую ветвь, например **главную ветвь.**
1. Измените поток компакт-дисков. Мы по умолчанию используем триггеры **pollSCM** при нажатии нового изменения в **главную ветвь.**
1. Создайте учетные данные [конвейера](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins для удержания основных учетных данных служб Azure и учетных данных учетных записей M365.
1. При необходимости измените сценарии сборки.
1. Удалите тестовые скрипты, если у вас нет тестов.

### <a name="credentials-for-jenkins"></a>Учетные данные для Jenkins

Выполните [использование учетных данных](https://www.jenkins.io/doc/book/using/using-credentials/) для создания учетных данных в Jenkins.

|Имя|Описание|
|---|---|
|AZURE_SERVICE_PRINCIPAL_NAME|Основное имя службы Azure, используемого для предоставления ресурсов.|
|AZURE_SERVICE_PRINCIPAL_PASSWORD|Пароль директора службы Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|M365_ACCOUNT_NAME|Учетная запись M365 для создания и публикации Teams App.|
|M365_ACCOUNT_PASSWORD|Пароль учетной записи M365.|
|M365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Узнайте больше о том, как найти [ваш ID клиента M365](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant).|

## <a name="get-started-guide-for-other-platforms"></a>Начало руководства для других платформ

Вы можете следовать перечисленным заранее заранее определенным сценариям bash для создания и настройки ci или CD-конвейеров на других платформах:

* [Скрипты CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Сценарии основаны на средстве командной строки TeamsFx [teamsFx teamsFx-CLI.](https://www.npmjs.com/package/@microsoft/teamsfx-cli) Вы можете установить его с `npm install -g @microsoft/teamsfx-cli` [документацией и следовать](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) за ней, чтобы настроить сценарии.

> [!NOTE]
> * Чтобы включить `@microsoft/teamsfx-cli` работу в режиме CI, включив `CI_ENABLED` `export CI_ENABLED=true` . В режиме CI `@microsoft/teamsfx-cli` удобно для ci или CD.
> * Чтобы включить `@microsoft/teamsfx-cli` работу в неинактивном режиме, установите глобальную конфигуру с командой: `teamsfx config set -g interactive false` . В неинактивном `@microsoft/teamsfx-cli` режиме не будет задавать вопросы для входных данных в интерактивном режиме.

Убедитесь в безопасном наборе учетных данных Azure и M365 в переменных среды. Например, если вы используете GitHub в качестве хранилища исходных кодов. Дополнительные сведения см. в [дополнительных сведениях в github Secrets.](https://docs.github.com/en/actions/reference/encrypted-secrets)

## <a name="create-azure-service-principals"></a>Создание принципов служб Azure

Для обеспечения и развертывания ресурсов, нацеленных на Azure в ci/CD, необходимо создать главную службу Azure для использования.

Выполните следующие действия для создания принципов служб Azure:
1. Регистрация приложения Azure AD в одном клиенте.
2. Назначьте роль приложению Azure AD для доступа к подписке Azure, и рекомендуется `Contributor` роль. 
3. Создайте новый секрет приложения Azure AD.

> [!TIP]
> Сохраните ваш id клиента, id приложения (AZURE_SERVICE_PRINCIPAL_NAME) и секрет (AZURE_SERVICE_PRINCIPAL_PASSWORD) для будущего использования.

Дополнительные сведения см. в [руководстве по принципам](/azure/active-directory/develop/howto-create-service-principal-portal)служб Azure. Ниже 3 способа создания основной службы: 
* [Портал Azure](/azure/active-directory/develop/howto-create-service-principal-portal)
* [PowerShell](/azure/active-directory/develop/howto-authenticate-service-principal-powershell)
* [Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)

## <a name="publish-teams-app-using-teams-developer-portal"></a>Публикация Teams с помощью Teams портала разработчиков
Если в файле манифеста Teams изменения, возможно, Teams приложение для обновления манифеста.

Чтобы опубликовать Teams приложение вручную, вы можете использовать [портал разработчика для Teams.](https://dev.teams.microsoft.com/home)

Выполните следующие действия для публикации приложения:
1. Во входе на портал [разработчика для Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
2. Импорт пакета приложения в zip путем выбора `App -> Import app -> Replace` .
3. Выберите целевое приложение в списке приложений.
4. Публикация приложения путем выбора `Publish -> Publish to your org`

### <a name="see-also"></a>См. также

* [Быстрый запуск для GitHub действий](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Создание первого Azure DevOps конвейера](/azure/devops/pipelines/create-first-pipeline)
* [Создание первого конвейера Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Управление приложениями с помощью портала разработчиков для Microsoft Teams](/concepts/build-and-test/teams-developer-portal)
