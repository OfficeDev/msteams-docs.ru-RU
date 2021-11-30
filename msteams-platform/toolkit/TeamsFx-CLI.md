---
title: Интерфейс командной строки TeamsFx
author: MuyangAmigo
description: Описывает интерфейс командной строки TeamsFx
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: b5ef65ec8d1377a99ddebe298e8f3ec4c4c8d3f0
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227770"
---
# <a name="teamsfx-command-line-interface"></a>Интерфейс командной строки TeamsFx

TeamsFx CLI — это интерфейс командной строки на основе текста, который ускоряет Teams разработку приложений. Она направлена на обеспечение работы с клавиатурой при создании Teams приложений. Он также включает сценарий CI/CD, в котором CLI можно легко интегрировать в скрипты для автоматизации.

* [Исходный код](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli) 
* [Пакет (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>Начало работы

Давайте начнем с установки и запуска, `teamsfx-cli` чтобы проверить все доступные `npm` `teamsfx -h` команды:

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>Поддерживаемые команды

| `teamsfx` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx new`       | Создайте новое Teams приложение. |
| `teamsfx account`   | Управление учетной записью облачной службы. Поддерживаемые облачные службы — это Azure и Microsoft 365.          |
| `teamsfx env`       | Управление средами. |
| `teamsfx capability`| Добавьте новые возможности в текущее приложение.         |
| `teamsfx resource`  | Управление ресурсами в текущем приложении.         |
| `teamsfx provision` | Предоставление облачных ресурсов в текущем приложении.             |
| `teamsfx deploy`    | Развертывание текущего приложения.  |
| `teamsfx package`   | Создайте Teams приложение в пакет для публикации.         |
| `teamsfx validate`  | Проверка текущего приложения.             |
| `teamsfx publish`   | Опубликуй приложение Teams.             |
| `teamsfx preview`   | Просмотр текущего приложения. |
| `teamsfx config`    | Управление данными конфигурации. |
| `teamsfx permission`| Сотрудничайте с другими разработчиками в том же проекте.|

## `teamsfx new`

`teamsfx new`будет по умолчанию перейти в интерактивный режим и направлять вас в процессе создания нового приложения Teams, задавая несколько вопросов. Вы также можете сделать это в неинактивном режиме, установив `--interactive` флаг `false` .

| `teamsFx new` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | Создание приложения из существующего шаблона |
| `teamsfx new template list`     | Список всех доступных шаблонов |

### <a name="parameters-for-teamsfx-new"></a>Параметры для `teamsfx new`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--app-name` | Да| Имя вашего Teams приложения.|
|`--interactive`| Нет | Выберите параметры в интерактивном режиме. Параметры `true` и `false` . Значение по умолчанию — `true`.|
|`--capabilities`| Нет| Выберите Teams приложений, несколько вариантов: `tab` , `bot` и `messaging-extension` `tab-spfx` . Значение по умолчанию: `tab` .|
|`--programming-language`| Нет| Язык программирования для проекта. Параметры `javascrip` или значение по `typescript` умолчанию: `javascript` .|
|`--folder`| Нет | Project каталога. В этом каталоге будет создана папка sub с именем приложения. Значение по умолчанию: `./` .|
|`--spfx-framework-type`| Нет| Применимо, `Tab(SPfx)` если выбрана возможность. Frontend Framework. Параметры `none` `react` и, значение по умолчанию: `none` .|
|`--spfx-web part-name`| Нет | Применимо, `Tab(SPfx)` если выбрана возможность. Имя веб-части. Значение по умолчанию: "helloworld". |
|`--spfx-web part-desp`| Нет | Применимо, `Tab(SPfx)` если выбрана возможность. Описание веб-части. По умолчанию значение: "helloworld description". |
|`--azure-resources`| Нет| Применимо, если содержит `tab` возможности. Добавьте ресурсы Azure в проект. Параметры (Несколько) `sql` являются (База данных SQL Azure) и `function` (Azure Functions). |

### <a name="scenarios-for-teamsfx-new"></a>Сценарии для `teamsfx new`

С помощью интерактивного режима для создания Teams приложение является супер интуитивно понятным, попробуйте его, начиная с `teamsfx new` . Ниже приводится несколько scenerios для управления всеми параметрами:

#### <a name="a-tab-app-hosted-on-spfx-using-react"></a>Приложение вкладки, которое SPFx с React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="a-teams-app-in-javascript-contains-tab-bot-capabilities-and-azure-functions"></a>Приложение Teams JavaScript содержит вкладку, возможности бота и функции Azure

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="a-teams-tab-app-with-azure-functions-and-azure-sql"></a>Приложение Teams с azure Functions и Azure SQL

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

Управление учетной записью облачной службы. Поддерживаемые облачные службы `Azure` являются и `Microsoft 365` .

| `teamsFx account` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx account login <service>`      | Войдите в выбранную облачную службу. |
| `teamsfx account logout <service>`      | выйти из выбранной облачной службы. |
| `teamsfx account set --subscription`      | Обновление параметров учетной записи, чтобы установить ID подписки. |

## `teamsfx env`

Управление средами.

| `teamsfx env` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | Добавьте новую среду путем копирования из указанной среды. |
| `teamsfx env list` | Список всех сред. |

### <a name="scenarios-for-teamsfx-env"></a>Сценарии для `teamsfx env`

#### <a name="create-a-new-environment"></a>Создание новой среды

Добавление новой среды путем копирования из существующей среды разработчиков:

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

Добавьте новые возможности в текущее приложение.

| `teamsFx capability` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx capability add tab`      | Добавьте вкладку. |
| `teamsfx capability add bot`      | Добавьте бот. |
| `teamsfx capability add messaging-extension`      | Добавление расширения обмена сообщениями. |

> [!NOTE]
> После того как в проект включен бот, расширение обмена сообщениями больше не может быть добавлено, и оно применяется наоборот. При создании нового проекта приложения можно включить в проект как расширения бота, так и Teams сообщений.

## `teamsfx resource`

Управление ресурсами в текущем приложении. `<resource-type>`Поддерживаются: `azure-sql` `azure-function` и `azure-apim` .

| `teamsFx resource` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | Добавьте ресурс в текущее приложение.|
| `teamsfx resource show <resource-type>`      | Показать сведения о конфигурации ресурса. |
| `teamsfx resource list`      | Список всех ресурсов в текущем приложении. |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>Параметры для `teamsfx resource add azure-function`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--function-name`| Да | Укай имя функции. Значение по умолчанию: `getuserprofile` . |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>Параметры для `teamsfx resource add azure-sql`

#### `--function-name`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--function-name`| Да | Укай имя функции. Значение по умолчанию: `getuserprofile` . |

> [!NOTE]
> Имя функции проверяется, SQL необходимо получить доступ из рабочей нагрузки сервера. Если проект не содержит, он `Azure Functions` будет создан для вас.

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>Параметры для `teamsfx resource add azure-apim`

> [!TIP]
> Ниже приведены параметры, которые вступает в силу при попытке использования существующего `APIM` экземпляра. По умолчанию не нужно указывать какие-либо параметры, и он создаст новый экземпляр во время `teamsfx provision` шага.

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--subscription`| Да | Выберите подписку Azure|
|`--apim-resource-group`| Да| Имя группы ресурсов. |
|`--apim-service-name`| Да | Имя экземпляра службы управления API. |
|`--function-name`| Да | Укай имя функции. Значение по умолчанию: `getuserprofile` . |

> [!NOTE]
> Мы просим имя функции, `Azure API Management` так как необходимо работать с `Azure Functions` . Если проект не содержит, `Azure Functions` мы создадим его для вас.

## `teamsfx provision`

Предоставление облачных ресурсов в текущем приложении.

### <a name="parameters-for-teamsfx-provision"></a>Параметры для `teamsfx provision`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите среду для проекта. |
|`--subscription`| Нет | Укажите ID подписки Azure. |
|`--resource-group`| Нет | Установите имя существующей группы ресурсов. |
|`--sql-admin-name`| Нет | Применимо при SQL в проекте. Имя администратора SQL.|
|`--sql-password`| Нет| Применимо при SQL в проекте. Пароль администратора SQL.|

## `teamsfx deploy`

Эта команда используется для развертывания текущего приложения. По умолчанию он будет развертывать весь проект, но также можно развернуть частично. Параметры (Несколько) являются: `frontend-hosting` `function` , , , `apim` `teamsbot` `spfx` .

### <a name="parameters-for-teamsfx-deploy"></a>Параметры для `teamsfx deploy`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--env`| Да| Выберите существующую среду для проекта. |
|`--open-api-document`| Нет | Применимо, если в проекте есть ресурс AIM. Путь файла документов Открытого API. |
|`--api-prefix`| Нет | Применимо, если в проекте есть ресурс AIM. Префикс имени API. Уникальное имя API по умолчанию `{api-prefix}-{resource-suffix}-{api-version}` будет . |
|`--api-version`| Нет | Применимо, если в проекте есть ресурс AIM. Версия API. |

## `teamsfx validate`

Проверка текущего приложения. Эта команда будет проверять файл манифеста вашего приложения.

### <a name="parameters-for-teamsfx-validate"></a>Параметры для `teamsfx validate`

`--env`: (Обязательно) Выберите существующую среду для проекта.

## `teamsfx publish`

Опубликуй приложение Teams.

### <a name="parameters-for-teamsfx-publish"></a>Параметры для `teamsfx publish`

`--env`: (Обязательно) Выберите существующую среду для проекта.

## `teamsfx package`

Создайте Teams приложение в пакет для публикации.

## `teamsfx preview`

Просмотр текущего приложения из локального или удаленного.

### <a name="parameters-for-teamsfx-preview"></a>Параметры для `teamsfx preview`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--local`| Нет | Просмотр приложения из локального. `--local` является эксклюзивным `--remote` с . |
|`--remote`| Нет | Просмотр приложения с удаленного. `--remote` является эксклюзивным `--local` с . |
|`--env`| Нет | Выберите существующую среду для проекта при приложении `--remote` параметра. |
|`--folder`| Нет | Project корневого каталога. Значение по умолчанию — `./`. |
|`--browser`| Нет | Браузер для открытия Teams веб-клиента. Параметры `chrome` — `edge` и `default` (браузер по умолчанию системы). Значение по умолчанию — `default`. |
|`--browser-arg`| Нет | Аргумент, который необходимо передать в браузер, требует --browser, можно использовать несколько раз (например, --browser-args="--guest") |
|`--sharepoint-site`| Нет | SharePoint URL-адрес сайта, например `{your-tenant-name}.sharepoint.com` (только для SPFx удаленного предварительного просмотра проекта). |

### <a name="scenarios-for-teamsfx-preview"></a>Сценарии для `teamsfx preview`

#### <a name="local-preview"></a>Локальный предварительный просмотр

Зависимости:

- Node.js
- SDK .NET
- Основные средства Azure Functions

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>Удаленный просмотр

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!Note]
> Журналы фоновых служб, таких как React, будут сохранены `~/.fx/cli-log/local-preview/` в .

## `teamsfx config`

Управление данными конфигурации в области пользователя или области проекта.

| `teamsfx config` Команды  | Описания |
|:----------------  |:-------------|
| `teamsfx config get [option]` | Просмотр значения конфигурации параметра |
| `teamsfx config set <option> <value>` | Обновление значения параметра конфигурации |

### <a name="parameters-for-teamsfx-config"></a>Параметры для `teamsfx config`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Выберите существующую среду для проекта. |
|`--folder`| Нет | Project каталога. Это используется при настройке проекта get/set. Значение по умолчанию: `./` . |
|`--global`| Нет | Справиться с конфигурацией. Если это так, область ограничивается областью пользователей, а не областью проекта. Значение по умолчанию: `false` . В настоящее время поддерживается глобальная конфигурация, включая: `telemetry` , `validate-dotnet-sdk` , `validate-func-core-tools` `validate-node` . |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios для `teamsfx config`

Секреты в `.userdata` файле шифруются, `teamsfx config` могут помочь просматривать и обновлять эти значения.

#### <a name="stop-sending-telemetry-data"></a>Остановка отправки данных телеметрии

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>Отключение проверки среды

Для включения и отключения Node.js включите или отключите три конфигуратора, проверка основных средств SDK и Azure Functions, и все они включены по умолчанию. Если вам не нужна проверка зависимостей и вы хотите самостоятельно установить зависимости, можно настроить конфигурирование. Проверьте руководство [Node.js](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)установки, руководство по установке [SDK и](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk) руководство по установке основных средств [Azure Functions.](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)

Например, чтобы отключить проверку SDK .NET, можно использовать следующую команду.

```bash
teamsfx config set validate-dotnet-sdk off
```

Чтобы включить проверку SDK .NET, можно использовать следующую команду.

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>Просмотр всей конфигурации области пользователя

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>Просмотр всей конфигурации в проекте

Секрет будет автоматически расшифровываться:

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>Обновление секретной конфигурации в проекте

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI предоставляет `teamsFx permission` команды для сценария совместной работы.

| `teamsFx permission` Команды | Описания |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | Предоставление разрешения для учетной записи Microsoft 365 для проекта указанной среды. |
| `teamsfx permission status` | Показать состояние разрешений для проекта |

### <a name="parameters-for-teamsfx-permission-grant"></a>Параметры для `teamsfx permission grant`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укай имя env. |
|`--email`| Да | Предопишите адрес электронной почты Microsoft 365 соавтора. Обратите внимание, что учетная запись соавтора должна быть в одном клиенте с создателем. |

### <a name="parameters-for-teamsfx-permission-status"></a>Параметры для `teamsfx permission status`

| Параметры  | Обязательно | Описания |
|:----------------  |:-------------|:-------------|
|`--env`| Да | Укай имя env. |
|`--list-all-collaborators` | Нет | С помощью этого флага Teams набор средств CLI распечатает всех сотрудников для этого проекта. |

### <a name="scenarios-for-teamsfx-permission"></a>Сценарии для `teamsfx permission`

Вот несколько примеров, чтобы улучшить обработку разрешений для `TeamsFx` проектов.

#### <a name="grant-permission"></a>Разрешение на предоставление

Project разработчики и сотрудники могут использовать команду для добавления нового соавтора `teamsfx permission grant` в проект:

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

После успешного предоставления разрешения создатель проекта и сотрудники могут поделиться проектом с новым сотрудником Github, и новый сотрудник будет иметь все разрешения для Microsoft 365 учетной записи.

#### <a name="show-permission-status"></a>Показать состояние разрешений

Project и соавторы могут использовать команду для просмотра разрешения Microsoft 365 учетной записи для `teamsfx permission status` конкретной env:

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>Список всех сотрудников

Project и соавторы могут использовать команду для просмотра всех сотрудников для `teamsfx permission status` конкретного env:

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>Рабочий поток совместной работы E2E в CLI

Как создатель проекта:

- Создайте новый проект Tab TeamsFx (вы также можете выбрать бота), а тип размещения — Azure.

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

- Вход Microsoft 365 учетной записи и учетной записи Azure.

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

- Подготовка проекта.

  ```bash
  teamsfx provision
  ```

- Просмотр сотрудников. Вы должны увидеть себя здесь.

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  ![list-all-collaborators](./images/permission-status-all.png)
- Добавьте другую учетную запись в качестве соавтора. Обратите внимание, что добавленная учетная запись должна быть под тем же клиентом:

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  ![add-new-collaborator](./images/permission-grant.png)
- Нажмите кнопку GitHub

Как сотрудник Project:

- Клонировать проект из GitHub.
- Учетная запись Microsoft 365 входа. Обратите внимание, что Microsoft 365 учетная запись должна быть такой же, как добавленная выше:

  ```bash
  teamsfx account login Microsoft 365
  ```

- Учетная запись Login Azure, которая имеет разрешение участника для всех ресурсов Azure.

  ```bash
  teamsfx account login azure
  ```

- Проверка состояния разрешений. У вас должно быть разрешение владельца проекта:

  ```bash
  teamsfx permission status --env dev
  ```

  ![Состояние разрешения](./images/permission-status.png)
- Обнови код вкладки и разверни проект на удаленный.
- Запуск удаленного и проект должен работать нормально.
