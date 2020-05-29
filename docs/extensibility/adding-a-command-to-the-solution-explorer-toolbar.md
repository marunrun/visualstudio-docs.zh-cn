---
title: 将命令添加到解决方案资源管理器工具栏 |Microsoft Docs
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
ms.openlocfilehash: fbb84dd8c8a8240e4fec7791305029304ccce8f7
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2020
ms.locfileid: "84183725"
---
# <a name="add-a-command-to-the-solution-explorer-toolbar"></a>将命令添加到解决方案资源管理器工具栏
本演练演示如何将按钮添加到**解决方案资源管理器**工具栏中。

 工具栏或菜单上的任何命令均称为 Visual Studio 中的按钮。 单击该按钮时，将执行命令处理程序中的代码。 通常，相关命令组合在一起形成一个组。 菜单或工具栏充当组的容器。 优先级确定组中的单个命令在菜单或工具栏上出现的顺序。 您可以通过控制按钮的可见性来阻止工具栏或菜单上的按钮显示。 在 .vsct 文件的部分中列出的命令 `<VisibilityConstraints>` 仅 *.vsct*显示在关联的上下文中。 可见性不能应用于组。

 有关菜单、工具栏命令和 *.vsct*文件的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

> [!NOTE]
> 使用 XML 命令表（*. .vsct*）文件而不是命令表配置（*.ctc*）文件来定义菜单和命令在你的 vspackage 中的显示方式。 有关详细信息，请参阅[Visual Studio 命令表（。.Vsct）文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-menu-command"></a>使用菜单命令创建扩展
 创建一个名为的 VSIX 项目 `SolutionToolbar` 。 添加一个名为**ToolbarButton**的菜单命令项模板。 有关如何执行此操作的信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="add-a-button-to-the-solution-explorer-toolbar"></a>将按钮添加到解决方案资源管理器工具栏
 本演练的此部分演示如何将按钮添加到**解决方案资源管理器**工具栏中。 单击该按钮时，将运行回调方法中的代码。

1. 在*ToolbarButtonPackage. .vsct*文件中，请参阅 `<Symbols>` 部分。 `<GuidSymbol>`节点包含由包模板生成的菜单组和命令。 向 `<IDSymbol>` 此节点添加一个元素，以声明将保存命令的组。

    ```xml
    <IDSymbol name="SolutionToolbarGroup" value="0x0190"/>
    ```

2. 在 `<Groups>` 部分中，在 "现有组" 项之后，定义你在上一步中声明的新组。

    ```xml
    <Group guid="guidToolbarButtonPackageCmdSet"
           id="SolutionToolbarGroup" priority="0xF000">
            <Parent guid="guidSHLMainMenu" id="IDM_VS_TOOL_PROJWIN"/>
          </Group>
    ```

     将父 GUID： ID 对设置为， `guidSHLMainMenu` 并将 `IDM_VS_TOOL_PROJWIN` 此组放在**解决方案资源管理器**工具栏上，并设置高优先级值，将其放在其他命令组之后。

3. 在 `<Buttons>` 部分中，更改所生成条目的父 ID， `<Button>` 以反映你在上一步中定义的组。 修改后的 `<Button>` 元素应如下所示：

    ```xml
    <Button guid="guidToolbarButtonPackageCmdSet" id="ToolbarButtonId" priority="0x0100" type="Button">
        <Parent guid="guidToolbarButtonPackageCmdSet" id="SolutionToolbarGroup" />
        <Icon guid="guidImages" id="bmpPicStrikethrough" />
        <Strings>
            <ButtonText>Invoke ToolbarButton</ButtonText>
        </Strings>
    </Button>
    ```

4. 生成项目并启动调试。 将显示实验实例。

     **解决方案资源管理器**工具栏应在现有按钮右侧显示 "新建命令" 按钮。 按钮图标是删除线。

5. 单击 "新建" 按钮。

     应显示一个对话框，其中包含在**SolutionToolbar 中 ToolbarButtonPackage**的消息 "ToolbarButton"。

## <a name="control-the-visibility-of-a-button"></a>控制按钮的可见性
 本演练的此部分演示如何控制工具栏上的按钮的可见性。 通过将上下文设置为 `<VisibilityConstraints>` *SolutionToolbar. .vsct*文件的节中的一个或多个项目，可将按钮限制为仅在项目打开时才显示。

### <a name="to-display-a-button-when-one-or-more-projects-are-open"></a>打开一个或多个项目时显示按钮

1. 在 `<Buttons>` *ToolbarButtonPackage*的节中，将两个命令标志添加到现有元素中 `<Button>` 的 `<Strings>` 和标记之间 `<Icons>` 。

   ```xml
   <CommandFlag>DefaultInvisible</CommandFlag>
   <CommandFlag>DynamicVisibility</CommandFlag>
   ```

    `DefaultInvisible` `DynamicVisibility` 必须设置和标志，以便部分中的项 `<VisibilityConstraints>` 可以生效。

2. 创建 `<VisibilityConstraints>` 包含两个条目的部分 `<VisibilityItem>` 。 将新部分置于结束 `</Commands>` 标记之后。

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

    每个可见性项表示在其下显示指定按钮的条件。 若要应用多个条件，必须为同一按钮创建多个条目。

3. 生成项目并启动调试。 将显示实验实例。

    **解决方案资源管理器**工具栏不包含删除线按钮。

4. 打开包含项目的任何解决方案。

    删除线按钮显示在工具栏上的 "现有" 按钮右侧。

5. 在 **“文件”** 菜单上，单击 **“关闭解决方案”**。 该按钮将从工具栏中消失。

   在加载 VSPackage 之前，按钮的可见性受控制 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 加载 VSPackage 后，该按钮的可见性由 VSPackage 控制。  有关详细信息，请参阅[menucommand 与 OleMenuCommands](/visualstudio/misc/menucommands-vs-olemenucommands?view=vs-2015)。

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
