---
title: 如何：实施嵌套项目 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- nested projects, implementing
- projects [Visual Studio SDK], nesting
ms.assetid: d20b8d6a-f0e0-4115-b3a3-edda893ae678
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8d9dfe567db0b8788b93b13aeb760d45f4c05b57
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707975"
---
# <a name="how-to-implement-nested-projects"></a>如何：实现嵌套项目

创建嵌套项目类型时，必须实现几个附加步骤。 父项目承担与解决方案对其嵌套（子）项目承担的一些相同职责。 父项目是类似于解决方案的项目容器。 特别是，有几个事件必须由解决方案和父项目引发，才能生成嵌套项目的层次结构。 这些事件在以下创建嵌套项目的过程中进行了描述。

## <a name="create-nested-projects"></a>创建嵌套项目

1. 集成开发环境 （IDE） 通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsProjectFactory>接口加载父项目的项目文件和启动信息。 父项目将创建并添加到解决方案中。

    > [!NOTE]
    > 此时，父项目创建嵌套项目的过程还为时过早，因为必须先创建父项目，然后才能创建子项目。 遵循此序列，父项目可以将设置应用于子项目，并且子项目可以根据需要从父项目获取信息。 此序列是客户端（如源代码控制 （SCC） 和**解决方案资源管理器**等 需要它。

     父项目必须等待 IDE<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>调用该方法，然后才能创建其嵌套（子）项目或项目。

2. IDE 对`QueryInterface`的父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject>。 如果此调用成功，IDE 将调用父<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren%2A>项的方法以打开父项目的所有嵌套项目。

3. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnBeforeOpeningChildren%2A>方法以通知侦听器即将创建嵌套项目。 例如，SCC 正在侦听这些事件，了解解决方案和项目创建过程中的步骤是否按顺序进行。 如果步骤顺序不正确，则可能无法正确注册源代码管理。

4. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProject%2A>方法或其每个子<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.AddVirtualProjectEx%2A>项目上的方法。

     传递给<xref:Microsoft.VisualStudio.Shell.Interop.__VSADDVPFLAGS>`AddVirtualProject`方法以指示应将虚拟（嵌套）项目添加到项目窗口，从生成中排除，添加到源代码控件，依如此。 `VSADDVPFLAGS`允许您控制嵌套项目的可见性，并指示与其关联的功能。

     如果重新加载以前存在的子项目，该项目 GUID 存储在父项目的项目文件中，则父项目将调用`AddVirtualProjectEx`。 `AddVirtualProject`之间的`AddVirtualProjectEX`唯一区别是，具有`AddVirtualProjectEX`一个参数，使父项目能够为每个实例`guidProjectID`指定一个子项目，以便启用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfGuid%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.GetProjectOfProjref%2A>正常运行。

     如果没有 GUID 可用（例如，当您添加新嵌套项目时）时，解决方案会在项目添加到父项目时为该项目创建一个。 父项目有责任在其项目文件中保留该项目 GUID。 如果删除嵌套项目，也可以删除该项目的 GUID。

5. IDE 调用父<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.OpenChildren>项目的每个子项目上的方法。

     如果要嵌套项目，则必须`IVsParentProject`实现父项目。 但是，父项目即使其`QueryInterface`下方`IVsParentProject`有父项目，也从不调用。 解决方案处理对 的`IVsParentProject`调用，如果实现，则调用`OpenChildren`以创建嵌套项目。 `AddVirtualProjectEX`始终从`OpenChildren`调用 。 父项目绝不应调用它来保持层次结构创建事件的顺序。

6. IDE 调用子<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterOpenProject%2A>项目上的方法。

7. 父项目调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpeningChildren%2A>方法以通知侦听器父项的子项目已创建。

8. 打开所有子项目<xref:Microsoft.VisualStudio.Shell.Interop.IVsFireSolutionEvents.FireOnAfterOpenProject%2A>后，IDE 将调用父项目上的方法。

     如果不存在，父项目通过调用`CoCreateGuid`为每个嵌套项目创建 GUID。

    > [!NOTE]
    > `CoCreateGuid`是在创建 GUID 时调用的 COM API。 有关详细信息，请参阅`CoCreateGuid`MSDN 库中的 GUID。

     父项目将此 GUID 存储在其项目文件中，以便下次在 IDE 中打开时将其检索。 有关调用`AddVirtualProjectEX`检索`guidProjectID`子项目的详细信息，请参阅步骤 4。

9. <xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>然后，将调用父 ItemID，通过约定，将该方法委派给嵌套项目。 检索<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetProperty%2A>嵌套要在父级上调用项目时要委派的项目的节点的属性。

     由于父项目和子项目以编程方式实例化，因此此时可以为嵌套项目设置属性。

    > [!NOTE]
    > 您不仅从嵌套项目中接收上下文信息，还可以通过检查__VSHPROPID来询问父项目是否有任何该项的上下文[。VSHPROPID_UserContext](<xref:Microsoft.VisualStudio.Shell.Interop.__VSHPROPID.VSHPROPID_UserContext>). 通过这种方式，您可以添加特定于单个嵌套项目的额外动态帮助属性和菜单选项。

10. 层次结构是为在**解决方案资源管理器**中显示而构建的，并调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsHierarchy.GetNestedHierarchy%2A>该方法。

     通过将层次结构传递给环境`GetNestedHierarchy`，以生成要在解决方案资源管理器中显示的层次结构。 通过这种方式，解决方案知道项目存在，并且可以由生成管理器进行管理以生成，或者允许将项目中的文件置于源代码控制之下。

11. 创建 Project1 的所有嵌套项目后，控件将传回解决方案，并重复 Project2 的过程。

     对于具有子项的子项目，将发生相同的创建嵌套项目的过程。 在这种情况下，如果作为 Project1 的子项的 BuildProject1 具有子项目，则这些项目将在生成 Project1 之后和 Project2 之前创建。 该过程是递归的，层次结构是从自上而下构建的。

     当嵌套项目由于用户关闭解决方案或特定项目本身而关闭时，将调用 上`IVsParentProject`<xref:Microsoft.VisualStudio.Shell.Interop.IVsParentProject.CloseChildren%2A>的另一种方法。 父项目用<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolution.RemoveVirtualProject%2A><xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnBeforeClosingChildren%2A>和<xref:Microsoft.VisualStudio.Shell.Interop.IVsSolutionEvents3.OnAfterClosingChildren%2A>方法将调用换行，以通知侦听器到解决方案事件，嵌套项目正在关闭。

以下主题涉及实现嵌套项目时要考虑的其他几个概念：

- [卸载和重新加载嵌套项目的注意事项](../../extensibility/internals/considerations-for-unloading-and-reloading-nested-projects.md)
- [对嵌套项目的向导支持](../../extensibility/internals/wizard-support-for-nested-projects.md)
- [为嵌套项目实现命令处理](../../extensibility/internals/implementing-command-handling-for-nested-projects.md)
- [筛选嵌套项目的"添加项目"对话框](../../extensibility/internals/filtering-the-additem-dialog-box-for-nested-projects.md)

## <a name="see-also"></a>请参阅

- [将项目添加到"添加新项目"对话框](../../extensibility/internals/adding-items-to-the-add-new-item-dialog-boxes.md)
- [注册项目和项目模板](../../extensibility/internals/registering-project-and-item-templates.md)
- [检查表：创建新的项目类型](../../extensibility/internals/checklist-creating-new-project-types.md)
- [上下文参数](../../extensibility/internals/context-parameters.md)
- [向导 （.vsz） 文件](../../extensibility/internals/wizard-dot-vsz-file.md)
