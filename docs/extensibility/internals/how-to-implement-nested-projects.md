---
title: 如何：实现嵌套项目 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3b1ac3c147962b943499172435c3f601115d36a9
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905355"
---
# <a name="how-to-implement-nested-projects"></a>如何：实现嵌套项目

创建嵌套项目类型时，还必须实现几个附加步骤。 父项目采用解决方案对其嵌套（子）项目具有的一些相同责任。 父项目是类似于解决方案的项目的容器。 具体而言，解决方案和父项目必须引发若干事件，才能生成嵌套项目的层次结构。 以下创建嵌套项目的过程中介绍了这些事件。

## <a name="create-nested-projects"></a>创建嵌套项目

1. 集成开发环境（IDE）通过调用接口加载父项目的项目文件和启动信息 <xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory> 。 将创建父项目并将其添加到解决方案中。

    > [!NOTE]
    > 此时，它在父项目创建嵌套项目的过程中过于早，因为必须先创建父项目，然后才能创建子项目。 按照此顺序，父项目可以将设置应用于子项目，子项目可以根据需要从父项目获取信息。 此顺序是客户端（如源代码管理（SCC）和**解决方案资源管理器**）需要此序列。

     父项目必须等待 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> IDE 调用方法，然后才能创建其嵌套（子）项目或项目。

2. IDE 对 `QueryInterface` 的父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject> 。 如果此调用成功，IDE 将调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A> 父类的方法来打开父项目的所有嵌套项目。

3. 父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A> 方法，以通知侦听器将要创建的嵌套项目。 例如，SCC 正在侦听这些事件，以了解解决方案和项目创建过程中的步骤是否按顺序发生。 如果步骤顺序不正确，则解决方案可能不会正确地注册到源代码管理中。

4. 父项目对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A> 其每个子项目调用方法或方法。

     传递 <xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS> 给方法， `AddVirtualProject` 以指示应将虚拟（嵌套）项目添加到项目窗口中，从生成中排除，并将其添加到源代码管理中，等等。 `VSADDVPFLAGS`允许您控制嵌套项目的可见性，并指示与之相关联的功能。

     如果重新加载一个以前存在的子项目，该项目的项目 GUID 存储在父项目的项目文件中，则父项目会调用 `AddVirtualProjectEx` 。 和之间唯一的区别在于 `AddVirtualProject` `AddVirtualProjectEX` ， `AddVirtualProjectEX` 有一个参数，该参数允许父项目为子项目指定每个实例， `guidProjectID` 以使其能够 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A> 正常工作。

     如果没有可用的 GUID （如添加新的嵌套项目时），解决方案会在将项目添加到父级时为其创建一个。 父项目负责在其项目文件中持久保存该项目 GUID。 如果删除嵌套项目，则还可以删除该项目的 GUID。

5. IDE 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren> 父项目的每个子项目调用方法。

     如果要嵌套项目，则父项目必须实现 `IVsParentProject` 。 但父项目永远不会调用 `QueryInterface` ， `IVsParentProject` 即使它位于其下的父项目。 解决方案处理对的调用 `IVsParentProject` ，如果实现，则调用 `OpenChildren` 以创建嵌套项目。 `AddVirtualProjectEX`始终从调用 `OpenChildren` 。 父项目永远不应调用它来保持层次结构创建事件的顺序。

6. IDE 对 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A> 子项目调用方法。

7. 父项目调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A> 方法，以通知侦听器已创建父对象的子项目。

8. <xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A>打开所有子项目后，IDE 将对父项目调用方法。

     如果它尚不存在，则父项目通过调用为每个嵌套项目创建一个 GUID `CoCreateGuid` 。

    > [!NOTE]
    > `CoCreateGuid`是要创建 GUID 时调用的 COM API。 有关详细信息，请参阅 `CoCreateGuid` MSDN Library 中的和 guid。

     父项目将此 GUID 存储在它的项目文件中，以便在下一次在 IDE 中打开它时进行检索。 请参阅步骤4，以获取与调用 `AddVirtualProjectEX` 以检索子项目的相关的详细信息 `guidProjectID` 。

9. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>然后为父 ItemID 调用方法，按约定将委托到嵌套项目。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>检索一个节点的属性，该节点嵌套在父项上调用的项目。

     由于父项目和子项目以编程方式实例化，因此，此时可以设置嵌套项目的属性。

    > [!NOTE]
    > 您不仅从嵌套项目接收上下文信息，还可以通过检查 __VSHPROPID 来询问父项目是否具有该项目的上下文[。VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>)。 通过这种方式，可以添加特定于单个嵌套项目的额外的动态帮助属性和菜单选项。

10. 该层次结构是使用对方法的调用在**解决方案资源管理器**中显示而生成的 <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A> 。

     您可以通过将层次结构传递到环境， `GetNestedHierarchy` 以生成在解决方案资源管理器中显示的层次结构。 通过这种方式，解决方案知道项目存在并可由生成管理器进行管理，或者允许将项目中的文件置于源代码管理下。

11. 如果已创建 Project1 的所有嵌套项目，则会将控制传递回解决方案，并为 Project2 重复此过程。

     对于具有子项目的子项目，创建嵌套项目的过程是相同的。 在这种情况下，如果 BuildProject1 是 Project1 的子项目，则会在 BuildProject1 之后和 Project2 之前创建子项目。 流程是递归的，并从上到下构建了层次结构。

     当由于用户关闭了解决方案或特定项目本身而关闭嵌套项目时，将调用上的其他方法 `IVsParentProject` <xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A> 。 父项目包装对方法的调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A> ，并包装 <xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A> 方法以通知侦听器解决方案事件嵌套项目将关闭。

以下主题介绍了在实现嵌套项目时要考虑的其他一些概念：

- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [实现嵌套项目的命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的 AddItem 对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>另请参阅

- [向 "添加新项" 对话框添加项](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [清单：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导（.vsz）文件](../../extensibility/internals/wizard-dot-vsz-file.md)
