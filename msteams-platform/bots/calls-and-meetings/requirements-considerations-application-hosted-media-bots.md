---
title: Требования и рекомендации для медиа-ботов, размещаемых в приложениях
description: Узнайте, как создавать размещенные в приложениях боты мультимедиа для Microsoft Teams, масштабируемость и производительность. См. примеры для различных сценариев удаленного и локального мультимедиа.
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 11/16/2018
ms.openlocfilehash: 8643575f2fcb64cbfe6349c32d0b1b3df98ea31e
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100877"
---
# <a name="requirements-and-considerations-for-application-hosted-media-bots"></a>Требования и рекомендации для медиа-ботов, размещаемых в приложениях

An application-hosted media bot requires the [`Microsoft.Graph.Communications.Calls.Media` .NET library](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) to access the audio and video media streams. The bot must be deployed on a Windows Server on-premises machine or a Windows Server guest Operating System (OS) in Azure.

> [!NOTE]
>
> * Руководство по разработке ботов для обмена сообщениями и интерактивного голосового ответа (IVR) не полностью применимо к созданию ботов мультимедиа, размещаемых в приложениях.
> * Поскольку Microsoft Real-time Media Platform для ботов находится на стадии предварительной версии для разработчиков, рекомендации в этом документе могут быть изменены.

## <a name="c-or-net-and-windows-server-for-development"></a>C# или .NET и Windows Server для разработки

Для медиа-бота, размещаемого в приложении, требуется следующее:

* Бот должен быть разработан на C# и стандартной платформе .NET Framework и развернут в Microsoft Azure. Нельзя использовать API-интерфейсы C++ и Node.js для доступа к мультимедиа в реальном времени, а .NET Core не поддерживается для ботов мультимедиа, размещенных в приложении.

* Бот может быть размещен в одной из следующих сред службы Azure:
  * Облачная служба
  * Service Fabric с масштабируемыми наборами виртуальных машин (VMSS).
  * Инфраструктура как услуга (IaaS) Виртуальная машина (ВМ).  
  
* Невозможно развернуть бот как веб-приложение Azure.

* Бот должен работать в последней версии библиотеки .NET.`Microsoft.Graph.Communications.Calls.Media`. Бот должен использовать новейшую доступную версию [пакета NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) или версию не старше трех месяцев. Более старые версии библиотеки устарели и не работают через несколько месяцев. Поддержание `Microsoft.Graph.Communications.Calls.Media` библиотеки в актуальном состоянии обеспечивает наилучшее взаимодействие между ботом и Microsoft Teams.

В следующем разделе содержится подробная информация о том, где находятся мультимедийные вызовы в реальном времени.

## <a name="real-time-media-calls-stay-where-theyre-created"></a>Вызовы мультимедиа в режиме реального времени остаются там, где они создаются

Мультимедийные вызовы в реальном времени остаются на том компьютере, на котором они были созданы. Мультимедийный вызов в реальном времени закрепляется за экземпляром виртуальной машины (ВМ), который принял или инициировал вызов. Мультимедиа из звонка или собрания Teams передаются в этот экземпляр виртуальной машины, а мультимедиа, отправляемые ботом обратно в Teams, также должны поступать с этой виртуальной машины. Если при остановке виртуальной машины выполняются какие-либо мультимедийные вызовы в реальном времени, эти вызовы внезапно прерываются. Если бот заранее знает об ожидающем отключении виртуальной машины, он может завершить вызовы.

В следующем разделе приведены сведения о доступности медиа-ботов, размещаемых в приложениях.

## <a name="application-hosted-media-bots-accessible-on-the-internet"></a>Медиа-боты, размещенные в приложениях, доступны в Интернете

Медиа-боты, размещаемые в приложениях, должны быть напрямую доступны в Интернете. Эти боты должны включать следующие функции:

* Каждый экземпляр виртуальной машины, на котором размещается мультимедийный бот, размещенный в приложении, в Azure, должен быть напрямую доступен из Интернета с использованием общедоступного IP-адреса на уровне экземпляра (ILPIP).
  * Чтобы получить и настроить ILPIP для облачной службы Azure, см. [Классический обзор общедоступного IP-адреса на уровне экземпляра](/azure/virtual-network/virtual-networks-instance-level-public-ip).
  * Чтобы настроить ILPIP для масштабируемого набора виртуальных машин, см. [Общедоступный IPv4 для каждой виртуальной машины](/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine).
* Служба, в которой размещается бот мультимедиа, размещаемый в приложении, также должна настроить каждый экземпляр виртуальной машины с общедоступным портом, который сопоставляется с конкретным экземпляром.
  * Облачной службе Azure для этого требуется входная конечная точка экземпляра. Подробнее в статье [Включение связи для экземпляров ролей в Azure](/azure/cloud-services/cloud-services-enable-communication-role-instances).
  * Для масштабируемого набора виртуальных машин необходимо настроить правило NAT в подсистеме балансировки нагрузки. Подробнее в статье [Виртуальные сети и виртуальные машины в Azure](/azure/virtual-machines/windows/network-overview).

* Боты мультимедиа, размещенные в приложении, не поддерживаются эмулятором Bot Framework.

В следующем разделе приведены подробные сведения о масштабируемости и производительности медиа-ботов, размещаемых в приложениях.

## <a name="scalability-and-performance-considerations"></a>Рекомендации по масштабируемости и производительности

Для ботов мультимедиа с приложениями необходимо учитывать масштабируемость и производительность:

* Для ботов мультимедиа, размещенных в приложениях, требуется больше вычислительных ресурсов и пропускной способности сети (пропускной способности), чем для ботов обмена сообщениями, что может привести к более высоким эксплуатационным затратам. Разработчик медиа-бота в реальном времени должен тщательно измерить масштабируемость бота и убедиться, что бот не принимает больше одновременных вызовов, чем может обработать. Бот с поддержкой видео может поддерживать только один или два одновременных мультимедийных сеанса на ядро ​​​​ЦП (при использовании ''сырых'' видеоформатов RGB24 или NV12).
* Платформа мультимедиа в реальном времени сейчас не использует какие-либо графические процессоры (GPU), доступные на виртуальной машине, для разгрузки кодирования и декодирования видео H.264. Вместо этого кодирование и декодирование видео выполняются программно на ЦП. Если доступен графический процессор, бот может использовать его для собственной отрисовки графики, например, если бот использует модуль 3D-графики.
* Экземпляр ВМ, на котором размещается медиа-бот в реальном времени, должен иметь как минимум 2 ядра ЦП. Для Azure рекомендуется виртуальная машина серии Dv2. Для других типов виртуальных машин Azure требуется как минимум система с четырьмя виртуальными ЦП (вЦП). Подробная информация о типах ВМ Azure доступна в [Документации по Azure](/azure/virtual-machines/windows/sizes-general).

## <a name="code-sample"></a>Пример кода

Ниже приведены примеры медиа-ботов, размещенных в приложении.

| **Название примера** | **Описание** | **Microsoft Graph** |
|------------|-------------|-----------|
| Образец локального мультимедиа | Пример, иллюстрирующий различные сценарии локальных носителей. | [Просмотр](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples) |
| Пример удаленного мультимедиа | Пример, иллюстрирующий различные сценарии удаленного носителя. | [Просмотр](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/RemoteMediaSamples) |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Поддерживаемые форматы медиа](~/resources/media-formats.md)

## <a name="see-also"></a>Дополнительные ресурсы

* [Документация SDK по вызову Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
* Боты требуют больше вычислительных ресурсов и пропускной способности сети, чем боты обмена сообщениями, и требуют более высоких эксплуатационных расходов. Разработчик медиа-бота в реальном времени должен тщательно измерить масштабируемость бота и убедиться, что бот не принимает больше одновременных вызовов, чем может обработать. Бот с поддержкой видео может поддерживать только один или два одновременных мультимедийных сеанса на ядро ​​ЦП при использовании необработанных видеоформатов RGB24 или NV12.
* Платформа мультимедиа в режиме реального времени в настоящее время не использует преимущества графических процессоров (GPU), доступных на виртуальной машине для загрузки или декодирования видео H.264. Вместо этого кодирование и декодирование видео выполняются программно на ЦП. Если доступен графический процессор, бот использует его для собственной отрисовки графики, например, если бот использует модуль 3D-графики.
* Экземпляр ВМ, на котором размещается медиа-бот в реальном времени, должен иметь как минимум 2 ядра ЦП. Для Azure рекомендуется виртуальная машина серии Dv2. Для других типов виртуальных машин Azure требуется минимальный размер системы с 4 виртуальными ЦП (вЦП). Подробнее о типах ВМ Azure в [Документации Azure](/azure/virtual-machines/windows/sizes-general).

В следующем разделе представлены примеры, иллюстрирующие различные сценарии использования локальных носителей.

## <a name="samples-and-additional-resources"></a>Образцы и дополнительные ресурсы

* [Образцы приложений](https://github.com/microsoftgraph/microsoft-graph-comms-samples/tree/master/Samples/V1.0Samples/LocalMediaSamples)
* [Документация SDK по вызову Graph](https://microsoftgraph.github.io/microsoft-graph-comms-samples/docs/)
