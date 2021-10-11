---
title: Локальная отладка бота для звонков и собраний
description: Узнайте, как можно также использовать ngrok для разработки вызовов и сетевых ботов собраний на локальном компьютере.
ms.topic: how-to
ms.localizationpriority: medium
keywords: туннель ngrok локальной разработки
ms.date: 11/18/2018
ms.openlocfilehash: 2b3da582f6529fd676ae8964acb09a038e39162a
ms.sourcegitcommit: c04a1a792773a9d5c61169c5702d94a8c478ad1c
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2021
ms.locfileid: "60260660"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Разработка ботов вызовов и сетевых собраний на локальном компьютере

В [run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet. В этом разделе узнайте, как можно также использовать ngrok и локальный компьютер для разработки ботов, поддерживаюших вызовы и собрания в Интернете.

Боты обмена сообщениями используют HTTP, но вызовы и сетевые боты собраний используют TCP более низкого уровня. Ngrok поддерживает тоннели TCP в дополнение к туннелям HTTP. 

## <a name="configure-ngrokyml"></a>Настройка ngrok.yml

Перейдите [в ngrok и](https://ngrok.com) зарегистриройте бесплатную учетную запись или войдите в существующую учетную запись. После того как вы войдите, перейдите на панель [мониторинга](https://dashboard.ngrok.com) и получите маркер auth.

Создайте файл конфигурации ngrok `ngrok.yml` и добавьте следующую строку. Дополнительные сведения о расположении файла см. в [сайте ngrok:](https://ngrok.com/docs#config)

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Настройка сигнализации

В [ботах вызовов](./calls-meetings-bots-overview.md)и сетевых собраний мы обсудили сигналы вызова о том, как боты обнаруживают и реагируют на новые вызовы и события во время вызова. События сигнализации вызовов отправляются через HTTP POST в конечную точку вызова бота.

Как и в API обмена сообщениями бота, для того чтобы медиаплатформа в режиме реального времени общается с ботом, ваш бот должен быть досяжим через Интернет. Ngrok делает это простым. Добавьте в ngrok.yml следующие строки:

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a>Настройка локальных средств массовой информации

> [!NOTE]
> Этот раздел необходим только для медиа-ботов, на которые есть приложения, и его можно пропустить, если вы сами не разовьете носители.

Носители, на которые есть приложения, используют сертификаты и тоннели TCP. Необходимы следующие действия:

1. Общедоступные конечные точки TCP Ngrok зафиксировали URL-адреса. Они `0.tcp.ngrok.io` , `1.tcp.ngrok.io` и так далее. Для службы должна быть запись DNS CNAME, которая указывает на эти URL-адреса. Например, скажем, `0.bot.contoso.com` ссылается `0.tcp.ngrok.io` на , `1.bot.contoso.com` ссылается на , и так `1.tcp.ngrok.io` далее.
2. Для URL-адресов необходим сертификат SSL. Чтобы сделать это проще, используйте SSL-сертификат, выданный домену wild card. В этом случае это будет `*.bot.contoso.com` . Этот SSL-сертификат проверяется средствами массовой информации SDK, поэтому он должен совпадать с общедоступным URL-адресом вашего бота. Обратите внимание на отпечатки пальцев и установите его в сертификаты компьютера.
3. Теперь установите туннель TCP для перенастройки трафика в localhost. Напишите в ngrok.yml следующие строки:

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a>Запуск ngrok

Теперь, когда конфигурация ngrok готова, запустите ее:

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

Это запускает ngrok и определяет общедоступные URL-адреса, которые предоставляют тоннели локальному каналу. Ниже приводится пример вывода:

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

Здесь находится порт сигнализации, который является портом, на который находится приложение, и удаленный порт мультимедиа, открытый `12345` `8445` `12332` ngrok. Обратите внимание, что у нас есть `1.bot.contoso.com` переад. `1.tcp.ngrok.io` Это будет использоваться в качестве URL-адреса мультимедиа для бота. Конечно, эти номера портов являются только примерами, и вы можете использовать любой доступный порт.

### <a name="update-code"></a>Обновление кода

После запуска ngrok обнови код, чтобы использовать только что настроенную конфигуру.

#### <a name="update-signaling"></a>Обновление сигнализации

В вызове BotBuilder измените URL-адрес сигнала, `NotificationUrl` предоставленный ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Замените сигнал на сигнал, предоставленный ngrok, и на путь `NotificationEndpoint` контроллера, который получает уведомление.

> [!IMPORTANT]
> * URL-адрес `SetNotificationUrl` должен быть HTTPS.
> 
> Локальный экземпляр должен прослушивать трафик HTTP в порту сигналов. Запросы, сделанные платформой звонков и онлайн-собраний, будут достигать бота в качестве локального трафика HTTP, если не будет настроено end-to-end шифрование.

#### <a name="update-media"></a>Обновление мультимедиа

Обновите `MediaPlatformSettings` следующее:

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
> Отпечатки сертификатов, предоставленные в `MediaPlatformSettings` обязательном удостоверении, соответствуют службе FQDN. Поэтому требуются записи DNS.

## <a name="caveats"></a>Оговорки

- Бесплатные учетные записи Ngrok **не обеспечивают** end-to-end шифрования. Данные HTTPS заканчиваются URL-адресом ngrok, а потоки данных не расшифрованы из ngrok в `localhost` . Если требуется end-to-end шифрование, рассмотрите платную учетную запись ngrok. См. [в tLS-туннелях](https://ngrok.com/docs#tls) шаги по настройке безопасных конечных туннелей.
- Так как URL-адрес вызова бота динамический, для сценариев входящих вызовов требуется часто обновлять конечные точки ngrok. Один из способов исправить это — использовать платную учетную запись ngrok, которая предоставляет фиксированные поддомены, на которые можно указать бот и платформу.
- Тоннели Ngrok также можно использовать с [помощью Azure Service Fabric.](/azure/service-fabric/service-fabric-overview) Пример этого см. в примере [приложения HueBot.](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot)

 
