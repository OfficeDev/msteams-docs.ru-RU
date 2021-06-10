---
title: Локальная отладка бота для звонков и собраний
description: Узнайте, как можно также использовать ngrok для разработки вызовов и сетевых ботов собраний на локальном компьютере.
ms.topic: how-to
localization_priority: Normal
keywords: туннель ngrok локальной разработки
ms.date: 11/18/2018
ms.openlocfilehash: 0f29f77e5030a7dbef9e8f7cefae4e055b7cc5b5
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020164"
---
# <a name="develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="3d99e-104">Разработка ботов вызовов и сетевых собраний на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="3d99e-104">Develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="3d99e-105">В [run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span><span class="sxs-lookup"><span data-stu-id="3d99e-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="3d99e-106">В этом разделе узнайте, как можно также использовать ngrok и локальный компьютер для разработки ботов, поддерживаюших вызовы и собрания в Интернете.</span><span class="sxs-lookup"><span data-stu-id="3d99e-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="3d99e-107">Боты обмена сообщениями используют HTTP, но вызовы и сетевые боты собраний используют TCP более низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="3d99e-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="3d99e-108">Ngrok поддерживает тоннели TCP в дополнение к туннелям HTTP.</span><span class="sxs-lookup"><span data-stu-id="3d99e-108">Ngrok supports TCP tunnels in addition to HTTP tunnels.</span></span> 

## <a name="configure-ngrokyml"></a><span data-ttu-id="3d99e-109">Настройка ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="3d99e-109">Configure ngrok.yml</span></span>

<span data-ttu-id="3d99e-110">Перейдите [в ngrok и](https://ngrok.com) зарегистриройте бесплатную учетную запись или войдите в существующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="3d99e-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="3d99e-111">После того как вы войдите, перейдите на панель [мониторинга](https://dashboard.ngrok.com) и получите маркер auth.</span><span class="sxs-lookup"><span data-stu-id="3d99e-111">After you've signed in, go to the [dashboard](https://dashboard.ngrok.com) and get your auth token.</span></span>

<span data-ttu-id="3d99e-112">Создайте файл конфигурации ngrok `ngrok.yml` и добавьте следующую строку.</span><span class="sxs-lookup"><span data-stu-id="3d99e-112">Create an ngrok configuration file `ngrok.yml` and add the following line.</span></span> <span data-ttu-id="3d99e-113">Дополнительные сведения о расположении файла см. в [сайте ngrok:](https://ngrok.com/docs#config)</span><span class="sxs-lookup"><span data-stu-id="3d99e-113">For more information on where the file can be located, see [ngrok](https://ngrok.com/docs#config):</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="set-up-signaling"></a><span data-ttu-id="3d99e-114">Настройка сигнализации</span><span class="sxs-lookup"><span data-stu-id="3d99e-114">Set up signaling</span></span>

<span data-ttu-id="3d99e-115">В [ботах вызовов](./calls-meetings-bots-overview.md)и сетевых собраний мы обсудили сигналы вызова о том, как боты обнаруживают и реагируют на новые вызовы и события во время вызова.</span><span class="sxs-lookup"><span data-stu-id="3d99e-115">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling on how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="3d99e-116">События сигнализации вызовов отправляются через HTTP POST в конечную точку вызова бота.</span><span class="sxs-lookup"><span data-stu-id="3d99e-116">Call signaling events are sent through HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="3d99e-117">Как и в API обмена сообщениями бота, для того чтобы медиаплатформа в режиме реального времени общается с ботом, ваш бот должен быть досяжим через Интернет.</span><span class="sxs-lookup"><span data-stu-id="3d99e-117">As with the bot's messaging API, for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="3d99e-118">Ngrok делает это простым.</span><span class="sxs-lookup"><span data-stu-id="3d99e-118">Ngrok makes this simple.</span></span> <span data-ttu-id="3d99e-119">Добавьте в ngrok.yml следующие строки:</span><span class="sxs-lookup"><span data-stu-id="3d99e-119">Add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="set-up-local-media"></a><span data-ttu-id="3d99e-120">Настройка локальных средств массовой информации</span><span class="sxs-lookup"><span data-stu-id="3d99e-120">Set up local media</span></span>

> [!NOTE]
> <span data-ttu-id="3d99e-121">Этот раздел необходим только для медиа-ботов, на которые есть приложения, и его можно пропустить, если вы сами не разовьете носители.</span><span class="sxs-lookup"><span data-stu-id="3d99e-121">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="3d99e-122">Носители, на которые есть приложения, используют сертификаты и тоннели TCP.</span><span class="sxs-lookup"><span data-stu-id="3d99e-122">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="3d99e-123">Необходимы следующие действия:</span><span class="sxs-lookup"><span data-stu-id="3d99e-123">The following steps are required:</span></span>

1. <span data-ttu-id="3d99e-124">Общедоступные конечные точки TCP Ngrok зафиксировали URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3d99e-124">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="3d99e-125">Они `0.tcp.ngrok.io` , `1.tcp.ngrok.io` и так далее.</span><span class="sxs-lookup"><span data-stu-id="3d99e-125">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="3d99e-126">Для службы должна быть запись DNS CNAME, которая указывает на эти URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="3d99e-126">You must have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="3d99e-127">Например, скажем, `0.bot.contoso.com` ссылается `0.tcp.ngrok.io` на , `1.bot.contoso.com` ссылается на , и так `1.tcp.ngrok.io` далее.</span><span class="sxs-lookup"><span data-stu-id="3d99e-127">For example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
2. <span data-ttu-id="3d99e-128">Для URL-адресов необходим сертификат SSL.</span><span class="sxs-lookup"><span data-stu-id="3d99e-128">An SSL certificate is required for your URLs.</span></span> <span data-ttu-id="3d99e-129">Чтобы сделать это проще, используйте SSL-сертификат, выданный домену wild card.</span><span class="sxs-lookup"><span data-stu-id="3d99e-129">To make it easy, use an SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="3d99e-130">В этом случае это будет `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="3d99e-130">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="3d99e-131">Этот SSL-сертификат проверяется средствами массовой информации SDK, поэтому он должен совпадать с общедоступным URL-адресом вашего бота.</span><span class="sxs-lookup"><span data-stu-id="3d99e-131">This SSL certificate is validated by the media SDK, so it must match your bot's public URL.</span></span> <span data-ttu-id="3d99e-132">Обратите внимание на отпечатки пальцев и установите его в сертификаты компьютера.</span><span class="sxs-lookup"><span data-stu-id="3d99e-132">Note the thumbprint and install it in your machine certificates.</span></span>
3. <span data-ttu-id="3d99e-133">Теперь установите туннель TCP для перенастройки трафика в localhost.</span><span class="sxs-lookup"><span data-stu-id="3d99e-133">Now, set up a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="3d99e-134">Напишите в ngrok.yml следующие строки:</span><span class="sxs-lookup"><span data-stu-id="3d99e-134">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="3d99e-135">Запуск ngrok</span><span class="sxs-lookup"><span data-stu-id="3d99e-135">Start ngrok</span></span>

<span data-ttu-id="3d99e-136">Теперь, когда конфигурация ngrok готова, запустите ее:</span><span class="sxs-lookup"><span data-stu-id="3d99e-136">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="3d99e-137">Это запускает ngrok и определяет общедоступные URL-адреса, которые предоставляют тоннели локальному каналу.</span><span class="sxs-lookup"><span data-stu-id="3d99e-137">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="3d99e-138">Ниже приводится пример вывода:</span><span class="sxs-lookup"><span data-stu-id="3d99e-138">Following is an example of the output:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="3d99e-139">Здесь находится порт сигнализации, который является портом, на который находится приложение, и удаленный порт мультимедиа, открытый `12345` `8445` `12332` ngrok.</span><span class="sxs-lookup"><span data-stu-id="3d99e-139">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="3d99e-140">Обратите внимание, что у нас есть `1.bot.contoso.com` переад. `1.tcp.ngrok.io`</span><span class="sxs-lookup"><span data-stu-id="3d99e-140">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="3d99e-141">Это будет использоваться в качестве URL-адреса мультимедиа для бота.</span><span class="sxs-lookup"><span data-stu-id="3d99e-141">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="3d99e-142">Конечно, эти номера портов являются только примерами, и вы можете использовать любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="3d99e-142">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="3d99e-143">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="3d99e-143">Update code</span></span>

<span data-ttu-id="3d99e-144">После запуска ngrok обнови код, чтобы использовать только что настроенную конфигуру.</span><span class="sxs-lookup"><span data-stu-id="3d99e-144">After ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="3d99e-145">Обновление сигнализации</span><span class="sxs-lookup"><span data-stu-id="3d99e-145">Update signaling</span></span>

<span data-ttu-id="3d99e-146">В вызове BotBuilder измените URL-адрес сигнала, `NotificationUrl` предоставленный ngrok.</span><span class="sxs-lookup"><span data-stu-id="3d99e-146">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="3d99e-147">Замените сигнал на сигнал, предоставленный ngrok, и на путь `NotificationEndpoint` контроллера, который получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="3d99e-147">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="3d99e-148">URL-адрес `SetNotificationUrl` должен быть HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3d99e-148">The URL in `SetNotificationUrl` must be HTTPS.</span></span>
> 
> <span data-ttu-id="3d99e-149">Локальный экземпляр должен прослушивать трафик HTTP в порту сигналов.</span><span class="sxs-lookup"><span data-stu-id="3d99e-149">Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="3d99e-150">Запросы, сделанные платформой звонков и онлайн-собраний, будут достигать бота в качестве локального трафика HTTP, если не будет настроено end-to-end шифрование.</span><span class="sxs-lookup"><span data-stu-id="3d99e-150">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="3d99e-151">Обновление мультимедиа</span><span class="sxs-lookup"><span data-stu-id="3d99e-151">Update media</span></span>

<span data-ttu-id="3d99e-152">Обновите `MediaPlatformSettings` следующее:</span><span class="sxs-lookup"><span data-stu-id="3d99e-152">Update your `MediaPlatformSettings` as following:</span></span>

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
> <span data-ttu-id="3d99e-153">Отпечатки сертификатов, предоставленные в `MediaPlatformSettings` обязательном удостоверении, соответствуют службе FQDN.</span><span class="sxs-lookup"><span data-stu-id="3d99e-153">The certificate thumbprint provided in the `MediaPlatformSettings` must match the Service FQDN.</span></span> <span data-ttu-id="3d99e-154">Поэтому требуются записи DNS.</span><span class="sxs-lookup"><span data-stu-id="3d99e-154">That is why the DNS entries are required.</span></span>

## <a name="caveats"></a><span data-ttu-id="3d99e-155">Оговорки</span><span class="sxs-lookup"><span data-stu-id="3d99e-155">Caveats</span></span>

- <span data-ttu-id="3d99e-156">Бесплатные учетные записи Ngrok **не обеспечивают** end-to-end шифрования.</span><span class="sxs-lookup"><span data-stu-id="3d99e-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="3d99e-157">Данные HTTPS заканчиваются URL-адресом ngrok, а потоки данных не расшифрованы из ngrok в `localhost` .</span><span class="sxs-lookup"><span data-stu-id="3d99e-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="3d99e-158">Если требуется end-to-end шифрование, рассмотрите платную учетную запись ngrok.</span><span class="sxs-lookup"><span data-stu-id="3d99e-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="3d99e-159">См. [в tLS-туннелях](https://ngrok.com/docs#tls) шаги по настройке безопасных конечных туннелей.</span><span class="sxs-lookup"><span data-stu-id="3d99e-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="3d99e-160">Так как URL-адрес вызова бота динамический, для сценариев входящих вызовов требуется часто обновлять конечные точки ngrok.</span><span class="sxs-lookup"><span data-stu-id="3d99e-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="3d99e-161">Один из способов исправить это — использовать платную учетную запись ngrok, которая предоставляет фиксированные поддомены, на которые можно указать бот и платформу.</span><span class="sxs-lookup"><span data-stu-id="3d99e-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="3d99e-162">Тоннели Ngrok также можно использовать с [помощью Azure Service Fabric.](/azure/service-fabric/service-fabric-overview)</span><span class="sxs-lookup"><span data-stu-id="3d99e-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="3d99e-163">Пример этого см. в примере [приложения HueBot.](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)</span><span class="sxs-lookup"><span data-stu-id="3d99e-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
