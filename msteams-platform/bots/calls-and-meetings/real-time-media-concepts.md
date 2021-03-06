---
title: Вызовы мультимедиа в режиме реального времени и встречи с Microsoft Teams
description: Понимание ключевых понятий в создании бота, который может проводить аудио- и видеозвоки в режиме реального времени, а также собрания в Интернете.
ms.topic: conceptual
localization_priority: Normal
keywords: аудиопоток видеопотока аудио- и видеосвязи собрания в режиме реального времени мультимедиа-приложений, размещенной в средствах массовой информации, размещенной в средствах массовой информации
ms.openlocfilehash: deedc47f67fe6848cf7f84457247d2271257e3f0
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020157"
---
# <a name="real-time-media-calls-and-meetings-with-microsoft-teams"></a>Вызовы и встречи с Microsoft Teams

Медиаплатформа в режиме реального времени позволяет ботам взаимодействовать с Microsoft Teams и собраниями с помощью обмена голосом, видео и экранами в режиме реального времени. Это расширенный потенциал, который позволяет боту отправлять и получать кадр голосового и видеоконтента по кадру. Бот имеет необработанные доступ к потокам мультимедиа для обмена голосом, видео и экранами. Существуют более простые медиа-боты, которые используют медиаплатформу в режиме реального времени для всех средств обработки мультимедиа. Боты, которые сами обработать носители, называются медиа-ботами с хостингом приложений.

Например, при вызове 1:1 с ботом, как говорит пользователь, бот получает 50 аудиорамок в секунду, каждый кадр содержит 20 миллисекунд (ms) звука. В режиме реального времени при приеме аудиокадров может выполняться распознавание речи в режиме реального времени, а не ждать записи после того, как пользователь перестает говорить. Кроме того, бот может отправлять и получать видео с высоким разрешением, в том числе контент для совместного доступа к экранам на основе видео.

Платформа предоставляет простой API, похожий на розетку, для бота для отправки и получения мультимедиа. Он обрабатывает кодировки и декодирования аудио- или видео пакетов в режиме реального времени с помощью кодеков, таких как SILK и G.722 для аудио и H.264 для видео. Платформа также обрабатывает все шифрование пакетов мультимедиа или расшифровку и передачу пакетов сети автоматически. Бот имеет дело только с фактическим аудио- или видеоконтентом. Медиа-бот в режиме реального времени участвует в вызовах 1:1, а также в собраниях с несколькими участниками.

## <a name="media-session"></a>Сеанс мультимедиа

Когда медиа-бот в режиме реального времени отвечает на входящий вызов или присоединяется к собранию Teams, он должен объявить, какие методы он должен поддерживать. Для каждого поддерживаемого модальности бот объявляет, может ли он отправлять и получать носителю, получать только или отправлять только. Например, бот, предназначенный для обработки вызовов 1:1 Teams, должен отправлять и получать звук, но только отправлять видео, так как для получения видео вызываемого не требуется. Набор режимов аудио- и видеосвязи, установленных между ботом и Teams или собранием, называется сеансом мультимедиа.

Поддерживаются два типа видео- и видео- и видеоконференции. Основное видео используется для транспортировки видео с веб-камеры пользователя. Совместное использование экрана на основе видео позволяет пользователю делиться своим экраном в качестве видеопотока. Платформа позволяет боту отправлять и получать оба типа видео.

Когда к собранию Teams, бот может получать несколько основных видеопотоков одновременно до десяти за сеанс мультимедиа. Это позволяет боту видеть несколько участников собрания.

В следующем разделе приводится подробная информация о отправке и получении средства массовой информации в качестве последовательности кадров.

## <a name="frames-and-frame-rate"></a>Частота кадров и кадров

Медиа-бот в режиме реального времени напрямую взаимодействует с режимами аудио- и видеосвязи сеанса мультимедиа. Это означает, что бот отправляет и получает носителю в качестве последовательности кадров, где каждый кадр представляет собой единицу контента. Одна секунда звука передается в качестве последовательности из 50 кадров, каждый кадр содержит 20 мс, что составляет 1/50 секунды содержимого речи. Одна секунда видео передается в качестве последовательности из 30 неуявных изображений, каждая из которых предназначена для просмотра всего за 33,3 мс, что составляет 1/30 секунды до отображения следующего кадра видео. Количество передаваемых или отрисовок кадров в секунду называется частотой кадров.

В следующем разделе приводится подробная информация о аудио- и видеоформате, используемом для звонков и собраний в режиме реального времени.

## <a name="audio-and-video-format"></a>Формат аудио и видео

В аудиоформате каждая секунда звука представлена в виде 16 000 образцов, каждый пример которых содержит 16-битные данные. Аудиорамка 20 мс содержит 320 образцов, что составляет 640 bytes данных.

В формате видео поддерживаются несколько форматов. Двумя ключевыми свойствами формата видео являются размер кадра и цветной формат. Поддерживаемые размеры кадров включают 640x360, то есть 360 пикселей, 1280x720 — 720 пикселей, а 1920x1080 — 1080 пикселей. Поддерживаемые цветовые форматы включают NV12 размером 12 бит на пиксель и RGB24 — 24 бита на пиксель.

Видеокадр 720p содержит 921 600 пикселей, что в 1280 раз больше 720 пикселей. В цветовом формате RGB24 каждый пиксель представлен в виде 3-битных 24-битных компоненты красного, зеленого и синего цветов. Таким образом, для одной видеокадры RGB24 с объемом 720p требуется 2 764 800 бет данных, что составляет 921 600 пикселей, а это 3 б.п. на пиксель. При частоте кадров 30 fps отправка видеорамок RGB24 720p означает обработку примерно 80 мегабайт в секунду контента, который существенно сжимается видео-кодеком H.264 перед сетевой передачей.

Расширенные возможности платформы позволяют боту отправлять или получать видео в качестве закодированной кадров H.264. Это поддерживает ботов, которые предоставляют собственный коддер или декодер H.264 или не требуют декодирования видеопотока в необработанные битм-карты RGB24 или NV12.

В следующем разделе приводится подробная информация о том, какие участники собрания говорят, которые являются активными и доминирующими ораторами.

## <a name="active-and-dominant-speakers"></a>Активные и доминирующие динамики

Когда к собранию Teams, состоящему из нескольких участников, бот может определить, какие участники собрания в настоящее время говорят. Активные динамики определяют, какие участники слышны в каждом полученном звуковом кадре. Доминирующие динамики определяют, какие участники в настоящее время являются наиболее активными или доминирующими в групповой беседе, даже если их голос не слышен в каждом звуковом кадре. Набор доминирующих динамиков может изменяться по мере того, как разные участники по очереди говорят.

В следующем разделе приводится подробная информация о запросах на подписку на видео, сделанных ботом.

## <a name="video-subscription"></a>Подписка на видео

При вызове 1:1 бот автоматически получает видео вызываемого, если бот включен для получения видео. Во время Teams, бот должен указать платформе, какие участники он хочет видеть. Подписка на видео — это запрос бота на получение основного видео или контента для обмена экранами участника. По мере того как участники собрания ведут беседу, бот изменяет нужные подписки на видео на основе обновлений доминирующего набора динамиков или уведомлений, указывающих, какой участник в настоящее время обменивается экранами.

В следующем разделе приводится подробная информация о том, что необходимо установить, а также требования к разработке медиа-бота с хостингом приложения.

## <a name="developer-resources"></a>Ресурсы разработчика

Чтобы разработать медиа-бот с хостингом приложения, необходимо установить [Microsoft.Graph. Библиотека Calls.Media .NET NuGet](https://www.nuget.org/packages/Microsoft.Graph.Communications.Calls.Media/) в рамках Visual Studio проекта.

Для веб-ботов мультимедиа с приложениями требуется .NET или C# и Windows Server. Дополнительные сведения см. в дополнительных сведениях о требованиях и соображениях к медийным ботам с [хостингом приложений.](requirements-considerations-application-hosted-media-bots.md#c-or-net-and-windows-server-for-development)

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Регистрация бота вызовов](~/bots/calls-and-meetings/registering-calling-bot.md)
