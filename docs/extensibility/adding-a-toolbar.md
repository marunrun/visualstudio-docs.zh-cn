---
title: 添加工具栏 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 655cd87fe59cf4f42361cc24a63eb56653caae1a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740215"
---
# <a name="add-a-toolbar"></a>添加工具栏
本演练演示如何向可视化工作室 IDE 添加工具栏。

 工具栏是一个水平或垂直条带，其中包含绑定到命令的按钮。 根据其实现，IDE 中的工具栏可以重新定位、停靠在主 IDE 窗口的任何一侧，或使其位于其他窗口的前面。

 此外，用户可以向工具栏添加命令，或使用 **"自定义"** 对话框将其从工具栏中删除。 通常，VS 包中的工具栏是用户可自定义的。 IDE 处理所有自定义，VS包响应命令。 VSPackage 不必知道命令的物理位置。

 有关菜单的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>先决条件
 从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-toolbar"></a>使用工具栏创建扩展
 创建名为 的`IDEToolbar`VSIX 项目。 添加名为**工具栏测试命令 的**菜单命令项模板。 有关如何执行此操作的信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="create-a-toolbar-for-the-ide"></a>为 IDE 创建工具栏

1. 在*工具栏TestCommandPackage.vsct 中*，查找"符号"部分。 在名为 GuidToolbarTestCommandPackageCmdSet 的 GuidSymbol 元素中，添加工具栏和工具栏组的声明，如下所示。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. 在"命令"部分的顶部，创建菜单部分。 向"菜单"部分添加"菜单"元素以定义工具栏。

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

     工具栏不能像子菜单一样嵌套。 因此，您不必分配父组。 此外，您不必设置优先级，因为用户可以移动工具栏。 通常，工具栏的初始放置以编程方式定义，但用户的后续更改将保持不变。

3. 在现有组条目之后的["组](../extensibility/groups-element.md)"部分中，定义一个[组](../extensibility/group-element.md)元素以包含工具栏的命令。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. 使按钮显示在工具栏上。 在"按钮"部分中，将"按钮"中的父块替换为工具栏。 生成的按钮块应如下所示：

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果工具栏没有命令，则不会显示。

5. 生成项目并启动调试。 应出现实验实例。

6. 右键单击"视觉工作室"菜单栏可获取工具栏列表。 选择**测试工具栏**。

7. 现在，您应该将工具栏视为"在文件中查找"图标右侧的图标。 单击该图标时，应看到一个显示**工具栏TestCommandPackage的消息框。IDE 工具栏内.工具栏测试命令.Menuitem 回拨（）**.

## <a name="see-also"></a>请参阅
- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
