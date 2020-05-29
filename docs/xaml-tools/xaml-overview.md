---
title: XAML 概述
ms.date: 05/20/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 97f3bc7777023903d5fc38ad1bda7cde45b683b6
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183478"
---
# <a name="overview-of-xaml"></a>XAML 概述

可扩展应用程序标记语言 (XAML) 是一种基于 XML 的声明性语言。 XAML 广泛用于以下类型的应用程序来生成用户界面：

- [Windows Presentation Foundation （WPF）应用](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [通用 Windows 平台（UWP）应用](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用](/xamarin/xamarin-forms/xaml/)

以下 XAML 代码用于定义简单的按钮控件。

```xaml
<Button Click="ButtonClick">Show updates</Button>
```

XAML 还用于定义 [Windows WorkFlow Foundation (WF) 应用](/dotnet/framework/windows-workflow-foundation/serializing-workflows-and-activities-to-and-from-xaml)中的工作流。

## <a name="xaml-designer"></a>XAML 设计器

Visual Studio 和 Blend for Visual Studio 提供了 XAML 设计器，可帮助你为 WPF、UWP 和 Xamarin.Forms 应用生成用户界面 (UI)。 可以从“工具箱”或“资产”窗口中拖动控件并在“属性”窗口中设置属性。 当你执行此操作时，Visual Studio 和 Blend for Visual Studio 会创建相应的 XAML 代码。 如果希望直接编辑 XAML 代码，则也可以这样做。

本文档集中的文章介绍了 Visual Studio 和 Blend for Visual Studio 中的 XAML 设计器。

## <a name="whats-new"></a>新增功能

有关最新信息，请参阅[Visual studio 2019 中的 xaml 开发人员工具中的新增功能](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)，请参阅 visual studio 中的 xaml 开发人员工具博客文章中对[visual studio 2019 版本 16.7 Preview 1 中的 Xaml 工具的改进](https://devblogs.microsoft.com/visualstudio/improvements-to-xaml-tooling-in-visual-studio-2019-version-16-7-preview-1/)，以及 YouTube 上[VISUAL studio 中的新 xaml 功能](https://youtu.be/yI9OyA4ZM2E)。

## <a name="see-also"></a>请参阅

- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
