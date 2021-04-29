---
title: Начало работы — сборка и запуск первого приложения
author: girliemac
description: Быстро создайте приложение Microsoft Teams, которое отображает "Hello, World!" сообщение с помощью microsoft Teams набор средств.
ms.author: timura
ms.date: 03/22/2021
ms.topic: quickstart
ms.openlocfilehash: b34409919f073535c741a48edf30f3edd8c6bc8f
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068803"
---
# <a name="create-your-first-microsoft-teams-app"></a>Создание первого приложения Microsoft Teams

Этот quickstart учит вас создавать и запускать приложение Microsoft Teams, которое отображает "Hello, World!"

## <a name="prerequisites"></a>Необходимые условия

Перед началом работы необходимо настроить клиента разработки [Teams](#set-up-your-teams-development-tenant) и [установить средства разработки Teams.](#install-your-development-tools)

### <a name="set-up-your-teams-development-tenant"></a>Настройка клиента разработки Teams

Клиент **—** это как контейнер для организации. В терминах Teams клиент — это место, где люди из этого орга-чата делятся файлами и запускают собрания. В качестве разработчика необходимо, чтобы клиент перегружал и тестировали строимые приложения Teams.  

# <a name="do-not-have-a-tenant"></a>[Нет клиента](#tab/do-not-have-a-tenant)

Вы можете получить бесплатную тестовую учетную запись Teams, которая включает клиента, который позволяет загрузку приложений, присоединившись к программе разработчика Microsoft 365. Процесс регистрации занимает примерно две минуты.

**Чтобы получить клиента**

1. Перейдите к [программе разработчика Microsoft 365.](https://developer.microsoft.com/microsoft-365/dev-program)
1. Выберите **Join Now** и следуйте инструкциям на экране.
1. На экране Welcome выберите **настройка подписки E5.**
1. Настройка учетной записи разработчика Microsoft 365. 
   После завершения отображается следующий экран:

   :::image type="content" source="../assets/images/build-your-first-app/dev-program-subscription.png" alt-text="Пример того, что вы видите после регистрации на программу разработчика Microsoft 365.":::

1. Во входе в Teams с новой учетной записью.
1. В клиенте Teams выберите **Приложения.**
1. Убедитесь, что вы можете увидеть **параметр Upload настраиваемого** приложения. Если вы это сделаете, это означает, что вы можете перегружать приложения.

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::

# <a name="have-a-tenant"></a>[Иметь клиента](#tab/have-a-tenant)

Если у вас уже есть клиент, проверьте, можно ли перегружать приложения в Teams.

**Убедитесь, что приложения можно перегружать в сторону** 

1. В клиенте Teams выберите **Приложения.** 
1.  Убедитесь, что вы можете увидеть **параметр Upload настраиваемого** приложения. Если вы это сделаете, это означает, что вы можете перегружать приложения. 

   :::image type="content" source="../assets/images/build-your-first-app/upload-custom-app-closeup.png" alt-text="Иллюстрация, показывающая, где в Teams можно загрузить настраиваемые приложения.":::

---

### <a name="install-your-development-tools"></a>Установка средств разработки

Чтобы создать это приложение, для быстрого начала работы набор средств teams Visual Studio код. Вы также можете создавать приложения Teams с любыми из заранее. 

> [!NOTE]
> Teams отображает содержимое приложения только с помощью подключений HTTPS. Чтобы отламыть определенные типы приложений локально, например бот, вы узнаете, как использовать ngrok для запуска безопасного туннеля между Teams и вашим приложением.
> 
> Приложения Production Teams находятся в облаке.

**Установка средств Microsoft Teams**

1. Установите [Node.js](https://nodejs.org/en/).
1. Если вы планируете создать расширение бота или обмена сообщениями, установите [ngrok](https://ngrok.com/download) и выставите локальный интернет с помощью [ngrok.](../tutorials/get-started-dotnet-app-studio.md#tunnel-using-ngrok)
1. Установка последней версии [Visual Studio кода](https://code.visualstudio.com/download). 
   
   > [!NOTE]
   > Набор инструментов не поддерживает более ранние версии Visual Studio Code.

1. В левой панели действий выберите **Расширения.** :::image type="icon" source="../assets/icons/vs-code-extensions.png":::
1. В **Microsoft Teams набор средств** установите **.**

   :::image type="content" source="../assets/images/build-your-first-app/vsc-install-toolkit.png" alt-text="Иллюстрация, на которой Visual Studio коде можно установить расширение Microsoft Teams набор средств.":::

## <a name="1-create-your-app-project"></a>1. Создание проекта приложения

1. Откройте Visual Studio код.
1. Выберите **Microsoft Teams набор средств** создать новое приложение :::image type="icon" source="../assets/icons/vsc-toolkit.png":::  >  **Teams.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-02.png" alt-text="Снимок экрана, показывающий, как создать проект приложения с помощью Visual Studio команд кода набор средств.":::
   
1. Во входе с учетной записью разработки Microsoft 365. Либо только что созданная учетная запись, либо уже созданная учетная запись, которая позволяет загрузку приложения в сторону.
1. На экране **Выберите проект** перейдите в приложение **Personal и** выберите **JS** (JavaScript) > **Далее**.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-03.png" alt-text="Снимок экрана, показывающий, как настроить проект приложения с помощью Visual Studio команд кода набор средств.":::

1. Введите имя приложения Teams.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-04.png" alt-text="Снимок экрана, показывающий, как добавить имя в проект приложения с помощью Visual Studio code Teams набор средств.":::

1. Выберите **Готово**. 
   Теперь проект настроен. 

## <a name="2-understand-your-app-project-components"></a>2. Понимание компонентов проекта приложения

После того как набор инструментов настроит проект приложения, у вас будут компоненты для создания "Hello, World!". Приложение Teams. Каталоги и файлы проекта находятся в Visual Studio Code Explorer. 

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-05.png" alt-text="Снимок экрана, показывающий леса в проекте приложения с Visual Studio code Teams набор средств.":::

Набор инструментов автоматически создает строительные леса приложений в каталоге на основе возможностей, добавленных `src` во время установки. Так как вы создали вкладку во время настройки, файл в каталоге обрабатывает инициализацию и `App.js` `src/components` маршрутизацию приложения. Файл также вызывает SDK клиента Microsoft Teams JavaScript для установления связи между вашим приложением и teams. 

## <a name="3-build-and-run-your-app"></a>3. Сборка и запуск приложения

Создайте и запустите приложение локально, чтобы сэкономить время. 

**Создание и запуск приложения**

1. В Visual Studio коде выберите **Терминал**  >  **Представления**.
1. Запуск `npm install` .
1. Запуск `npm start` .
  
  **Компилировать успешно!** сообщение отображается в терминале. Ваше приложение теперь работает на локальном сайте по `https://localhost:3000` . 

## <a name="4-sideload-your-app-in-teams"></a>4. Sideload ваше приложение в Teams

Sideloading — это процесс установки приложения в Teams, которое не было утверждено вашим администратором или Корпорацией Майкрософт. При тестировании и отладке приложений Teams часто используется боковая загрузка.

По умолчанию Teams не разрешает загрузку приложений. Этот параметр можно изменить в центре администрирования Teams.

**Чтобы включить загрузку приложений в Teams**

1. Во входе в [центр администрирования Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) с учетными данными администратора.  
1. Выберите **Показать все**  >  **команды.** 

   ![изображение меню центра администрирования](~/assets/images/prepare-test-tenant/admin-center.png)

   > [!Note] 
   > Для появления параметра **Teams** может занять до 24 часов. 

1. Перейдите к **политикам установки приложений Teams**  >    >  **Global** (по умолчанию в масштабах всей организации).

   ![включить представление боковой нагрузки](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

1. Включите **переключить настраиваемые приложения** для загрузки.

1. Выберите **Сохранить,** чтобы сохранить изменения.

   Клиент тестового клиента теперь разрешает настраиваемую загрузку приложений.

   > [!Note]
   > Проверьте проблемы перед загрузкой приложения с помощью функции проверки в App Studio, которая входит в набор инструментов. Устранение ошибок для успешной загрузки приложения.


### <a name="sideload-your-app"></a>Боковая загрузка приложения

1. В Visual Studio коде откройте командную набор средств.
1. Перейдите в **App Studio**.  
1. Выберите **тест и раздайте**  >  **установку.**

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-appstudio.png" alt-text="Снимок экрана, показывающий, как перегрузить приложение в клиент Teams с помощью Visual Studio команд кода набор средств.":::

**В качестве альтернативы**

1. Выберите **клавишу F5,** чтобы открыть окно браузера для установки. Это позволит пропустить процесс установки в **App Studio** и lauch Teams в браузере.
1. В диалоговом окте установки выберите **Добавить** для установки приложения в Teams.

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install.png" alt-text="Снимок экрана, показывающий, как перегрузить приложение в клиент Teams.":::

   > [!Note]
   > App Studio также доступен в качестве отдельного приложения для клиента Teams.

### <a name="troubleshoot-sideloading-issues"></a>Устранение неполадок при перегрузке

**Сбой установки**

Если сообщение об ошибке появляется при установке приложения, убедитесь, что сведения о приложении правильно `Manifest parsing has failed` введены.

**Проверка сведений о приложении**

* В командной набор средств перейдите в **App Studio** App и убедитесь, что вся необходимая информация введена  >   правильно.
*  Если вы вручную редактировали файл, убедитесь, что JSON хорошо определен в `manifest.json` **инструменте Манифест** приложения в App Studio.

**Содержимое вкладки, которое не отображается**

Убедитесь, что приложение запущено. Если это не так, перейдите к терминалу и запустите `npm start` .

## <a name="see-also"></a>См. также

* [Подготовка клиента Microsoft 365](https://docs.microsoft.com/microsoftteams/platform/concepts/build-and-test/prepare-your-o365-tenant)
* [Выбор установки для тестирования и отлаговки приложения Microsoft Teams](../concepts/build-and-test/debug.md)
* [Создание вкладок и других опытом работы с клиентом Microsoft Teams JavaScript SDK](../tabs/how-to/using-teams-client-sdk.md)
* [Подготовка к отправке AppSource](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)
* [Быстрая разработка приложений с помощью App Studio для Microsoft Teams](../concepts/build-and-test/app-studio-overview.md)
* [Создание вкладки канала](../build-your-first-app/build-channel-tab.md)

## <a name="next-step"></a>Следующий шаг

> [!div class="nextstepaction"]
> [Создание личной вкладки для Microsoft Teams](../build-your-first-app/build-personal-tab.md)
