---
title: Тестирование и отлагивание бота
description: Описывает, как тестировать ботов в Microsoft Teams
keywords: тестирование ботов команд
ms.topic: how-to
localization_priority: Normal
ms.date: 03/20/2019
ms.openlocfilehash: 269b0680e45d764cf4cb0269c40d3d202145edb8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566462"
---
# <a name="test-and-debug-your-microsoft-teams-bot"></a>Тестирование и отлагивание Microsoft Teams бота

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

При тестировании бота необходимо учитывать как контекст(ы), так и все функциональные возможности, которые могут быть добавлены к боту, которые требуют данных, определенных для Microsoft Teams. Убедитесь, что выбранный метод тестирования бота соответствует его функциональным возможностям.

## <a name="test-by-uploading-to-teams"></a>Проверьте, загрузив Teams

Наиболее полный способ тестирования бота — это создание пакета приложений и его загрузка в Teams. Это единственный способ тестирования всех функциональных возможностей, доступных вашему боту, во всех сферах.

Существует два метода для загрузки приложения. Вы можете использовать [App Studio,](~/concepts/build-and-test/app-studio-overview.md) чтобы помочь вам, или вы можете вручную создать пакет приложений [и](~/concepts/build-and-test/apps-package.md) загрузить [приложение](~/concepts/deploy-and-publish/apps-upload.md). Если необходимо изменить манифест и повторно загрузить приложение, [](#deleting-a-bot-from-teams) перед отправкой измененного пакета приложения следует удалить бот.

## <a name="debug-your-bot-locally"></a>Отламывка бота локально

Если во время разработки вы размещены локально, вам потребуется использовать службу тоннелей, например [ngrok,](https://ngrok.com/) чтобы протестировать бота. После загрузки и установки ngrok запустите приведенную ниже команду, чтобы запустить службу тоннелей. Возможно, вам потребуется добавить ngrok на свой путь.

```bash
ngrok http <port> -host-header=localhost:<port>
```

Используйте конечную точку https, предоставленную ngrok в манифесте приложения. Если вы закроете окно команды и перезапустите, вы получите новый URL-адрес, и вам потребуется обновить конечный адрес бота, чтобы использовать его.

## <a name="testing-your-bot-without-uploading-to-teams"></a>Тестирование бота без загрузки в Teams

Иногда может потребоваться протестировать бот, не устанавливая его в качестве приложения в Teams. Ниже приведены два метода. Тестирование бота без его установки в качестве приложения может быть полезным для обеспечения того, что бот доступен и отвечает, однако это не позволит вам проверить всю широту функциональных возможностей Microsoft Teams, которые вы могли добавить в бот. Если необходимо полностью протестировать бот, следуйте инструкциям по [тестированию, загрузив](#test-by-uploading-to-teams).

### <a name="use-the-bot-emulator"></a>Использование эмулятора бота

The Bot Framework Emulator это настольное приложение, которое позволяет разработчикам-ботам тестировать и отлагировать свои боты локально или удаленно. С помощью эмулятора можно общаться с ботом и проверять сообщения, которые отправляет и получает бот. Это может быть полезно для проверки того, что ваш бот доступен и отвечает, однако эмулятор не позволит вам проверить какие-либо функциональные возможности, определенные Teams, которые вы добавили в бот, равно как и ответы от бота будут точным визуальным представлением того, как они будут отрисовываны в Teams. Если вам нужно проверить любой из этих вещей, лучше всего [загрузить бот](#test-by-uploading-to-teams).

Полные инструкции по Bot Framework Emulator можно найти [здесь](/azure/bot-service/bot-service-debug-emulator?view=azure-bot-service-4.0&preserve-view=true).

### <a name="talk-to-your-bot-directly-by-id"></a>Поговорите с ботом напрямую по ID

>[!Important]
>Беседа с ботом по ID предназначена только для тестирования.

Вы также можете инициировать беседу с ботом с помощью его ID. Ниже приведены два метода для этого. Когда бот был добавлен с помощью одного из этих методов, он не может быть адресоварен в беседах с каналами, и вы не можете воспользоваться другими возможностями Microsoft Teams приложения, такими как вкладки или расширения обмена сообщениями.

1. На странице [Панель мониторинга](https://dev.botframework.com/bots) бота для бота в **статье Channels** выберите **Добавить Microsoft Teams**. Microsoft Teams запустится с помощью личного чата с ботом.
2. Непосредственно ссылаться на ID приложения вашего бота из Microsoft Teams:
   * На странице [Панель мониторинга бота](https://dev.botframework.com/bots) для бота в **статье Details** скопируйте **ID приложения Microsoft для** бота.
  
     ![Получение приложения для бота](~/assets/images/bots_appid_botframework.png)
  
   * На Microsoft Teams области **чата** выберите значок **Добавить чат.** Для: **вклейте** ID Microsoft App вашего бота.
  
     ![Загрузка приложения для бота](~/assets/images/bots_uploading.png)

     ID приложения должен разрешить имя бота.

   * Выберите бот и отправьте сообщение для начала беседы.
   * Кроме того, вы можете вклеить ID приложения вашего бота в поле поиска в верхнем левом Microsoft Teams. На странице результаты поиска перейдите на вкладку People, чтобы увидеть бота и начать с ним общаться в чате.

Ваш бот получит событие так же, как и боты, добавленные в команду, но без сведений о команде `conversationUpdate` в `channelData` объекте.

## <a name="blocking-a-bot-in-personal-chat"></a>Блокировка бота в личном чате

Обратите внимание, что пользователи могут заблокировать бот от отправки личных сообщений чата. Они могут переметнуть это, щелкнув бот правой кнопкой мыши в канале чата и выбрав **блок-бот-беседу.** Это означает, что ваши боты будут продолжать отправлять сообщения, но пользователь не будет получать эти сообщения.

![Блокировка бота](~/assets/images/bots/botdisable.png)

## <a name="removing-a-bot-from-a-team"></a>Удаление бота из группы

Пользователи могут удалить бот, выбрав значок корзины в списке ботов в представлении команд. Обратите внимание, что это только удаляет бот из использования этой группы; отдельные пользователи по-прежнему смогут взаимодействовать в личном контексте.

Боты в личном контексте не могут быть отключены или удалены пользователем, если не полностью удалить бот из Teams.

## <a name="disabling-a-bot-in-teams"></a>Отключение бота в Teams

Чтобы остановить получение сообщений ботом, перейдите к панели мониторинга ботов и отредактировать канал Microsoft Teams. Очистка **параметра Включить Microsoft Teams.** Это не позволяет пользователям взаимодействовать с ботом, но он по-прежнему будет обнаруживаемым, и пользователи по-прежнему смогут добавлять его в команды.

## <a name="deleting-a-bot-from-teams"></a>Удаление бота из Teams

Чтобы полностью удалить бот из Teams, перейдите к панели мониторинга ботов и отредактировать Microsoft Teams канал. Выберите **кнопку Удалить** в нижней части. Это не позволяет пользователям открывать, добавлять или взаимодействовать с вашим ботом. Обратите внимание, что это не удаляет бота из экземпляров других Teams, хотя он также перестанет функционировать для них.

## <a name="removing-your-bot-from-appsource"></a>Удаление бота из AppSource

Если вы хотите удалить бот из приложения Teams в AppSource (ранее Office Store), необходимо удалить бот из манифеста приложения и повторно переподвести приложение для проверки. Дополнительные сведения см. в [публикации Microsoft Teams приложения в AppSource.](~/concepts/deploy-and-publish/apps-publish.md)
