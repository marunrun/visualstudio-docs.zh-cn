---
title: 使用 XAML 热重载编写和调试 XAML
description: XAML 热重载或 XAML "编辑并继续" 允许在运行应用时更改 XAML 代码
ms.date: 08/05/2019
ms.topic: conceptual
helpviewer_keywords:
- xaml edit and continue
- xaml hot reload
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e49049d05a285889c54906534200acadaf2397e
ms.sourcegitcommit: 034c503ae04e22cf840ccb9770bffd012e40fb2d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72306204"
---
# <a name="write-and-debug-running-xaml-code-with-xaml-hot-reload-in-visual-studio"></a>在 Visual Studio 中通过 XAML 热重载编写和调试正在运行的 XAML 代码

XAML 热重载可帮助你在应用运行时对 XAML 代码进行更改，从而生成 WPF 或 UWP 应用用户界面（UI）。 热重载适用于 Visual Studio 和 Blend for Visual Studio。 利用此功能，您可以通过运行中应用的数据上下文、身份验证状态以及在设计时难以模拟的其他真实复杂性的优点，逐步生成和测试 XAML 代码。 如果需要帮助排查 XAML 热重载问题，请参阅[排查 Xaml 热重载问题](xaml-hot-reload-troubleshooting.md)。

> [!NOTE]
> 如果使用的是 Xamarin，请参阅[适用于 xamarin 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)。

XAML 热重载在这些情况下特别有用：

* 修复在调试模式下启动应用后在 XAML 代码中发现的 UI 问题。

* 为正在开发的应用生成新的 UI 组件，同时利用应用的运行时上下文。

|支持的应用程序类型|操作系统和工具|
|-|-|-|
|Windows Presentation Foundation (WPF) |.NET Framework 4.6 + 和 .NET Core</br>Windows 7 和更高版本 |
|通用 Windows 应用（UWP）|Windows 10 及更高版本，以及 [windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 14393 + |

下图演示了如何使用实时可视化树打开源代码，然后使用 XAML 热重载来更改按钮文本和按钮颜色。

![XAML 热重载](../debugger/media/xaml-hot-reload-using.gif)

> [!NOTE]
> 当前仅当在 Visual Studio 中运行应用程序，Blend for Visual Studio 或在调试器中运行时（按**F5**或**启动调试**），才支持 Visual studio XAML 热重载。 除非[手动设置环境变量](xaml-hot-reload-troubleshooting.md#verify-that-you-use-start-debugging-rather-than-attach-to-process)，否则不能使用 "[附加到进程](../debugger/attach-to-running-processes-with-the-visual-studio-debugger.md)" 启用此体验。

## <a name="known-limitations"></a>已知限制

下面是 XAML 热重载的已知限制。 若要解决遇到的任何限制，只需停止调试器，然后完成操作。

|限制|WPF|UWP|说明|
|-|-|-|-|
|在应用程序运行时将事件布线到控件|不支持|不支持|请参阅错误：*确保事件失败*。 请注意，在 WPF 中，可以引用现有的事件处理程序。 在 UWP 应用中，不支持引用现有的事件处理程序。|
|在资源字典中创建资源对象，如应用的页面/窗口或*应用程序*中的资源对象。|从 Visual Studio 2019 Update 2 开始支持|支持|示例：将 @no__t 0 添加到用于 @no__t 的资源字典中。</br>注意:使用 XAML 热重载时，可以应用/使用写入资源字典的静态资源、样式转换器和其他元素。 仅资源的创建不受支持。</br> 更改资源字典 `Source` 属性。|
|在应用程序运行时向项目添加新控件、类、窗口或其他文件|不支持|不支持|无|
|管理 NuGet 包（添加/删除/更新包）|不支持|不支持|无|
|更改使用 {x:Bind} 标记扩展的数据绑定|不可用|从 Visual Studio 2019 开始支持|这需要 Windows 10 版本1809（build 10.0.17763）。 在 Visual Studio 2017 或早期版本中不受支持。|
|不支持更改 X：Uid 指令|不可用|不支持|无|

## <a name="error-messages"></a>错误消息

使用 XAML 热重载时，可能会遇到以下错误。

|错误消息|描述|
|-|-|
|确保事件失败|错误指示你正在尝试将事件连接到你的某个控件，而你的应用程序在运行时不受支持。|
|XAML 热重载不支持此更改，并且不会在调试会话过程中应用此更改。|错误表明 XAML 热重载不支持你正在尝试的更改。 停止调试会话，进行更改，然后重新启动调试会话。 如果你发现不受支持的方案，请使用[Visual Studio 开发人员社区](https://developercommunity.visualstudio.com/spaces/8/index.html)中的新的 "建议功能" 选项。 |

## <a name="see-also"></a>请参阅

* [排查 XAML 热重载问题](xaml-hot-reload-troubleshooting.md)
* [适用于 Xamarin 的 XAML 热重载](/xamarin/xamarin-forms/xaml/hot-reload)
* [编辑并继续 (Visual C#)](../debugger/edit-and-continue-visual-csharp.md)
