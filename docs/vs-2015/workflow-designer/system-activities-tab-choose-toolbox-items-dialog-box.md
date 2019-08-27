---
title: System.Activities 选项卡上，选择工具箱项对话框 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES_COMPONENTS
- VS.CHOOSEITEMS.SYSTEM.ACTIVITIES COMPONENTS
ms.assetid: cef390cd-eeda-42e6-9d2e-18c8325a4f06
caps.latest.revision: 5
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 29eb905a4852bf521ebee72a498b44edbdcef8df
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63445402"
---
# <a name="systemactivities-tab-choose-toolbox-items-dialog-box"></a>“System.Activities”选项卡 ->“选择工具箱项”对话框
此选项卡**选择工具箱项**对话框中显示的列表[!INCLUDE[wf](../includes/wf-md.md)]活动、 模板和项目可用。 若要显示此列表，请选择**选择工具箱项**从**工具**菜单或通过右击**工具箱**并选择**选择项**以显示**选择工具箱项**对话框中，并选择其**System.Activities**选项卡。默认情况下，该列表包含 System.Activities、 System.ServiceModel.Activities 和 System.Activities.Core.Presentation 程序集; 的工作流活动但是，仅系统提供所示的活动和活动通过显示在其他程序集添加**工具箱**默认情况下选中。 最近添加的活动，会自动选中，并显示在**工具箱**当你单击**确定**对话框上。 此外，这些项显示在**工具箱**对应于活动/项/模板所在的命名空间的新类别下。  
  
> [!WARNING]
> 如果您试图添加未包含任何工作流活动的程序集，则将显示一个错误对话框，指出该程序集没有包含任何活动。  
  
 此对话框是项目不可知，因此**System.Activities**选项卡继续显示在独立 XAML 或非工作流项目类型。  
  
 对每个选项卡都会执行筛选。这意味着不能添加到工作流活动 **.NET 组件**选项卡。他们需要通过添加**System.Activities**选项卡本身。  
  
 你可以取消选中不想要查看在任何的项**工具箱**在此对话框中选项卡上，或者，您可以使用来完成**删除**中的上下文菜单选项**工具箱**和取消引用程序集不会删除中的项**工具箱**。  
  
 通过将活动拖放到设计器上来实例化该活动会自动将包含该项的程序集添加到引用的程序集列表中。 此外，如果该活动引用程序集 C，它不会将 C 添加到引用的程序集列表中。 程序集 C 必须在 gac 中或与活动 B 位于同一目录中在独立情况下，程序集必须位于 GAC 中或 VS 的 Probe 路径。 只有在那时，您可以拖动和删除工作流设计器图面上的活动。  
  
 **工具箱**设置默认情况下保存为用户选项，因此，当你下次打开的时**工具箱**，它将显示自定义工作流活动的列表。 这一个副作用是，如果已添加到将特定域项**工具箱**通过**选择工具箱项**对话框中，你仍能看见那些项时使用的工作流控制台应用程序。 如果您不想要看到它们，然后使用上下文菜单删除它们或通过取消选中**选择工具箱项**对话框按前面所述。  
  
 此对话框中的列包含以下信息：  
  
 名称  
 列出当前已在您的本地计算机上注册的工作流活动的名称。  
  
 命名空间  
 显示定义活动结构的 .NET Framework 类库命名空间的层次结构。  
  
 程序集名称  
 显示包含活动的 .NET Framework 程序集的名称和版本。  
  
 目录  
 显示包含工作流活动的 .NET Framework 程序集的位置。 所有程序集的默认位置是全局程序集缓存。  
  
 若要对所列组件排序，请选择任意列标题。