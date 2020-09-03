---
title: 向菜单栏添加菜单 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
caps.latest.revision: 52
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 64ab627d785e8b00b5159969a01dc1102df30359
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184931"
---
# <a name="adding-a-menu-to-the-visual-studio-menu-bar"></a>将菜单添加到 Visual Studio 菜单栏
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本演练演示如何将菜单添加到 Visual Studio 集成开发环境 (IDE) 的菜单栏中。 IDE 菜单栏包含 " **文件**"、" **编辑**"、" **视图**"、" **窗口**" 和 " **帮助**" 等菜单类别。

 在将新菜单添加到 Visual Studio 菜单栏之前，请考虑是否应将命令置于现有菜单中。 有关命令放置的详细信息，请参阅 [Visual Studio 的菜单和命令](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)。

 菜单在项目的 .vsct 文件中声明。 有关菜单和 .vsct 文件的详细信息，请参阅 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

 完成本演练后，可以创建一个名为 **TestMenu** 的菜单，其中包含一个命令。

## <a name="prerequisites"></a>必备条件
 从 Visual Studio 2015 开始，你不需要从下载中心安装 Visual Studio SDK。 它作为 Visual Studio 安装程序中的可选功能提供。 你还可以在以后安装 VS SDK。 有关详细信息，请参阅 [安装 Visual STUDIO SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="creating-a-vsix-project-that-has-a-custom-command-item-template"></a>创建具有自定义命令项模板的 VSIX 项目

1. 创建一个名为的 VSIX 项目 `TopLevelMenu` 。 可以在 "**新建项目**" 对话框中的 " **Visual c #**  /  **扩展性**" 下找到 VSIX 项目模板。  有关详细信息，请参阅 [使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 当项目打开时，添加一个名为 **testcommand (** 的自定义命令项模板。 在 **解决方案资源管理器**中，右键单击项目节点，然后选择 " **添加/新建项**"。 在 " **添加新项** " 对话框中，切换到 " **Visual c #/扩展性** "，然后选择 " **自定义命令**"。 在窗口底部的 " **名称** " 字段中，将命令文件名更改为 **TestCommand.cs**。

## <a name="creating-a-menu-on-the-ide-menu-bar"></a>在 IDE 菜单栏上创建菜单

#### <a name="to-create-a-menu"></a>创建菜单

1. 在 **解决方案资源管理器**中，打开 .vsct。

     在文件末尾，有一个 \<Symbols> 节点包含多个 \<GuidSymbol> 节点。 在名为 guidTestCommandPackageCmdSet 的节点中，添加一个新符号，如下所示：

    ```xml
    <IDSymbol name="TopLevelMenu" value="0x1021"/>
    ```

2. \<Menus>在节点中创建一个空节点 \<Commands> ，就在之前 \<Groups> 。 在 \<Menus> 节点中，添加 \<Menu> 节点，如下所示：

    ```xml
    <Menus>
          <Menu guid="guidTestCommandPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
            <Parent guid="guidSHLMainMenu"
                    id="IDG_VS_MM_TOOLSADDINS" />
            <Strings>
              <ButtonText>TestMenu</ButtonText>
              <CommandName>TestMenu</CommandName>
            </Strings>
        </Menu>
    </Menus>
    ```

     `guid`菜单的和 `id` 值指定命令集和命令集中的特定菜单。

     在 `guid` `id` Visual Studio 菜单栏中包含 "工具" 和 "外接程序" 菜单的部分中，父位置的和值。

     字符串的值 `CommandName` 指定文本应该出现在菜单项中。

3. 在 \<Groups> 部分中，找到 \<Group> 并将元素更改 \<Parent> 为指向刚刚添加的菜单：

    ```csharp
    <Groups>
          <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
            <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
          </Group>
        </Groups>
    ```

     这会使组成为新菜单的一部分。

4. 找到 `Buttons` 节。 请注意， [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 包模板生成了 `Button` 其父项设置为的元素 `MyMenuGroup` 。 因此，此命令将显示在菜单上。

## <a name="building-and-testing-the-extension"></a>生成和测试扩展

1. 生成项目并启动调试。 应显示实验实例的实例。

2. 实验实例中的菜单栏应包含 **TestMenu** 菜单。

3. 在 " **TestMenu** " 菜单上，单击 " **调用测试命令**"。

     将出现一个消息框，并显示消息 "Testcommand (Package TopLevelMenu Testcommand (. MenuItemCallback ( # A1"。 这表示新命令正常工作。

## <a name="see-also"></a>另请参阅
 [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
