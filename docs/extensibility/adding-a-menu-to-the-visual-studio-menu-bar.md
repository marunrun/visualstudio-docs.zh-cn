---
title: 将菜单添加到 Visual Studio 菜单栏 |Microsoft Docs
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a28e7f69ed8e9a76e11d8892ee677435f75c99b2
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66349795"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>向 Visual Studio 菜单栏添加菜单

本演练演示如何将菜单添加到 Visual Studio 集成的开发环境 (IDE) 的菜单栏。 IDE 菜单栏包含菜单类别，如**文件**，**编辑**，**视图**，**窗口**，并**帮助**.

在将新菜单添加到 Visual Studio 菜单栏中之前, 请考虑是否应在现有菜单内放置你的命令。 有关命令放置的详细信息，请参阅[Visual Studio 的菜单和命令](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)。

菜单中的声明 *.vsct*项目文件。 有关详细信息，有关菜单和 *.vsct*文件，请参阅[命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

通过完成本演练，您可以创建一个名为菜单**TestMenu** ，其中包含一个命令。

> [!NOTE]
> 在 VS 2019 顶级菜单由扩展提供置于下**扩展**菜单。

## <a name="prerequisites"></a>系统必备

从 Visual Studio 2015 开始，您并不安装 Visual Studio SDK 从下载中心获得。 它是作为 Visual Studio 安装程序中的可选功能包含在内。 此外可以在以后安装 VS SDK。 有关详细信息，请参阅[安装 Visual Studio SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>创建具有自定义命令项模板的 VSIX 项目

1. 创建一个名为的 VSIX 项目`TopLevelMenu`。 您可以发现中的 VSIX 项目模板**新的项目**通过搜索"vsix"对话框。  有关详细信息，请参阅[与菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 项目打开后，添加名为的自定义命令项模板**TestCommand**。 在中**解决方案资源管理器**，右键单击项目节点并选择**添加** >  **新项**。 在中**添加新项**对话框中，转到**Visual C# / 可扩展性**，然后选择**自定义命令**。 在中**名称**在窗口底部字段中，将命令文件名称更改为*TestCommand.cs*。

## <a name="create-a-menu-on-the-ide-menu-bar"></a>在 IDE 的菜单栏上创建菜单

::: moniker range="vs-2017"

1. 在中**解决方案资源管理器**，打开*TestCommandPackage.vsct*。

    在文件末尾，还有\<符号 > 节点，其中包含几个\<GuidSymbol > 节点。 在名为 guidTestCommandPackageCmdSet 节点中，添加一个新的符号，按如下所示：

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 创建一个空\<菜单 > 中的节点\<命令 > 节点，再\<组 >。 在中\<菜单 > 节点中，添加\<菜单 > 节点，按如下所示：

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

    `guid`和`id`菜单的值设置的命令中指定设置的命令和特定的菜单。

    `guid`和`id`父级值定位的一部分包含工具和外接程序菜单在 Visual Studio 菜单栏上的菜单。

    值`CommandName`字符串指定的文本应出现在菜单项。

3. 在中\<组 > 部分中，找到\<组 > 并将更改\<父 > 元素以指向我们刚添加的菜单：

   ```csharp
   <Groups>
         <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    这使得新菜单的组部分。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在中**解决方案资源管理器**，打开*TopLevelMenuPackage.vsct*。

    在文件末尾，还有\<符号 > 节点，其中包含几个\<GuidSymbol > 节点。 在名为 guidTopLevelMenuPackageCmdSet 节点中，添加一个新的符号，按如下所示：

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 创建一个空\<菜单 > 中的节点\<命令 > 节点，再\<组 >。 在中\<菜单 > 节点中，添加\<菜单 > 节点，按如下所示：

   ```xml
   <Menus>
         <Menu guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu" priority="0x700" type="Menu">
           <Parent guid="guidSHLMainMenu"
                   id="IDG_VS_MM_TOOLSADDINS" />
           <Strings>
             <ButtonText>TestMenu</ButtonText>
             <CommandName>TestMenu</CommandName>
           </Strings>
       </Menu>
   </Menus>
   ```

    `guid`和`id`菜单的值设置的命令中指定设置的命令和特定的菜单。

    `guid`和`id`父级值定位的一部分包含工具和外接程序菜单在 Visual Studio 菜单栏上的菜单。

    值`CommandName`字符串指定的文本应出现在菜单项。

3. 在中\<组 > 部分中，找到\<组 > 并将更改\<父 > 元素以指向我们刚添加的菜单：

   ```csharp
   <Groups>
         <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    这使得新菜单的组部分。

::: moniker-end

4. 查找`Buttons`部分。 请注意，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]生成包模板`Button`已设置为其父级的元素`MyMenuGroup`。 因此，此命令显示在你的菜单上。

## <a name="build-and-test-the-extension"></a>生成并测试此扩展

1. 生成项目并启动调试。 应显示在实验实例的实例。

::: moniker range="vs-2017"

2. 应包含在实验实例中的菜单栏**TestMenu**菜单。

::: moniker-end

::: moniker range=">=vs-2019"

2. **扩展**应包含在实验实例中的菜单**TestMenu**菜单。

::: moniker-end

3. 上**TestMenu**菜单上，单击**调用测试命令**。

     一个消息框应该显示并显示消息"第包内 TopLevelMenu.TestCommand.MenuItemCallback() TestCommand"。

## <a name="see-also"></a>请参阅

- [命令、 菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)