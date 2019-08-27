---
title: XAML 概述
ms.date: 07/31/2019
ms.topic: reference
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a9b04012e2f0b046b3fd31058c9838740e833281
ms.sourcegitcommit: 90c3187d804ad7544367829d07ed4b47d3f8a72d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2019
ms.locfileid: "68823913"
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

## <a name="xaml-designer"></a>XAML 设计器

Visual Studio 和 Blend for Visual Studio 提供了 XAML 设计器，可帮助你为 WPF、UWP 和 Xamarin.Forms 应用生成用户界面 (UI)。 可以从“工具箱”或“资产”窗口中拖动控件并在“属性”窗口中设置属性。 执行这些操作时，Visual Studio 和 Blend for Visual Studio 会创建相应的 XAML 代码。 如果希望直接编辑 XAML 代码，则也可以这样做。

本文档集中的文章介绍了 Visual Studio 和 Blend for Visual Studio 中的 XAML 设计器。

## <a name="see-also"></a>请参阅

- [WPF 应用中的 XAML](/dotnet/framework/wpf/advanced/xaml-in-wpf)
- [UWP 应用中的 XAML](/windows/uwp/xaml-platform/xaml-overview)
- [Xamarin.Forms 应用中的 XAML](/xamarin/xamarin-forms/xaml/)