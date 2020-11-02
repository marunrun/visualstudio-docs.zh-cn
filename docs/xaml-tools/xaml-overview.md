---
title: XAML 概述
description: 了解 Visual Studio 中的 XAML 和 XAML 代码编辑器及 XAML 设计器工具的基本信息。
ms.custom: SEO-VS-2020
ms.date: 06/23/2020
ms.topic: overview
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 997a35414f38af16d028770044c28652e13149be
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2020
ms.locfileid: "93049188"
---
# <a name="overview-of-xaml"></a>XAML 概述

可扩展应用程序标记语言 (XAML) 是一种基于 XML 的声明性语言。 XAML 广泛用于以下类型的应用程序来生成用户界面：

- [Windows Presentation Foundation (WPF) 应用](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [通用 Windows 平台 (UWP) 应用](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用](/xamarin/xamarin-forms/xaml/)

以下 XAML 代码用于定义简单的按钮控件。

```xaml
<Button Click="ButtonClick">Show updates</Button>
```

XAML 还用于定义 [Windows WorkFlow Foundation (WF) 应用](/dotnet/framework/windows-workflow-foundation/serializing-workflows-and-activities-to-and-from-xaml)中的工作流。

## <a name="xaml-code-editor"></a>XAML 代码编辑器

Visual Studio IDE 中的 [XAML 代码编辑器](xaml-code-editor.md)包括为 Windows 平台和 Xamarin.Forms 创建 WPF 和 UWP 应用所需的所有工具。 尽管 Visual Studio 中的 IDE（集成开发环境）提供许多可用于为其他平台开发应用的功能，但它也具有一些 XAML 独有的功能。

## <a name="xaml-designer"></a>XAML 设计器

Visual Studio 和 Blend for Visual Studio 提供了 [XAML 设计器](creating-a-ui-by-using-xaml-designer-in-visual-studio.md)，可帮助你为 WPF、UWP 和 Xamarin.Forms 应用生成用户界面 (UI)。 可以从“工具箱”或“资产”窗口中拖动控件并在“属性”窗口中设置属性。 执行此操作时，Visual Studio 和 Blend for Visual Studio 会创建相应的 XAML 代码。 如果希望直接编辑 XAML 代码，则也可以这样做。

## <a name="whats-new"></a>新增功能

有关最新信息，请参阅以下资源：

- [Visual Studio 2019 版本 16.7 预览版 1 中对 XAML 工具的改进](https://devblogs.microsoft.com/visualstudio/improvements-to-xaml-tooling-in-visual-studio-2019-version-16-7-preview-1/)博客文章
- [Visual Studio 2019 中 XAML 开发人员工具的新增功能](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)博客文章
- YouTube 上的 [Visual Studio 中的新增 XAML 功能](https://youtu.be/yI9OyA4ZM2E)视频

## <a name="see-also"></a>另请参阅

- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
