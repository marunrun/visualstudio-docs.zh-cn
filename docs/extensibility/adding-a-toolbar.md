---
title: 将工具栏添加 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 12fcf63c09d805f23fcbf0d041ab41ede7f85f32
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66352352"
---
# <a name="add-a-toolbar"></a>添加工具栏
本演练演示如何将工具栏添加到 Visual Studio IDE。

 工具栏是水平或垂直条包含绑定到命令的按钮。 具体取决于其实现中，在 IDE 中的工具栏可以重新定位、 停靠在主 IDE 窗口的任意一侧或制作需守候其他窗口。

 此外，用户可以将命令添加到工具栏或从中删除通过使用**自定义**对话框。 通常情况下，在 Vspackage 中的工具栏是用户可自定义。 IDE 处理所有自定义和 VSPackage 响应命令。 VSPackage 不需要知道命令是物理位置。

 有关菜单的详细信息，请参阅[命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

## <a name="prerequisites"></a>系统必备
 从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-an-extension-with-a-toolbar"></a>用工具栏创建扩展
 创建一个名为的 VSIX 项目`IDEToolbar`。 添加一个名为的菜单命令项模板**ToolbarTestCommand**。 有关如何执行此操作的信息，请参阅[与菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

## <a name="create-a-toolbar-for-the-ide"></a>为 IDE 创建工具栏

1. 在中*ToolbarTestCommandPackage.vsct*，查找符号部分。 在名为 guidToolbarTestCommandPackageCmdSet GuidSymbol 元素中，添加一个工具栏和工具栏组声明，如下所示。

    ```xml
    <IDSymbol name="Toolbar" value="0x1000" />
    <IDSymbol name="ToolbarGroup" value="0x1050" />

    ```

2. 在顶部的命令部分，创建一个菜单的部分。 将菜单元素添加到菜单部分来定义您的工具栏。

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

     不能像子菜单嵌套工具栏。 因此，无需分配父组。 此外，您无需设置优先级，因为用户可以移动工具栏。 通常情况下，初始放置工具栏的定义以编程方式，但用户的后续更改永久保存。

3. 在中[组](../extensibility/groups-element.md)部分中，现有的组项之后, 定义[组](../extensibility/group-element.md)元素以包含工具栏的命令。

    ```xml
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"
          priority="0x0000">
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>
    </Group>
    ```

4. 请在工具栏上显示的按钮。 在按钮部分中，将为到工具栏按钮中的父块。 生成的按钮块应如下所示：

    ```xml
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />
                <Icon guid="guidImages" id="bmpPic1" />
        <Strings>
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>
        </Strings>
    </Button>
    ```

     默认情况下，如果一个工具栏不具有任何命令，它不会不显示。

5. 生成项目并启动调试。 应显示在实验实例。

6. 右键单击 Visual Studio 菜单栏，以获取工具栏的列表。 选择**测试工具栏**。

7. 现在应为一个图标文件图标中查找右侧看到您的工具栏。 当单击图标时，应看到一个消息框，显示**ToolbarTestCommandPackage。Inside IDEToolbar.ToolbarTestCommand.MenuItemCallback()** .

## <a name="see-also"></a>请参阅
- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)