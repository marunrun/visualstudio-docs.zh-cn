---
title: 在设计时调试 |Microsoft Docs
ms.custom: ''
ms.date: 01/10/2019
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- debugging [Visual Studio], design-time
- breakpoints, design-time debugging
- Immediate window, design-time debugging
- design-time debugging
ms.assetid: 35bfdd2c-6f60-4be1-ba9d-55fce70ee4d8
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: beb16ae52f880e31bd19a185d47b13c02026752f
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2020
ms.locfileid: "75916146"
---
# <a name="debug-at-design-time-in-visual-studio-c-ccli-visual-basic-f"></a>在设计时在 Visual Studio 中调试C#（ C++、/cli、Visual Basic F#）

若要在设计时（而不是在应用程序运行时）调试代码，可以使用 "**即时**" 窗口。

若要在 XAML 设计器中调试应用程序背后的 XAML 代码，如声明性数据绑定方案，可以使用 "**调试**" > "**附加到进程**"。

## <a name="use-the-immediate-window"></a>使用 "即时" 窗口

你可以使用 Visual Studio 的 "**即时**" 窗口来执行函数或子例程，而无需运行你的应用程序。 如果函数或子例程包含断点，则 Visual Studio 会在断点处中断。 随后即可使用调试器窗口检查程序状态。 此功能*在设计时称为调试*。

下面的示例在 Visual Basic 中。 你还可以在C#、 F#和C++/cli 应用的设计时使用 "**即时**" 窗口。

1. 将以下代码粘贴到空白 Visual Basic 控制台应用中：

   ```vb
   Module Module1

       Sub Main()
           MySub()
       End Sub

       Function MyFunction() As Decimal
           Static i As Integer
           i = i + 1
           Return i
       End Function

       Sub MySub()
           MyFunction()

       End Sub
   End Module
   ```

1. 在行**End 函数**上设置断点。

1. 通过选择 "**调试**" > **Windows** > "**即时**" 打开 "**即时**" 窗口。 在窗口中键入 `?MyFunction`，然后按**enter**。

   命中断点，而在 "**局部变量**" 窗口中， **MyFunction**的值为**1**。 当应用处于中断模式时，可以检查调用堆栈和其他调试窗口。

1. 在 Visual Studio 工具栏上选择 "**继续**"。 应用结束，在 "**即时**" 窗口中返回**1** 。 请确保仍处于设计模式。

1. 再次在 "**即时**" 窗口中键入 `?MyFunction`，然后按**enter**。 命中断点，而在 "**局部变量**" 窗口中**MyFunction**的值为**2**。

1. 如果不选择 "**继续**"，请在 "**即时**" 窗口中键入 `?MySub()`，然后按**enter**。 命中断点，而在 "**局部变量**" 窗口中， **MyFunction**的值为**3**。 当应用处于中断模式时，可以检查应用程序状态。

1. 选择**继续**。 再次命中断点，"**局部变量**" 窗口中的**MyFunction**值现在为**2**。 **立即**窗口返回**Expression，但没有值**。

1. 再次选择 "**继续**"。 应用结束后，在 "**即时**" 窗口中返回**2** 。 确保仍处于设计模式。

1. 若要清除 "**即时**" 窗口的内容，请在窗口中右键单击，然后选择 "**全部清除**"。

## <a name="debug-a-custom-xaml-control-at-design-time-by-attaching-to-xaml-designer"></a>通过附加到 XAML 设计器在设计时调试自定义 XAML 控件

1. 在 Visual Studio 中打开解决方案或项目。

1. 生成解决方案/项目。

1. 打开包含要调试的自定义控件的 XAML 页。

   对于面向 Windows 版本16299或更高版本的 UWP 项目，此步骤将启动*UwpSurface*进程。 对于 Windows 版本16299之前的 WPF 或 UWP 版本，此步骤将启动*xdesproc.exe*进程。

1. 打开 Visual Studio 的第二个实例。 不要在第二个实例中打开解决方案或项目。

1. 在 Visual Studio 的第二个实例中，打开 "**调试**" 菜单，然后选择 "**附加到进程 ...** "。

1. 根据项目类型（请参阅前面的步骤），从可用进程的列表中选择 " *UwpSurface* " 或 " *xdesproc.exe* " 进程。

1. 在 "**附加到进程**" 对话框的 "**附加到**" 字段中，为要调试的自定义控件选择正确的代码类型。

   如果自定义控件已经用 .NET 语言编写，请选择相应的 .NET 代码类型，如 "**托管" （CoreCLR）** 。 如果已在中C++编写自定义控件，请选择 "**本机**"。

1. 单击 "**附加**" 按钮，附加 Visual Studio 的第二个实例。

1. 在 Visual Studio 的第二个实例中，打开与要调试的自定义控件关联的代码文件。 请确保只打开文件，而不是整个解决方案或项目。

1. 在以前打开的文件中放置必要的断点。

1. 在 Visual Studio 的第一个实例中，关闭包含要调试的自定义控件的 XAML 页（在前面的步骤中打开的同一页）。

1. 在 Visual Studio 的第一个实例中，打开您在上一步中关闭的 XAML 页。 这将导致调试器在 Visual Studio 的第二个实例中设置的第一个断点处停止。

1. 在 Visual Studio 的第二个实例中调试代码。

## <a name="see-also"></a>另请参阅
- [初探调试器](../debugger/debugger-feature-tour.md)
- [调试器安全](../debugger/debugger-security.md)