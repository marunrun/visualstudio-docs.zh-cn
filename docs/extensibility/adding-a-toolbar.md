---
title: 添加工具栏 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: beb97356daf3c932470bf2598e58e1f5b40ea233
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85904078"
---
# <a name="add-a-toolbar"></a>添加工具栏
本演练演示如何将工具栏添加到 Visual Studio IDE。

 工具栏是包含绑定到命令的按钮的水平或垂直条带。 根据其实现，IDE 中的工具栏可以重新定位、停靠在 IDE 主窗口的任何一侧，或在其他窗口之前。

 此外，用户还可以将命令添加到工具栏中，或通过使用 "**自定义**" 对话框将其删除。 通常，Vspackage 中的工具栏是用户可自定义的。 IDE 处理所有自定义，而 VSPackage 响应命令。 VSPackage 无需知道命令的实际位置。

 有关菜单的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-toolbar"></a>使用工具栏创建扩展
 创建一个名为的 VSIX 项目 `IDEToolbar` 。 添加一个名为**ToolbarTestCommand**的菜单命令项模板。 有关如何执行此操作的信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="create-a-toolbar-for-the-ide"></a>为 IDE 创建工具栏

1. 在*ToolbarTestCommandPackage .vsct*中，查找 "符号" 部分。 在名为 guidToolbarTestCommandPackageCmdSet 的 GuidSymbol 元素中，为工具栏和工具栏组添加声明，如下所示。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. 在 "命令" 部分的顶部，创建一个菜单部分。 将 Menu 元素添加到 "菜单" 部分以定义工具栏。

    ```xml
    <Menus>
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"
            type="Toolbar" >
            <CommandFlag>DefaultDocked</CommandFlag>
            <Strings>
                <ButtonText>Test Toolbar</ButtonText>
                <CommandName>Test Toolbar</CommandName>
            </Strings>
          </Menu>
    </Menus>
    ```

     工具栏不能像子菜单一样嵌套。 因此，您无需分配父组。 此外，您不必设置优先级，因为用户可以移动工具栏。 通常，将以编程方式定义工具栏的初始位置，但会保留用户的后续更改。

3. 在 "[组](../extensibility/groups-element.md)" 部分中的 "现有组" 条目后面，定义一个[组](../extensibility/group-element.md)元素以包含工具栏的命令。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. 使按钮显示在工具栏上。 在 "按钮" 部分中，将按钮中的父块替换到工具栏中。 生成的按钮块应如下所示：

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏不包含命令，则它不会显示。

5. 生成项目并启动调试。 应显示实验实例。

6. 右键单击 Visual Studio 菜单栏以获取工具栏列表。 选择 "**测试工具栏**"。

7. 现在，你应该将工具栏显示为 "在文件中查找" 图标右侧的图标。 单击图标时，应会看到一个消息框，其中显示 " **ToolbarTestCommandPackage"。MenuItemCallback （）中的 IDEToolbar**。

## <a name="see-also"></a>另请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
