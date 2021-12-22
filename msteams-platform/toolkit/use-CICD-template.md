---
title: Поддержка ci или CD для Teams разработчиков приложений
author: MuyangAmigo
description: Шаблоны CICD
ms.author: ruhe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: acd12a96365bf97bd419045c415e71efd3a118e2
ms.sourcegitcommit: aede47694894d281f6b725083bc0b46ab0e4846d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/22/2021
ms.locfileid: "61591780"
---
# <a name="ci-or-cd-support-for-teams-application-developers"></a>Поддержка ci или CD для Teams разработчиков приложений

TeamsFx помогает автоматизировать рабочий процесс разработки при создании Teams приложения. Документ предоставляет инструменты и предварительно приготовленные шаблоны для начала работы при настройке конвейеров ci или CD с наиболее популярными платформами разработки, включая GitHub, Azure Devops и Jenkins.

|Инструменты и шаблоны|Описание|
|---|---|
|[teamsfx-cli-action](https://github.com/OfficeDev/teamsfx-cli-action)|Готовый к использованию GitHub, который интегрируется с TeamsFx CLI.|
|[github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) и [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml)| GitHub ci или CD-шаблоны для Teams приложения. |
|[jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) и [jenkins-cd-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile)|Шаблоны ci Или CD Jenkins для Teams приложения.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) и [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Шаблоны скриптов для автоматизации повсюду за пределами GitHub. |

## <a name="ci-or-cd-workflow-templates-in-github"></a>Шаблоны рабочего процесса ci или CD в GitHub

**Включить рабочий процесс ci или CD** для автоматизации Teams разработки приложений в GitHub:

1. Создание папки под `.github/workflows`
1. Скопируйте файлы шаблонов (один или оба):
    * [github-ci-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-ci-template.yml) для рабочего процесса CI.
    * [github-cd-template.yml](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/github-cd-template.yml) для рабочего процесса CD.
1. Настройте эти процессы, чтобы соответствовать вашим сценариям.

### <a name="customize-ci-workflow"></a>Настройка рабочего процесса CI

Чтобы адаптировать рабочий процесс для проекта, можно внести следующие изменения:

1. Измените, как запускается поток CI. По умолчанию по умолчанию создается запрос на тягу для `dev` филиала.
1. Используйте сценарий сборки npm или настройте способ создания проекта в коде автоматизации.
1. Используйте тестовый сценарий npm, который возвращает ноль для успеха и/или меняет команды тестирования.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Следующие действия по настройке рабочего процесса CD:

1. По умолчанию запускается рабочий процесс CD, когда в филиале будут сделаны новые `main` коммиты.
1. Создание GitHub [в среде](https://docs.github.com/en/actions/reference/encrypted-secrets) для удержания учетных данных Azure или Microsoft 365 входа. В следующей таблице перечислены все секреты, которые необходимо создать в GitHub, а для подробного использования обратитесь к GitHub Действия [README.md](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md).
1. При необходимости измените сценарии сборки.
1. Удалите тестовые скрипты, если у вас нет тестов.

> [!Note]
> Этап предоставления не входит в шаблон CD, так как обычно выполняется только один раз. Можно выполнить положение в Teams набор средств, TeamsFx CLI или с помощью отдельного рабочего процесса. Пожалуйста, не забудьте о фиксации после подготовка (результаты подготовка будут депонироваться в папке) и сохранить содержимое файла в GitHub хранилища с именем для будущего `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` [](https://docs.github.com/en/actions/reference/encrypted-secrets) `USERDATA_CONTENT` использования.

### <a name="environment-variables"></a>Переменные среды

Действия по созданию переменных среды в GitHub::

1. На странице **проекта Параметры** перейдите в раздел **Environments** и выберите новую **среду.**
1. Введите имя для среды. Имя среды по умолчанию, предоставленное в шаблоне, `test_environment` является . Выберите **Настройка среды для** работы.
1. На следующей странице выберите **добавить секрет,** чтобы добавить секреты для каждого из элементов, перечисленных в таблице ниже.

|Имя|Описание|
|---|---|
|AZURE_ACCOUNT_NAME|Имя учетной записи Azure, используемой для предоставления ресурсов.|
|AZURE_ACCOUNT_PASSWORD|Пароль учетной записи Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|Microsoft 365_ACCOUNT_NAME|Учетная Microsoft 365 для создания и публикации Teams App.|
|Microsoft 365_ACCOUNT_PASSWORD|Пароль учетной записи Microsoft 365.|
|Microsoft 365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Узнайте больше о том, как найти [Microsoft 365 клиента.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> [!NOTE]
> Обратитесь к учетным данным [Configure Microsoft 365 Или Azure,](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) чтобы убедиться, что вы отключили многофакторную проверку подлинности и по умолчанию безопасности для учетных данных, используемых в рабочего процесса.

## <a name="set-up-ci-or-cd-pipelines-with-azure-devops"></a>Настройка ci или CD-Pipelines с Azure DevOps

Вы можете настроить автоматические конвейеры в Azure DevOps и сделать ссылку на скрипты. Выполните шаги, которые приведены ниже, чтобы начать работу:

* [Скрипты CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

### <a name="set-up-ci-pipeline"></a>Настройка ci Pipeline

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

Возможные изменения, которые можно внести для определения скрипта или рабочего процесса:

1. Измените, как запускается поток CI. По умолчанию мы отодвигаем новый коммит в `dev` ветвь.
1. Измените способ установки узла и npm.
1. Используйте сценарий сборки npm или настройте способ сборки в коде автоматизации.
1. Используйте тестовый сценарий npm, который возвращает нулевой для успеха и/или меняет команды тестирования.

### <a name="set-up-cd-pipeline"></a>Настройка конвейера CD

1. Добавьте [cd-скрипты](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) в Azure DevOps репозиторий и сделайте необходимые настройки, как вы можете сделать вывод из комментариев в файле скрипта.
1. Создайте Azure DevOps конвейера для CD, как вы можете ссылаться на [эту ссылку](/azure/devops/pipelines/create-first-pipeline). Определение Конвейера можно сослаться на следующее определение примера для CI Pipeline.
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

- task: DownloadSecureFile@1
  name: userdata
  inputs:
    secureFile: 'staging.userdata'
- task: Bash@3
  inputs:
    targetType: 'inline'
    script: |
      mkdir -p .fx/states/
      cp $(userdata.secureFilePath) .fx/states/staging.userdata
  
- task: Bash@3
  env:
    AZURE_ACCOUNT_NAME: $(AZURE_ACCOUNT_NAME)
    AZURE_ACCOUNT_PASSWORD: $(AZURE_ACCOUNT_PASSWORD)
    AZURE_TENANT_ID: $(AZURE_TENANT_ID)
    Microsoft 365_ACCOUNT_NAME: $(Microsoft 365_ACCOUNT_NAME)
    Microsoft 365_ACCOUNT_PASSWORD: $(Microsoft 365_ACCOUNT_PASSWORD)
  inputs:
    filePath: './others-script-cd-template.sh'
```

Возможные изменения, которые можно внести для определения скрипта или рабочего процесса:

1. Как запускается поток CD. По умолчанию это происходит, когда в главную ветвь будут сделаны новые **коммиты.**
1. Измените способ установки узла и npm.
1. Измените имя среды, по умолчанию его **постановка**.
1. Убедитесь, что у вас есть сценарий сборки npm или настройка способа сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает нулевой для успеха и/или измените команды тестирования.

> [!Note]
> Этап предоставления не входит в шаблон CD, так как обычно выполняется только один раз. Можно выполнить положение в Teams набор средств, TeamsFx CLI или с помощью разделенного рабочего процесса. Пожалуйста, не забудьте о фиксации после подготовка (результаты подготовка будут депонироваться в папке) и загрузить в Azure DevOps безопасные файлы `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` для будущего использования. [](/azure/devops/pipelines/library/secure-files)

### <a name="environment-variables-for-azure-devops"></a>Переменные среды для Azure DevOps

Действия по созданию переменных Pipeline в Azure DevOps:

1. На странице редактирования конвейера выберите **Переменные** в правом верхнем справа и выберите **новую переменную.**
1. Введите пару Name/Value для переменной.
1. Чтобы при необходимости засекретить это **значение,** загляйте в почтовый ящик.
1. Выберите **ОК** для создания переменной.

|Имя|Описание|
|---|---|
|AZURE_ACCOUNT_NAME|Имя учетной записи Azure, используемой для предоставления ресурсов.|
|AZURE_ACCOUNT_PASSWORD|Пароль учетной записи Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|Microsoft 365_ACCOUNT_NAME|Учетная Microsoft 365 для создания и публикации Teams App.|
|Microsoft 365_ACCOUNT_PASSWORD|Пароль учетной записи Microsoft 365.|
|Microsoft 365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Узнайте больше о том, как найти [Microsoft 365 клиента.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|

> [!NOTE]
> Этап предоставления не входит в шаблон CD, так как обычно выполняется только один раз. Можно выполнить положение в Teams набор средств, TeamsFx CLI или с помощью разделенного рабочего процесса. Пожалуйста, не забудьте совершить после подготовка (результаты подготовка будут депонироваться в папке) и сохранить содержимое файла в учетных данных `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` Jenkins для будущего использования.

## <a name="ci-or-cd-pipeline-templates-in-jenkins"></a>Шаблоны конвейера CI или CD в Дженкинсе

Чтобы добавить эти шаблоны в репозиторий, вам потребуется версия [jenkins-ci-template. Jenkinsfile](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-ci-template.Jenkinsfile) и  [jenkins-cd-template. Jenkinsfile,](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/jenkins-cd-template.Jenkinsfile) который будет расположен в репозитории по филиалу.

Кроме того, необходимо создать ci или CD-конвейеры в Дженкинсе, которые указывают на конкретный **Jenkinsfile** соответственно.

Выполните следующие действия, чтобы проверить, как подключить Jenkins к различным платформам SCM:

1. [Дженкинс с GitHub](https://www.jenkins.io/solutions/github/)
2. [Дженкинс с Azure DevOps](https://www.dragonspears.com/blog/ci-cd-with-jenkins-and-azure-devops-services)
3. [Дженкинс с GitLab](https://docs.gitlab.com/ee/integration/jenkins.html)
4. [Jenkins with Bitbucket](https://medium.com/ampersand-academy/integrate-bitbucket-jenkins-c6e51103d0fe)

### <a name="customize-ci-pipeline"></a>Настройка конвейера CI

Существует несколько возможных изменений, которые можно внести для адаптации проекта:

1. Переименуй файл шаблона в **Jenkinsfile,** так как это распространенная практика, и поместите его под целевую ветвь, например, **ветвь разработчиков.**
1. Измените, как запускается поток CI. Мы по умолчанию используем триггеры **pollSCM** при нажатии нового изменения в **ветвь разработчиков.**
1. Убедитесь, что у вас есть сценарий сборки npm или настройка способа сборки в коде автоматизации.
1. Убедитесь, что у вас есть тестовый сценарий npm, который возвращает нулевой для успеха и/или измените команды тестирования.

### <a name="customize-cd-pipeline"></a>Настройка конвейера CD

Измените следующие действия, чтобы настроить конвейер CD:

1. Переименуй файл шаблона в **Jenkinsfile,** так как это распространенная практика, и поместите его под целевую ветвь, например, **главную ветвь.**
1. Как запускается поток CD. Мы по умолчанию используем триггеры **pollSCM** при нажатии нового изменения в **главную ветвь.**
1. Создайте учетные данные [конвейера](https://www.jenkins.io/doc/book/using/using-credentials/) Jenkins для удержания учетных данных Azure/Microsoft 365 входа. В таблице ниже перечислены все учетные данные, которые необходимо создать в Jenkins.
1. При необходимости измените сценарии сборки.
1. Удалите тестовые скрипты, если у вас нет тестов.

> [!Note]
 Этап предоставления не входит в шаблон CD, так как обычно выполняется только один раз. Можно выполнить положение в Teams набор средств, TeamsFx CLI или с помощью отдельного рабочего процесса. Пожалуйста, не забудьте совершить после подготовка (результаты подготовка будут депонироваться в папке) и сохранить содержимое файла в учетных данных `.fx` `.fx/states/{YOUR_ENV_NAME}.userdata` Jenkins для будущего использования.

### <a name="environment-variables-for-jenkins"></a>Переменные среды для Jenkins

Выполните [использование учетных данных](https://www.jenkins.io/doc/book/using/using-credentials/) для создания учетных данных в Jenkins.

|Имя|Описание|
|---|---|
|AZURE_ACCOUNT_NAME|Имя учетной записи Azure, используемой для предоставления ресурсов.|
|AZURE_ACCOUNT_PASSWORD|Пароль учетной записи Azure.|
|AZURE_SUBSCRIPTION_ID|Определение подписки, в которой будут предусмотрены ресурсы.|
|AZURE_TENANT_ID|Определение клиента, в котором находится подписка.|
|Microsoft 365_ACCOUNT_NAME|Учетная запись M3icrosoft 365 для создания и публикации Teams App.|
|Microsoft 365_ACCOUNT_PASSWORD|Пароль учетной записи Microsoft 365.|
|Microsoft 365_TENANT_ID|Определение клиента, в котором Teams будет создано или опубликовано приложение. Это значение является необязательным, если у вас нет учетной записи с несколькими клиентами и вы хотите использовать другого клиента. Узнайте больше о том, как найти [Microsoft 365 клиента.](/azure/active-directory/fundamentals/active-directory-how-to-find-tenant)|
> Примечание. Обратитесь к учетным данным [Configure Microsoft 365 или Azure,](https://github.com/OfficeDev/teamsfx-cli-action/blob/main/README.md#configure-m365azure-credentials-as-github-secret) чтобы убедиться, что вы отключили многофакторную проверку подлинности и по умолчанию безопасности для учетных данных, используемых в конвейере.

## <a name="get-started-guide-for-other-platforms"></a>Начало руководства для других платформ

Вы можете следовать перечисленным заранее заранее определенным сценариям bash для создания и настройки ci или CD-конвейеров на других платформах:

* [Скрипты CI](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [Cd Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh) Сценарии довольно просты, и большинство частей из них являются межплатформенными CLI, поэтому их легко преобразовать в другие типы скриптов, например PowerShell.

Сценарии основаны на средстве командной строки TeamsFx [teamsFx teamsFx-CLI.](https://www.npmjs.com/package/@microsoft/teamsfx-cli) Вы можете установить его с `npm install -g @microsoft/teamsfx-cli` [документацией и следовать](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) за ней, чтобы настроить сценарии.

> [!Note]
> Чтобы включить `@microsoft/teamsfx-cli` работу в режиме CI, включив `CI_ENABLED` `export CI_ENABLED=true` . В режиме CI `@microsoft/teamsfx-cli` удобно для ci или CD.

Убедитесь в безопасном наборе учетных данных Azure и M365 в переменных среды. Например, если вы используете GitHub в качестве хранилища исходных кодов, можно использовать [секреты Github](https://docs.github.com/en/actions/reference/encrypted-secrets) для безопасного хранения переменных среды.

## <a name="publish-teams-app-using-teams-developer-portal"></a>Публикация Teams с помощью Teams портала разработчиков

Если в файле манифеста Teams изменения, возможно, Teams приложение для обновления манифеста.

Чтобы опубликовать Teams приложение вручную, вы можете использовать [портал разработчика для Teams.](https://dev.teams.microsoft.com/home)

**Публикация приложения**

1. Вопишите [на портале разработчиков Teams](https://dev.teams.microsoft.com) с помощью соответствующей учетной записи.
2. Импорт пакета приложения в zip путем выбора `App -> Import app -> Replace` .
3. Выберите целевое приложение в списке приложений и перейдите на страницу обзоров.
4. Публикация приложения путем выбора `Publish -> Publish to your org`

### <a name="see-also"></a>См. также

* [Быстрый запуск для GitHub действий](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Создание первого Azure DevOps конвейера](/azure/devops/pipelines/create-first-pipeline)
* [Создание первого конвейера Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
