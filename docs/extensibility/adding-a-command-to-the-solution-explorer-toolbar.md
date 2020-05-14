---
title: 向解决方案资源管理器工具栏添加命令 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding buttons
- buttons [Visual Studio], adding to Solution Explorer
- Solution Explorer, adding buttons
ms.assetid: f6411557-2f4b-4e9f-b02e-fce12a6ac7e9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44a14d87fbb5754d7af35d3add9e438351877a49
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740336"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>向解决方案资源管理器工具栏添加命令
本演练演示如何向**解决方案资源管理器**工具栏添加按钮。

 工具栏或菜单上的任何命令都称为 Visual Studio 中的按钮。 单击该按钮时，将执行命令处理程序中的代码。 通常，相关命令被分组到一个组。 菜单或工具栏充当组的容器。 优先级确定组中单个命令在菜单或工具栏上显示的顺序。 您可以通过控制按钮的可见性来防止按钮显示在工具栏或菜单上。 在 *.vsct*文件`<VisibilityConstraints>`部分中列出的命令仅在关联的上下文中显示。 可见性不能应用于组。

 有关菜单、工具栏命令和 *.vsct*文件的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

> [!NOTE]
> 使用 XML 命令表 *（.vsct*） 文件而不是命令表配置 *（.ctc*） 文件来定义菜单和命令在 VS 包中的显示方式。 有关详细信息，请参阅[可视化工作室命令表 （。Vsct） 文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展
 创建名为 的`SolutionToolbar`VSIX 项目。 添加名为**工具栏按钮**的菜单命令项模板。 有关如何执行此操作的信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>向解决方案资源管理器工具栏添加按钮
 本演练的这一部分演示如何向**解决方案资源管理器**工具栏添加按钮。 单击该按钮时，将运行回调方法中的代码。

1. 在*工具栏Button包.vsct*文件中，转到该`<Symbols>`部分。 该`<GuidSymbol>`节点包含包模板生成的菜单组和命令。 向此`<IDSymbol>`节点添加一个元素，以声明将保存命令的组。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. 在"`<Groups>`部分中，在现有组条目之后，定义您在上一步中声明的新组。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     将父 GUID：ID 对`guidSHLMainMenu`设置为`IDM_VS_TOOL_PROJWIN`并将此组放在**解决方案资源管理器**工具栏上，并设置高优先级值将其置于其他命令组之后。

3. 在本节`<Buttons>`中，更改生成的`<Button>`条目的父 ID 以反映您在上一步中定义的组。 修改后的`<Button>`元素应如下所示：

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. 生成项目并启动调试。 出现实验实例。

     **解决方案资源管理器**工具栏应在现有按钮的右侧显示新的命令按钮。 按钮图标是击穿。

5. 单击新按钮。

     应显示一个对话框，其中包含消息工具栏**按钮包（解决方案工具栏.工具栏.MenuItem 回调）。**

## <a name="control-the-visibility-of-a-button"></a>控制按钮的可见性
 演练的这一部分演示如何控制工具栏上按钮的可见性。 通过在`<VisibilityConstraints>`*解决方案工具栏.vsct*文件部分中设置上下文到一个或多个项目，可以将按钮限制为仅在项目或项目打开时显示。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>打开一个或多个项目时显示按钮

1. 在`<Buttons>`*工具栏ButtonPackage.vsct*部分中，在`<Button>``<Strings>`和`<Icons>`标记之间向现有元素添加两个命令标志。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    必须`DefaultInvisible`设置`DynamicVisibility`和 标志，以便节中的`<VisibilityConstraints>`条目可以生效。

2. 创建包含`<VisibilityConstraints>`两`<VisibilityItem>`个条目的节。 将新部分放在结束`</Commands>`标记之后。

   ```xml
   <VisibilityConstraints>
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasSingleProject" />
       <VisibilityItem guid="guidToolbarButtonPackageCmdSet"
             id="ToolbarButtonId"
             context="UICONTEXT_SolutionHasMultipleProjects" />
   </VisibilityConstraints>
   ```

    每个可见性项表示显示指定按钮的条件。 要应用多个条件，必须为同一按钮创建多个条目。

3. 生成项目并启动调试。 出现实验实例。

    **解决方案资源管理器**工具栏不包含打击按钮。

4. 打开包含项目的任何解决方案。

    打击按钮将显示在现有按钮右侧的工具栏上。

5. 在 **“文件”** 菜单上，单击 **“关闭解决方案”**。 该按钮从工具栏中消失。

   按钮的可见性由控制[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]，直到加载 VSPackage。 加载 VSPackage 后，按钮的可见性由 VSPackage 控制。  有关详细信息，请参阅[菜单命令与 OleMenu 命令](/visualstudio/extensibility/menucommands-vs-olemenucommands?view=vs-2015)。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
