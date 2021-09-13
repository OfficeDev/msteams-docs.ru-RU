---
title: 1-на-1 беседы с ботами
description: Описывает конечный сценарий беседы 1 на 1 с ботом в Microsoft Teams
keywords: сценарии команд 1on1 1to1 беседы бота
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 2fd76b8bc5fa4cd260b70e15b92bef2dec2de683
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 09/12/2021
ms.locfileid: "59156109"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>Личная беседа (один на один) с Microsoft Teams ботом

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams позволяет пользователям вести прямые беседы с ботами, построенными на [Microsoft Bot Framework.](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) Пользователи могут найти ботов в галерее Discover Apps и добавить их в Teams для личных бесед. Владельцы и пользователи группы с соответствующими разрешениями также могут добавлять ботов в качестве членов группы. Дополнительные сведения см. в ссылке [Interact in a team channel,](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)которая не только делает их доступными в каналах этой группы, но и для личного чата для всех этих пользователей.

Личный чат отличается от чата в каналах тем, что пользователю не нужно @mention бота. Если бот используется в нескольких контекстах, таких как личный, групповой или канал, необходимо определить, находится ли бот в групповом чате или канале, и обрабатывать сообщения немного по-другому. Дополнительные сведения см. в [ссылке Interact in a team channel or group chat.](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)

## <a name="designing-a-great-personal-bot"></a>Проектирование большого личного бота

Отличный бот в Microsoft Teams помогает пользователям получать необходимую информацию в контексте Teams. Личные беседы с ботом — это частные обмены между ботом и его пользователем; это отличный способ предоставить сведения, соответствующие данному пользователю в личном контексте. Бот в личном чате — это диалоговое окно между вашей службой и отдельным человеком, где бот в групповом чате или канале передает все группе людей.

В зависимости от возможностей, которые необходимо создать, боту может потребоваться работать в нескольких сферах — личном, групповом и командном. Работа по поддержке более чем одной области минимальна. Существует никаких ожиданий в Teams, что ваш бот функции во всех сферах, но вы должны убедиться, что ваш бот имеет смысл и предоставляет пользователю значение в любой области (ы) вы решите поддерживать.

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>Best practice: Welcome messages in personal conversations

Ваш бот [должен](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) заблаговременно отправлять приветствие в личный чат в первый раз (и только в первый раз) пользователь инициирует личный чат с ботом. Эта рекомендация не применяется к первым контактам в канале.
