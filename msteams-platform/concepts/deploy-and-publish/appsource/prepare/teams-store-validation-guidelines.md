---
title: Microsoft Teams проверки хранения
description: Описывает правила, которые должны следовать всем приложениям, представленным в Teams (AppSource).
author: heath-hamilton
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 79cdc032ee1e7479f7737e5dc71f8f01bb024da8
ms.sourcegitcommit: 25539046d408c4270b988fd826d7cf1275f4b9dd
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 06/04/2021
ms.locfileid: "52763117"
---
# <a name="microsoft-teams-store-validation-guidelines"></a>Microsoft Teams проверки хранения

В соответствии с этими рекомендациями повышается вероятность того, что ваше приложение пройдет процесс Microsoft Teams хранения. Эти Teams, которые дополняют политики сертификации коммерческих рынков [Майкрософт](/legal/marketplace/certification-policies) и часто обновляются с учетом новых возможностей, отзывов пользователей и изменений бизнес-правил.

> [!NOTE]
> Некоторые рекомендации могут не применяться к вашему приложению. Например, если в вашем приложении нет бота, можно игнорировать рекомендации, связанные с ботами.

## <a name="value-proposition"></a>Предложение значения

### <a name="app-name"></a>Имя приложения

Имя приложения играет важную роль в том, как пользователи обнаруживают его в магазине. Помните следующее о именах приложений:

* Имя должно включать термины, соответствующие вашим пользователям.
* Имена основных Teams функций&#8212;, таких как **Chat,** **Contacts**, **Calendar**, **Calls**, **Files**, **Activity**, **Teams,** **Apps** и **Help**&#8212;не должны быть включены в имя приложения.
* Общие существители должны быть префиксом или суффиксом с именем разработчика (например, **Задачи Contoso,** а не **задачи).**
* Не следует **использовать Teams** или другие имена продуктов Майкрософт, которые могут ложно указывать на совместное брендинг или совместное продажу. (Дополнительные сведения о ссылках на программное обеспечение, продукты и службы Майкрософт см. в руководстве по товарным знакам и [брендам Майкрософт).](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general)
* Если ваше приложение является частью официального партнерства с Корпорацией Майкрософт, имя приложения должно быть первым (например, **Contoso Connector для Microsoft Teams).**
* Не следует копировать имя приложения, перечисленного в магазине или другого предложения на коммерческом рынке.
* Не должен содержать ненормативную или пренебожную лексику. Имя также не должно включать расовый или культурный нечувствительный язык.
* Должно быть уникальным. Например, нельзя перечислить несколько приложений для разных регионов с одинаковым именем и функциональными возможностями.

### <a name="suitable-for-workplace-consumption"></a>Подходит для потребления на рабочем месте

Содержимое приложения должно быть подходящим для общего потребления на рабочем месте и соблюдать все ограничения, перечисленные в политиках сертификации коммерческих рынков. Запрещается контент, связанный с религией, политикой, азартными играми и длительными развлечениями. Дополнительные сведения см. в политике сертификации коммерческих [рынков.](/legal/marketplace/certification-policies#10010-inappropriate-content)

Ваше приложение должно облегчить совместную работу с группой, повысить производительность отдельных лиц или и то, и другое. Приложения, предназначенные для склейки и общения с командой, должны быть совместными и предназначены для нескольких участников. Эти типы приложений также не должны требовать значительных затрат времени или ощутимо влиять на производительность.

### <a name="similar-platforms-and-services"></a>Аналогичные платформы и службы

Приложения должны сосредоточиться на Teams и не включать имена, значки или изображения других аналогичных платформ или служб на основе чата, если ваше приложение не обеспечивает определенную совместную работу.

### <a name="feature-names"></a>Имена функций

Имена функций приложений в кнопках и другом тексте пользовательского интерфейса не должны противоречить терминологии, зарезервированной для Teams и других продуктов Майкрософт. Например, **Начните собрание,** **вызов или** **начните чат.** Включите имя приложения, если этого не удалось полностью избежать, например собрание **Start Contoso** вместо **start meeting.**

## <a name="security"></a>Безопасность

### <a name="microsoft-365-app-compliance-program"></a>Соответствие требованиям для приложений Microsoft 365

Программа [Microsoft 365 приложения](/microsoft-365-app-certification/overview) предназначена для того, чтобы помочь организациям оценить риски и управлять ими, оценив сведения о безопасности и соответствии требованиям о вашем приложении. Если вы публикуете приложение в Teams магазине, необходимо выполнить следующие уровни программы:

* [Publisher проверки:](/azure/active-directory/develop/publisher-verification-overview)помогает администраторам и конечным пользователям понять подлинность разработчиков приложений, интегрируясь с платформа удостоверений Майкрософт. По завершению синий "проверенный" значок отображается на диалоговом Azure Active Directory согласия (Azure AD) и на других экранах. Дополнительные сведения см. в [](/azure/active-directory/develop/mark-app-as-publisher-verified)часто [задаваемом вопросе,](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)о том, как пометить ваше приложение как проверенного издателя и устранить [неполадки в проверке издателя.](/azure/active-directory/develop/troubleshoot-publisher-verification)
* [Publisher:](/microsoft-365-app-certification/docs/attestation)процесс, в котором вы делитесь общими данными, обработкой данных, а также сведениями о безопасности и соответствии требованиям, чтобы помочь потенциальным клиентам принимать обоснованные решения об использовании приложения.

> [!NOTE]
> Если вы отправили приложение, которое не было перечислены ранее, вы не можете официально завершить проверку Publisher до тех пор, пока ваше приложение не будет Teams магазине. Если вы обновляете перечисленное приложение, Publisher проверку перед отправкой последней версии приложения.

### <a name="bots"></a>Боты

Для приложений, которые используют службу Microsoft Azure ботов (например, боты и расширения обмена сообщениями), необходимо соблюдать все требования, определенные в терминах Microsoft [Online Services.](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46)

Боты должны всегда спрашивать разрешения на отправку файла и отображение сообщения подтверждения после отправки файла.

### <a name="external-domains"></a>Внешние домены

В большинстве случаев не следует включать в конфигурации домена приложения домены, не включающие подконтрольные организации (в том числе поддиальды) и службы тоннелей. К следующим исключениям относятся следующие:

* Если ваше приложение использует OAuthCard службы Azure Bot, необходимо включить в качестве допустимого домена или кнопка Вход не `token.botframework.com` будет работать. 
* Если приложение полагается на SharePoint, можно включить связанный корневой SharePoint как допустимый домен с помощью `{teamSiteDomain}` свойства контекста.

### <a name="authentication"></a>Проверка подлинности

Сведения о реализации проверки подлинности приложений см. в [Teams.](~/concepts/authentication/authentication.md)

#### <a name="authenticating-with-external-services"></a>Проверка подлинности с помощью внешних служб

Помните следующее, если ваше приложение проверки подлинности пользователей с помощью внешней службы.

* **Вход, вход и регистрацию опытом:**
  * Приложения, зависят от внешних учетных записей или служб, должны предоставлять четкий и простой вход, вход и регистрацию.
  * Когда пользователь выходит, он должен выйти только из приложения и оставаться входным в Teams.
* Возможности обмена контентом. Приложения, которые требуют проверки подлинности с внешней службой для общего доступа к контенту в Teams каналах, должны четко указанить в справке документацию (или аналогичные ресурсы), как отключить или отключить контент, если эта функция поддерживается во внешней службе. Это не означает, что в вашем приложении должна присутствовать возможность Teams контента.

#### <a name="government-community-cloud-listings"></a>облако сообщества для государственных организаций списков

Чтобы распространять приложение для облако сообщества для государственных организаций (GCC) пользователей, избегая дублирования списков в магазине Teams, процесс проверки подлинности должен определять и маршрутировать пользователей на определенный GCC или ожидаемый URL-адрес.

### <a name="sensitive-content"></a>Конфиденциальный контент

Ваше приложение не должно размещать конфиденциальные данные, такие как данные кредитной карты или финансовых инструментов оплаты. Приложение также не должно отображать сведения о состоянии здоровья, отслеживании контактов или других идентифицируемых лично данных (PII) для аудитории, не предназначенной для просмотра этого контента.

Предостеречь пользователей перед загрузкой файлов или исполняемых файлов (.exe) в компьютер или среду пользователя.

### <a name="financial-information"></a>Финансовые сведения

Приложения не должны просить пользователей делать платежи в Teams интерфейсе. Сведения о финансовых инструментах не должны передаваться пользователям с помощью интерфейса бота.

Вы можете связаться с защищенными внешними платежами только в том случае, если вы сделали соответствующее раскрытие с точки зрения использования, политики конфиденциальности или любой страницы профиля или веб-сайта до того, как пользователь согласился использовать приложение.

Приложения, работающие на iOS или Android версии Teams должны придерживаться следующих рекомендаций:

* Приложения не должны включать покупки в приложении, пробные предложения или пользовательский интерфейс, которые направлены на то, чтобы довести до платных версий или ссылок на интернет-магазины, где пользователи могут приобрести или приобрести другой контент, приложения или надстройки.
* Если вашему приложению требуется учетная запись, пользователи должны иметь возможность зарегистрироваться для учетной записи бесплатно. Использование бесплатной **или** бесплатной учетной записи **термином** запрещено.
* Вы можете определить, активна ли учетная запись на неопределенный срок или на ограниченное время, но если срок действия учетной записи истекает, не будет показан пользовательский интерфейс, текст или ссылки, указывающие на необходимость оплаты.
* Политика конфиденциальности вашего приложения и условия использования страниц должны быть свободны от любого пользовательского интерфейса или ссылок, связанных с коммерцией.

## <a name="general-functionality-and-performance"></a>Общие функциональные возможности и производительность

### <a name="launching-external-functionality"></a>Запуск внешних функций

Приложения не должны принимать пользователей из-за Teams для основных сценариев пользователей. Содержимое приложения и взаимодействия могут возникать в Teams, таких как боты, карты и модули задач.

Вы должны связать пользователей в Teams, а не с внешним сайтом или приложением. Для сценариев, которые требуют внешних функций, приложение должно иметь явное разрешение пользователя для запуска этой функции.

### <a name="compatibility"></a>Совместимость

Приложения должны быть полностью функциональными в следующих операционных системах и браузерах:

* Microsoft Windows 7 и более поздней
* macOS 10.10 и более поздней
* Microsoft Edge 12 и более поздних версий
* Mozilla Firefox 47.0 и более поздний
* Google Chrome 51.0 и более поздний
* iOS 9.0 и более поздней
* Android 4.4 и более поздний

### <a name="response-time"></a>Response time (Время ответа)

Teams приложения должны отвечать в разумные сроки, которые зависят от возможностей.

* Вкладки должны отвечать в течение трех секунд или отображать сообщение о загрузке или предупреждение.
* Боты должны отвечать на команды пользователей в течение двух секунд или отображать индикатор ввода.
* Расширения обмена сообщениями должны отвечать на команды пользователей в течение пяти секунд.
* Уведомления должны отображаться в течение пяти секунд после действия пользователя.

## <a name="app-package-and-store-listing"></a>Список пакета приложений и магазина

Пакеты приложений должны быть правильно отформатированы и включают все необходимые сведения и компоненты.

### <a name="app-manifest"></a>Манифест приложения

Манифест Teams определяет конфигурации вашего приложения.

* Манифест должен соответствовать последней схеме манифеста. Сведения см. в [справке манифеста](~/resources/schema/manifest-schema.md).
* Если приложение включает расширение бота или обмена сообщениями, манифест должен соответствовать метаданным Bot Framework, включая имя бота, логотип, ссылку на политику конфиденциальности и условия ссылки на службу.
* Если приложение использует Azure Active Directory (Azure AD) для проверки подлинности, включите в манифест идентификацию приложения Azure AD (клиент). Дополнительные сведения см. в [справке манифеста](~/resources/schema/manifest-schema.md#webapplicationinfo).

### <a name="app-icons"></a>Значки приложений

Значки являются одним из основных элементов, которые люди видят при просмотре Teams магазина. Значки должны сообщать о фирме и цели приложения, придерживаясь следующих требований:

* Пакет приложения должен включать две версии значка приложения PNG: значок цвета и значок контура.
* Цветная версия значка отображается в большинстве Teams и должна быть 192x192 пикселей. Символ значка (96x96 пикселей) может быть любым цветом или цветом, но он должен сидеть на твердом или полностью прозрачном квадратном фоне.
* Схематическая версия значка отображает, когда приложение используется и "подъехалось" на панели приложений слева от Teams и когда пользователь пин-коды расширения обмена сообщениями вашего приложения. Он должен быть 32x32 пикселей и может быть белым с прозрачным фоном или прозрачным с белым фоном (другие цвета не разрешены). Значок не должен иметь дополнительных обивок вокруг символа.
* Правильно размер и форматированные значки должны быть включены в пакет приложений. Значки также должны соответствовать представленным метаданным списка магазина.

Дополнительные сведения, рекомендации и примеры см. в руководстве Teams [приложения.](~/concepts/build-and-test/apps-package.md#app-icons)

### <a name="app-descriptions"></a>Описания приложений

Вы должны иметь краткое и длинное описание приложения. Описания конфигураций приложений и Центра партнеров должны быть одинаковыми.

Описания не должны прямо или посредством инсинуации диспарентно отгоражить другую марку (microsoft owned or otherwise). Убедитесь, что в описании не содержатся утверждения, которые не могут быть обоснованы (например, "Гарантированное 200-процентное повышение эффективности").

#### <a name="short-description"></a>Краткое описание

Краткое описание — это краткое описание приложения, которое выделяет его предложение и направляется в адрес целевой аудитории.

**Рекомендуется:**

* Сохраняй краткое описание в одном предложении.
* Сначала разместите наиболее важные сведения.
* Включай ключевые слова, которые клиенты, скорее всего, будут искать.

**Не рекомендуется:**

* Повторите имя приложения.
* Используйте слово **app в** кратком описании.

#### <a name="long-description"></a>Подробное описание

Длинное описание может предоставить привлекательный повествование, которое подчеркивает предложение стоимости вашего приложения, основной аудитории и целевой отрасли. Хотя это описание может быть до 4000 символов, большинство пользователей будут читать только между 300-500 слов.

**Рекомендуется:**

* Используйте [Markdown для](https://support.office.com/article/use-markdown-formatting-in-teams-4d10bd65-55e2-4b2d-a1f3-2bebdcd2c772) формата описания.
* Используйте активный голос и поговорите с пользователями напрямую. Например, *вы можете ...*.
* Список функций с точками пули, поэтому проще сканировать описание.
* Четко описывают ограничения, условия или исключения для функций, функций и доставляемых материалов, описанных в списке и связанных с ними материалах, прежде чем пользователь установит приложение. Возможности Teams, поддерживаемые приложением, должны относиться к основным функциям, которые описывается в списке.
* Включаем ссылку справка или поддержка.
* Обратитесь **Microsoft 365** вместо **Office 365**.
* Если вам нужно ссылаться **на Teams,** напишите первую ссылку как **Microsoft Teams**. Последующие ссылки можно сократить до **Teams.**
* Используйте следующий язык при описании работы приложения с Teams (или Microsoft 365):
  * "... работает с Microsoft Teams".
  * "... работа с Microsoft Teams".
  * "... в Microsoft Teams".
  * "... для Microsoft Teams".

**Не рекомендуется:**

* Более 500 слов.
* Сокращение Microsoft **в качестве MS** **или** **MSFT**.
* Указать, что приложение — это предложение от Корпорации Майкрософт, в том числе с помощью слоганы или taglines Майкрософт.
* Используйте имена брендов, защищенные авторским правом, которые не принадлежат вам.
* Включайте опечатки, грамматические ошибки и ненужные капитализации (например, **Пользователи** вместо **пользователей).**
* Включай ссылки на AppSource.
* Используйте следующий язык, если вы не сертифицированный партнер Майкрософт:
  * "... интегрирована с Microsoft Teams"
  * "... интегрируется с ..."
  * "... создан для ..."
  * "... построено на ..."
  * "... работает на ..."
  * "... включено ..."
  * "... сертифицировано для ..."
  * "... разработано для ..."
  * "... предназначен для ..."

### <a name="screenshots"></a>Снимки экрана

Скриншоты предоставляют видную визуальную предварительную версию приложения в дополнение к имени, значку и описаниям приложения. Помните следующие снимки экрана:

* В списке может быть до пяти снимков экрана.
* Поддерживаемые типы файлов включают PNG, JPEG и GIF.
* Размеры должны быть 1366x768 пикселей.
* Максимальный размер 1024 КБ.

**Рекомендуется:**

* Сосредоточься на возможностях приложения (например, на том, как люди могут общаться с вашим ботом).
* Включите содержимое, которое точно представляет ваше приложение.
* Используйте текст разумно.
* Снимок экрана кадра с цветом, который отражает ваш бренд и включает маркетинговый контент, аналогичный примеру списка [Freshdesk](https://appsource.microsoft.com/product/office/WA104381505?src=office&tab=Overview) (требования к размеру применяются к всему изображению, а не только к скриншоту).

**Не рекомендуется:**

* Показ определенных устройств, например телефонов или ноутбуков.
* Отображение хрома или пользовательского интерфейса, не в приложении.
* Захват любого пользовательского Teams браузера на скриншотах.
* Включите макеты, которые неточно отражают фактический пользовательский интерфейс вашего приложения, например отображение приложения, используемого вне Teams.

> [!TIP]
> Видео может быть наиболее эффективным способом общения, почему люди должны использовать ваше приложение. Видео также первое, что пользователи видят в вашем списке (по умолчанию видео отображается перед скриншотами). Дополнительные сведения см. [в видеоролике для списка магазина.](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#create-a-video)

### <a name="privacy-policy"></a>Политика конфиденциальности

Политика конфиденциальности может быть специфичную для Teams приложения или общей политики для всех служб.

* Если вы используете общий шаблон политики конфиденциальности, вы должны  ссылаться на службы, приложения и платформы, чтобы включить Teams приложение и службу или веб-сайт.
* Должен включать в себя обработку хранения, хранения и удаления пользовательских данных. Необходимо также описать элементы управления безопасностью, которые вы используете для защиты данных.
* Обязательно включите контактные данные.
* Не следует содержать URL-адреса, которые не будут сломлены или для бета-версии или для постановок.
* Не следует включать ссылки на AppSource.

### <a name="terms-of-use"></a>Условия использования

Условия использования должны быть конкретными и применимыми к вашему предложению.

### <a name="support-links"></a>Ссылки на поддержку

URL-адреса поддержки приложения не должны требовать проверки подлинности. Например, пользователям не нужно входить в систему, чтобы связаться с вами.

### <a name="localization"></a>Локализация

Если ваше приложение поддерживает локализацию, в пакет приложения должен быть включен файл с языковыми переводами, отображаемой на основе Teams языкового параметра. Файл должен соответствовать схеме Teams локализации. Дополнительные сведения см. в [Teams схеме локализации.](~/concepts/build-and-test/apps-localization.md)

## <a name="tabs"></a>Вкладки

Если приложение включает вкладку, убедитесь, что оно соответствует этим рекомендациям.

> [!TIP]
> Сведения о создании высококачественного приложения см. в Teams руководства по разработке [вкладок.](~/tabs/design/tabs.md)

### <a name="setup"></a>Настройка

* Установка вкладки не должна затмить нового пользователя. Предоставление сообщения о том, как завершить действие или рабочий процесс.
* Проверка подлинности должна происходить во время установки вкладок, а не после.

### <a name="views"></a>Представления

* Область экрана для входов не должна использовать большие логотипы или отображать всю веб-страницу.
* Содержимое можно упростить, разбив его на несколько вкладок.
* Вкладки не должны иметь дубликат загона. Удалите логотип из iframe, так как на вкладке уже отображаются значок и имя приложения.

### <a name="navigation"></a>Навигация

* Вкладки не должны иметь более трех уровней навигации.
* Вкладки не должны предоставлять навигацию, которая противоречит основному Teams навигации.
* Вторичные и трехуровневые страницы на вкладке должны открываться в представлении уровня 2 и 3 уровня в области основной вкладки, которая осуществляется с помощью сухарей или левого nav. Вы также можете включить следующие компоненты для навигации вкладок:
    * Кнопки назад
    * Заглавные страницы
    * Меню гамбургеров
* Вкладка не должна иметь горизонтального прокрутки.
* Глубокие ссылки на вкладки должны быть связаны не с внешней веб-страницей, а с Teams. Например, модули задач или другие вкладки.
* Вкладки не должны позволять пользователям перемещаться Teams для основного приложения.

### <a name="usability"></a>Usability

* Вкладки должны предоставлять значение, не только размещение существующего веб-сайта.
* Пользователи должны иметь возможность отменить последнее действие на вкладке.
* Вкладки в личном контексте могут агрегировать содержимое из общих экземпляров приложения.
* Вкладки должны реагировать на Teams темы. При смене темы пользователь должен отражать выбор темы приложения.
* Вкладки должны использовать Teams, такие как шрифты Teams, пандусы типа, цветовая палитра, система сетки, движение, тон голоса и так далее, когда это возможно.
* Необходимо включить **вкладку Параметры.**
* Вкладки должны следовать Teams взаимодействия, например, навигации на странице, позиции и использования диалогов, иерархии информации и так далее, когда это возможно.
* Содержимое вкладки в iframe не должно включать функции, имитирующие Teams основных возможностей. Например, боты, расширения обмена сообщениями, вызовы, собрания и так далее.

> [!TIP]
>
> * Включи личный бот вместе с личной вкладке.
> * Разрешить пользователям обмениваться контентом со своей личной вкладки.

## <a name="bots"></a>Боты

Если в вашем приложении есть бот, убедитесь, что оно соответствует этим рекомендациям.

> [!TIP]
> Сведения о создании высококачественного приложения см. в Teams руководства по разработке [ботов.](~/bots/design/bots.md)

### <a name="bot-commands"></a>Команды бота

Анализ входных данных пользователей и прогнозирование намерений пользователей затруднены. Команды ботов предоставляют пользователям набор слов или фраз, которые понимает бот, чтобы им (и вашему боту) не нужно угадать.

* Рекомендуется перечислять поддерживаемые команды ботов в конфигурациях приложений. Эти команды отображаются в поле составить, когда пользователь пытается отправить сообщение боту.
* Все команды, поддерживаемые ботом, должны работать правильно, включая команду **Привет,** **Привет** и **Справка.**

> [!TIP]
> Для личных ботов включите **вкладку Справка,** которая далее описывает, что может сделать ваш бот.

### <a name="bot-welcome-messages"></a>Сообщения приветствия бота

* Боты почти всегда должны отправлять приветствие во время первого запуска. Для лучшего опыта сообщение должно включать предложение о значении бота, настройку бота и краткое описание всех поддерживаемых команд бота. Вы можете отобразить сообщение с помощью адаптивной карты с кнопками для улучшения использования. Дополнительные сведения см. [в сообщении о запуске приветствия бота.](~/bots/how-to/conversations/send-proactive-messages.md)
* Приветствия ботов в каналах и чатах необязательны во время первого запуска, особенно если бот доступен для личного использования и выполняет аналогичные действия. Если ваш бот отправляет приветствия, он не должен отправлять их пользователям по отдельности (это считается [нежелательной почтой).](#bot-message-spamming) В сообщении также должен быть упомянут человек, который добавил бот.
* Только для уведомлений боты должны отправлять приветствие, которое передает сообщения, которые не отвечают на сообщения пользователей.

> [!TIP]
> В приветствиях отдельным пользователям тур карусель может предоставить эффективный обзор бота и любых других функций приложения. Рекомендуется включить кнопки, которые пользователи могут попробовать команды ботов. Например, **создание задачи.**

### <a name="bot-message-spamming"></a>Спам сообщений ботов

Боты не должны нежелательной почты пользователей, отправляя несколько сообщений в короткие последовательности.

* **Сообщения бота в каналах** и чатах: не спам пользователей путем создания отдельных сообщений. Создайте одну публикацию с ответами в одном потоке.
* **Бот-сообщения в личных приложениях:** не отправлять несколько сообщений в быстрой последовательности. Отправьте одно сообщение с полной информацией. Избегайте многооборотных бесед, чтобы завершить один рабочий процесс. Вместо этого рассмотрите возможность использования формы (или модуля задач) для одновременного сбора всех входных данных от пользователя.
* **Приветствие сообщений.** Повторение одного и того же приветствия через регулярные интервалы не допускается и считается нежелательной почтой. Например, при добавлении нового участника в команду не спамить других участников с приветствием. Сообщение нового члена лично вместо этого.

### <a name="bot-notifications"></a>Уведомления бота

Уведомления бота должны включать содержимое, соответствующее области, определяемой для бота (команда, чат или личное).

### <a name="bots-and-adaptive-cards"></a>Боты и адаптивные карты

Адаптивные карты — это рекомендуемый способ отображения сообщений ботов. Ваши карты должны быть легкими и включать только 1-3 действия. Если требуется отобразить больше контента, рассмотрите возможность использования модуля задач или вкладки.

Дополнительные сведения можно найти в следующих материалах:

* [Проектирование адаптивной карточки](~/task-modules-and-cards/cards/design-effective-cards.md)
* [Ссылки на карточки](~/task-modules-and-cards/cards/cards-reference.md#types-of-cards)

## <a name="messaging-extensions"></a>Расширения для система обмена сообщениями

Если приложение включает расширение обмена сообщениями, убедитесь, что оно соответствует этим рекомендациям.

> [!TIP]
> Сведения о создании высококачественного приложения см. в руководстве по разработке Teams [сообщений.](~/messaging-extensions/design/messaging-extension-design.md)

### <a name="action-commands"></a>Команды действий

Расширения обмена сообщениями на основе действий должны делать следующее:

* Разрешить пользователям запускать действия в сообщении, не завершая промежуточные действия, например вход.
* Передай контекст сообщения в следующее состояние работы.

### <a name="preview-links-link-unfurling"></a>Просмотр ссылок (разгрузка ссылок)

Расширения обмена сообщениями должны предварительно просматривать признанные ссылки в Teams окне. Не добавляйте домены, которые находятся вне вашего контроля (абсолютные URL-адреса или подстройки). Например, `yourapp.onmicrosoft.com` допустимо, `*.onmicrosoft.com` но не является допустимым. Домены верхнего уровня также запрещены (например, `*.com` или `*.org` ).

### <a name="search-commands"></a>Команды поиска

* Расширения обмена сообщениями на основе поиска должны предоставлять текст, который помогает пользователям эффективно искать.
* @mention исполняемые должны быть понятными, понятными и читаемыми.

## <a name="task-modules"></a>Модули задач

Модуль задач должен включать значок и короткое имя связанного с ним приложения.

> [!TIP]
> Сведения о создании высококачественного приложения см. в Teams руководства по разработке [модулей задач.](~/task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="meeting-extensions"></a>Расширения для собраний

Если ваше приложение включает расширение собрания, убедитесь, что оно соблюдает эти рекомендации.

> [!TIP]
> Сведения о создании высококачественного приложения см. в Teams руководства по расширению [собрания.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)

### <a name="pre--and-post-meeting-experience"></a>Опыт подготовки и после собрания

* Экраны предварительного и после собраний должны придерживаться общих рекомендаций по разработке вкладок. Дополнительные сведения см. в [Teams руководства по разработке.](~/tabs/design/tabs.md)
* Вкладки не должны иметь горизонтальной прокрутки.
* Вкладки должны иметь организованный макет при отобраии нескольких элементов. Например, более 10 опросов или опросов. См. [пример макета](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#after-a-meeting).
* Ваше приложение должно уведомлять пользователей об экспорте результатов опроса или опроса, указав: "Результаты успешно скачали".

### <a name="in-meeting-experience"></a>Опыт в собрании

* Приложения должны использовать только темную тему во время собраний. Дополнительные сведения см. в [Teams руководства по разработке.](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md#theming)
* Средство должно отображать имя приложения при наведении на значок приложения во время собраний.
* Расширения обмена сообщениями должны работать так же во время собраний, как и на внешних собраниях.

### <a name="in-meeting-tabs"></a>Вкладки на собрании

* Должно быть отзывчивым. Убедитесь, что поддерживается обивка и размеры компонентов.
* Должна быть кнопка "Назад", если существует несколько уровней навигации.
* Не должно включать более одной кнопки увольнения или закрытия. Это может запутать пользователей, так как уже есть встроенная кнопка загона, чтобы отклонять вкладку.
* Не должно иметь горизонтальной прокрутки.

### <a name="in-meeting-dialogs"></a>Диалоги на собрании

* Следует использовать экономно и для сценариев, которые являются легкими и ориентированными на задачи.
* Должен отображать содержимое в одном столбце и не иметь нескольких уровней навигации.
* Не следует использовать модули задач.
* Должно совпадать с центром стадии собрания.
* Следует отклонять, когда пользователь выбирает кнопку или выполняет действие.

## <a name="notifications"></a>Уведомления

Если ваше приложение использует API-API каналов активности, предоставляемые [корпорацией Майкрософт Graph, убедитесь,](/graph/teams-send-activityfeednotifications)что оно придерживается следующих рекомендаций.

### <a name="general"></a>Общий

* Все триггеры уведомлений, указанные в конфигурациях приложения, должны получать уведомление в приложении.
* Уведомления должны быть локализованы на поддерживаемых языках, настроенных для вашего приложения.
* Уведомления должны отображаться в течение пяти секунд после действий пользователя.

### <a name="avatars"></a>Аватары

* Аватар уведомлений должен соответствовать значку цвета вашего приложения.
* Уведомления, запускаемые пользователем, должны включать аватар пользователя.

### <a name="spamming"></a>Спам

* Приложения не должны отправлять пользователю более 10 уведомлений в минуту.
* Боты и канал действий не должны запускать дублирующие уведомления.
* Уведомления должны иметь некоторое значение для пользователей и не использоваться для тривиальных или нерелевантных событий.

### <a name="navigation-and-layout"></a>Навигация и макет

* Уведомления должны соответствовать макету Teams действий и опыту.
* При выборе уведомления пользователь должен быть направлен на соответствующий контент в Teams и не вывез Teams.

## <a name="advertising"></a>Реклама

Приложения не должны отображать рекламу, в том числе динамическую, баннерную и рекламу в сообщениях.

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Создание учетной записи Центра партнеров](~/concepts/deploy-and-publish/appsource/prepare/create-partner-center-dev-account.md)
