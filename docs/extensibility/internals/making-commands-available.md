---
title: 使命令可用 |Microsoft Docs
ms.date: 03/22/2018
ms.topic: conceptual
helpviewer_keywords:
- menus [Visual Studio SDK], commands
- best practices, menu and toolbar commands
- toolbars [Visual Studio], best practices
- menu commands, best practices
ms.assetid: 3ffc4312-c6db-4759-a946-a4bb85f4a17a
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d30d71290c08019acfdc75313516d8b1b1c4be3a
ms.sourcegitcommit: 40bd5b27f247a07c2e2514acb293b23d6ce03c29
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2019
ms.locfileid: "73186355"
---
# <a name="making-commands-available"></a>使命令可用

将多个 Vspackage 添加到 Visual Studio 时，用户界面（UI）可能会 overcrowded 命令。 你可以对包进行编程以帮助减少此问题，如下所示：

- 对包进行编程，使其仅在用户需要时加载。

- 对包进行编程，使其命令仅在集成开发环境（IDE）的当前状态上下文中可能需要时才显示。

## <a name="delayed-loading"></a>延迟加载

启用延迟加载的典型方式是设计 VSPackage，以便在 UI 中显示其命令，但在用户单击其中一个命令之前，不会加载包本身。 若要实现此目的，请在 .vsct 文件中创建没有命令标志的命令。

下面的示例演示如何从 .vsct 文件定义菜单命令。 这是在选择模板中的**菜单命令**选项时由 Visual Studio 包模板生成的命令。

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

在此示例中，如果父组 `MyMenuGroup`是顶级菜单（如 "**工具**" 菜单）的子级，则该命令将在该菜单上可见，但在用户单击该命令之前，将不会加载执行命令的包。 但是，通过对命令进行编程以实现 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口，你可以在第一次展开包含命令的菜单时启用包加载。

请注意，延迟加载还可以提高启动性能。

## <a name="current-context-and-the-visibility-of-commands"></a>当前上下文和命令的可见性

您可以根据 VSPackage 数据的当前状态或当前相关的操作，对 VSPackage 命令进行可见或隐藏。 您可以通过使用 <xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget> 接口中 <xref:EnvDTE.IDTCommandTarget.QueryStatus%2A> 方法的实现来使 VSPackage 设置其命令的状态，但这需要先加载 VSPackage，然后才能执行该代码。 相反，我们建议您让 IDE 在不加载包的情况下管理命令的可见性。 为此，请在 .vsct 文件中将命令与一个或多个特殊 UI 上下文相关联。 这些 UI 上下文由 GUID 标识，该 GUID 称为 "*命令上下文 guid*"。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 监视用户操作（例如加载项目或从编辑到生成）所产生的更改。 发生更改时，IDE 的外观会自动修改。 下表显示 [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 监视器的四个主要的 IDE 更改上下文。

| 上下文类型 | 描述 |
|-------------------------| - |
| 活动项目类型 | 对于大多数项目类型，此 `GUID` 值与实现项目的 VSPackage 的 GUID 相同。 但 [!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)] 项目使用项目类型 `GUID` 作为值。 |
| 活动窗口 | 通常，这是为键绑定建立当前 UI 上下文的最后一个活动文档窗口。 不过，它也可以是具有类似于内部 Web 浏览器的键绑定表的工具窗口。 对于多选项卡式文档窗口（如 HTML 编辑器），每个选项卡都有不同的命令上下文 `GUID`。 |
| 活动语言服务 | 与当前在文本编辑器中显示的文件关联的语言服务。 |
| 活动工具窗口 | 打开并具有焦点的工具窗口。 |

第五个主要的上下文区域是 IDE 的 UI 状态。 UI 上下文由 active command context `GUID`s 标识，如下所示：

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

这些 Guid 标记为活动或非活动状态，具体取决于 IDE 的当前状态。 多个 UI 上下文可以同时处于活动状态。

### <a name="hide-and-display-commands-based-on-context"></a>基于上下文隐藏和显示命令

可以在 IDE 中显示或隐藏包命令，而无需加载包本身。 为此，请使用 `DefaultDisabled`、`DefaultInvisible`和 `DynamicVisibility` 命令标志在包的 .vsct 文件中定义该命令，并将一个或多个[VisibilityItem](../../extensibility/visibilityitem-element.md)元素添加到[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)节。 当指定的命令上下文 `GUID` 变为活动状态时，将显示该命令而不加载包。

### <a name="custom-context-guids"></a>自定义上下文 Guid

如果尚未定义适当的命令上下文 GUID，则可在 VSPackage 中定义一个，然后根据需要对其进行编程，使其保持活动或非活动状态，以控制命令的可见性。 使用 <xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection> 服务可以：

- 注册上下文 Guid （通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A> 方法）。

- 获取上下文 `GUID` 的状态（通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A> 方法）。

- 打开和关闭上下文 `GUID`（通过调用 <xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A> 方法）。

    > [!CAUTION]
    > 请确保 VSPackage 不会影响任何现有的上下文 GUID 的状态，因为其他 Vspackage 可能依赖于它们。

## <a name="example"></a>示例

下面的 VSPackage 命令示例演示了命令上下文管理的命令的动态可见性，而无需加载 VSPackage。

如果解决方案存在，则将此命令设置为启用并显示。也就是说，每当以下命令上下文 Guid 之一处于活动状态时：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

在此示例中，请注意，每个命令标志都是单独的[命令标志](../../extensibility/command-flag-element.md)元素。

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

另请注意，每个 UI 上下文都必须在单独的 `VisibilityItem` 元素中提供，如下所示。

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

- [将命令添加到解决方案资源管理器工具栏](../../extensibility/adding-a-command-to-the-solution-explorer-toolbar.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)
- [动态添加菜单项](../../extensibility/dynamically-adding-menu-items.md)
