---
title: Локальная отладка бота для звонков и собраний
description: Узнайте, как можно также использовать ngrok для разработки вызовов и сетевых ботов собраний на локальном компьютере.
ms.topic: how-to
ms.localizationpriority: medium
keywords: туннель ngrok локальной разработки
ms.date: 11/18/2018
ms.openlocfilehash: c55ec6e5d7296f4ee04ae3ad3de0f9bb82cfd276
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453364"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a>Разработка ботов вызовов и сетевых собраний на локальном компьютере

В [run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet. В этом разделе узнайте, как можно также использовать ngrok и локальный компьютер для разработки ботов, поддерживаюших вызовы и собрания в Интернете.

Боты обмена сообщениями используют HTTP, но вызовы и сетевые боты собраний используют TCP более низкого уровня. Ngrok поддерживает тоннели TCP в дополнение к туннелям HTTP.

## <a name="configure-ngrokyml"></a>Настройка ngrok.yml

Перейдите [в ngrok и](https://ngrok.com) зарегистриройте бесплатную учетную запись или войдите в существующую учетную запись. После того как вы войдите, перейдите на панель [мониторинга](https://dashboard.ngrok.com) и получите маркер auth.

Создайте файл конфигурации ngrok и `ngrok.yml` добавьте следующую строку. Дополнительные сведения о расположении файла см. в [ngrok](https://ngrok.com/docs#config):

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a>Настройка сигнализации

В [ботах вызовов](./calls-meetings-bots-overview.md) и сетевых собраний мы обсудили сигналы вызова о том, как боты обнаруживают и реагируют на новые вызовы и события во время вызова. События сигнализации вызовов отправляются через HTTP POST в конечную точку вызова бота.

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

1. Общедоступные конечные точки TCP Ngrok зафиксировали URL-адреса. Они , `0.tcp.ngrok.io`и `1.tcp.ngrok.io`так далее. Для службы должна быть запись DNS CNAME, которая указывает на эти URL-адреса. Например, скажем, ссылается `0.bot.contoso.com` на `0.tcp.ngrok.io`, `1.bot.contoso.com` ссылается на `1.tcp.ngrok.io`, и так далее.
2. Для URL-адресов необходим сертификат SSL. Чтобы сделать это проще, используйте SSL-сертификат, выданный домену wild card. В этом случае это будет `*.bot.contoso.com`. Этот SSL-сертификат проверяется средствами массовой информации SDK, поэтому он должен совпадать с общедоступным URL-адресом вашего бота. Обратите внимание на отпечатки пальцев и установите его в сертификаты компьютера.
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

Здесь находится `12345` порт сигнализации, который является портом, `8445` на который находится приложение, `12332` и удаленный порт мультимедиа, открытый ngrok. Обратите внимание, что у нас есть переад.`1.bot.contoso.com` `1.tcp.ngrok.io` Это будет использоваться в качестве URL-адреса мультимедиа для бота. Конечно, эти номера портов являются только примерами, и вы можете использовать любой доступный порт.

### <a name="update-code"></a>Обновление кода

После запуска ngrok обнови код, чтобы использовать только что настроенную конфигуру.

#### <a name="update-signaling"></a>Обновление сигнализации

В вызове BotBuilder измените URL-адрес `NotificationUrl` сигнала, предоставленный ngrok.

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> Замените сигнал на сигнал, предоставленный ngrok, `NotificationEndpoint` и на путь контроллера, который получает уведомление.

> [!IMPORTANT]
>
> * URL-адрес должен `SetNotificationUrl` быть HTTPS.
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
> Отпечатки сертификатов, предоставленные в обязательном `MediaPlatformSettings` удостоверении, соответствуют службе FQDN. Поэтому требуются записи DNS.

## <a name="caveats"></a>Оговорки

* Бесплатные учетные записи Ngrok **не обеспечивают** end-to-end шифрования. Данные HTTPS заканчиваются URL-адресом ngrok, а потоки данных не расшифрованы из ngrok в `localhost`. Если требуется end-to-end шифрование, рассмотрите платную учетную запись ngrok. См [. в tLS-туннелях](https://ngrok.com/docs#tls) шаги по настройке безопасных конечных туннелей.
* Так как URL-адрес вызова бота динамический, для сценариев входящих вызовов требуется часто обновлять конечные точки ngrok. Один из способов исправить это — использовать платную учетную запись ngrok, которая предоставляет фиксированные поддомены, на которые можно указать бот и платформу.
* Тоннели Ngrok также можно использовать в [Azure Service Fabric](/azure/service-fabric/service-fabric-overview). Пример этого см. в примере [приложения HueBot](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples/HueBot/HueBot).
