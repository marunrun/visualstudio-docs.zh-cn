---
title: 在调试器中创建数据的自定义视图 |Microsoft Docs
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
ms.openlocfilehash: 63dc11736e92013719fcda2bae0ba9599a8835aa
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/18/2019
ms.locfileid: "72569003"
---
# <a name="create-custom-views-of-data-in-the-visual-studio-debugger-c-visual-basic-c"></a>在 Visual Studio 调试器中创建数据的自定义视图C#（、Visual Basic C++、）

@No__t_0 调试器提供了许多用于检查和修改程序状态的工具。 这些工具中的大多数仅在中断模式下有效。

## <a name="create-custom-views-of-data-in-variable-windows-and-datatips"></a>在变量窗口和数据提示中创建数据的自定义视图

 许多[调试器窗口](../debugger/debugger-windows.md)（**如 "自动**" 和 "**监视**" 窗口）都允许您检查变量。 您可以自定义C++类型、托管对象以及您自己的类型在调试器变量窗口和[数据提示](../debugger/view-data-values-in-data-tips-in-the-code-editor.md)中的显示方式。 有关详细信息，请参阅[创建对象的C++自定义视图](../debugger/create-custom-views-of-native-objects.md)和[创建托管对象的自定义视图](../debugger/create-custom-views-of-managed-objects.md)。

## <a name="create-custom-visualizers"></a>创建自定义可视化工具

 可视化工具使您能够以有意义的方式查看对象或变量的内容。 在 Visual Studio 调试器中，可视化工具是指可以使用放大镜![VisualizerIcon](../debugger/media/dbg-tips-visualizer-icon.png "可视化工具图标")图标打开的其他窗口。 例如，HTML 可视化工具显示 HTML 字符串如何在浏览器中进行解释和显示。 你可以通过数据提示、"**监视**" 窗口 **、"自动**" 窗口和 "**局部变量**" 窗口访问可视化工具。 "**快速监视**" 对话框还提供可视化工具。 有关详细信息，请参阅[创建自定义可视化工具](../debugger/create-custom-visualizers-of-data.md)。

## <a name="see-also"></a>请参阅

- [初探调试器](../debugger/debugger-feature-tour.md)
- [“命令”窗口](../ide/reference/command-window.md)
- [调试器安全](../debugger/debugger-security.md)
