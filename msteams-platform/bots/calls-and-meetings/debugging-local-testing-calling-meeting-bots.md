---
title: Как разрабатывать звонки на Боты и собраний по сети на локальном компьютере
description: Узнайте, как использовать ngrok для разработки звонков и собраний по сети боты на локальном компьютере.
keywords: Локальная разработка ngrok туннеля
ms.date: 11/18/2018
ms.openlocfilehash: b6cd2ba5a3866da8085b3da42377ab9e21f12f5f
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 02/01/2020
ms.locfileid: "41675585"
---
# <a name="how-to-develop-calling-and-online-meeting-bots-on-your-local-pc"></a><span data-ttu-id="d55a7-104">Как разрабатывать звонки на Боты и собраний по сети на локальном компьютере</span><span class="sxs-lookup"><span data-stu-id="d55a7-104">How to develop calling and online meeting bots on your local PC</span></span>

<span data-ttu-id="d55a7-105">В разделе [Запуск и отладка приложения](../../concepts/build-and-test/debug.md) мы объясним, как использовать [ngrok](https://ngrok.com) для создания туннеля между локальным компьютером и Интернетом.</span><span class="sxs-lookup"><span data-stu-id="d55a7-105">In [Run and debug your app](../../concepts/build-and-test/debug.md) we explain how to use [ngrok](https://ngrok.com) to create a tunnel between your local computer and the internet.</span></span> <span data-ttu-id="d55a7-106">В этом разделе рассказывается о том, как использовать ngrok и локальный компьютер для разработки Боты, поддерживающих звонки и собрания по сети.</span><span class="sxs-lookup"><span data-stu-id="d55a7-106">In this topic, learn how you can also use ngrok and your local PC to develop bots that support calls and online meetings.</span></span>

<span data-ttu-id="d55a7-107">Обмен сообщениями Боты использовать HTTP, но звонки и собрания по сети Боты используют протокол TCP нижнего уровня.</span><span class="sxs-lookup"><span data-stu-id="d55a7-107">Messaging bots use HTTP, but calls and online meeting bots use the lower-level TCP.</span></span> <span data-ttu-id="d55a7-108">Ngrok поддерживает туннели TCP в дополнение к туннелям HTTP; Вы узнаете, как ниже.</span><span class="sxs-lookup"><span data-stu-id="d55a7-108">Ngrok supports TCP tunnels in addition to HTTP tunnels; you'll learn how, below.</span></span>

## <a name="configuring-ngrokyml"></a><span data-ttu-id="d55a7-109">Настройка ngrok. yml</span><span class="sxs-lookup"><span data-stu-id="d55a7-109">Configuring ngrok.yml</span></span>

<span data-ttu-id="d55a7-110">Перейдите в [ngrok](https://ngrok.com) и запишитесь на бесплатную учетную запись или войдите в существующую учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d55a7-110">Go to [ngrok](https://ngrok.com) and sign up for a free account or log into your existing account.</span></span> <span data-ttu-id="d55a7-111">Войдя в систему, перейдите на [панель мониторинга](https://dashboard.ngrok.com) и получите аустокен.</span><span class="sxs-lookup"><span data-stu-id="d55a7-111">Once you've logged in, go to the [dashboard](https://dashboard.ngrok.com) and get your authtoken.</span></span>

<span data-ttu-id="d55a7-112">Создайте файл `ngrok.yml` конфигурации ngrok [(Подробнее о](https://ngrok.com/docs#config) том, где можно найти этот файл) и добавьте следующую строку:</span><span class="sxs-lookup"><span data-stu-id="d55a7-112">Create an ngrok configuration file `ngrok.yml` (see [here](https://ngrok.com/docs#config) for more information on where this file can be located) and add this line:</span></span>

  `authtoken: <Your-AuthToken>`

## <a name="setting-up-signaling"></a><span data-ttu-id="d55a7-113">Настройка сигнализации</span><span class="sxs-lookup"><span data-stu-id="d55a7-113">Setting up signaling</span></span>

<span data-ttu-id="d55a7-114">В разделе [звонки и собрания по сети Боты](./calls-meetings-bots-overview.md)мы обсуждали сигнал о вызове, как боты обнаруживает и реагирует на новые вызовы и события во время вызова.</span><span class="sxs-lookup"><span data-stu-id="d55a7-114">In [Calls and online meetings bots](./calls-meetings-bots-overview.md), we discussed call signaling — how bots detect and respond to new calls and events during a call.</span></span> <span data-ttu-id="d55a7-115">События сигнализации вызовов отправляются по протоколу HTTP POST в конечную точку абонента Bot.</span><span class="sxs-lookup"><span data-stu-id="d55a7-115">Call signaling events are sent via HTTP POST to the bot's calling endpoint.</span></span>

<span data-ttu-id="d55a7-116">Как и в случае с API обмена сообщениями Bot, чтобы платформа для работы с мультимедийными данными в режиме реального времени применялись к Bot, ваш робот должен быть достижим через Интернет.</span><span class="sxs-lookup"><span data-stu-id="d55a7-116">As with the bot's messaging API, in order for the Real-time Media Platform to talk to your bot, your bot must be reachable over the internet.</span></span> <span data-ttu-id="d55a7-117">Ngrok делает это простым — добавьте следующие строки в Ngrok. yml:</span><span class="sxs-lookup"><span data-stu-id="d55a7-117">Ngrok makes this simple — add the following lines to your ngrok.yml:</span></span>

```yaml
tunnels:
    signaling:
        addr: 12345
        proto: http
```

## <a name="setting-up-local-media"></a><span data-ttu-id="d55a7-118">Настройка локальных носителей</span><span class="sxs-lookup"><span data-stu-id="d55a7-118">Setting up local media</span></span>

> [!NOTE]
> <span data-ttu-id="d55a7-119">Этот раздел необходим только для приложений Media Боты, размещаемых в приложении, и может быть пропущен, если вы не размещаете мультимедиа самостоятельно.</span><span class="sxs-lookup"><span data-stu-id="d55a7-119">This section is only required for application-hosted media bots and can be skipped if you don't host media yourself.</span></span>

<span data-ttu-id="d55a7-120">На носителях, размещаемых в приложении, используются сертификаты и туннели TCP.</span><span class="sxs-lookup"><span data-stu-id="d55a7-120">Application-hosted media uses certificates and TCP tunnels.</span></span> <span data-ttu-id="d55a7-121">Необходимо выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d55a7-121">The following steps are required:</span></span>

- <span data-ttu-id="d55a7-122">Общедоступные конечные точки TCP Ngrok имеют фиксированные URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d55a7-122">Ngrok's public TCP endpoints have fixed URLs.</span></span> <span data-ttu-id="d55a7-123">Они есть `0.tcp.ngrok.io`, `1.tcp.ngrok.io`и так далее.</span><span class="sxs-lookup"><span data-stu-id="d55a7-123">They are `0.tcp.ngrok.io`, `1.tcp.ngrok.io`, and so on.</span></span> <span data-ttu-id="d55a7-124">Для службы должна быть указана запись CNAME DNS, указывающая на эти URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="d55a7-124">You should have a DNS CNAME entry for your service that points to these URLs.</span></span> <span data-ttu-id="d55a7-125">В `0.bot.contoso.com` этом примере подразумевается, что давайте будем `0.tcp.ngrok.io`ссылаться `1.bot.contoso.com` `1.tcp.ngrok.io`на и т. д.</span><span class="sxs-lookup"><span data-stu-id="d55a7-125">In this example, let's say `0.bot.contoso.com` refers to `0.tcp.ngrok.io`, `1.bot.contoso.com` refers to `1.tcp.ngrok.io`, and so on.</span></span>
- <span data-ttu-id="d55a7-126">Для URL-адресов необходим SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="d55a7-126">A SSL certificate is required for your URLs.</span></span> <span data-ttu-id="d55a7-127">Чтобы упростить этот процесс, используйте SSL-сертификат, выданный для домена с подстановочными знаками.</span><span class="sxs-lookup"><span data-stu-id="d55a7-127">To make it easy, use a SSL certificate issued to a wild card domain.</span></span> <span data-ttu-id="d55a7-128">В этом случае это будет `*.bot.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="d55a7-128">In this case, it would be `*.bot.contoso.com`.</span></span> <span data-ttu-id="d55a7-129">Этот SSL-сертификат проверяется с помощью пакета SDK Media, поэтому он должен быть сопоставлен общедоступному URL-адресу Bot.</span><span class="sxs-lookup"><span data-stu-id="d55a7-129">This SSL certificate is validated by the media SDK, so it should match your bot's public URL.</span></span> <span data-ttu-id="d55a7-130">Обратите внимание на отпечаток и установите его в сертификатах компьютера.</span><span class="sxs-lookup"><span data-stu-id="d55a7-130">Note the thumbprint and install it in your machine certificates.</span></span>
- <span data-ttu-id="d55a7-131">Теперь настройте туннель TCP, чтобы переадресовать трафик на localhost.</span><span class="sxs-lookup"><span data-stu-id="d55a7-131">Now, setup a TCP tunnel to forward the traffic to localhost.</span></span> <span data-ttu-id="d55a7-132">Запишите следующие строки в файл ngrok. yml:</span><span class="sxs-lookup"><span data-stu-id="d55a7-132">Write the following lines into your ngrok.yml:</span></span>

    ```yaml
    media:
        addr: 8445
        proto: tcp
    ```

## <a name="start-ngrok"></a><span data-ttu-id="d55a7-133">Запуск ngrok</span><span class="sxs-lookup"><span data-stu-id="d55a7-133">Start ngrok</span></span>

<span data-ttu-id="d55a7-134">Теперь, когда конфигурация ngrok готова, запустите ее:</span><span class="sxs-lookup"><span data-stu-id="d55a7-134">Now that the ngrok configuration is ready, launch it:</span></span>

  `ngrok.exe start -all -config <Path to your ngrok.yml>`

<span data-ttu-id="d55a7-135">При этом запускается ngrok и определяются общедоступные URL-адреса, которые обеспечивают туннель для локального узла.</span><span class="sxs-lookup"><span data-stu-id="d55a7-135">This starts ngrok and defines the public URLs which provide the tunnels to your localhost.</span></span> <span data-ttu-id="d55a7-136">Результат выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="d55a7-136">The output looks like the following:</span></span>

```cmd
Forwarding  http://signal.ngrok.io -> localhost:12345
Forwarding  https://signal.ngrok.io -> localhost:12345
Forwarding  tcp://1.tcp.ngrok.io:12332 -> localhost:8445
```

<span data-ttu-id="d55a7-137">`12345` Это сигнальный порт, `8445` размещенный в приложении, и `12332` является удаленным портом мультимедиа, предоставляемым ngrok.</span><span class="sxs-lookup"><span data-stu-id="d55a7-137">Here, `12345` is the signaling port, `8445` is the application-hosted port, and `12332` is the remote media port exposed by ngrok.</span></span> <span data-ttu-id="d55a7-138">Обратите внимание, что у нас `1.bot.contoso.com` есть `1.tcp.ngrok.io`переадресация из.</span><span class="sxs-lookup"><span data-stu-id="d55a7-138">Note that we have a forwarding from `1.bot.contoso.com` to `1.tcp.ngrok.io`.</span></span> <span data-ttu-id="d55a7-139">Он будет использоваться в качестве URL-адреса для устройства Bot.</span><span class="sxs-lookup"><span data-stu-id="d55a7-139">This will be used as the media URL for the bot.</span></span> <span data-ttu-id="d55a7-140">Конечно, эти номера портов являются простыми примерами, и вы можете использовать любой доступный порт.</span><span class="sxs-lookup"><span data-stu-id="d55a7-140">Of course, these port numbers are just examples and you can use any available port.</span></span>

### <a name="update-code"></a><span data-ttu-id="d55a7-141">Обновление кода</span><span class="sxs-lookup"><span data-stu-id="d55a7-141">Update code</span></span>

<span data-ttu-id="d55a7-142">После запуска и запуска ngrok обновите код, чтобы использовать только что настроенную конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="d55a7-142">Once ngrok is up and running, update the code to use the config you just set up.</span></span>

#### <a name="update-signaling"></a><span data-ttu-id="d55a7-143">Обновление сигналов</span><span class="sxs-lookup"><span data-stu-id="d55a7-143">Update signaling</span></span>

- <span data-ttu-id="d55a7-144">В вызове Ботбуилдер замените `NotificationUrl` на сигнальный URL-адрес, предоставленный ngrok.</span><span class="sxs-lookup"><span data-stu-id="d55a7-144">In the BotBuilder call, change the `NotificationUrl` to the signaling URL provided by ngrok.</span></span>

```csharp
statefulClientBuilder.SetNotificationUrl(
    new Uri("https://signal.ngrok.io/notificationEndpoint"))
```

> [!NOTE]
> <span data-ttu-id="d55a7-145">Замените сигнал на тот, который предоставляется ngrok, и `NotificationEndpoint` путь к контроллеру, который получает уведомление.</span><span class="sxs-lookup"><span data-stu-id="d55a7-145">Replace signal with the one provided by ngrok and the `NotificationEndpoint` with the controller path that receives notification.</span></span>

> <span data-ttu-id="d55a7-146">**Важно!** URL-адрес `SetNotificationUrl` должен иметь значение HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d55a7-146">**IMPORTANT**: The URL in `SetNotificationUrl` must be HTTPS.</span></span>

> <span data-ttu-id="d55a7-147">**Важно!** локальный экземпляр должен прослушивать трафик HTTP в сигнальном порте.</span><span class="sxs-lookup"><span data-stu-id="d55a7-147">**IMPORTANT**: Your local instance must be listening to HTTP traffic on the signaling port.</span></span> <span data-ttu-id="d55a7-148">Запросы, совершенные на платформе "звонки и собрания по сети", будут достигать HTTP-трафика localhost, если не настроено сквозное шифрование.</span><span class="sxs-lookup"><span data-stu-id="d55a7-148">The requests made by the calls and online meetings platform will reach the bot as localhost HTTP traffic unless end-to-end encryption is set up.</span></span>

#### <a name="update-media"></a><span data-ttu-id="d55a7-149">Обновление мультимедиа</span><span class="sxs-lookup"><span data-stu-id="d55a7-149">Update media</span></span>

<span data-ttu-id="d55a7-150">`MediaPlatformSettings` Обновите указанные ниже.</span><span class="sxs-lookup"><span data-stu-id="d55a7-150">Update your `MediaPlatformSettings` to the following.</span></span>

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
> <span data-ttu-id="d55a7-151">Указанный выше отпечаток сертификата должен быть соответствующим полному доменному имени службы.</span><span class="sxs-lookup"><span data-stu-id="d55a7-151">The certificate thumbprint provided above should match the Service FQDN.</span></span> <span data-ttu-id="d55a7-152">Причина в том, что записи DNS являются обязательными.</span><span class="sxs-lookup"><span data-stu-id="d55a7-152">That is why the DNS entries are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d55a7-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d55a7-153">Next steps</span></span>

<span data-ttu-id="d55a7-154">Теперь Bot можно запускать локально и все потоки работают с локального узла.</span><span class="sxs-lookup"><span data-stu-id="d55a7-154">Your bot can now run locally and all the flows work from your localhost.</span></span>

## <a name="caveats"></a><span data-ttu-id="d55a7-155">Предостережения</span><span class="sxs-lookup"><span data-stu-id="d55a7-155">Caveats</span></span>

- <span data-ttu-id="d55a7-156">Свободные учетные записи Ngrok **не** обеспечивают сквозное шифрование.</span><span class="sxs-lookup"><span data-stu-id="d55a7-156">Ngrok free accounts **don't** provide end-to-end encryption.</span></span> <span data-ttu-id="d55a7-157">Данные HTTPS заканчиваются на URL-адресе ngrok и потоки данных, не зашифрованные `localhost`из ngrok в.</span><span class="sxs-lookup"><span data-stu-id="d55a7-157">The HTTPS data ends at the ngrok URL and the data flows unencrypted from ngrok to `localhost`.</span></span> <span data-ttu-id="d55a7-158">Если требуется сквозное шифрование, рассмотрите платную учетную запись ngrok.</span><span class="sxs-lookup"><span data-stu-id="d55a7-158">If you require end-to-end encryption, consider a paid ngrok account.</span></span> <span data-ttu-id="d55a7-159">Для выполнения действий, описанных в статье Настройка безопасных сквозных туннельных туннелей, обратитесь к разделу [туннели TLS](https://ngrok.com/docs#tls) .</span><span class="sxs-lookup"><span data-stu-id="d55a7-159">See [TLS tunnels](https://ngrok.com/docs#tls) for steps on setting up secure end-to-end tunnels.</span></span>
- <span data-ttu-id="d55a7-160">Так как URL-адрес обратного вызова Bot является динамическим, для входящих сценариев вызовов требуется часто обновлять конечные точки ngrok.</span><span class="sxs-lookup"><span data-stu-id="d55a7-160">Because the bot callback URL is dynamic, incoming call scenarios require you to frequently update your ngrok endpoints.</span></span> <span data-ttu-id="d55a7-161">Одним из способов устранения этой ошибки является использование платной учетной записи ngrok, предоставляющей фиксированные поддомены, для которых можно указать вашу Bot и платформу.</span><span class="sxs-lookup"><span data-stu-id="d55a7-161">One way to fix this is to use a paid ngrok account which provides fixed subdomains to which you can point your bot and the platform.</span></span>
- <span data-ttu-id="d55a7-162">Туннели Ngrok также можно использовать с [фабрикой служб Azure](/azure/service-fabric/service-fabric-overview).</span><span class="sxs-lookup"><span data-stu-id="d55a7-162">Ngrok tunnels can also be used with [Azure Service Fabric](/azure/service-fabric/service-fabric-overview).</span></span> <span data-ttu-id="d55a7-163">Пример, как это сделать, приведен в [примере приложения хуебот](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span><span class="sxs-lookup"><span data-stu-id="d55a7-163">For an example of how to do this, see the [HueBot sample app](/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/LocalMediaSamples/HueBot/HueBot).</span></span>
