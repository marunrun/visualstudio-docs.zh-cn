---
title: 在数据提示中查看变量值 | Microsoft Docs
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
ms.openlocfilehash: bf5eda8205dbe0629d0b2801473de83c2f91257e
ms.sourcegitcommit: 8e123bcb21279f2770b28696995450270b4ec0e9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/25/2019
ms.locfileid: "75404271"
---
# <a name="view-data-values-in-datatips-in-the-code-editor"></a>在代码编辑器中查看数据提示中的数据值

使用数据提示功能，可以在调试期间方便地查看程序中变量的有关信息。 数据提示功能只能在中断模式下可用，并且只对当前执行范围内的变量有效。 如果是首次尝试调试代码，那么在阅读本文前，可能需要阅读[零基础调试](../debugger/debugging-absolute-beginners.md)和[调试技术和工具](../debugger/write-better-code-with-visual-studio.md)。

## <a name="work-with-datatips"></a>使用数据提示

数据提示功能只在中断模式下可用，并且只对当前执行范围内的变量有效。

### <a name="display-a-datatip"></a>显示数据提示

1. 在代码中设置断点，然后按 F5 或选择“调试” > “开始调试”以开始调试  。

1. 在断点处暂停时，将鼠标悬停在当前范围内的任何变量上。 将会出现数据提示，其中显示变量的名称和当前值。

### <a name="make-a-datatip-transparent"></a>使数据提示显示为透明

若要使数据提示显示为透明以便查看其下方的代码，请在数据提示中按 Ctrl。 只要按住 Ctrl 键，数据提示就会保持透明状态。 此操作不适用于固定或浮动的数据提示。
### <a name="pin-a-datatip"></a>固定数据提示

若要固定数据提示以使其保持打开状态，请选择图钉“固定到源”图标。

![固定数据提示](../debugger/media/dbg-tips-data-tips-pinned.png "固定数据提示")

可以通过在代码窗口中拖动固定的数据提示来移动它。 在数据提示固定到的行旁边的装订线中会显示一个图钉图标。

>[!NOTE]
>数据提示始终在执行暂停的上下文中进行评估，而不是在当前光标位置或数据提示位置。 如果将鼠标指针悬停在另一函数中的变量的上方，且该变量与当前上下文中的某个变量同名，则会显示当前上下文中的变量的值。

### <a name="unpin-a-datatip-from-source"></a>从源中取消固定数据提示

若要将已固定的数据提示设置为浮动状态，请将鼠标悬停在数据提示上，然后从上下文菜单中选择图钉图标。

图钉图标将更改至取消固定的位置，并且数据提示现在处于浮动状态，也可将其拖动到所有打开的窗口上方。 在调试会话结束时，浮动的数据提示将关闭。

### <a name="repin-a-datatip"></a>重新固定数据提示

若要将浮动的数据提示重新固定到源，请将鼠标悬停在代码编辑器中，然后选择图钉图标。 图钉图标将变换到固定的位置，数据提示会再次仅固定到代码窗口。

如果数据提示浮动在非源代码窗口上，图钉图标将不可用，并且无法重新固定数据提示。 若要找到图钉图标，请将数据提示拖动回代码编辑器窗口，或通过将焦点转至代码窗口来让数据提示回到代码编辑器窗口。

### <a name="close-a-datatip"></a>关闭数据提示

若要关闭数据提示，请将鼠标悬停在数据提示上，然后从上下文菜单中选择关闭 (x) 图标。

### <a name="close-all-datatips"></a>关闭所有数据提示

若要关闭所有数据提示，请在“调试”菜单上选择“清除所有数据提示” 。

### <a name="close-all-datatips-for-a-specific-file"></a>关闭特定文件的所有数据提示

若要关闭特定文件的所有数据提示，请在“调试”菜单上选择“清除固定到 \<文件名> 的所有数据提示” 。

## <a name="expand-and-edit-information"></a>展开并编辑信息
利用数据提示功能，可以展开数组、结构或对象以查看其成员。 从数据提示还可以编辑变量的值。

### <a name="expand-a-variable"></a>展开变量

若要在数据提示中展开某个对象以查看其元素，请将鼠标悬停在该项的名称之前的展开箭头上，以树状显示其元素。 对于固定的数据提示，请选择变量名称前面的“+”并展开元素树。

![展开数据提示](../debugger/media/dbg-tour-data-tips.png "展开数据提示")

可以使用鼠标或键盘上的箭头键在展开的视图中上下移动。

若要将展开的项固定到固定的数据提示，请将鼠标悬停在项上并选择其图钉图标。 折叠树后，这些元素会显示在固定的数据提示中。

### <a name="edit-the-value-of-a-variable"></a>编辑变量的值

若要在数据提示中编辑某个变量或元素的值，请选择该值，键入新值，然后按 Enter。 禁止选择只读值。

::: moniker range=">= vs-2019"

## <a name="pin-properties-in-datatips"></a>在数据提示中固定属性

> [!NOTE]
> .NET Core 3.0 或更高版本支持此功能。

使用“可固定属性”工具，可以按属性快速检查数据提示中的对象。  要使用此工具，请将鼠标悬停在某个属性上，并选择出现的固定图标，或右键单击并选择所显示上下文菜单中的“将成员固定到收藏夹”选项。  这会将该属性以气泡形式显示到该对象的属性列表顶部，并且属性名称和值会显示在数据提示的右列中。  要取消固定属性，请再次选择固定图标，或在上下文菜单中选择“取消将成员固定到收藏夹”选项。

![在数据提示中固定属性](../debugger/media/basic-pin-datatip.gif "在数据提示中固定属性")

在数据提示中查看对象的属性列表时，还可以切换属性名称并筛选出非固定属性。  若要采用其中任一选项，请右键单击包含属性的行并在上下文菜单中选择“仅显示已固定的成员”或“在值中隐藏已固定的成员名称”选项 。

::: moniker-end

## <a name="visualize-complex-data-types"></a>可视化复杂数据类型

在数据提示中，变量或元素旁边的放大镜图标表示有一个或多个[可视化工具](../debugger/create-custom-visualizers-of-data.md)（例如[文本可视化工具](../debugger/string-visualizer-dialog-box.md)）可用于该变量。 可视化工具能以更有意义的方式（有时是图形）显示信息。

若要使用数据类型的默认可视化工具查看元素，请选择放大镜图标![可视化工具图标](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")。 选择放大镜图标旁边的箭头，从该数据类型的可视化工具列表中进行选择。

## <a name="add-a-variable-to-a-watch-window"></a>将变量添加到监视窗口

如果要继续监视某个变量，可在数据提示中将其添加到“监视”窗口。 在数据提示中右键单击该变量，然后选择“添加监视”。

变量随即会显示在“监视”窗口中。 如果使用的 Visual Studio 版本支持多个“监视”窗口，则该变量将显示在“监视 1”中 。

## <a name="import-and-export-datatips"></a>导入和导出数据提示

可以将数据提示导出到 XML 文件中，然后能将其共享给其他人，或者使用文本编辑器来对其进行编辑。 还可以导入已接收或编辑的数据提示 XML 文件。

**导出数据提示：**

1. 选择“调试” > “导出数据提示” 。

1. 在“导出数据提示”对话框中，导航到要保存 XML 文件的位置，键入文件名，然后选择“保存” 。

**导入数据提示：**

1. 选择“调试” > “导入数据提示” 。

1. 在“导入数据提示”对话框中，选择要打开的数据提示 XML 文件，然后选择“打开” 。

## <a name="see-also"></a>请参阅
- [什么是调试？](../debugger/what-is-debugging.md)
- [调试技术和工具](../debugger/write-better-code-with-visual-studio.md)
- [初探调试](../debugger/debugger-feature-tour.md)
- [查看调试器中的数据](../debugger/viewing-data-in-the-debugger.md)
- [监视和快速监视窗口](../debugger/watch-and-quickwatch-windows.md)
- [创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)
