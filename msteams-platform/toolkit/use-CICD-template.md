---
title: Узнайте, как использовать шаблоны конвейера CI/CD в GitHub, Azure DevOps и Jenkins для разработчиков приложений Teams.
author: MuyangAmigo
description: Шаблоны CI/CD
ms.author: ruhe
ms.localizationpriority: high
ms.topic: overview
ms.date: 04/20/2022
ms.openlocfilehash: 2242f5820495cc3004b7fcbf9c65bce94e7220d1
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111565"
---
# <a name="set-up-cicd-pipelines"></a>Настройка конвейеров CI/CD

TeamsFx помогает автоматизировать рабочий процесс разработки при создании приложения Teams. Ниже приведены инструменты и шаблоны, которые можно использовать для настройки конвейеров CI/CD, создания шаблонов рабочих процессов и настройки рабочего процесса CI/CD с помощью GitHub, Azure DevOps, Jenkins и других платформ. Чтобы подготовить и развернуть ресурсы, вы можете создать субъекты-службы Azure и опубликовать приложение Teams с помощью портала разработчиков Teams. Чтобы опубликовать приложение Teams вручную, вы можете использовать [Портал разработчика для Teams](https://dev.teams.microsoft.com/home).


|Инструменты и шаблоны | Описание |
|---|---|
|[TeamsFx-CLI-Action](https://github.com/OfficeDev/teamsfx-cli-action)|Действие GitHub, которое интегрируется с интерфейсом командной строки TeamsFx.|
|[Набор инструментов Teams в Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)| Расширение Visual Studio Code, помогающее разрабатывать приложение Teams, а также рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins. |
|[TeamsFx CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli) | Инструмент командной строки, помогающий разрабатывать приложения Teams, а также рабочие процессы автоматизации для GitHub, Azure DevOps и Jenkins.|
|[script-ci-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh) и [script-cd-template.sh](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)| Шаблоны скриптов для автоматизации за пределами GitHub, Azure DevOps или Jenkins. |


## <a name="set-up-pipelines"></a>Настройка конвейеров

Вы можете настроить конвейеры на следующих платформах:

1. [Настройка конвейеров с помощью GitHub](#set-up-pipelines-with-github)
1. [Настройка конвейеров с помощью Azure DevOps](#set-up-pipelines-with-azure-devops)
1. [Настройка конвейеров с помощью Jenkins](#set-up-pipelines-with-jenkins)
1. [Настройка конвейеров для других платформ](#set-up-pipelines-for-other-platforms)


### <a name="set-up-pipelines-with-github"></a>Настройка конвейеров с помощью GitHub

Чтобы настроить конвейеры с GitHub для CI/CD:

1. Создание шаблонов рабочего процесса.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.


## <a name="create-workflow-templates-with-github"></a>Создание шаблонов рабочих процессов с помощью GitHub

**Создание шаблонов рабочих процессов с помощью набора инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
1. Выберите значок **Teams Toolkit** на панели действий Visual Studio Code.
1. Выберите **Добавить рабочие процессы CI/CD.**.
1. Выберите среду из командной строки.
1. Выберите **GitHub** в качестве поставщика CI/CD.
1. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
1. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
1. Следуйте файлам README в разделе `.github/workflows`, чтобы настроить рабочий процесс в GitHub.

**Создавайте шаблоны рабочих процессов с помощью TeamsFX CLI.**

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

### <a name="set-up-pipelines-with-azure-devops"></a>Настройка конвейеров с помощью Azure DevOps

Чтобы настроить конвейеры с помощью Azure DevOps для CI/CD:

1. Создание шаблонов рабочего процесса.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.


## <a name="create-workflow-templates-with-azure-devops"></a>Создание шаблонов рабочих процессов с помощью Azure DevOps

**Создание шаблонов рабочих процессов с помощью набора инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
2. Выберите значок **Teams Toolkit** на панели действий Visual Studio Code.
3. Выберите **Добавить рабочие процессы CI/CD.**.
4. Выберите среду из командной строки.
5. Выберите **Azure DevOps** в качестве поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision и Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.azure/pipelines`, чтобы настроить рабочий процесс в Azure DevOps.

**Создавайте шаблоны рабочих процессов с помощью интерфейса командной строки TeamsFX.**

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

Ниже перечислены изменения, которые вы можете внести в сценарий или определение рабочего процесса.

1. Используйте скрипт сборки npm или настройте способ сборки кода автоматизации.
1. Используйте тестовый скрипт npm, который возвращает ноль в случае успеха, и измените тестовые команды.

### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Ниже перечислены изменения, которые вы можете внести в сценарий или определение рабочего процесса.

1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки кода автоматизации.
1. Убедитесь, что у вас есть тестовый скрипт npm, который возвращает ноль в случае успеха, или измените тестовые команды.

### <a name="set-up-pipelines-with-jenkins"></a>Настройка конвейеров с помощью Jenkins

Чтобы настроить конвейеры с Jenkins для CI/CD:

1. Создание шаблонов рабочего процесса.

   * Visual Studio Code
   * TeamsFx CLI

1. Настройка рабочего процесса CI/CD.

## <a name="create-workflow-templates-with-jenkins"></a>Создавайте шаблоны рабочих процессов с помощью Jenkins

**Создание шаблонов рабочих процессов с помощью набора инструментов Teams в Visual Studio Code**

1. Создание нового проекта приложения Teams с помощью Teams Toolkit.
2. Выберите значок **Teams Toolkit** на боковой панели кода Visual Studio.
3. Выберите **Добавить рабочие процессы CI/CD.**.
4. Выберите среду из командной строки.
5. Выберите **Jenkins** в качестве поставщика CI/CD.
6. Выберите хотя бы один шаблон из следующих вариантов: CI, CD, Provision или Publish to Teams.
7. Откройте шаблон и настройте рабочие процессы, соответствующие сценариям.
8. Следуйте файлам README в разделе `.jenkins/pipelines`, чтобы настроить рабочий процесс с Jenkins.

**Создавайте шаблоны рабочих процессов с помощью TeamsFX CLI.**

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

Ниже приведены некоторые изменения, которые вы можете внести в свой проект:

1. Измените способ запуска потока CI. По умолчанию используются триггеры **pollSCM**, когда новое изменение помещается в ветку **dev**.
1. Убедитесь, что у вас есть скрипт сборки npm, или настройте способ сборки кода автоматизации.
1. Убедитесь, что у вас есть тестовый скрипт npm, который возвращает ноль в случае успеха, или измените тестовые команды.


### <a name="customize-cd-workflow"></a>Настройка рабочего процесса CD

Выполните следующие шаги, чтобы настроить конвейер компакт-дисков:

1. Изменение потока CD. По умолчанию используются триггеры `pollSCM`, когда новое изменение помещается в ветку `main`.
1. При необходимости измените сценарии сборки.
1. Удалите тестовые сценарии, если у вас нет тестов.


### <a name="set-up-pipelines-for-other-platforms"></a>Настройка конвейеров для других платформ

Вы можете следовать предопределенным перечисленным сценариям bash для создания и настройки конвейеров CI/CD на других платформах:

* [CI Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-ci-template.sh)
* [CD Scripts](https://github.com/OfficeDev/TeamsFx/blob/main/docs/cicd_insider/others-script-cd-template.sh)

Скрипты основаны на кроссплатформенном инструменте командной строки TeamsFx [TeamsFx-CLI](https://www.npmjs.com/package/@microsoft/teamsfx-cli). Вы можете установить его `npm install -g @microsoft/teamsfx-cli` и следовать [документации](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md), чтобы настроить скрипты.

> [!NOTE]
>
> * Чтобы включить `@microsoft/teamsfx-cli` работающий в режиме CI, включите `CI_ENABLED` с помощью `export CI_ENABLED=true`. В режиме CI `@microsoft/teamsfx-cli` подходит для CI/CD.
> * Чтобы `@microsoft/teamsfx-cli` работал в неинтерактивном режиме, установите глобальный config командой: `teamsfx config set -g interactive false`. В неинтерактивном режиме `@microsoft/teamsfx-cli` не требует ввода.

Обязательно настройте учетные данные Azure и Microsoft 365 в переменных среды безопасно. Например, если вы используете GitHub в качестве репозитория исходного кода, см. [Секреты Github](https://docs.github.com/en/actions/reference/encrypted-secrets).


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

При наличии каких-либо изменений, связанных с файлом манифеста приложения Teams, вы можете обновить манифест и снова опубликовать приложение Teams.

Чтобы опубликовать приложение Teams вручную, вы можете использовать [Портал разработчика для Teams](https://dev.teams.microsoft.com/home).

Выполните следующие шаги, чтобы опубликовать приложение:

1. Войдите на [Портал разработчика для Teams](https://dev.teams.microsoft.com), используя соответствующую учетную запись.
2. Импортируйте пакет приложения в формате zip, выбрав `App -> Import app -> Replace`.
3. Выберите целевое приложение в списке приложений.
4. Опубликуйте приложение, выбрав `Publish -> Publish to your org`.

### <a name="see-also"></a>Дополнительные ресурсы

* [Быстрый старт для действий GitHub](https://docs.github.com/en/actions/quickstart#creating-your-first-workflow)
* [Создайте свой первый конвейер Azure DevOps.](/azure/devops/pipelines/create-first-pipeline)
* [Создайте свой первый конвейер Jenkins](https://www.jenkins.io/doc/pipeline/tour/hello-world/)
* [Управление приложениями Microsoft Teams с помощью портала разработчика](/concepts/build-and-test/teams-developer-portal)
