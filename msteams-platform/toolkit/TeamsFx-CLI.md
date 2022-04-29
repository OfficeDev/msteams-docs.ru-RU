---
title: Интерфейс командной строки TeamsFx
author: MuyangAmigo
description: Описание интерфейса командной строки TeamsFx
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ab9bad973d337d783c1de70c2ad8575a67d6cb6e
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111439"
---
# <a name="teamsfx-library"></a>Библиотека TeamsFx

Microsoft Teams Framework (TeamsFx) — это библиотека, объединяющая распространенные функции и шаблоны интеграции (например, упрощенный доступ к удостоверению Майкрософт). Вы можете создавать приложения для Microsoft Teams с нулевой конфигурацией.

Ниже приведен список основных функций TeamsFx.

* **Совместная работа в TeamsFx**. Разрешите разработчикам и владельцу проекта приглашать других участников совместной работы в проект TeamsFx. Вы можете совместно выполнять отладку и развертывание проекта TeamsFx.

* **TeamsFx CLI**. Ускоряет разработку приложений Teams. Он также включает сценарий CI/CD, позволяющий интегрировать интерфейс командной строки в сценарии для автоматизации.

* **Пакет SDK TeamsFx**. Пакет средств разработки программного обеспечения (SDK) TeamsFx — это основная библиотека кода TeamsFx, содержащая простую проверку подлинности как для клиентского, так и для серверного кода, предназначенного для разработчиков Teams.

## <a name="teamsfx-command-line-interface"></a>Интерфейс командной строки TeamsFx

TeamsFx CLI — это интерфейс командной строки на основе текста, который ускоряет разработку приложений Teams. Он предназначен для обеспечения взаимодействия на основе клавиатуры при создании приложений Teams. Он также включает сценарий CI/CD, позволяющий интегрировать интерфейс командной строки в сценарии для автоматизации.

Дополнительные сведения см. в указанных ниже статьях.

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Начало работы

Установите `teamsfx-cli` из `npm` и запустите `teamsfx -h`, чтобы проверить все доступные команды:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Поддерживаемые команды

| Команда | Описание |
|----------------|-------------|
| `teamsfx new`| Создание приложения Teams.|
| `teamsfx account`| Управление учетными записями облачных служб. Поддерживаются облачные службы Azure и Microsoft 365. |
| `teamsfx env` | Управление средами. |
| `teamsfx capability`| Добавление новых возможностей в текущее приложение.|
| `teamsfx resource`  | Управление ресурсами в текущем приложении.|
| `teamsfx provision` | Подготовка облачных ресурсов в текущем приложении.|
| `teamsfx deploy` | Развертывание текущего приложения.  |
| `teamsfx package` | Сборка приложения Teams в пакет для публикации.|
| `teamsfx validate` | Проверка текущего приложения.|
| `teamsfx publish` | Публикация приложения в Teams.|
| `teamsfx preview` | Предварительный просмотр текущего приложения. |
| `teamsfx config`  | Управление данными конфигурации. |
| `teamsfx permission`| Совместная работа с другими разработчиками в одном проекте.|

## `teamsfx new`

По умолчанию `teamsfx new` переходит в интерактивный режим и предоставляет инструкции в процессе создания приложения Teams. Вы также можете работать в неинтерактивном режиме, присвоив флагу `--interactive` значение `false`.

| Команда `teamsFx new` | Описание |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Создание приложения на основе существующего шаблона |
| `teamsfx new template list`     | Перечисление всех доступных шаблонов |

### <a name="parameters-for-teamsfx-new"></a>Параметры для `teamsfx new`

| Параметр | Требования | Описание |
|:---------------- |:-------------|:-------------|
|`--app-name` | Да| Имя приложения Teams.|
|`--interactive`| Нет | Интерактивный выбор параметров. Варианты: `true` и `false`. Значение по умолчанию — `true`.|
|`--capabilities`| Нет| Выбор возможностей приложения Teams. Множественные варианты: `tab`, `bot`, `messaging-extension` и `tab-spfx`. Значение по умолчанию — `tab`.|
|`--programming-language`| Нет| Язык программирования для проекта. Варианты: `javascript` или `typescript`. Значение по умолчанию — `javascript`.|
|`--folder`| Нет | Каталог проекта. В этом каталоге создается вложенная папка с именем вашего приложения. Значение по умолчанию — `./`.|
|`--spfx-framework-type`| Нет| Применимо, если выбрана возможность `Tab(SPfx)`. Интерфейсная платформа. Варианты: `none` и `react`. Значение по умолчанию — `none`.|
|`--spfx-web part-name`| Нет | Применимо, если выбрана возможность `Tab(SPfx)`. Значение по умолчанию — "helloworld".|
|`--spfx-web part-desp`| Нет | Применимо, если выбрана возможность `Tab(SPfx)`. Значение по умолчанию — "helloworld description". |
|`--azure-resources`| Нет| Применимо, если содержит возможность `tab`. Добавление ресурсов Azure в проект. Множественные варианты: `sql` (база данных SQL Azure) и `function` (Функции Azure). |

### <a name="scenarios-for-teamsfx-new"></a>Сценарии для `teamsfx new`

Вы можете использовать интерактивный режим для создания приложения Teams. Ниже приведены сценарии управления всеми параметрами с `teamsfx new`.

#### <a name="tab-app-hosted-on-spfx-using-react"></a>Приложение вкладки, размещенное в SPFx с использованием React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Приложение Teams в JavaScript со вкладкой, возможностями бота и Функциями Azure

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Приложение вкладки Teams с Функциями Azure и Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Управление учетными записями облачных служб. Поддерживаемые облачные службы: `Azure` и `Microsoft 365`.

| Команда `teamsFx account` | Описание |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | Вход в выбранную облачную службу. |
| `teamsfx account logout <service>`  | Выход из выбранной облачной службы. |
| `teamsfx account set --subscription` | Обновление параметров учетной записи для настройки идентификатора подписки. |

## `teamsfx env`

Управление средами.

| Команда `teamsfx env`  | Описание |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Добавление новой среды путем копирования из указанной среды. |
| `teamsfx env list` | Перечисление всех сред. |

### <a name="scenarios-for-teamsfx-env"></a>Сценарии для `teamsfx env`

Ниже приведены сценарии для `teamsfx env`.

#### <a name="create-a-new-environment"></a>Создание среды

Добавление новой среды путем копирования из существующей среды разработки:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Добавление новых возможностей в текущее приложение.

| Команда `teamsFx capability`  | Описание |
|:----------------  |:-------------|
| `teamsfx capability add tab` | Добавление вкладки |
| `teamsfx capability add bot` | Добавление бота |
| `teamsfx capability add messaging-extension`| Добавление расширения для сообщений |

> [!NOTE]
> Если ваш проект содержит бота, расширение для сообщений невозможно добавить (это верно и наоборот). Вы можете включить в свой проект как бота, так и расширения для сообщений при создании проекта приложения Teams.

## `teamsfx resource`

Управление ресурсами в текущем приложении. Поддерживаемые значения `<resource-type>`: `azure-sql`, `azure-function` и `azure-apim`.

| Команда `teamsFx resource`  | Описание |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Добавление ресурса в текущее приложение.|
| `teamsfx resource show <resource-type>`      | Отображение сведений о конфигурации ресурса. |
| `teamsfx resource list`      | Перечисление всех ресурсов в текущем приложении. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Параметры для `teamsfx resource add azure-function`

| Параметр  | Требования | Описание |
|----------------  |-------------|-------------|
|`--function-name`| Да | Указание имени функции. Значение по умолчанию — `getuserprofile`. |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Параметры для `teamsfx resource add azure-sql`

#### `--function-name`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--function-name`| Да | Указание имени функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> Имя функции проверяется как SQL и должно быть доступно из рабочей нагрузки сервера. Если ваш проект не содержит `Azure Functions`, создайте одну из них.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Параметры для `teamsfx resource add azure-apim`

> [!TIP]
> Параметры применяются при попытке использовать существующий экземпляр `APIM`. По умолчанию вам не нужно указывать какие-либо параметры, а новый экземпляр создается на этапе `teamsfx provision`.

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--subscription`| Да | Выбор подписки Azure|
|`--apim-resource-group`| Да| Имя группы ресурсов. |
|`--apim-service-name`| Да | Имя экземпляра службы управления API. |
|`--function-name`| Да | Указание имени функции. Значение по умолчанию — `getuserprofile`. |

> [!NOTE]
> `Azure API Management` должен работать с `Azure Functions`. Если ваш проект не содержит `Azure Functions`, вы можете создать одну из них.

## `teamsfx provision`

Подготовка облачных ресурсов в текущем приложении.

### <a name="parameters-for-teamsfx-provision"></a>Параметры для `teamsfx provision`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выбор среды для проекта. |
|`--subscription`| Нет | Указание идентификатора подписки Azure. |
|`--resource-group`| Нет | Настройка имени существующей группы ресурсов. |
|`--sql-admin-name`| Нет | Применимо при наличии SQL в проекте. Имя администратора SQL.|
|`--sql-password`| Нет| Применимо при наличии SQL в проекте. Пароль администратора SQL.|

## `teamsfx deploy`

Эта команда используется для развертывания текущего приложения. По умолчанию она разворачивает весь проект, но его также можно развернуть частично. Множественные варианты: `frontend-hosting`, `function`, `apim`, `teamsbot` и `spfx`.

### <a name="parameters-for-teamsfx-deploy"></a>Параметры для `teamsfx deploy`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выбор существующей среды для проекта. |
|`--open-api-document`| Нет | Применимо, если в проекте есть ресурс APIM. Открытый путь к файлу документа API. |
|`--api-prefix`| Нет | Применимо, если в проекте есть ресурс APIM. Префикс имени API. Уникальное имя по умолчанию для API: `{api-prefix}-{resource-suffix}-{api-version}`. |
|`--api-version`| Нет | Применимо, если в проекте есть ресурс APIM. Версия API. |

## `teamsfx validate`

Проверка текущего приложения. Эта команда проверяет файл манифеста приложения.

### <a name="parameters-for-teamsfx-validate"></a>Параметры для `teamsfx validate`

`--env`: выбор существующей среды для проекта.

## `teamsfx publish`

Публикация приложения в Teams.

### <a name="parameters-for-teamsfx-publish"></a>Параметры для `teamsfx publish`

`--env`: выбор существующей среды для проекта.

## `teamsfx package`

Сборка приложения Teams в пакет для публикации.

## `teamsfx preview`

Предварительный просмотр текущего приложения из локальной или удаленной среды.

### <a name="parameters-for-teamsfx-preview"></a>Параметры для `teamsfx preview`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--local`| Нет | Предварительный просмотр приложения из локальной среды. `--local` исключает использование `--remote`. |
|`--remote`| Нет | Предварительный просмотр приложения из удаленной среды. `--remote` исключает использование `--local`. |
|`--env`| Нет | Выбор существующей среды для проекта, когда добавлен параметр `--remote`. |
|`--folder`| Нет | Корневой каталог проекта. Значение по умолчанию — `./`. |
|`--browser`| Нет | Браузер для открытия веб-клиента Teams. Варианты: `chrome`, `edge` и `default`, например системный браузер по умолчанию. Значение — `default`. |
|`--browser-arg`| Нет | Аргумент для передачи в браузер. Требует: --browser. Может использоваться несколько раз, например --browser-args="--guest" |
|`--sharepoint-site`| Нет | URL-адрес сайта SharePoint, например `{your-tenant-name}.sharepoint.com` для удаленного предварительного просмотра проекта SPFx. |

### <a name="scenarios-for-teamsfx-preview"></a>Сценарии для `teamsfx preview`

#### <a name="local-preview"></a>Локальный предварительный просмотр

Зависимости:

* Node.js
* Пакет SDK для .NET
* Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Удаленный предварительный просмотр

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> Журналы фоновых служб, например React, сохраняются в `~/.fx/cli-log/local-preview/`.

## `teamsfx config`

Управление данными конфигурации в области пользователя или проекта.

| Команда `teamsfx config`  | Описание |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Просмотр значения конфигурации параметра |
| `teamsfx config set <option> <value>` | Обновление значения конфигурации параметра |

### <a name="parameters-for-teamsfx-config"></a>Параметры для `teamsfx config`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Выбор существующей среды для проекта. |
|`--folder`| Нет | Каталог проекта. Используется для получения или настройки конфигурации проекта. Значение по умолчанию — `./`. |
|`--global`| Нет | Область конфигурации. Если присвоено значение true, область ограничена областью пользователя, а не областью проекта. Значение по умолчанию — `false`. В настоящее время поддерживаемые глобальные конфигурации включают `telemetry`, `validate-dotnet-sdk`, `validate-func-core-tools`, `validate-node`. |

### <a name="scenerios-for-teamsfx-config"></a>Сценарии для `teamsfx config`

Секреты в файле `.userdata` зашифрованы. `teamsfx config` помогает просматривать или обновлять значения.

#### <a name="stop-sending-telemetry-data"></a>Остановка отправки данных телеметрии

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Отключение средства проверки среды

Существует три конфигурации для включения и отключения проверки Node.js, пакета SDK для .NET и Azure Functions Core Tools. Все они включены по умолчанию. Если вам не нужна проверка зависимостей и вы хотите установить зависимости самостоятельно, можно установить для конфигурации значение "off". Ознакомьтесь со следующими руководствами.

* [Руководство по установке Node.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [Руководство по установке пакета SDK для .NET](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Руководство по установке Azure Functions Core Tools](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools).

Чтобы отключить проверку пакета SDK для .NET, вы можете использовать следующую команду.

```bash
teamsfx config set validate-dotnet-sdk off
```

Чтобы включить проверку пакета SDK для .NET, вы можете использовать следующую команду.

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Просмотр всей конфигурации области пользователя

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Просмотр всей конфигурации в проекте

Секрет расшифровывается автоматически:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Обновление конфигурации секрета в проекте

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI предоставляет команды `teamsFx permission` для сценария совместной работы.

| Команда `teamsFx permission` | Описание |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Предоставление разрешения для учетной записи Microsoft 365 участника совместной работы для проекта указанной среды. |
| `teamsfx permission status` | Отображение состояния разрешений для проекта |

### <a name="parameters-for-teamsfx-permission-grant"></a>Параметры для `teamsfx permission grant`

| Параметр  | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Указание имени среды. |
|`--email`| Да | Указание адреса электронной почты Microsoft 365 участника совместной работы. Убедитесь, что учетная запись участника совместной работы находится в одном клиенте с создателем. |

### <a name="parameters-for-teamsfx-permission-status"></a>Параметры для `teamsfx permission status`

| Параметр | Требования | Описание |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Указание имени среды. |
|`--list-all-collaborators` | Нет | С помощью этого флага CLI набора средств Teams печатает всех участников совместной работы для этого проекта. |

### <a name="scenarios-for-teamsfx-permission"></a>Сценарии для `teamsfx permission`

Разрешения для проектов `TeamsFx` перечислены ниже.

#### <a name="grant-permission"></a>Предоставление разрешения

Создатель проекта и участники совместной работы могут использовать команду `teamsfx permission grant` для добавления нового участника совместной работы в проект:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

Получив необходимое разрешение, создатель проекта и участники совместной работы могут предоставить общий доступ к проекту новому участнику совместной с помощью GitHub, а новый участник совместной работы может получить все разрешения для учетной записи Microsoft 365.

#### <a name="show-permission-status"></a>Отображение состояния разрешения

Автор проекта и участники совместной работы могут использовать команду `teamsfx permission status` с целью просмотра разрешения учетной записи Microsoft 365 для определенной среды:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Перечисление всех участников совместной работы

Автор проекта и участники совместной работы могут использовать команду `teamsfx permission status` для просмотра всех участников совместной работы для конкретной среды:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Рабочий процесс совместной работы E2E в CLI

Как создатель проекта:

* Чтобы создать проект бота или вкладки TeamsFx и выбрать Azure в качестве типа узла:

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* Чтобы войти в учетную запись Microsoft 365 и учетную запись Azure:

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* Чтобы подготовить проект:

  ```bash
  teamsfx provision
  ```

* Чтобы просмотреть участников совместной работы:

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* Чтобы добавить другую учетную запись в качестве участника совместной работы. Убедитесь, что добавленная учетная запись находится в том же клиенте:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* Чтобы отправить проект в GitHub

Как участник совместной работы над проектом:

* Клонируйте проект из GitHub.
* Войдите в учетную запись Microsoft 365. Убедитесь, что добавлена та же учетная запись Microsoft 365:

  ```bash
  teamsfx account login Microsoft 365
  ```

* Войдите в учетную запись Azure с разрешением участника для всех ресурсов Azure.

  ```bash
  teamsfx account login azure
  ```

* Проверьте состояние разрешения. У вас должно быть разрешение владельца проекта:

  ```bash
  teamsfx permission status --env dev
  ```

  ![состояние разрешения](./images/permission-status.png)

* Обновите код вкладки и разверните проект в удаленной среде.
* Запустите в удаленном режиме. Проект должен работать нормально.

## <a name="see-also"></a>Дополнительные ресурсы

* [Пакет SDK TeamsFx для TypeScript или JavaScript](TeamsFx-SDK.md)
* [Управление несколькими средами в наборе средств Teams](TeamsFx-multi-env.md)
* [Совместная работа над проектом Teams с помощью набора средств Teams](TeamsFx-collaboration.md)
* [Общие сведения о наборе средств Teams](teams-toolkit-fundamentals.md)
