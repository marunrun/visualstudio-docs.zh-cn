---
title: 调试混合模式应用程序 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], mixed-mode
- mixed-mode debugging, property evaluation
- Call Stack window
- mixed-mode debugging
- Call Stack window, mixed-mode debugging
- debugging managed code, mixed code
- mixed-mode debugging, call stack
ms.assetid: 60e34477-ae4e-48c7-9093-3e37f72e1bc3
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1c245b6c56b7480a9395394d707aa0f02fb22fc9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738184"
---
# <a name="debugging-mixed-mode-applications"></a>调试混合模式应用程序
混合模式应用程序是任何组合了本机代码 (C++) 与托管代码（在公共语言运行时上运行的 Visual Basic、Visual C# 或 C++）的应用程序。 在 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 中调试混合模式应用程序基本上是透明的；它与调试单模式应用程序没有太大区别。 但有几个特殊的注意事项。

## <a name="enable-c-edit-and-continue-in-mixed-mode-debugging"></a>在混合模式调试下启用 C++“编辑并继续”

若要为启用C++"编辑并继续"，请参阅[如何启用和禁用 "编辑并继续](../debugger/how-to-enable-and-disable-edit-and-continue.md)"。

> [!NOTE]
> 若要使用 Visual Studio 2013 中的 C++“编辑并继续”功能，你必须还原为旧调试引擎。 请参阅“Microsoft 应用程序生命周期管理”博客上的 [Switching to Managed Compatibility Mode in Visual Studio 2013](https://devblogs.microsoft.com/devops/switching-to-managed-compatibility-mode-in-visual-studio-2013/)（切换为 Visual Studio 2013 中的托管兼容性模式）。

## <a name="property-evaluation-in-mixed-mode-applications"></a>混合模式应用程序中的属性求值
 在混合模式应用程序中，调试器执行的属性求值是一个资源消耗很大的操作。 因此，调试操作（如单步执行）可能会很慢。 有关详细信息，请参阅[单步执行](https://docs.microsoft.com/previous-versions/visualstudio/visual-studio-2010/ek13f001(v=vs.100))。 如果混合模式调试的性能很低，你可能希望在调试器窗口中关闭属性求值。

> [!NOTE]
> 显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于你现用的设置或版本。 若要更改设置，请在 **“工具”** 菜单上选择 **“导入和导出设置”** 。 有关详细信息，请参阅[重置设置](../ide/environment-settings.md#reset-settings)。

### <a name="to-turn-off-property-evaluation"></a>关闭属性求值

1. 在 **“工具”** 菜单上，选择 **“选项”** 。

2. 在“选项”对话框中，打开“调试”文件夹并选择“常规”类别。

3. 清除“启用属性求值和其他隐式函数调用”复选框。

   由于本机调用堆栈和托管调用堆栈不同，因此调试器不能总是为混合代码提供完整的调用堆栈。 当本机代码调用托管代码时，你可能会注意到某些差异。 有关详细信息，请参阅[“调用堆栈”窗口中的混合代码与缺失信息](../debugger/mixed-code-and-missing-information-in-the-call-stack-window.md)。

## <a name="see-also"></a>请参阅

- [调试托管代码](../debugger/debugging-managed-code.md)