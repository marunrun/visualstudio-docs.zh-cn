---
title: 在 XAML 设计器中调试或禁用项目代码
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: ac600581-8fc8-49e3-abdf-1569a3483d74
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.openlocfilehash: ce29bcef43877ec8a41235545652278645cad123
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "82921165"
---
# <a name="debug-or-disable-project-code-in-xaml-designer"></a>在 XAML 设计器中调试或禁用项目代码

很多情况下，造成 XAML 设计器中出现未处理异常的原因可能为：项目代码尝试访问在设计器运行应用程序时返回不同值或以不同方式运行的属性/方法。 可通过在 Visual Studio 的其他实例中调试项目代码解决这些异常，也可通过禁用设计器中的项目代码暂时阻止这些异常。

项目代码包括：

- 自定义控件和用户控件

- 类库

- 值转换器

- 针对从项目代码生成的设计时数据绑定

当禁用项目代码时，Visual Studio 会显示占位符。 例如，Visual Studio 会显示所含数据不再可用的绑定的属性名称，或显示不再运行的控件的占位符。

![未经处理的异常对话框](media/xaml_unhandledexception.png)

## <a name="to-determine-if-project-code-is-causing-an-exception"></a>确定项目代码是否会导致异常

1. 在未处理的异常对话框中，选择“单击此处重载设计器” **** 链接。

2. 在菜单栏上，选择 "**调试** > " "**开始调试**" 以生成和运行应用程序。

     如果应用程序成功生成和运行，则设计时异常可能由设计器中运行的项目代码引起。

## <a name="to-debug-project-code-running-in-the-designer"></a>调试设计器中运行的项目代码

1. 在未处理的异常对话框中，选择“单击此处禁用正在运行的项目代码并重载设计器” **** 链接。

2. 在 Windows 任务管理器中，选择“结束任务” **** 按钮以关闭当前运行的 Visual Studio XAML 设计器的任何实例。

     ![TaskManager 中的 XAML 设计器实例](media/xaml_taskmanager.png)

3. 在 Visual Studio 中，打开 XAML 页面，其中包含要调试的代码或控件。

4. 打开 Visual Studio 的新实例，然后打开项目的第二个实例。

5. 在项目代码中设置断点。

6. 在 Visual Studio 的新实例中，在菜单栏上选择 "**调试** > " "**附加到进程**"。

7. 在“附加到进程” **** 对话框中，从“可用进程” **** 列表中选择“XDesProc.exe” ****，然后选择“附加” **** 按钮。

     ![XAML 设计器进程](media/xaml_attach.png)

     这是 Visual Studio 的第一个实例中 XAML 设计器的进程。

8. 在 Visual Studio 的第一个实例中，在菜单栏上选择 "**调试** > " "**启动调试**"。

     现即可单步执行设计器中运行的代码。

## <a name="to-disable-project-code-in-the-designer"></a>禁用设计器中的项目代码

- 在未处理的异常对话框中，选择“单击此处禁用正在运行的项目代码并重载设计器” **** 链接。

- 或者，在**XAML 设计器**的工具栏中，选择 "**禁用项目代码**" 按钮。

     ![“禁用项目代码”按钮](media/xaml_disablecode.png)

     你可以再次切换按钮以重新启用项目代码。

    > [!NOTE]
    > 对于面向 ARM 或 X64 处理器的项目，Visual Studio 无法在设计器中运行项目代码，因此禁用设计器中的“禁用项目代码” **** 按钮。

- 其中任一选项都会导致设计器重载，然后会禁用关联项目的所有代码。

    > [!NOTE]
    > 禁用项目代码可能导致设计时数据丢失。 或者调试在设计器中运行的代码。

## <a name="control-display-options"></a>控件显示选项

> [!NOTE]
> “控件显示选项”**** 仅适用于定目标到 Windows 10 Fall Creators Update（生成号 16299）或更高版本的通用 Windows 平台应用程序。 Visual Studio 2017 版本 15.9 或更高版本提供“控件显示选项”**** 功能。

在 XAML 设计器中，可以将“控件显示选项”更改为，仅显示 Windows SDK 中的平台控件。 这可能会提升 XAML 设计器的可靠性。

若要更改“控件显示选项”，请单击设计器窗口左下角的图标，再选择“控件显示选项”**** 下的选项：

![控件显示选项](media/control_display_options.png)

当你选中“仅显示平台控件”**** 后，SDK 中的所有自定义控件、客户用户控件等都不会完整呈现。 相反，它们会被替换为回退控件，以展示控件的大小和位置。

## <a name="see-also"></a>另请参阅

- [在 Visual Studio 和 Blend for Visual Studio 中设计 XAML](designing-xaml-in-visual-studio.md)
