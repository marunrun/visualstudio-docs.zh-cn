---
title: XAML 概述
ms.date: 01/10/2020
ms.topic: reference
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: 2556387f523769bba93708a9c00d1f7c62429c0f
ms.sourcegitcommit: aa302af53de342e75793bd05b10325939dc69b53
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2020
ms.locfileid: "82921225"
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

有关最新信息，请参阅[Visual studio 2019 中的 XAML 开发人员工具的新增功能](https://devblogs.microsoft.com/visualstudio/whats-new-in-xaml-developer-tools-in-visual-studio-2019-for-wpf-uwp/)博客文章和 YouTube 上[visual Studio 中的新 XAML 功能](https://youtu.be/yI9OyA4ZM2E)视频。

## <a name="see-also"></a>另请参阅

- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)
