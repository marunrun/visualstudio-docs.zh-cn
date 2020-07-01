---
title: 刷新 UWP 应用 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- JavaScript debugging, refreshing pages [UWP apps]
- debugging, refreshing pages [UWP apps]
- DOM Explorer, Refresh [UWP apps]
- Refresh [UWP apps]
ms.assetid: fd99ee60-fa94-46df-8b17-369f60bfd908
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- uwp
ms.openlocfilehash: dd38a758a69b2e19079a2bc2511e7edf5cbfb0ab
ms.sourcegitcommit: c076fe12e459f0dbe2cd508e1294af14cb53119f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2020
ms.locfileid: "85348153"
---
# <a name="refresh-a-uwp-app-in-visual-studio"></a>在 Visual Studio 中刷新 UWP 应用

 可在进行调试时对代码进行更改，然后通过选择“调试”工具栏上的“刷新 Windows 应用”按钮，刷新使用 JavaScript 的 UWP 应用 。 选择此按钮将重新加载应用程序，但不会停止并重新启动调试器。 通过“刷新”功能，可修改 HTML、CSS 和 JavaScript 代码并迅速看到结果。 UWP 应用支持此功能。

 刷新功能不保持应用程序状态，也不反映对应用程序的以下更改：

- 程序包清单文件更改，其中包括对程序包清单中指定图像的更改。

- 引用更改（如添加或移除 SDK 引用）或 Windows 运行时组件（.winmd 文件）更改。

- 资源更改，如对 .resjson 文件中字符串的更改。

- 导致路径名更改、新建项目文件或删除文件的项目文件更改。

- 项目和项属性更改（如对所选调试设备的更改）或对文件的程序包操作的更改（在“属性”窗口中）。

> [!IMPORTANT]
> 在更改引用或包清单或者进行上面的列表中指定的其他更改时，必须停止并重新启动调试器以更新 HTML、CSS 和 JavaScript 源文件。

### <a name="to-refresh-an-app"></a>刷新应用程序

1. 在 Visual Studio 中打开 UWP 项目后，选择“本地计算机”作为调试目标。

     ![选择调试目标列表](../debugger/media/js_select_target.png "JS_Select_Target")

3. 按 F5 以在调试模式下运行应用程序。

4. 切换到 Visual Studio。

5. 在 UWP 应用的主页中，编辑其中一些 HTML。

7. 单击“刷新 Windows 应用”按钮，该按钮如下所示：![“刷新 Windows 应用”按钮](../debugger/media/js_refresh.png "JS_Refresh")。 （或按 F4。）

8. 切换到该应用程序。 应用重载，并使用更新的 HTML 呈现应用。

## <a name="see-also"></a>请参阅
- [快速入门：调试 HTML 和 CSS](../debugger/quickstart-debug-html-and-css.md)