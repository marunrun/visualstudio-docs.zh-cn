---
title: 在 XAML 设计器中调试或禁用项目代码 | Microsoft Docs
ms.prod: visual-studio-dev14
ms.technology: vs-ide-designers
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: ac600581-8fc8-49e3-abdf-1569a3483d74
caps.latest.revision: 7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: d56a36693d995687a2dddede3d60ada44c8d32bd
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436203"
---
# <a name="debugging-or-disabling-project-code-in-xaml-designer"></a>在 XAML 设计器中调试或禁用项目代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

很多情况下，造成 XAML 设计器中出现未处理异常的原因可能为：项目代码尝试访问在设计器运行应用程序时返回不同值或以不同方式运行的属性/方法。 可以通过在 Visual Studio 的其他实例中调试项目代码来解决这些异常，也可通过禁用设计器中的项目代码暂时阻止它们。  
  
 项目代码包括：  
  
- 自定义控件和用户控件  
  
- 类库  
  
- 值转换器  
  
- 针对从项目代码生成的设计时数据绑定  
  
  当禁用项目代码时，Visual Studio 将显示占位符，如绑定中数据不再可用的属性的名称；或显示不再运行的控件的占位符。  
  
  ![“未经处理的异常”对话框](../designers/media/xaml-unhandledexception.png "XAML_UnhandledException")  
  
#### <a name="to-determine-if-project-code-is-causing-an-exception"></a>确定项目代码是否会导致异常  
  
1. 在未处理的异常对话框中，选择“单击此处重载设计器”  链接。  
  
2. 在菜单栏上，依次选择“调试” 和“启动调试”  以生成和运行应用程序。  
  
     如果应用程序成功生成和运行，则设计时异常可能由设计器中运行的项目代码引起。  
  
#### <a name="to-debug-project-code-running-in-the-designer"></a>调试设计器中运行的项目代码  
  
1. 在未处理的异常对话框中，选择“单击此处禁用正在运行的项目代码并重载设计器”  链接。  
  
2. 在 Windows 任务管理器中，选择“结束任务”  按钮以关闭当前运行的 Visual Studio XAML 设计器的任何实例。  
  
     ![TaskManager 中的 XAML 设计器实例](../designers/media/xaml-taskmanager.png "XAML_TaskManager")  
  
3. 在 Visual Studio 中，打开 XAML 页面，其中包含要调试的代码或控件。  
  
4. 打开 Visual Studio 的新实例，然后打开项目的第二个实例。  
  
5. 在项目代码中设置断点。  
  
6. 在 Visual Studio 的新实例中，依次选择菜单栏上的“调试” 和“附加到进程” 。  
  
7. 在“附加到进程”  对话框中，从“可用进程”  列表中选择“XDesProc.exe” ，然后选择“附加”  按钮。  
  
     ![XAML 设计器进程](../designers/media/xaml-attach.png "XAML_Attach")  
  
     这是 Visual Studio 的第一个实例中 XAML 设计器的进程。  
  
8. 在 Visual Studio 的第一个实例中，依次选择菜单栏上的“调试” 和“启动调试” 。  
  
     现即可单步执行设计器中运行的代码。  
  
#### <a name="to-disable-project-code-in-the-designer"></a>禁用设计器中的项目代码  
  
- 在未处理的异常对话框中，选择“单击此处禁用正在运行的项目代码并重载设计器”  链接。  
  
- 或者，在 XAML 设计器的工具栏上，选择“禁用项目代码”  按钮。  
  
     ![“禁用项目代码”按钮](../designers/media/xaml-disablecode.png "XAML_DisableCode")  
  
     你可以再次切换按钮以重新启用项目代码。  
  
    > [!NOTE]
    > 对于面向 ARM 或 X64 处理器的项目，Visual Studio 无法在设计器中运行项目代码，因此禁用设计器中的“禁用项目代码”  按钮。  
  
- 其中任一选项都将导致设计器重载，然后会禁用关联项目的所有代码。  
  
    > [!NOTE]
    > 禁用项目代码可能导致设计时数据丢失。 或者调试在设计器中运行的代码。  
  
## <a name="see-also"></a>请参阅  
 [在 Visual Studio 和 Blend for Visual Studio 中设计 XAML](../designers/designing-xaml-in-visual-studio.md)
