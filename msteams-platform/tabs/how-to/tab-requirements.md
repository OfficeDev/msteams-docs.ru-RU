---
title: Требования к вкладке
author: laujan
description: Каждая вкладка в Microsoft Teams должна соответствовать этим требованиям.
keywords: Настраиваемый канал группы вкладок teams
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1f5a3eaa8ca16878944288d5dbbfa78cfe9fa3ce
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797944"
---
# <a name="tab-requirements"></a>Требования к вкладке

Вкладки Teams должны соответствовать следующим требованиям:

* Необходимо разрешить, чтобы страницы вкладок обслуживались в iFrame с помощью X-Frame-Options и/или http-response-headers content-Security-Policy.
  * Установите заголок: `Content-Security-Policy: frame-ancestors teams.microsoft.com *.teams.microsoft.com *.skype.com`
  * Для совместимости Internet Explorer 11 также установите `X-Content-Security-Policy` этот режим.
  * Кроме того, установите заголок. `X-Frame-Options: ALLOW-FROM https://teams.microsoft.com/` Этот заголовщик является неподдеравающим, но по-прежнему соблюдается большинством браузеров.
* Как правило, в качестве меры защиты от разметки щелчка страницы входа не отрисовыются в iFrame. Следовательно, логика проверки подлинности должна использовать метод, не относячий к перенаправлению (например, использовать проверку подлинности на основе маркеров или файлов cookie).

> [!NOTE]
> Chrome 80, запланированный на начало 2020 г., представляет новые значения файлов cookie и по умолчанию налагает политики файлов cookie. Рекомендуется устанавливать предназначенное для файлов cookie использование, а не полагаться на поведение браузера по умолчанию. *См.* [атрибут cookie SameSite (обновление 2020).](../../resources/samesite-cookie-update.md)

* Браузеры придерживаются ограничения политики одинакового источника, которое не позволяет веб-странице делать запросы к домену, который отличается от домена, обслуживаемого веб-страницей. Однако может потребоваться перенаправить страницу конфигурации или контента на другой домен или поддомен. Логика навигации между доменами должна позволять клиенту Teams проверять источник на статическом списке допустимого домена в манифесте приложения при загрузке или связи с вкладкой.

* Чтобы у вас было простое решение, необходимо создать стиль вкладок в зависимости от темы, дизайна и намерения клиента Teams. Как правило, вкладки лучше всего работают, если они построены для решения конкретных задач и фокуса на небольшом наборе задач или подмножество данных, соответствующих расположению канала вкладки.

* На странице контента добавьте ссылку на [клиентский SDK JavaScript для Microsoft Teams](/javascript/api/overview/msteams-client) с помощью тегов скриптов. После загрузки страницы вызовите . `microsoftTeams.initialize()` В этом случае страница не будет отображаться.