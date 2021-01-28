---
title: Локальная отладка бота для звонков и собраний
description: Узнайте, как можно также использовать ngrok для разработки звонков и ботов собраний по сети на локальном компьютере.
ms.topic: how-to
keywords: локальный туннель ngrok для разработки
ms.date: 11/18/2018
ms.openlocfilehash: e9b77df18c8d80f02134dc7912b5796023082039
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014308"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="2383a-104">Разработка ботов для звонков и собраний по сети на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="2383a-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="2383a-105">В [окне "Запуск и отлагивание"](../../concepts/build-and-test/debug.md) приложения мы объясним, как использовать [ngrok](https://ngrok.com) для создания туннеля между локальным компьютером и Интернетом.</span><span class="sxs-lookup"><span data-stu-id="2383a-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="2383a-106">В этом разделе вы узнаете, как можно также использовать ngrok и локальный компьютер для разработки ботов, которые поддерживают звонки и собрания по сети.</span><span class="sxs-lookup"><span data-stu-id="2383a-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="2383a-107">Боты для обмена сообщениями используют протокол HTTP, но боты для звонков и собраний по сети используют TCP более низкого уровня.</span><span class="sxs-lookup"><span data-stu-id="2383a-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="2383a-108">Ngrok поддерживает также туннели TCP, а также туннели HTTP; вы узнаете, как это сделать, ниже.</span><span class="sxs-lookup"><span data-stu-id="2383a-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="2383a-109">Настройка ngrok.yml</span><span class="sxs-lookup"><span data-stu-id="2383a-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="2383a-110">Перейдите [в ngrok](https://ngrok.com) и зарегистрйдите для бесплатной учетной записи или войдите в существующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="2383a-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="2383a-111">После входа перейдите на панель мониторинга и [получите](https://dashboard.ngrok.com) свой authtoken.</span><span class="sxs-lookup"><span data-stu-id="2383a-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="2383a-112">Создайте файл конфигурации ngrok (дополнительные сведения о расположении этого файла) и добавьте `ngrok.yml` данная строка: [](https://ngrok.com/docs#config)</span><span class="sxs-lookup"><span data-stu-id="2383a-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="2383a-113">Настройка сигналов</span><span class="sxs-lookup"><span data-stu-id="2383a-113">Setting up signaling</span></span>

<span data-ttu-id="2383a-114">В [ботах звонков](./calls-meetings-bots-overview.md)и собраний по сети мы обсуждают сигналы звонков — как боты обнаруживают новые вызовы и события во время звонка и реагируют на них.</span><span class="sxs-lookup"><span data-stu-id="2383a-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="2383a-115">События сигналов вызова отправляются через HTTP POST в конечную точку вызова бота.</span><span class="sxs-lookup"><span data-stu-id="2383a-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="2383a-116">Как и в API сообщений бота, для связи с ботом с помощью платформы мультимедиа в режиме реального времени бот должен быть досяжим через Интернет.</span><span class="sxs-lookup"><span data-stu-id="2383a-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="2383a-117">Ngrok упрощает эту и добавляет следующие строки в ngrok.yml:</span><span class="sxs-lookup"><span data-stu-id="2383a-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="2383a-118">Настройка локального носители</span><span class="sxs-lookup"><span data-stu-id="2383a-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="2383a-119">Этот раздел необходим только для ботов мультимедиа, которые есть в приложении, и его можно пропустить, если вы не разведете мультимедиа самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="2383a-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="2383a-120">Носители, которые используются в приложении, используют сертификаты и туннели TCP.</span><span class="sxs-lookup"><span data-stu-id="2383a-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="2383a-121">Необходимы следующие действия:</span><span class="sxs-lookup"><span data-stu-id="2383a-121">The following steps are required:</span></span>

- <span data-ttu-id="2383a-122">Общедоступные конечные точки TCP Ngrok имеют фиксированные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2383a-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="2383a-123">Это `0.tcp.ngrok.io` и `1.tcp.ngrok.io` так далее.</span><span class="sxs-lookup"><span data-stu-id="2383a-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="2383a-124">Для службы должна быть запись DNS CNAME, которая указывает на эти URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="2383a-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="2383a-125">В этом примере, предположим, `0.bot.contoso.com` относится `0.tcp.ngrok.io` к , `1.bot.contoso.com` относится и так `1.tcp.ngrok.io` далее.</span><span class="sxs-lookup"><span data-stu-id="2383a-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="2383a-126">Для URL-адресов требуется SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="2383a-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="2383a-127">Чтобы у вас было просто, используйте SSL-сертификат, выданный для домена с поддиапными карточками.</span><span class="sxs-lookup"><span data-stu-id="2383a-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="2383a-128">В этом случае это будет `*.bot.contoso.com` .</span><span class="sxs-lookup"><span data-stu-id="2383a-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="2383a-129">Этот SSL-сертификат проверяется с помощью media SDK, поэтому он должен совпадать с общедоступным URL-адресом бота.</span><span class="sxs-lookup"><span data-stu-id="2383a-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="2383a-130">Обратите внимание на отпечаток и установите его в сертификаты компьютера.</span><span class="sxs-lookup"><span data-stu-id="2383a-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="2383a-131">Теперь настроим туннель TCP, чтобы перенапорять трафик на localhost.</span><span class="sxs-lookup"><span data-stu-id="2383a-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="2383a-132">Напишите в ngrok.yml следующие строки:</span><span class="sxs-lookup"><span data-stu-id="2383a-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="2383a-133">Запуск ngrok</span><span class="sxs-lookup"><span data-stu-id="2383a-133">Start ngrok</span></span>

<span data-ttu-id="2383a-134">Теперь, когда конфигурация ngrok готова, запустите ее:</span><span class="sxs-lookup"><span data-stu-id="2383a-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="2383a-135">При этом запускается ngrok и определяются общедоступные URL-адреса, которые предоставляют туннеля для localhost.</span><span class="sxs-lookup"><span data-stu-id="2383a-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="2383a-136">Выходные данные выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="2383a-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="2383a-137">Здесь находится сигнальный порт, который является портом, который находится в приложении и является удаленным портом мультимедиа, который `12345` `8445` `12332` выставил ngrok.</span><span class="sxs-lookup"><span data-stu-id="2383a-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="2383a-138">Обратите внимание, что у нас есть переад `1.bot.contoso.com` вперед. `1.tcp.ngrok.io`</span><span class="sxs-lookup"><span data-stu-id="2383a-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="2383a-139">Он будет использоваться в качестве URL-адреса мультимедиа для бота.</span><span class="sxs-lookup"><span data-stu-id="2383a-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="2383a-140">Конечно, эти номера портов являются лишь примерами, и вы можете использовать любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="2383a-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="2383a-141">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="2383a-141">Update code</span></span>

<span data-ttu-id="2383a-142">После запуска ngrok обновите код, чтобы использовать только что настроенную вами config.</span><span class="sxs-lookup"><span data-stu-id="2383a-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="2383a-143">Обновление сигналов</span><span class="sxs-lookup"><span data-stu-id="2383a-143">Update signaling</span></span>

- <span data-ttu-id="2383a-144">В вызове BotBuilder измените url-адрес сигнала, `NotificationUrl` предоставленный ngrok.</span><span class="sxs-lookup"><span data-stu-id="2383a-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="2383a-145">Замените сигнал на сигнал, предоставленный ngrok, и путь `NotificationEndpoint` контроллера, который получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="2383a-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="2383a-146">**ВАЖНО!** URL-адрес `SetNotificationUrl` должен иметь значение HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2383a-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="2383a-147">**ВАЖНО!** Локальный экземпляр должен прослушивать ТРАФИК HTTP на сигнальный порт.</span><span class="sxs-lookup"><span data-stu-id="2383a-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="2383a-148">Запросы, сделанные платформой звонков и собраний по сети, будут достигать бота в качестве HTTP-трафика localhost, если не настроено шифрование.</span><span class="sxs-lookup"><span data-stu-id="2383a-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="2383a-149">Обновление носители</span><span class="sxs-lookup"><span data-stu-id="2383a-149">Update media</span></span>

<span data-ttu-id="2383a-150">`MediaPlatformSettings`Обновите свою следующую версию.</span><span class="sxs-lookup"><span data-stu-id="2383a-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="2383a-151">Отпечаток сертификата, предоставленный выше, должен соответствовать FQDN службы.</span><span class="sxs-lookup"><span data-stu-id="2383a-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="2383a-152">Именно поэтому требуются записи DNS.</span><span class="sxs-lookup"><span data-stu-id="2383a-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2383a-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2383a-153">Next steps</span></span>

<span data-ttu-id="2383a-154">Теперь бот может запускаться локально, и все потоки работают с вашего localhost.</span><span class="sxs-lookup"><span data-stu-id="2383a-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="2383a-155">Предостереские оговорки</span><span class="sxs-lookup"><span data-stu-id="2383a-155">Caveats</span></span>

- <span data-ttu-id="2383a-156">Бесплатные учетные записи Ngrok **не** обеспечивают шифрование.</span><span class="sxs-lookup"><span data-stu-id="2383a-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="2383a-157">Данные HTTPS заканчиваются URL-адресом ngrok, а потоки данных незашифровываются из ngrok в `localhost` .</span><span class="sxs-lookup"><span data-stu-id="2383a-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="2383a-158">Если требуется все шифрование, рассмотрите возможность платной учетной записи ngrok.</span><span class="sxs-lookup"><span data-stu-id="2383a-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="2383a-159">Шаги по настройке безопасных конечных туннелях см. в туннелях [TLS.](https://ngrok.com/docs#tls)</span><span class="sxs-lookup"><span data-stu-id="2383a-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="2383a-160">Так как URL-адрес для вызова бота является динамическим, для сценариев входящих вызовов требуется часто обновлять конечные точки ngrok.</span><span class="sxs-lookup"><span data-stu-id="2383a-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="2383a-161">Один из способов устранить эту проблему — использовать платную учетную запись ngrok, которая предоставляет фиксированные поддомены, на которые можно указать бота и платформу.</span><span class="sxs-lookup"><span data-stu-id="2383a-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="2383a-162">Туннеля Ngrok также можно использовать с [Azure Service Fabric.](/azure/service-fabric/service-fabric-overview)</span><span class="sxs-lookup"><span data-stu-id="2383a-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="2383a-163">Пример этого см. в примере приложения [HueBot.](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot)</span><span class="sxs-lookup"><span data-stu-id="2383a-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
