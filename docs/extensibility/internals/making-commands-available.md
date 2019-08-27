---
title: 使命令可 |Microsoft Docs
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
ms.openlocfilehash: 0273c95655614cb5ef4ee3bbddcc9307a9a0084d
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66328644"
---
# <a name="making-commands-available"></a>使命令可

当多个 Vspackage 添加到 Visual Studio 中时，用户界面 (UI) 可能会变得 overcrowded 命令。 您可以编写您的程序包以帮助减少此问题，请按如下所示：

- 计划包，以便仅当用户加载需要它。

- 编程包，以便仅在它们可能需要在集成的开发环境 (IDE) 的当前状态的上下文中时显示其命令。

## <a name="delayed-loading"></a>延迟加载

若要启用的典型方法延迟加载是设计 VSPackage，使其命令显示在 UI 中，但直到用户单击其中一个命令不会加载包本身。 若要为此，在.vsct 文件中，创建不具有任何命令标志的命令。

下面的示例演示.vsct 文件中的菜单命令的定义。 这是由 Visual Studio 包模板生成的命令时**菜单命令**选择模板中的选项。

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

在示例中，如果父组中， `MyMenuGroup`，如是顶级菜单的子级**工具**菜单中，该命令将显示在该菜单上，但将不加载的包的执行的命令，直到单击该命令由用户。 但是，通过编程来实现命令<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，可以使包可以首先展开包含该命令的菜单时加载。

请注意，延迟的加载也可能会提高启动性能。

## <a name="current-context-and-the-visibility-of-commands"></a>当前上下文和命令的可见性

您可以编写 VSPackage 命令为可见或隐藏的具体取决于 VSPackage 数据或执行当前最相关的操作的当前状态。 可以使 VSPackage 可以设置其命令的状态通常通过使用实现<xref:EnvDTE.IDTCommandTarget.QueryStatus%2A>方法从<xref:Microsoft.VisualStudio.OLE.Interop.IOleCommandTarget>接口，但这需要在执行代码之前要加载的 VSPackage。 相反，我们建议你启用 IDE 管理命令的可见性，但不加载包。 为此，请在.vsct 文件中，将与一个或多个特殊的 UI 上下文相关联的命令。 由名为 GUID 标识这些 UI 上下文*命令上下文 GUID*。

[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] 监视而导致的用户操作，例如加载项目或编辑转到生成的更改。 发生更改时，会自动修改 IDE 的外观。 下表显示了四种主要上下文的 IDE 更改[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]监视器。

| 上下文的类型 | 描述 |
|-------------------------| - |
| 活动项目类型 | 对于大多数项目类型，这`GUID`值并作为 VSPackage 实现项目的 GUID 相同。 但是，[!INCLUDE[vcprvc](../../code-quality/includes/vcprvc_md.md)]项目使用的项目类型`GUID`作为值。 |
| 活动窗口 | 通常情况下，这是建立键绑定的当前 UI 上下文的最后一个活动文档窗口。 但是，它也可能是一个工具窗口，有一个类似于内部 Web 浏览器的键绑定表。 对于多选项卡式文档窗口，如 HTML 编辑器，每个选项卡都有一个不同的命令上下文`GUID`。 |
| 活动的语言服务 | 与当前显示在文本编辑器中的文件相关联的语言服务。 |
| 活动工具窗口 | 工具窗口处于打开状态且具有焦点。 |

第五个主要的上下文区域是在 IDE 的 UI 状态。 由活动命令上下文标识 UI 上下文`GUID`s，按如下所示：

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

这些 Guid 将标记为活动或非活动状态，具体取决于 IDE 的当前状态。 多个 UI 上下文可以同时处于活动状态。

### <a name="hide-and-display-commands-based-on-context"></a>隐藏和显示基于上下文的命令

可以显示或隐藏在 IDE 中的包命令而不加载包本身。 若要执行此操作，该命令在.vsct 文件中的包使用定义`DefaultDisabled`， `DefaultInvisible`，并`DynamicVisibility`命令标志并添加一个或多个[VisibilityItem](../../extensibility/visibilityitem-element.md)元素[VisibilityConstraints](../../extensibility/visibilityconstraints-element.md)部分。 当指定的命令上下文`GUID`将成为活动状态，该命令将显示而不加载包。

### <a name="custom-context-guids"></a>自定义上下文 Guid

如果尚未定义 GUID 不适当的命令上下文中，可以定义一个在你的 VSPackage 中，然后编写它是活动或非活动所需控制命令的可见性。 使用<xref:Microsoft.VisualStudio.Shell.Interop.SVsShellMonitorSelection>到服务：

- 注册上下文 Guid (通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.GetCmdUIContextCookie%2A>方法)。

- 获取上下文的状态`GUID`(通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.IsCmdUIContextActive%2A>方法)。

- 打开上下文`GUID`s 打开和关闭 (通过调用<xref:Microsoft.VisualStudio.Shell.Interop.IVsMonitorSelection.SetCmdUIContext%2A>方法)。

    > [!CAUTION]
    > 请确保你的 VSPackage 不因为其他 Vspackage 可能依赖于这些影响任何现有上下文 GUID 的状态。

## <a name="example"></a>示例

VSPackage 命令的下面的示例演示由命令上下文而不加载 VSPackage 的命令的动态可见性。

该命令设置为处于启用状态并显示时存在的解决方案;也就是说，每当将以下命令上下文 Guid 之一处于活动状态：

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.EmptySolution_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasMultipleProjects_guid>

- <xref:Microsoft.VisualStudio.VSConstants.UICONTEXT.SolutionHasSingleProject_guid>

在示例中，请注意，每个命令标志是单独[命令标志](../../extensibility/command-flag-element.md)元素。

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

此外请注意，必须在单独指定每个 UI 上下文`VisibilityItem`元素，按如下所示。

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
- [MenuCommands 与OleMenuCommands](../../extensibility/menucommands-vs-olemenucommands.md)
- [VSPackage 如何添加用户界面元素](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VSPackage 中的命令传送](../../extensibility/internals/command-routing-in-vspackages.md)
- [动态添加菜单项](../../extensibility/dynamically-adding-menu-items.md)
