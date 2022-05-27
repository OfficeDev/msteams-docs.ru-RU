---
title: Локальная отладка бота для звонков и собраний
description: Узнайте, как использовать ngrok для разработки вызовов и ботов для виртуальных собраний на локальном компьютере.
ms.topic: how-to
ms.localizationpriority: medium
keywords: туннель ngrok для локальной разработки
ms.date: 11/18/2018
ms.openlocfilehash: 7f85243e0a5d94711cd303ff542decd3bbc7847a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757117"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Разрабатывайте боты для вызовов и виртуальных собраний на локальном компьютере.

В [разделе "](../../concepts/build-and-test/debug.md)Запуск и отладка приложения" объясняется, как использовать [ngrok](https://ngrok.com) для создания туннеля между локальным компьютером и Интернетом. В этом разделе вы узнаете, как можно использовать ngrok и локальный компьютер для разработки ботов, поддерживающих вызовы и виртуальные собрания.

Боты для обмена сообщениями используют HTTP, но боты для вызовов и виртуальных собраний используют TCP более низкого уровня. Ngrok поддерживает туннели TCP в дополнение к туннелям HTTP.

## <a name="configure-ngrokyml"></a>Настроить ngrok.yml

Перейдите на [ngrok](https://ngrok.com) и зарегистрируйте бесплатную учетную запись или войдите в существующую учетную запись. После того, как вы вошли в систему, перейдите на [панель инструментов](https://dashboard.ngrok.com) и получите токен авторизации.

Создайте файл конфигурации ngrok и `ngrok.yml` добавьте следующую строку. Для получения дополнительной информации о том, где может быть расположен файл, см. [ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Настройка сигналов

В разделе [Вызовы и боты для виртуальных собраний](./calls-meetings-bots-overview.md) мы обсудили сигналы вызова о том, как боты обнаруживают и реагируют на новые вызовы и события во время вызова. События сигналов о вызове отправляются через HTTP POST на вызывающую конечную точку бота.

Как и в случае с API обмена сообщениями бота, для того, чтобы мультимедийная платформа в реальном времени могла общаться с ботом, бот должен быть доступен через Интернет. Ngrok упрощает эту процесс. Добавьте следующие строки в ngrok.yml:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Настройка локального носителя

> [!NOTE]
> Этот раздел необходим только для медиа-ботов, размещенных в приложении, и его можно пропустить, если вы не размещаете медиа-файлы самостоятельно.

Носители, размещаемые в приложениях, используют сертификаты и туннели TCP. Необходимо выполнить следующее:

1. Общедоступные конечные точки TCP Ngrok имеют фиксированные URL-адреса. Они есть `0.tcp.ngrok.io`, `1.tcp.ngrok.io`и т. д. У вас должна быть запись DNS CNAME для службы, указывающая на эти URL-адреса. Например, допустим, `0.bot.contoso.com` относится к `0.tcp.ngrok.io`, `1.bot.contoso.com` относится к `1.tcp.ngrok.io` и так далее.
2. SSL-сертификат требуется для URL-адресов. Чтобы упростить задачу, используйте SSL-сертификат, выданный домену с подстановочными знаками. В этом случае это будет `*.bot.contoso.com`. Этот SSL-сертификат проверяется мультимедийным SDK, поэтому он должен соответствовать общедоступному URL-адресу бота. Запишите отпечаток и установите его в сертификаты компьютера
3. Теперь настройте TCP-туннель для пересылки трафика на localhost. Напишите в файле ngrok.yml следующие строки:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Запустить ngrok

Теперь, когда конфигурация ngrok готова, запустите ее:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

При этом запускается ngrok и определяются общедоступные URL-адреса, которые предоставляют туннели для localhost. Ниже приведен пример вывода:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Здесь `12345` является сигнальным портом, `8445` — это порт, который находится в приложении, а `12332` — это удаленный порт мультимедиа, предоставляемый ngrok. Обратите внимание, что у нас есть переадресация с `1.bot.contoso.com` на `1.tcp.ngrok.io`. Это будет использоваться в качестве URL-адреса мультимедиа для бота. Конечно, эти номера портов являются лишь примерами, и вы можете использовать любой доступный порт.

### <a name="update-code"></a>Обновление кода

После запуска и запуска ngrok обновите код, чтобы использовать только что настроенную конфигурацию.

#### <a name="update-signaling"></a>Обновление сигналов

В вызове BotBuilder измените `NotificationUrl` на сигнальный URL-адрес, предоставленный ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Замените сигнал на тот, который предоставлен ngrok, и `NotificationEndpoint` путем контроллера, который получает уведомление.

> [!IMPORTANT]
>
> * URL-адрес в `SetNotificationUrl` должен быть HTTPS.
>
> Локальный экземпляр должен прослушивать HTTP-трафик на сигнальном порте. Запросы, сделанные платформой для вызовов и виртуальных собраний, будут достигать бота как HTTP-трафик локального хоста, если не настроено сквозное шифрование.

#### <a name="update-media"></a>Обновить носители

Обновите `MediaPlatformSettings` следующим образом:

```csharp
var mediaPlatform = new MediaPlatformSettings
{
    ApplicationId = <Your application id>
    MediaPlatformInstanceSettings = new MediaPlatformInstanceSettings
    {
        CertificateThumbprint = <Your SSL Cert thumbprint>,
        InstanceInternalPort = <Localhost media port>,
        InstancePublicPort = <Ngrok exposed remote media port>,
        InstancePublicIPAddress = new IPAddress(0x0),
        ServiceFqdn = <Media url for bot (eg: 1.bot.contoso.com)>,
    },
}
```

> [!NOTE]
> Отпечаток сертификата, указанный в `MediaPlatformSettings` должен соответствовать полному доменному имени службы. Вот почему записи DNS необходимы.

## <a name="caveats"></a>Предостережения

* Бесплатные учетные записи Ngrok **не** обеспечивают сквозное шифрование. Данные HTTPS заканчиваются на URL-адресе ngrok, и данные передаются в незашифрованном виде из ngrok в `localhost`. При необходимости сквозного шифрования, подумайте о платной учетной записи ngrok. Инструкции по настройке безопасных сквозных туннелей см. в разделе [TLS-туннели](https://ngrok.com/docs#tls).
* Поскольку URL-адрес обратного вызова бота является динамическим, сценарии входящих вызовов требуют частого обновления конечных точек ngrok. Один из способов исправить это — использовать платную учетную запись ngrok, которая предоставляет фиксированные поддомены, на которые можно указать бот и платформу.
* Туннели ngrok также можно использовать с [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Пример того, как это сделать, см. в [образце приложения HueBot](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot).
