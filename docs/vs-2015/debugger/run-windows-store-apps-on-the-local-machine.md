---
title: 在本地计算机上的运行 Windows 应用商店应用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
ms.assetid: e42a21a8-6423-4caf-b4dc-72b263e76019
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 031d764b95aa0f292702dde6167e0be9826270bf
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68196330"
---
# <a name="run-windows-store-apps-on-the-local-machine"></a>在本地计算机上运行 Windows 应用商店应用程序
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

仅适用于 Windows] (../Image/windows_only_content.png"windows_only_content")  
  
 要在 Windows 应用商店应用上调试、测试或运行性能分析，你可以在托管 Visual Studio 的相同计算机上运行该应用。 如果设备上的显示屏支持触控，你可以执行应用的完整功能；否则，你只能使用有限的鼠标和键盘手势。  
  
## <a name="BKMK_In_this_topic"></a> 在本主题中  
 可了解：  
  
 [如何在本地计算机上运行](#BKMK_How_to_run_on_a_local_machine)  
  
 [如何在单个监视器上的 Windows 应用商店应用程序和 Visual Studio 之间切换](#BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor)  
  
## <a name="BKMK_How_to_run_on_a_local_machine"></a> 如何在本地计算机上运行  
 若要在本地计算机上运行该应用，请选择**本地计算机**调试器上的启动调试按钮旁边的下拉列表**标准**工具栏。  
  
 ![本地计算机上运行](../debugger/media/vsrun-f5-local.png "VSRUN_F5_Local")  
  
 如果无法看到**标准**工具栏上，单击**视图**菜单上，指向**工具栏**，然后单击**标准**。  
  
 你在下拉列表中所做的选择将保留在项目属性文件中，并成为默认的运行目标。  
  
 你也可以直接在项目属性文件中设置运行目标。 右键单击项目名称在**解决方案资源管理器**，然后选择**属性**。 然后，执行下列操作之一：  
  
- 在 C# 和 Visual Basic 项目中，单击**调试**，然后选择**本地计算机**从**目标设备**下拉列表。  
  
     ![C&#35;和 Visual Basic 项目属性页](../debugger/media/vsrun-cs-vb-projprop-local.png "VSRUN_CS_VB_ProjProp_Local")  
  
- 在C++和 JavaScript 项目中，展开**配置属性**节点中，单击**调试**，然后选择**本地调试器**从**要启动的调试器**列表。  
  
     ![C&#43; &#43;和 JavaScript 项目属性页](../debugger/media/vsrun-cpp-js-projprop-local.png "VSRUN_CPP_JS_ProjProp_Local")  
  
## <a name="BKMK_How_to_switch_between_a_Windows_Store_app_and_Visual_Studio_on_a_single_monitor"></a> 如何在单个监视器上的 Windows 应用商店应用程序和 Visual Studio 之间切换  
 **若要从正在运行的 Windows 应用商店应用程序实例切换到 Visual Studio**  
  
 当你在本地计算机上运行 Windows 应用商店应用并且仅使用单个监视器时，你可能希望在保持应用运行的同时切换回 Visual Studio。 例如，应用可能处于断点无法达到的某个状态，例如等待事件或困在一个长期或无休止的循环中。 要返回到 Visual Studio，请按 ALT + TAB。
