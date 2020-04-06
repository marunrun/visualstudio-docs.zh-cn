---
title: 向视觉工作室菜单栏添加菜单 |微软文档
ms.date: 3/16/2019
ms.topic: conceptual
helpviewer_keywords:
- menus, creating top level
- top-level menus
ms.assetid: 58fc1a31-2aeb-441c-8e48-c7d5cbcfe501
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 91e5a6e1714dbb87abc67fbf722c3bbd1a194a5b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740307"
---
# <a name="add-a-menu-to-the-visual-studio-menu-bar"></a>向视觉工作室菜单栏添加菜单

本演练演示如何向 Visual Studio 集成开发环境 （IDE） 的菜单栏添加菜单。 IDE 菜单栏包含菜单类别，如 **"文件**"、"**编辑**"、"**查看**"、"**窗口**"和"**帮助**"。

在将新菜单添加到 Visual Studio 菜单栏之前，请考虑是否应将命令放置在现有菜单中。 有关命令放置的详细信息，请参阅[Visual Studio 的菜单和命令](../extensibility/ux-guidelines/menus-and-commands-for-visual-studio.md)。

菜单在项目的 *.vsct*文件中声明。 有关菜单和 *.vsct*文件的详细信息，请参阅[命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)。

通过完成本演练，您可以创建一个名为**TestMenu**的菜单，其中包含一个命令。

> [!NOTE]
> 在 VS 2019 中，由扩展提供的顶级菜单放在 **"扩展"** 菜单下。

## <a name="prerequisites"></a>先决条件

从 Visual Studio 2015 开始，您不会从下载中心安装 Visual Studio SDK。 它作为可选功能包含在可视化工作室设置中。 以后还可以安装 VS SDK。 有关详细信息，请参阅[安装可视化工作室 SDK](../extensibility/installing-the-visual-studio-sdk.md)。

## <a name="create-a-vsix-project-that-has-a-custom-command-item-template"></a>创建具有自定义命令项模板的 VSIX 项目

1. 创建名为 的`TopLevelMenu`VSIX 项目。 您可以通过搜索"vsix"在 **"新项目**"对话框中找到 VSIX 项目模板。  有关详细信息，请参阅[使用菜单命令创建扩展](../extensibility/creating-an-extension-with-a-menu-command.md)。

2. 打开项目时，添加名为**TestCommand**的自定义命令项模板。 在**解决方案资源管理器**中，右键单击项目节点并选择"**添加新** >  **项**"。 在"**添加新项目"** 对话框中，转到**可视化 C# / 扩展性**，然后选择 **"自定义命令**"。 在窗口底部的 **"名称"** 字段中，将命令文件名更改为*TestCommand.cs*。

## <a name="create-a-menu-on-the-ide-menu-bar"></a>在 IDE 菜单栏上创建菜单

::: moniker range="vs-2017"

1. 在**解决方案资源管理器中**，打开*测试命令包.vsct*。

    在文件末尾，有一个\<符号>节点，其中包含多个\<GuidSymbol>节点。 在名为 guidTestCommandPackageCmdSet 的节点中，添加一个新符号，如下所示：

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 在\<\<"组>"之前\<，在命令>节点中创建空菜单>节点。 在\<"菜单>节点"中，添加\<菜单>节点，如下所示：

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

    菜单`guid`的`id`和 值指定命令集和命令集中的特定菜单。

    父`guid`菜单`id`的 和 值将菜单放置在包含"工具和外接程序"菜单的 Visual Studio 菜单栏部分。

    `CommandName`字符串的值指定文本应出现在菜单项中。

3. 在"\<组>"部分中\<，查找组>并更改\<父>元素以指向我们刚刚添加的菜单：

   ```csharp
   <Groups>
         <Group guid="guidTestCommandPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTestCommandPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    这使得组成为新菜单的一部分。

::: moniker-end

::: moniker range=">=vs-2019"

1. 在**解决方案资源管理器中**，打开*顶级菜单包.vsct*。

    在文件末尾，有一个\<符号>节点，其中包含多个\<GuidSymbol>节点。 在名为 guidTopLevelMenuPackageCmdSet 的节点中，添加一个新符号，如下所示：

   ```xml
   <IDSymbol name="TopLevelMenu" value="0x1021"/>
   ```

2. 在\<\<"组>"之前\<，在命令>节点中创建空菜单>节点。 在\<"菜单>节点"中，添加\<菜单>节点，如下所示：

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

    菜单`guid`的`id`和 值指定命令集和命令集中的特定菜单。

    父`guid`菜单`id`的 和 值将菜单放置在包含"工具和外接程序"菜单的 Visual Studio 菜单栏部分。

    `CommandName`字符串的值指定文本应出现在菜单项中。

3. 在"\<组>"部分中\<，查找组>并更改\<父>元素以指向我们刚刚添加的菜单：

   ```csharp
   <Groups>
         <Group guid="guidTopLevelMenuPackageCmdSet" id="MyMenuGroup" priority="0x0600">
           <Parent guid="guidTopLevelMenuPackageCmdSet" id="TopLevelMenu"/>
         </Group>
       </Groups>
   ```

    这使得组成为新菜单的一部分。

::: moniker-end

4. 找到 `Buttons` 节。 请注意，[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]包模板已生成其`Button`父设置为`MyMenuGroup`的元素。 因此，此命令将显示在您的菜单上。

## <a name="build-and-test-the-extension"></a>生成和测试扩展

1. 生成项目并启动调试。 应出现实验实例的实例。

::: moniker range="vs-2017"

2. 实验实例中的菜单栏应包含**TestMenu 菜单**。

::: moniker-end

::: moniker range=">=vs-2019"

2. 实验实例中的**扩展**菜单应包含**TestMenu 菜单**。

::: moniker-end

3. 在 **"测试菜单"** 菜单上，单击 **"调用测试命令**"。

     应显示一个消息框并显示消息"顶级菜单中的测试命令包.TestCommand.MenuItem 回拨（）"。

## <a name="see-also"></a>请参阅

- [命令、菜单和工具栏](../extensibility/internals/commands-menus-and-toolbars.md)
