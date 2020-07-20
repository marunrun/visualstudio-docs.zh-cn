---
title: “选择代码类型”对话框 | Microsoft Docs
ms.date: 06/12/2020
ms.topic: reference
f1_keywords:
- vs.debug.selectengines
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
- SQL
helpviewer_keywords:
- debugging [Visual Studio], engine selection
- debugger, engine selection
- debugging engine selection dialog box
no-loc:
- Blazor WebAssembly
ms.assetid: 932269fe-94e3-43cb-8931-078f31afd177
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9ccfe636cd8981c2f9dcc1375fb795d6c026b572
ms.sourcegitcommit: 5e82a428795749c594f71300ab03a935dc1d523b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2020
ms.locfileid: "86211575"
---
# <a name="select-code-type-dialog-box"></a>“选择代码类型”对话框

若要打开此对话框，请打开“附加到进程”对话框，然后单击“选择”按钮 。

**自动确定要调试的代码类型**：根据正在运行的代码的类型选择适当的调试器。

调试以下代码类型：从提供的列表中，选择要调试的代码的一个或多个类型。 在[排除附加故障](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md#BKMK_Troubleshoot_attach_errors)时，这可能会很有帮助。 此选项限制为只检测要调试的这些类型代码。

   ::: moniker range=">=vs-2019"
   - Blazor WebAssembly - 客户端 Blazor WebAssembly
   - GPU - 软件模拟器 - 在 GPU 软件模拟器上运行的 C++ 代码
   - JavaScript (Chrome) - 在 Chrome 中运行的 JavaScript
   - JavaScript (Microsoft Edge - Chromium) - 在基于 Chromium 的 Microsoft Edge for Windows 10 上运行的 JavaScript
   - JavaScript CDP (V3) 调试程序 - Chrome DevTools 协议版本 3，用于在 CDP 客户端中进行调试
   - 托管 (CoreCLR) - .NET Core
   - 托管（本机编译）- C++/CLR 代码
   - 托管（v3.5、v3.0、v2.0）- .NET Framework 2.0 及更高版本（最高版本为 3.5）的 .NET Framework 代码
   - 托管（v4.6、v4.5、v4.0）- .NET Framework 4.0 及更高版本的 .NET Framework 代码
   - 本机 - C/C++
   - Node.js 调试 - 由 Node.js 运行时托管的代码
   - Python - Python 
   - 脚本 - 指定适用于 JavaScript 的通用脚本调试程序。 如果适用于你的方案（如 JavaScript (Chrome)），请使用限制性更强的选项。
   - T-SQL - Transact-SQL
   - Unity - Unity
   - 托管兼容性模式 - 指定用于托管代码的旧版调试程序，通常用于使用 C++/CLR 代码的混合模式调试（为混合模式启用“编辑并继续”），或用于支持定目标到旧版调试程序的扩展。 在大多数混合模式调试方案中，选择“本机”和相应的“托管”代码类型，而不是“托管兼容性模式”。
   ::: moniker-end

   在大多数情况下，不支持在同一调试会话中附加多个调试程序。 可以使用 Visual Studio 的第二个实例来完成此操作。

## <a name="see-also"></a>请参阅
- [调试器安全](../debugger/debugger-security.md)
- [附加到正在运行的进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)
