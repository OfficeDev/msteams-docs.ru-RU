---
title: Обзор холста Live Share
author: surbhigupta
description: В этом модуле вы узнаете больше о холсте Live Share, расширении, позволяющем рукописный ввод, лазерные указатели и курсоры для приложений для собраний.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 11f465072d496f466df28c37b8eee7289bae4180
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791449"
---
# <a name="live-share-canvas-overview"></a>Обзор холста Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="Снимок экрана: пример холста, синхронизированного с другими участниками собрания в собрании Teams.":::

В конференц-залах и аудиториях по всему миру доски являются ключевой частью совместной работы. В наше время, однако, доска больше не достаточно. Благодаря многочисленным цифровым инструментам, таким как PowerPoint, который является центром совместной работы в современную эпоху, важно реализовать тот же творческий потенциал.

Чтобы обеспечить более беспроблемную совместную работу, корпорация Майкрософт создала PowerPoint Live, которая сыграла важную роль в работе пользователей в Microsoft Teams. Выступающие могут добавлять заметки на слайды, чтобы все могли видеть, используя ручки, маркеры и лазерные указатели, чтобы привлечь внимание к ключевым понятиям. С помощью холста Live Share ваше приложение может принести возможности PowerPoint Live средств рукописного ввода с минимальными усилиями.

## <a name="install"></a>Установка

Чтобы добавить последнюю версию пакета SDK в приложение с помощью npm:

```bash
npm install @microsoft/live-share@next --save
npm install @microsoft/live-share-canvas@next --save
```

ИЛИ

Чтобы добавить последнюю версию пакета SDK в приложение с помощью [Yarn](https://yarnpkg.com/):

```bash
yarn add @microsoft/live-share@next
yarn add @microsoft/live-share-canvas@next
```

## <a name="setting-up-the-package"></a>Настройка пакета

На холсте Live Share есть два основных класса, которые обеспечивают совместную работу под ключ: `InkingManager` и `LiveCanvas`. `InkingManager` отвечает за присоединение полнофункционированного `<canvas>` элемента к приложению, а также `LiveCanvas` управляет удаленной синхронизацией с другими участниками собрания. При совместном использовании приложение может иметь полные функции, подобные доске, всего в нескольких строках кода.

| Классы                                                                     | Описание                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | Класс, который присоединяет `<canvas>` элемент к заданному `<div>` объекту для автоматического управления росчерками пера или маркера, лазерной указателем, линиями и стрелками, а также ластиками. Предоставляет набор API (для управления активным средством) и базовые параметры конфигурации. |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | Класс `SharedObject` , который синхронизирует росчерки и позиции курсора для `InkingManager` всех пользователей в сеансе Live Share.                                                                                                                   |

Пример.

```html
<body>
  <div id="canvas-host"></div>
</body>
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const { liveCanvas } = container.initialObjects;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```TypeScript
import { LiveShareClient } from "@microsoft/live-share";
import { InkingManager, LiveCanvas } from "@microsoft/live-share-canvas";
import { ContainerSchema } from "fluid-framework";

// Setup the Fluid container
const liveShare = new LiveShareClient();
const schema: ContainerSchema = {
  initialObjects: { liveCanvas: LiveCanvas },
};
const { container } = await liveShare.joinContainer(schema);
const liveCanvas = container.initialObjects.liveCanvas as LiveCanvas;

// Get the canvas host element
const canvasHostElement = document.getElementById("canvas-host");
const inkingManager = new InkingManager(canvasHostElement);

// Begin synchronization for LiveCanvas
await liveCanvas.initialize(inkingManager);
```

---

## <a name="canvas-tools-and-cursors"></a>Инструменты и курсоры холста

Теперь, когда холст Live Share настроен и синхронизирован, вы можете настроить холст для взаимодействия с пользователем, например кнопки для выбора инструмента пера. В этом разделе мы обсудим доступные средства и способы их использования.

### <a name="inking-tools"></a>Средства рукописного ввода

Каждый инструмент рукописного ввода на холсте Live Share отображает росчерки по мере рисования пользователем. При использовании сенсорного экрана или пера инструменты также поддерживают динамику давления, влияя на ширину штриха. Параметры конфигурации включают цвет кисти, толщину, форму и необязательную стрелку конца.

#### <a name="pen-tool"></a>Инструмент "Перо"

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="В GIF показан пример рисования росчерков на холсте с помощью инструмента пера.":::

Инструмент пера рисует сплошные росчерки, хранящиеся на холсте. Фигура кончика по умолчанию — круг.

```html
<div>
  <button id="pen">Enable Pen</button>
  <label for="pen-color">Select a color:</label>
  <input type="color" id="color" name="color" value="#000000" />
  <button id="pen-tip-size">Increase pen size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to pen
document.getElementById("pen").onclick = () => {
  inkingManager.tool = InkingTool.pen;
};
// Change the selected color for pen
document.getElementById("pen-color").onchange = () => {
  const colorPicker = document.getElementById("color");
  inkingManager.penBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for pen
document.getElementById("pen-tip-size").onclick = () => {
  inkingManager.penBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="highlighter-tool"></a>Средство выделения

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="В ФОРМАТЕ GIF показан пример рисования полупрозрачных штрихов на холсте с помощью средства выделения.":::

Средство выделения рисует полупрозрачные штрихи, хранящиеся на холсте. Фигура кончика по умолчанию — квадрат.

```html
<div>
  <button id="highlighter">Enable Highlighter</button><br />
  <label for="highlighter-color">Select a color:</label>
  <input type="color" id="highlighter-color" name="highlighter-color" value="#FFFC00" />
  <button id="highlighter-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to highlighter
document.getElementById("highlighter").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for highlighter
document.getElementById("highlighter-color").onchange = () => {
  const colorPicker = document.getElementById("highlighter-color");
  inkingManager.highlighterBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for highlighter
document.getElementById("highlighter-tip-size").onclick = () => {
  inkingManager.highlighterBrush.tipSize = inkingManager.penBrush.tipSize + 1;
};
```

#### <a name="eraser-tool"></a>Средство ластика

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="GIF показывает пример стирания штрихов на холсте с помощью средства ластика.":::

Средство ластика стирает целые штрихи, пересекающиеся с пути.

```html
<div>
  <button id="eraser">Enable Eraser</button><br />
  <button id="eraser-size">Increase eraser size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("eraser").onclick = () => {
  inkingManager.tool = InkingTool.eraser;
};
// Increase the tip size for eraser
document.getElementById("eraser-size").onclick = () => {
  inkingManager.eraserSize = inkingManager.eraserSize + 1;
};
```

#### <a name="point-eraser-tool"></a>Средство ластика точек

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="В GIF показан пример удаления отдельных точек в росчерках на холсте с помощью средства ластика точек.":::

Инструмент ластика точек стирает отдельные точки в штрихах, пересекающих его путь, разделяя существующие штрихи пополам. Это средство является ресурсоемким и может привести к снижению частоты кадров для пользователей.

> [!NOTE]
> Точечная ластик имеет тот же размер точки ластика, что и обычный ластик.

```html
<div>
  <button id="point-eraser">Enable Point Eraser</button><br />
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to eraser
document.getElementById("point-eraser").onclick = () => {
  inkingManager.tool = InkingTool.pointEraser;
};
```

#### <a name="laser-pointer"></a>Лазерная указка

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="GIF показывает пример рисования штрихов на холсте с помощью инструмента лазерной указки.":::

Лазерный указатель уникален, так как кончик лазера имеет конечный эффект при перемещении мыши. При рисовании штрихов конечный эффект отрисовывается в течение короткого периода, прежде чем полностью исчезнет. Это средство идеально подходит для указания информации на экране во время собрания, так как докладчику не нужно переключаться между инструментами для удаления штрихов.

```html
<div>
  <button id="laser">Enable Laser Pointer</button><br />
  <label for="laser-color">Select a color:</label>
  <input type="color" id="laser-color" name="laser-color" value="#000000" />
  <button id="laser-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to laser pointer
document.getElementById("laser").onclick = () => {
  inkingManager.tool = InkingTool.highlighter;
};
// Change the selected color for laser pointer
document.getElementById("laser-color").onchange = () => {
  const colorPicker = document.getElementById("laser-color");
  inkingManager.laserPointerBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for laser pointer
document.getElementById("laser-tip-size").onclick = () => {
  inkingManager.laserPointerBrush.tipSize = inkingManager.laserPointerBrush.tipSize + 1;
};
```

#### <a name="line-and-arrow-tools"></a>Инструменты со стрелками и линиями

:::image type="content" source="../assets/images/teams-live-share/canvas-line-tool.gif" alt-text="В GIF показан пример рисования прямых линий на холсте с помощью инструмента &quot;Линия и стрелка&quot;.":::

Инструмент "Линия" позволяет пользователям рисовать прямые линии из одной точки в другую с необязательной стрелкой, которую можно применить к концу.

```html
<div>
  <button id="line">Enable Line</button><br />
  <button id="line-arrow">Enable Arrow</button><br />
  <input type="color" id="line-color" name="line-color" value="#000000" />
  <button id="line-tip-size">Increase tip size</button>
</div>
```

```javascript
import {
  InkingManager,
  InkingTool,
  fromCssColor,
} from "@microsoft/live-share-canvas";
// ...

// Change the selected tool to line
document.getElementById("line").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "none";
};
// Change the selected tool to line
document.getElementById("line-arrow").onclick = () => {
  inkingManager.tool = InkingTool.line;
  inkingManager.lineBrush.endArrow = "open";
};
// Change the selected color for lineBrush
document.getElementById("line-color").onchange = () => {
  const colorPicker = document.getElementById("line-color");
  inkingManager.lineBrush.color = fromCssColor(colorPicker.value);
};
// Increase the tip size for lineBrush
document.getElementById("line-tip-size").onclick = () => {
  inkingManager.lineBrush.tipSize = inkingManager.lineBrush.tipSize + 1;
};
```

#### <a name="clear-all-strokes"></a>Очистка всех росчерков

Вы можете очистить все штрихи на холсте, вызвав .`inkingManager.clear()` При этом удаляются все штрихи с холста.

### <a name="cursors"></a>Курсоры

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="В ФОРМАТЕ GIF показан пример совместного использования курсора на холсте.":::

Вы можете включить динамические курсоры в приложении, чтобы пользователи могли отслеживать позиции курсоров друг друга на холсте. В отличие от средств рукописного ввода, курсоры полностью работают через `LiveCanvas` класс . При необходимости можно указать имя и рисунок для идентификации каждого пользователя. Курсоры можно включить отдельно или с помощью инструментов рукописного ввода.

```javascript
// Optional. Set user display info
liveCanvas.onGetLocalUserInfo = () => {
  return {
    displayName: "YOUR USER NAME",
    pictureUri: "YOUR USER PICTURE URI",
  };
};
// Toggle Live Canvas cursor enabled state
liveCanvas.isCursorShared = !isCursorShared;
```

## <a name="optimizing-across-devices"></a>Оптимизация на разных устройствах

Для большинства приложений в Интернете содержимое отображается по-разному в зависимости от размера экрана или состояния приложения. Если `InkingManager` приложение не оптимизировано правильно, это может привести к тому, что штрихи и курсоры будут отображаться по-разному для каждого пользователя. Холст Live Share поддерживает простой набор API, который позволяет `<canvas>` настраивать позиции росчерка для правильного выравнивания по содержимому.

По умолчанию холст Live Share во многом похож на приложение доски, при этом содержимое выравнивается по центру окна просмотра с 1-кратным масштабом. Только часть содержимого отображается в видимых границах `<canvas>`. Концептуально это похоже на запись видео с высоты птичьего полета. В то время как окно просмотра камеры записывает часть мира под ним, реальный мир растягивается почти бесконечно во всех направлениях.

Ниже приведена простая схема, помогая визуализировать эту концепцию:

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="Снимок экрана: полноэкранный макет холста для настольных и мобильных пользователей вместе.":::

Это поведение можно настроить следующими способами:

- Изменение начальной опорной точки на левый верхний угол холста.
- Измените положение смещения пикселей x и y окна просмотра.
- Изменение уровня масштабирования окна просмотра.

> [!NOTE]
> Опорные точки, смещения и уровни масштабирования являются локальными для клиента и не синхронизируются между участниками собрания.

Пример.

```html
<body>
  <button id="pan-left">Pan left</button>
  <button id="pan-up">Pan up</button>
  <button id="pan-right">Pan right</button>
  <button id="pan-down">Pan down</button>
  <button id="zoom-out">Zoom out</button>
  <button id="zoom-in">Zoom in</button>
  <button id="change-reference">Change reference</button>
</body>
```

```javascript
// ...

// Pan left
document.getElementById("pan-left").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x - 10,
    y: inkingManager.offset.y,
  };
};
// Pan up
document.getElementById("pan-up").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y - 10,
  };
};
// Pan right
document.getElementById("pan-right").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x + 10,
    y: inkingManager.offset.y,
  };
};
// Pan down
document.getElementById("pan-down").onclick = () => {
  inkingManager.offset = {
    x: inkingManager.offset.x,
    y: inkingManager.offset.y + 10,
  };
};
// Zoom out
document.getElementById("zoom-out").onclick = () => {
  if (inkingManager.scale > 0.1) {
    inkingManager.scale -= 0.1;
  }
};
// Zoom in
document.getElementById("zoom-in").onclick = () => {
  inkingManager.scale += 0.1;
};
// Change reference
document.getElementById("change-reference").onclick = () => {
  if (inkingManager.referencePoint === "center") {
    inkingManager.referencePoint = "topLeft";
  } else {
    inkingManager.referencePoint = "center";
  }
};
```

## <a name="ideal-scenarios"></a>Идеальные сценарии

Благодаря тому, что веб-страницы имеют все формы и размеры, невозможно создать холст Live Share для поддержки всех сценариев. Пакет идеально подходит для сценариев, в которых все пользователи одновременно просматривают одно и то же содержимое. Хотя не все содержимое должно быть видно на экране, это должно быть содержимое, которое масштабируется на устройствах линейно.

Вот несколько примеров сценариев, в которых холст Live Share является отличным вариантом для вашего приложения:

- Наложение изображений и видео, которые отображаются с одинаковым соотношением сторон на всех клиентах.
- Просмотр карты, трехмерной модели или доски под тем же углом поворота.

Оба сценария хорошо работают, так как содержимое может просматриваться одинаково на всех устройствах, даже если пользователи смотрят на него с разными уровнями масштабирования и смещения. Если макет или содержимое вашего приложения меняется в зависимости от размера экрана и невозможно создать общее представление для всех участников, холст Live Share может не подходить для вашего сценария.

## <a name="code-samples"></a>Примеры кода

| Название примера          | Описание                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Демонстрация Live Canvas     | Простое приложение доски.         | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| Шаблон мультимедиа React | Нарисуйте синхронизированный видеопроигрыватель. | [Просмотр](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Руководство для разработки игры в покер по гибкой методике](../sbs-teams-live-share.yml)

## <a name="see-also"></a>См. также

- [Вопросы и ответы по Live Share SDK](teams-live-share-faq.md)
- [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Справочная документация по пакету SDK для Live Share Canvas](/javascript/api/@microsoft/live-share-canvas/)
- [Приложения Teams на собраниях](teams-apps-in-meetings.md)
