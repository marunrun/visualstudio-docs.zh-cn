---
title: 在数据提示中查看变量值 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], DataTips
- DataTips tool
ms.assetid: ffa7bd18-439b-4685-a9b3-c7884b5de41f
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a4674dec4b15f608eb25ffaf62c97efcc2363ab
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929978"
---
# <a name="view-data-values-in-datatips-in-the-code-editor"></a>在代码编辑器中的数据提示中的视图数据值

使用数据提示功能，可以在调试期间方便地查看程序中变量的有关信息。 数据提示功能只能在中断模式下可用，并且只对当前执行范围内的变量有效。 如果这是你在尝试调试的代码的第一个时间，可能需要阅读[零基础调试](../debugger/debugging-absolute-beginners.md)并[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)之前开始阅读本文。

## <a name="work-with-datatips"></a>使用数据提示

数据提示显示仅在中断模式下，并且只能在当前作用域的执行中的变量上。

### <a name="display-a-datatip"></a>显示数据提示

1. 在代码中设置断点并开始调试通过按**F5**或选择**调试** > **开始调试**。

1. 在断点处暂停，将鼠标悬停在当前作用域中的任何变量。 数据提示中出现，显示的名称和变量的当前值。

### <a name="make-a-datatip-transparent"></a>将数据提示设置为透明

若要使数据提示透明若要查看其在数据提示中下面的代码，按**Ctrl**。 数据提示保持不透明，只要您按住**Ctrl**密钥。 这不适用于固定或浮动数据提示。
### <a name="pin-a-datatip"></a>固定数据提示

若要固定数据提示，使其保持打开，请选择图钉**固定到源**图标。

![固定数据提示](../debugger/media/dbg-tips-data-tips-pinned.png "固定数据提示")

可以通过拖动在代码窗口上四处移动固定数据提示。 图钉图标将显示在数据提示固定到行旁边的滚动条槽中。

>[!NOTE]
>在上下文中挂起执行，而不是当前游标或数据提示位置始终计算数据提示。 如果悬停在当前上下文中具有与变量同名的另一个函数中的变量时，将显示在当前上下文中变量的值。

### <a name="unpin-a-datatip-from-source"></a>取消固定数据提示中的来自源

Float 固定数据提示中，悬停在数据提示并从上下文菜单中选择图钉图标。

图钉图标将更改为解除固定位置，并且现在，数据提示浮动或可以拖动最重要的是打开的窗口。 在调试会话结束时，浮动数据提示功能关闭。

### <a name="repin-a-datatip"></a>重新固定数据提示

若要重新固定浮动到源的数据提示，鼠标指针悬停在代码编辑器中，并选择图钉图标。 图钉图标将更改为固定位置，并仅到代码窗口再次固定数据提示。

如果数据提示浮动在一个非源代码窗口中，图钉图标不可用，并且不能被重新固定数据提示。 若要访问的图钉图标，返回到代码编辑器窗口通过拖动它或代码窗口焦点转移数据提示。

### <a name="close-a-datatip"></a>关闭数据提示

若要关闭数据提示，悬停在数据提示，并选择关闭 (**x**) 从上下文菜单的图标。

### <a name="close-all-datatips"></a>关闭所有数据提示

若要关闭所有数据提示，请在**调试**菜单中，选择**清除所有数据提示**。

### <a name="close-all-datatips-for-a-specific-file"></a>关闭特定文件的所有数据提示

若要关闭特定文件的所有数据提示在**调试**菜单中，选择**清除所有数据提示固定到\<文件名 >** 。

## <a name="expand-and-edit-information"></a>展开和编辑信息
利用数据提示功能，可以展开数组、结构或对象以查看其成员。 从数据提示还可以编辑变量的值。

### <a name="expand-a-variable"></a>展开变量

若要展开的对象在数据提示中查看它的元素，将鼠标悬停在项名称可以在树的形式显示的元素之前的展开箭头。 对于固定数据提示中，选择 **+** 之前将变量命名，然后展开树。

![展开数据提示](../debugger/media/dbg-tour-data-tips.png "展开数据提示")

您可以使用鼠标或箭头键在键盘上向上和向下移动以展开的视图。

此外可以将固定数据提示的扩展的项固定其上悬停鼠标并选择其图钉图标。 元素然后出现在固定数据提示中之后，树处于折叠状态。

### <a name="edit-the-value-of-a-variable"></a>编辑变量的值

若要编辑的变量或在数据提示中的元素的值，请选择值，键入新值，然后按**Enter**。 选择是只读的值被禁用。

## <a name="visualize-complex-data-types"></a>可视化复杂数据类型

变量或在数据提示中的元素旁边的放大镜图标表示，其中一个或多个[可视化工具](../debugger/create-custom-visualizers-of-data.md)，如[文本可视化工具](../debugger/string-visualizer-dialog-box.md)，可用于该变量。 可视化工具中更有意义，有时图形方式显示信息。

若要查看使用的数据类型的默认可视化工具的元素，请选择放大镜图标![可视化工具图标](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")。 选择要从数据类型的可视化工具列表中选择的放大镜图标旁边的箭头。

## <a name="add-a-variable-to-a-watch-window"></a>将变量添加到监视窗口

如果你想要继续监视某个变量，您可以将其添加到**监视**从数据提示窗口。 右键单击该变量在数据提示中，然后选择**添加监视**。

该变量出现在**监视**窗口。 如果您的 Visual Studio 版本支持多个**Watch**窗口中，该变量出现在**监视 1**。

## <a name="import-and-export-datatips"></a>导入和导出数据提示

可以将数据提示导出到一个 XML 文件，其中可以共享，也可以使用文本编辑器编辑。 此外可以导入已接收或编辑的数据提示 XML 文件。

**导出数据提示：**

1. 选择**调试** > **导出数据提示**。

1. 在中**导出数据提示**对话框中，导航到要保存 XML 文件中，键入该文件的名称的位置，然后选择**保存**。

**导入数据提示：**

1. 选择**调试** > **导入数据提示**。

1. 在中**导入数据提示**对话框框中，选择你想要打开，并选择的数据提示功能 XML 文件**打开**。

## <a name="see-also"></a>请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [首先看一下调试](../debugger/debugger-feature-tour.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
