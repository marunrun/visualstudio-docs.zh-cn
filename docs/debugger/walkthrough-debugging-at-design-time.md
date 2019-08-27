---
title: 在设计时调试 |Microsoft Docs
ms.custom: seodec18
ms.date: 11/21/2018
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
ms.openlocfilehash: 82e82a75ce5ecff8e9b7e6d0b6aaf2e29728fc45
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901054"
---
# <a name="debug-at-design-time-in-visual-studio-c-c-visual-basic-f"></a>在设计时在 Visual Studio 中调试 (C#， C++，Visual Basic 中， F#)

若要在设计时而不是应用程序时调试代码正在运行，则可以使用**即时**窗口。

若要调试 XAML 代码隐藏应用程序从 XAML 设计器中，如数据绑定代码，可以使用**调试** > **附加到进程**。

## <a name="use-the-immediate-window"></a>使用即时窗口

可以使用 Visual Studio**即时**窗口来执行函数或子例程，而无需运行您的应用程序。 如果函数或子例程包含断点，Visual Studio 会在断点处中断。 随后即可使用调试器窗口检查程序状态。 此功能被称为*在设计时调试*。

下面的示例是在 Visual Basic 中。 此外可以使用**即时**窗口中的在设计时在C#， F#，和C++应用程序。

1. 将以下代码粘贴到空白的 Visual Basic 控制台应用程序：

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

1. 在行上设置断点**End Function**。

1. 打开**即时**通过选择窗口**调试** > **Windows** > **即时**。 类型`?MyFunction`中窗口中，然后按**Enter**。

   断点被命中和的值**MyFunction**中**局部变量**窗口**1**。 在应用处于中断模式中时，可以检查调用堆栈和其他调试窗口。

1. 选择**继续**Visual Studio 工具栏上。 应用程序结束，并**1**中返回**即时**窗口。 请确保仍处于设计模式。

1. 类型`?MyFunction`中**即时**窗口，然后按**Enter**。 断点被命中和的值**MyFunction**中**局部变量**窗口**2**。

1. 不选择**继续**，类型`?MySub()`中**即时**窗口中，，然后按**Enter**。 断点被命中和的值**MyFunction**中**局部变量**窗口**3**。 在应用处于中断模式中时，您可以检查应用程序状态。

1. 选择**继续**。 断点是同样，命中和的值**MyFunction**中**局部变量**现在已窗口**2**。 **即时**窗口将返回**表达式已经过评估，不具有任何值**。

1. 选择**继续**试。 应用程序结束，并**2**中返回**即时**窗口。 请确保仍处于设计模式。

1. 若要清除的内容**即时**窗口中，右键单击在窗口中，选择**清除所有**。

## <a name="attach-to-an-app-from-the-xaml-designer"></a>从 XAML 设计器附加到应用

在某些声明性数据绑定方案中，它可以帮助调试在 XAML 设计器中的代码隐藏。

1. 在 Visual Studio 项目中，添加一个新的 XAML 页，例如*temp.xaml*。 将新的 XAML 页面保留为空。

1. 生成解决方案。

1. 打开*temp.xaml*，这会加载 XAML 设计器中， *XDesProc.exe*，或*UwpSurface.exe* UWP 应用中。

1. 打开 Visual Studio 的新实例。 在新的实例中，选择**调试** > **附加到进程**。

1. 在中**附加到进程**对话框中，选择在设计器处理的来自**可用进程**列表。

   适用于 UWP 项目面向 Windows 内部版本 16299 或更高版本，设计器的进程*UwpSurface.exe*。 对于 WPF 或 UWP 版本低于版本 16299，设计器的进程是*XDesProc.exe*。

1. 请确保**将附加到**字段设置为正确的代码类型的.NET 版本，如**托管代码 (CoreCLR)**。

1. 选择“附加”。

1. 附加到进程时，切换到另一个 Visual Studio 实例，并想要调试您的应用程序背后的代码设置断点。

   例如，您可以设置断点类型转换器代码中为以下 XAML，这是将 TextBlock 绑定在设计时。

    ```xaml
    <TextBlock Text="{Binding title, ConverterParameter=lower, Converter={StaticResource StringFormatConverter}, Mode=TwoWay}"  />
    ```

   加载页时命中断点。

## <a name="see-also"></a>请参阅
- [初探调试器](../debugger/debugger-feature-tour.md)
- [调试器安全](../debugger/debugger-security.md)