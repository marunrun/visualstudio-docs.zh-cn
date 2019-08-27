---
title: 如何：实现嵌套的项目 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 427ef425c64323246ffe1141d081fd7d921506a6
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63435241"
---
# <a name="how-to-implement-nested-projects"></a>如何：实现嵌套项目
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

您创建的嵌套的项目类型时，必须实现几个附加步骤。 父项目需要某些解决方案包含它的嵌套 （子） 项目相同的职责。 父项目是类似于一种解决方案的项目的容器。 具体而言，有几个必须由该解决方案和要生成嵌套项目的层次结构的父项目引发的事件。 创建嵌套的项目的以下过程描述了这些事件。  
  
### <a name="to-create-nested-projects"></a>若要创建嵌套的项目  
  
1. 集成的开发环境 (IDE) 加载父项目的项目文件和启动信息通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>接口。 创建父项目并将其添加到解决方案。  
  
   > [!NOTE]
   > 此时，它是太早，父项目来创建嵌套的项目，因为必须创建父项目，然后才能创建子项目的过程中。 遵循此序列中，父项目可以将设置应用于子项目和子项目可以根据需要获取父项目中的信息。 此序列是如果它由源代码管理 (SCC) 和解决方案资源管理器等的客户端上所需。  
  
    父项目必须等待<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>项目，它可以创建其嵌套 （子） 之前由 IDE 调用的方法。  
  
2. IDE 调用`QueryInterface`上的父项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject>。 如果此调用成功，IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>方法要打开的所有嵌套项目的父项目的父级。  
  
3. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A>即将创建方法以通知嵌套项目的侦听器。 SCC，例如，侦听这些事件，以知道是否在顺序中发生的解决方案和项目创建过程中的步骤。 如果不按顺序执行步骤，解决方案可能不是与源代码管理正确注册。  
  
4. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A>方法或<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A>及其子项目的每个方法。  
  
    您传递<xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS>到`AddVirtualProject`方法，以指示应将虚拟 （嵌套） 的项目添加到项目窗口中，从生成中排除添加到源代码管理中，依次类推。 `VSADDVPFLAGS` 允许您控制的可见性嵌套的项目，并指示哪些功能是与之相关联。  
  
    如果你重新加载以前存在的子项目包含项目 GUID 存储在父项目的项目文件中，父项目调用`AddVirtualProjectEx`。 之间的唯一区别`AddVirtualProject`和`AddVirtualProjectEX`在于`AddVirtualProjectEX`具有一个参数，使父项目，以指定每个实例`guidProjectID`的子项目，以使<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A>函数正确。  
  
    如果没有 GUID，例如当您添加新的嵌套的项目，该解决方案将创建一个项目时将其添加到父。 它负责的父项目以保存该项目在其项目文件中的 GUID。 如果你删除嵌套的项目，还可以删除该项目的 GUID。  
  
5. IDE 调用`M:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren`父项目的每个子项目的方法。  
  
    父项目必须实现`IVsParentProject`如果你想要将嵌套的项目。 但项目永远不会调用的父级`QueryInterface`为`IVsParentProject`即使它具有其下的父项目。 该解决方案处理在调用`IVsParentProject`并实现它后，如果调用`OpenChildren`创建嵌套的项目。 `AddVirtualProjectEX` 始终从调用`OpenChildren`。 它永远不应由父项目保留在层次结构创建事件的顺序调用。  
  
6. IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>子项目的方法。  
  
7. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A>方法以通知侦听器已创建了父级的子项目。  
  
8. IDE 调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A>父项目之后已打开所有子项目的方法。  
  
    如果已存在，父项目通过调用创建的每个嵌套的项目 GUID `CoCreateGuid`。  
  
   > [!NOTE]
   > `CoCreateGuid` 若要创建一个 GUID 时调用 COM API。 有关详细信息，请参阅`CoCreateGuid`和 MSDN Library 中的 Guid。  
  
    父项目将此 GUID 存储在要从中检索下一次在 IDE 中打开其项目文件中。 请参阅有关的调用与相关的详细信息的步骤 4`AddVirtualProjectEX`来检索`guidProjectID`子项目。  
  
9. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>父 ItemID 然后调用方法，按照约定，委托中到嵌套的项目。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>检索嵌套了你想要调用父项上时委托中的项目节点的属性。  
  
     由于以编程方式实例化父和子项目，可以在这里设置嵌套项目的属性。  
  
    > [!NOTE]
    > 不仅能执行将收到的上下文信息从嵌套的项目，但您还可以要求父项目是否为该项的任何上下文通过检查<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID>。 这种方式，可以向嵌套的各个项目中添加额外的动态帮助属性和特定的菜单选项。  
  
10. 在层次结构生成显示在解决方案资源管理器通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>方法。  
  
     将层次结构传递给环境中，通过`GetNestedHierarchy`生成在解决方案资源管理器中显示的层次结构。 在这种方式，该解决方案知道项目存在，并且可以用于生成托管的生成管理器，或可以允许将受源代码管理项目中的文件。  
  
11. 在创建项目 1 的所有嵌套的项目了，控制权传递回解决方案并且为 Project2 重复此过程。  
  
     创建嵌套的项目的这一过程发生具有子级的子项目。 在这种情况下，如果 BuildProject1，是 Project1 的子级，具有子项目，则会创建之后 BuildProject1 和之前 Project2。 过程是递归的并在层次结构生成从顶部向下。  
  
     因为用户关闭解决方案或特定于项目本身，另一种方法在嵌套的项目的关闭时`IVsParentProject`， <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A>，调用。 父项目包装调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A>方法替换<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A>通知解决方案的事件侦听器，正在关闭嵌套的项目的方法。  
  
    以下主题处理多个实现嵌套的项目时要考虑其他概念：  
  
    [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)  
  
    [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)  
  
    [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)  
  
    [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)  
  
## <a name="see-also"></a>请参阅  
 [将项添加到添加新项对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)   
 [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)   
 [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)   
 [上下文参数](../../extensibility/internals/context-parameters.md)   
 [向导 (.Vsz) 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
