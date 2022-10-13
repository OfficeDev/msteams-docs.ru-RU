---
title: Общие сведения об холсте Live Share
author: surbhigupta
description: В этом модуле вы узнаете больше об холсте Live Share, расширении, включающего рукописный ввод, лазерную указку и курсоры для приложений для собраний.
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-ypalikila
ms.date: 10/04/2022
ms.openlocfilehash: 9d1a776432f728c1e56caa357089be6e47c17e4c
ms.sourcegitcommit: 1248901a5e59db67bae091f60710aabe7562016a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/13/2022
ms.locfileid: "68560612"
---
# <a name="live-share-canvas-overview"></a>Общие сведения об холсте Live Share

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-docs-feature-1.png" alt-text="Снимок экрана: пример холста, синхронизируются с другими участниками собрания в собрании Teams.":::

В конференц-залах и аудиториях по всему миру доски являются составной частью совместной работы. Однако в современном времени доски недостаточно. Так как многие цифровые инструменты, такие как PowerPoint, являются центром совместной работы в современной эре, важно обеспечить тот же творческий потенциал.

Чтобы обеспечить более бесперебойную совместную работу, корпорация Майкрософт PowerPoint Live, что очень важно для работы пользователей в Teams. Выступающие могут добавлять заметки на слайды, чтобы все могли видеть их с помощью перьев, маркеров и лазерных указателей, чтобы привлечь внимание к основным понятиям. С помощью холста Live Share ваше приложение может использовать возможности PowerPoint Live рукописного ввода с минимальными усилиями.

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

Холст Live Share имеет два основных класса, которые обеспечивают совместную работу пошаговую работу: `InkingManager` и `LiveCanvas`. `InkingManager` отвечает за присоединение `<canvas>` полнофакторного элемента к приложению, `LiveCanvas` а также управляет удаленной синхронизацией с другими участниками собрания. Совместное использование приложения может иметь полные функциональные возможности, как доска, всего в нескольких строках кода.

| Классы                                                                     | Описание                                                                                                                                                                                                                                      |
| --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [InkingManager](/javascript/api/@microsoft/live-share-canvas/inkingmanager) | Класс, который присоединяет `<canvas>` `<div>` элемент к заданному объекту для автоматического управления росчерками пера или маркера, лазерной указкой, линиями и стрелками, а также ластиками. Предоставляет набор API (для управления активным инструментом) и основные параметры конфигурации. |
| [LiveCanvas](/javascript/api/@microsoft/live-share-canvas/livecanvas)      | Класс `SharedObject` , который синхронизирует росчерки `InkingManager` и позиции курсоров для всех пользователей в сеансе Live Share.                                                                                                                   |

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

Теперь, когда холст Live Share настроен и синхронизирован, вы можете настроить холст для взаимодействия с пользователем, например кнопки для выбора пера. В этом разделе мы обсудим, какие средства доступны и как их использовать.

### <a name="inking-tools"></a>Средства рукописного ввода

Каждое средство рукописного ввода на холсте Live Share отображает росчерки при рисовании пользователями. При использовании сенсорного экрана или пера средства также поддерживают динамику давления, влияя на ширину росчерка. Параметры конфигурации включают цвет кисти, толщину, фигуру и необязательную стрелку конца.

#### <a name="pen-tool"></a>Инструмент пера

:::image type="content" source="../assets/images/teams-live-share/canvas-pen-tool.gif" alt-text="В GIF показан пример рисования росчерков на холсте с помощью пера.":::

Перо рисует сплошные штрихи, которые хранятся на холсте. Фигура подсказки по умолчанию — круг.

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

:::image type="content" source="../assets/images/teams-live-share/canvas-highlighter-tool.gif" alt-text="В GIF показан пример рисования прозрачных штрихов на холсте с помощью средства выделения.":::

Средство выделения рисует прозрачные штрихи, которые хранятся на холсте. Фигура подсказки по умолчанию — квадрат.

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

:::image type="content" source="../assets/images/teams-live-share/canvas-eraser-tool.gif" alt-text="В GIF показан пример стирания штрихов на холсте с помощью средства ластика.":::

Средство ластика удаляет целые штрихи, которые пересекают его путь.

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

:::image type="content" source="../assets/images/teams-live-share/canvas-point-eraser-tool.gif" alt-text="В GIF показан пример удаления отдельных точек в штрихах на холсте с помощью средства ластика точек.":::

Средство ластика точек удаляет отдельные точки внутри росчерков, которые пересекают его путь, разделив существующие штрихи пополам. Это средство требует вычислительных ресурсов и может привести к снижению частоты кадров для пользователей.

> [!NOTE]
> Ластик точек использует тот же размер точки ластика, что и обычный инструмент ластика.

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

:::image type="content" source="../assets/images/teams-live-share/canvas-laser-tool.gif" alt-text="В GIF показан пример рисования росчерков на холсте с помощью средства лазерной указки.":::

Лазерная указка уникальна, так как кончик лазера оказывает конечный эффект при перемещении мыши. При рисовании росчерков конечный эффект отрисовка выполняется в течение короткого периода времени, прежде чем он полностью исчезнет. Это средство идеально подходит для выделения информации на экране во время собрания, так как выступающим не нужно переключаться между инструментами для стирания росчерков.

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

Средство line позволяет пользователям рисовать прямые линии из одной точки в другую с помощью необязательной стрелки, которую можно применить к концу.

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

Вы можете очистить все штрихи на холсте, вызвав его `inkingManager.clear()`. При этом удаляются все штрихи с холста.

### <a name="cursors"></a>Курсоры

:::image type="content" source="../assets/images/teams-live-share/canvas-cursors.gif" alt-text="В GIF показан пример пользователей, совместное использование курсора на холсте.":::

Вы можете включить динамические курсоры в приложении, чтобы пользователи могли отслеживать позиции курсоров друг друга на холсте. В отличие от средств рукописного ввода курсоры работают полностью через `LiveCanvas` класс. При необходимости можно указать имя и рисунок для идентификации каждого пользователя. Курсоры можно включить отдельно или с помощью средств рукописного ввода.

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

Для большинства приложений в Интернете содержимое отображается по-разному в зависимости от размера экрана или изменения состояния приложения. Если `InkingManager` приложение оптимизировано неправильно, это может привести к тому, что росчерки и курсоры будут отображаться для каждого пользователя по-разному. Холст Live Share поддерживает простой набор API- интерфейсов, `<canvas>` позволяющих корректировать положение росчерков для правильного согласования с содержимым.

По умолчанию холст Live Share работает так же, как приложение доски, с выравниваемым по центру содержимым окна просмотра с масштабом в 1 раз. Только часть содержимого отрисовывается в пределах видимых границ .`<canvas>` По концептуальной схеме это похоже на запись видео с высоты экрана. В то время как область просмотра камеры записи части мира под ней, реальный мир растягивается почти бесконечно в каждом направлении.

Ниже приведена простая схема, которая поможет визуализировать эту концепцию:

:::image type="content" source="../assets/images/teams-live-share/live-share-canvas-capabilities-docs-diagram-1.png" alt-text="Снимок экрана: макет холста в полноэкранном режиме для пользователей рабочего стола и мобильных устройств.":::

Это поведение можно настроить следующими способами:

- Изменение начальной ссылки на левый верхний угол холста.
- Измените смещение пикселей x и y в окне просмотра.
- Измените уровень масштабирования окна просмотра.

> [!NOTE]
> Эталонные точки, смещения и уровни масштабирования являются локальными для клиента и не синхронизируются между участниками собрания.

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

Так как веб-страницы будут доступны во всех фигурах и размерах, невозможно сделать холст Live Share поддерживающих каждый сценарий. Пакет идеально подходит для сценариев, в которых все пользователи одновременно просматривают одно и то же содержимое. Хотя не все содержимое должно отображаться на экране, оно должно быть содержимоем, которое линейно масштабируется на разных устройствах.

Ниже приведено несколько примеров сценариев, в которых холст Live Share является отличным вариантом для вашего приложения:

- Наложение изображений и видео, которые отображаются с одинаковым соотношением сторон на всех клиентах.
- Просмотр карты, трехмерной модели или доски с того же угла поворота.

Оба сценария работают правильно, так как содержимое можно просматривать одинаково на всех устройствах, даже если пользователи просматривают его с разными уровнями масштабирования и смещением. Если макет или содержимое приложения изменяется в зависимости от размера экрана и невозможно создать общее представление для всех участников, холст Live Share может оказаться не очень подходящим для вашего сценария.

## <a name="code-samples"></a>Примеры кода

| Название примера          | Описание                            | JavaScript                                                                                |
| -------------------- | -------------------------------------- | ----------------------------------------------------------------------------------------- |
| Демонстрация динамического холста     | Простое приложение доски.         | [View](https://github.com/microsoft/live-share-sdk/tree/main/samples/03.live-canvas-demo) |
| Шаблон мультимедиа React | Нарисуйте синхронизированный видеопроигрыватель. | [Просмотр](https://aka.ms/liveshare-mediatemplate)                                            |

## <a name="next-step"></a>Следующий этап

> [!div class="nextstepaction"]
> [Руководство для разработки игры в покер по гибкой методике](../sbs-teams-live-share.yml)

## <a name="see-also"></a>См. также

- [Вопросы и ответы по Live Share SDK](teams-live-share-faq.md)
- [Справочные документы по пакету SDK Live Share](/javascript/api/@microsoft/live-share/)
- [Справочные материалы по пакету SDK для Live Share Canvas](/javascript/api/@microsoft/live-share-canvas/)
- [Приложения Teams на собраниях](teams-apps-in-meetings.md)
