---
title: 使命令可用 |微软文档
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2d64df85516e0a1ac326f8d40558755718c4644c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707324"
---
# <a name="making-commands-available"></a>使命令可用

当将多个 VS 包添加到 Visual Studio 时，用户界面 （UI） 可能会因命令而变得拥挤不堪。 您可以对包进行编程以帮助减少此问题，如下所示：

- 对包进行编程，使其仅在用户需要时加载。

- 对包进行编程，以便仅当在集成开发环境 （IDE） 的当前状态上下文中可能需要命令时才显示其命令。

## <a name="delayed-loading"></a>延迟加载

启用延迟加载的典型方法是设计 VSPackage，以便其命令显示在 UI 中，但在用户单击其中一个命令之前不会加载包本身。 为此，在 .vsct 文件中，创建没有命令标志的命令。

下面的示例显示了 .vsct 文件中菜单命令的定义。 这是选择模板中的**菜单命令**选项时由可视化工作室包模板生成的命令。

```xml
<Button guid="guidTopLevelMenuCmdSet" id="cmdidTestCommand" priority="0x0100" type="Button">
  <Parent guid="guidTopLevelMenuCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <Strings>
    <CommandName>cmdidTestCommand</CommandName>
    <ButtonText>Test Command</ButtonText>
  </Strings>
</Button>
```

在此示例中，如果父组`MyMenuGroup`（'a） 是顶级菜单（如 **"工具"** 菜单）的子级，则该命令将可见该菜单，但在用户单击该命令之前，不会加载执行该命令的包。 但是，通过编程命令来实现<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，可以在首次展开包含该命令的菜单时启用加载包。

请注意，延迟加载还可以提高启动性能。

## <a name="current-context-and-the-visibility-of-commands"></a>当前上下文和命令的可见性

您可以根据 VSPackage 数据的当前状态或当前相关的操作将 VSPackage 命令编程为可见或隐藏。 您可以使 VSPackage 能够设置其命令的状态，通常使用<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A><xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口中的方法的实现，但这需要加载 VSPackage 才能执行代码。 相反，我们建议您使 IDE 能够在不加载包的情况下管理命令的可见性。 为此，在 .vsct 文件中，将命令与一个或多个特殊 UI 上下文相关联。 这些 UI 上下文由称为*命令上下文 GUID*的 GUID 标识。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]监视用户操作（如加载项目或从编辑到生成）产生的更改。 当发生更改时，将自动修改 IDE 的外观。 下表显示了[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]监视的 IDE 更改的四个主要上下文。

| 上下文类型 | 描述 |
|-------------------------| - |
| 活动项目类型 | 对于大多数项目类型，此值`GUID`与实现项目的 VSPackage 的 GUID 相同。 但是，[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目使用项目类型`GUID`作为值。 |
| 活动窗口 | 通常，这是为密钥绑定建立当前 UI 上下文的最后一个活动文档窗口。 但是，它也可以是一个工具窗口，具有类似于内部 Web 浏览器的密钥绑定表。 对于多选项卡文档窗口（如 HTML 编辑器），每个选项卡都具有不同的命令上下文`GUID`。 |
| 活动语言服务 | 与当前显示在文本编辑器中的文件关联的语言服务。 |
| 活动工具窗口 | 打开且具有焦点的工具窗口。 |

第五个主要上下文区域是 IDE 的 UI 状态。 UI 上下文由活动命令上下文`GUID`标识，如下所示：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionBuilding_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Debugging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.Dragging_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.FullScreenMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.DesignMode_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.NoSolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionExists_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.CodeWindow_guid>

这些 GUID 标记为活动或非活动，具体取决于 IDE 的当前状态。 多个 UI 上下文可以同时处于活动状态。

### <a name="hide-and-display-commands-based-on-context"></a>基于上下文隐藏和显示命令

您可以在 IDE 中显示或隐藏包命令，而无需加载包本身。 为此，`DefaultDisabled`请使用 、`DefaultInvisible`和`DynamicVisibility`命令标志，并将一个或多个[可见性项目](../../extensibility/visibilityitem-element.md)元素添加到["可见性约束"](../../extensibility/visibilityconstraints-element.md)部分，从而定义包的 .vsct 文件中的命令。 当指定的命令上下文`GUID`变为活动时，将显示该命令而不加载包。

### <a name="custom-context-guids"></a>自定义上下文 GUID

如果尚未定义适当的命令上下文 GUID，则可以在 VSPackage 中定义一个，然后根据需要将其编程为活动或非活动，以控制命令的可见性。 使用该服务<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>：

- 注册上下文 GUID（通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>方法）。

- 获取上下文`GUID`的状态（通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法）。

- 打开和关闭上下文`GUID`（通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>方法）。

    > [!CAUTION]
    > 请确保您的 VS 包不会影响任何现有上下文 GUID 的状态，因为其他 VS 包可能依赖于它们。

## <a name="example"></a>示例

下面的 VSPackage 命令示例演示了由命令上下文管理而不加载 VSPackage 的命令的动态可见性。

命令设置为在存在解决方案时启用和显示;即，每当以下命令上下文之一处于活动状态时：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

在此示例中，请注意每个命令标志都是单独的[命令标志](../../extensibility/command-flag-element.md)元素。

```xml
<Button guid="guidDynamicVisibilityCmdSet" id="cmdidMyCommand"
        priority="0x0100" type="Button">
  <Parent guid="guidDynamicVisibilityCmdSet" id="MyMenuGroup" />
  <Icon guid="guidImages" id="bmpPic1" />
  <CommandFlag>DefaultDisabled</CommandFlag>
  <CommandFlag>DefaultInvisible</CommandFlag>
  <CommandFlag>DynamicVisibility</CommandFlag>
  <Strings>
    <CommandName>cmdidMyCommand</CommandName>
    <ButtonText>My Command name</ButtonText>
  </Strings>
</Button>
```

另请注意，每个 UI 上下文都必须在单独的`VisibilityItem`元素中提供，如下所示。

```xml
<VisibilityConstraints>
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_EmptySolution" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                      id="cmdidMyCommand" context="UICONTEXT_SolutionHasSingleProject" />
  <VisibilityItem guid="guidDynamicVisibilityCmdSet"
                  id="cmdidMyCommand" context="UICONTEXT_SolutionHasMultipleProjects" />
</VisibilityConstraints>
```

## <a name="see-also"></a>请参阅

- [向解决方案资源管理器工具栏添加命令](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)
- [动态添加菜单项](../../extensibility/dynamically-adding-menu-items.md)
