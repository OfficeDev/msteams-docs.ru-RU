---
title: Составить карту случаев использования для Teams возможностей приложения
author: surbhigupta
description: Определите, как могут работать случаи использования приложения в Teams работе.
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: b374f0ca81402effb548c1cfcb90ed3d316360f1
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068556"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>Составить карту случаев использования для Teams возможностей приложения

После того *как* вы определите, кто является пользователем и какую проблему вы решите, настало время решить, *как* решить проблему.  Кто, *что* и *как* завершает процесс понимания и сопоставления случаев использования для Teams возможностей приложения.  Необходимо определить область приложения на основе полученных от пользователя ответов на запросы, а затем определить, какие возможности лучше всего подходят для создания приложения.

> [!NOTE]
> Вы должны иметь хорошее представление о точках входа и [элементах пользовательского](../../concepts/extensibility-points.md) интерфейса, доступных для вашего приложения. Вы также должны убедиться, что вы [рассмотрели ваши случаи использования](../../concepts/design/understand-use-cases.md) тщательно.

## <a name="choose-the-correct-scope-for-your-app"></a>Выберите правильную область для приложения

При выборе области приложения рассмотрите следующие действия:

* Приложение может существовать в различных сферах.
* Возможности приложения, такие как расширения обмена сообщениями, следуют за пользователями в различных сферах.
* Пользователи часто не могут добавлять приложения в Teams или каналы.
* Гостевых пользователей можно получить доступ к контенту, Teams или каналах.

Вы можете выбрать между личной областью и областью группы или канала для приложения в зависимости от следующих ниже.

* Для личной области задайте следующие вопросы:
  * Существуют ли взаимодействия один на один с приложением, требуемого для конфиденциальности или по другим причинам? Например, проверка баланса отпусков или других частных сведений.
  * Будет ли совместная работа между пользователями, у которых может не быть общих Teams? Например, поиск предстоящих событий для широкой организации в компании.
  * Существуют ли персонализированные уведомления или сообщения, которые необходимо отправлять пользователю во время Teams приложения? Например, напоминания для утверждений или регистраций.
* Для общей области (группы, канала или чата) задайте следующие вопросы:
  * Являются ли сведения, представленные приложением на вкладке или с помощью бота, актуальными и полезными для большинства участников группы? Например, приложение Scrum.
  * Может ли контекст приложения измениться в зависимости от команды, в которую оно добавлено? Например, задачи планировщика отличаются в разных командах. 
  * Возможно ли, что все члены в персоне, которые должны сотрудничать, являются частью одной команды? Например, агенты, работающие над билетом.

В следующих сценариях вы сможете понять выбор точек входа и элементов пользовательского интерфейса, которые хорошо работают с возможностями Teams приложения:

> [!NOTE]
> Это не исчерпывающий список, но поможет вам продумать некоторые возможности, доступные для вас.

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>Создание, совместное и совместное создание элементов во внешней системе

Приложение для Microsoft Teams — это отличный способ взаимодействия с данными, из чего можно выбрать различные точки интеграции.

* **Расширения обмена сообщениями с командами** поиска: поиск внешних систем и обмен результатами в качестве интерактивной карты.

* **Расширения обмена сообщениями с командами действий:** сбор сведений для вставки в хранилище данных или выполнения расширенных поисков.

* **Вкладки.** Создание встроенных веб-опытом для просмотра, работы с данными и обмена ими.

* **Соединители и** веб-окки: простой способ нажать данные и отправить данные из Teams клиента.

* **Модули задач:** интерактивные модальные формы, откуда бы они ни были нужны для сбора или отображения информации.

## <a name="initiate-workflows-and-processes"></a>Инициировать процессы и процессы

Иногда просто требуется быстрый способ запуска процесса или рабочего процесса во внешней системе.

* **Команды действий** расширения обмена сообщениями: Триггер из сообщений, что позволяет пользователям быстро отправлять содержимое сообщения в веб-службы.

* **Модули задач:** Откройте их со вкладки, бота или расширения обмена сообщениями для сбора информации перед началом рабочего процесса.

* **Диалоговые боты.** Взаимодействуйте с пользователями с помощью текстовых и богатых карт.

* **Исходяние** веб-ок. Это хороший выбор для простого взаимодействия взад и вперед, если вам не нужно создавать весь разговорный бот.

## <a name="send-notifications-and-alerts"></a>Отправка уведомлений и оповещений

Отправка асинхронных уведомлений и оповещений пользователям в Teams. Используйте интерактивные карты, чтобы обеспечить быстрый доступ к часто используемым действиям и ссылкам на дополнительные сведения.

* **Диалоговые боты:** отправка активных сообщений группам, каналам или отдельным пользователям.

* **Соединители и входящие веб-окки:** разрешить каналу подписываться на получение сообщений. Соединитектор позволяет пользователям адаптировать подписку со страницей конфигурации.

## <a name="ask-questions-and-get-answers"></a>Задавать вопросы и получать ответы

У людей есть вопросы, и вы, вероятно, получили много ответов, хранимые где-то. К сожалению, часто довольно сложно подключить эти два.

* **Разговорные боты:** обработка естественного языка, ИИ, машинное обучение и все модные слова. Используйте бот, подключенный к интеллектуальному облаку, чтобы подключить пользователей к нужным ответам.

* **Вкладки.** Встраивайте существующий веб-портал в Teams или создайте Teams для добавленных функциональных возможностей.

## <a name="get-social"></a>Получить социальные

Платформа совместной работы по своей сути является социальной платформой. Позвольте вашей творческой стороне быть свободной и добавить немного веселья на рабочем месте. Все пользователи должны иметь возможность отправлять шутки, давать пометки, получать мемы, вышмеить некоторые эмодзи или что-либо еще, что поражает вашу фантазию.

## <a name="think-in-terms-of-a-single-page-app"></a>Мыслить с точки зрения одно-страницного приложения

Вкладки — это встроенные веб-страницы. Практически все, что вы можете сделать в SPA, вы можете сделать на вкладке в Teams. Просто обратите внимание на область действия. Вкладки группы и канала для общих вкладки и личные вкладки для личного опыта. Список вещей команды отправляется на вкладку канала, а список ваших вещей отправляется на личную вкладку.

## <a name="start-small"></a>Запуск с малого

Не знаете, с чего начать? Чувствуя себя немного перегружены с удивительным разнообразием вариантов, доступных для вас? Необходимо выбрать основную функцию приложения и запустить ее. После того как вы почувствуете поток информации в различных контекстах в Teams, гораздо проще представить более сложное взаимодействие.

## <a name="put-it-all-together"></a>Сложить все вместе

При этом лучшие приложения обычно сочетают в себе несколько функций, создав приложение, которое в нужный момент вовлекет пользователей в нужный контекст с нужными функциональными возможностями. Вы не должны принудить какие-либо функциональные возможности к месту, которое ему не принадлежит. Просто потому, что у вас есть хороший один к одному разговорный бот не означает, что вы добавляете его в любую команду. Различные точки разнонабности хорошо для разных вещей, играть на их сильные стороны для создания успешного приложения.

## <a name="see-also"></a>Дополнительные материалы

[Создание приложений для Microsoft Teams](../../overview.md)
