---
title: 在调试器中创建的数据的自定义视图 |Microsoft Docs
ms.date: 01/09/2019
ms.topic: conceptual
f1_keywords:
- vs.debug
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- debugging [Visual Studio], inspecting programs
- debugger, viewing data
ms.assetid: 13e1105f-f987-402e-9108-ec6ac12be042
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 32b3fddd13bd16ac2c846f02f54596ec846374b9
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62929994"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger-c-visual-basic-c"></a>在 Visual Studio 调试器中创建自定义视图的数据 (C#，Visual Basic 中， C++)

[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]调试器提供了许多工具，用于检查和修改程序状态。 这些工具中的大多数仅在中断模式下有效。

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>在变量窗口和数据提示中创建数据的自定义的视图

 许多[调试器窗口](../debugger/debugger-windows.md)，如**自动**并**观看**windows 中，可以检查变量。 你可以自定义如何C++在调试器变量窗口中并在显示类型、 托管的对象和你自己的类型[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)。 有关详细信息，请参阅[创建自定义视图的C++对象](../debugger/create-custom-views-of-native-objects.md)并[创建对象的自定义视图](../debugger/create-custom-views-of-dot-managed-objects.md)。

## <a name="create-custom-visualizers"></a>创建自定义可视化工具

 可视化工具，可查看的对象或变量的内容中有意义的方式。 在 Visual Studio 调试器可视化工具是指可以打开使用放大镜的不同窗口![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")图标。 例如，HTML 可视化工具显示了将如何解释和显示在浏览器中的 HTML 字符串。 您可以从数据提示功能，来访问可视化工具**Watch**窗口中，**自动**窗口中，并**局部变量**窗口。 **快速监视**对话框还提供了可视化工具。 有关详细信息，请参阅[创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)。

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [“命令”窗口](../ide/reference/command-window.md)
- [调试器安全](../debugger/debugger-security.md)