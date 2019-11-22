---
title: 'How to: Modify a Standard Menu Command in a Domain-Specific Language | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- .vsct files, adding commands to a domain-specific language
- Domain-Specific Language, adding custom commands
ms.assetid: 9b9d8314-d0d8-421a-acb9-d7e91e69825c
caps.latest.revision: 12
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 989367d395abb56e4f57c4aa2694b5f4ef17fb6e
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300876"
---
# <a name="how-to-modify-a-standard-menu-command-in-a-domain-specific-language"></a>如何：使用域特定语言修改标准的菜单命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可修改某些在 DSL 中自动定义的标准命令的行为。 For example, you could modify **Cut** so that it excludes sensitive information. 若要实现此目的，请重写命令集类中的方法。 这些类定义在 DslPackage 项目的 CommandSet.cs 文件中，并派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>。

 总之，若要修改命令，请执行以下操作：

1. [Discover what commands you can modify](#what).

2. [Create a partial declaration of the appropriate command set class](#extend).

3. [Override the ProcessOnStatus and ProcessOnMenu methods](#override) for the command.

   本主题解释了此过程。

> [!NOTE]
> If you want to create your own menu commands, see [How to: Add a Command to the Shortcut Menu](../modeling/how-to-add-a-command-to-the-shortcut-menu.md).

## <a name="what"></a> What commands can you modify?

#### <a name="to-discover-what-commands-you-can-modify"></a>发现可以修改的命令

1. In the `DslPackage` project, open `GeneratedCode\CommandSet.cs`. This C# file can be found in Solution Explorer as a subsidiary of `CommandSet.tt`.

2. Find classes in this file whose names end with "`CommandSet`", for example `Language1CommandSet` and `Language1ClipboardCommandSet`.

3. 在每个命令集类中，键入“`override`”，后跟一个空格。 IntelliSense 将显示可重写方法的列表。 每个命令具有一对其名称以“`ProcessOnStatus`”和“`ProcessOnMenu`”开头的方法。

4. 记录哪些命令集类包含你想要修改的命令。

5. 关闭该文件，无需保存编辑。

    > [!NOTE]
    > 通常，不应编辑已生成的文件。 任何编辑都将在下次生成文件时丢失。

## <a name="extend"></a> Extend the appropriate command set class
 创建包含命令集类的分部声明的新文件。

#### <a name="to-extend-the-command-set-class"></a>扩展命令集类

1. 在“解决方案资源管理器”中，在 DslPackage 项目中打开 GeneratedCode 文件夹，然后在 CommandSet.tt 下进行查找并打开其生成的文件 CommandSet.cs。 注意在此处定义的第一个类的命名空间和名称。 例如，你可能看到：

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. In **DslPackage**, create a folder named **Custom Code**. In this folder, create a new class file named `CommandSet.cs`.

3. 在该新文件中，编写具有与生成的分部类相同的命名空间和名称的分部声明。 例如:

    ```
    using System;
    using System.Collections.Generic;
    using System.ComponentModel.Design;
    namespace Company.Language1 /* Make sure this is correct */
    { internal partial class Language1CommandSet { ...
    ```

     **Note** If you used the class file template to create the new file, you must correct both the namespace and the class name.

## <a name="override"></a> Override the command methods
 Most commands have two associated methods: The method with a name like `ProcessOnStatus`... determines whether the command should be visible and enabled. 它将在每当用户右键单击关系图时调用，并应快速执行且不做任何更改。 `ProcessOnMenu`... is called when the user clicks the command, and should perform the function of the command. 你可能想要重写其中一个方法，或两者都进行重写。

### <a name="to-change-when-the-command-appears-on-a-menu"></a>更改命令何时显示在菜单上
 Override the ProcessOnStatus... method. 此方法应设置其参数 MenuCommand 的“可见”和“已启用”属性。 通常，命令查看 this.CurrentSelection 来确定命令是否应用到选定的元素，还可能查看其属性来确定命令是否可以应用到其当前状态中。

 一般原则是，“可见”属性应由选定了哪些什么元素来确定。 “已启用”属性（确定命令在菜单上是显示为黑色还是灰色）应取决于选择的当前状态。

 以下示例将在用户已选择多个形状时禁用“删除”菜单项。

> [!NOTE]
> 此方法不影响命令通过击键是否可用。 例如，禁用“删除”菜单项不会阻止通过 Delete 键来调用命令。

```
/// <summary>
/// Called when user right-clicks on the diagram or clicks the Edit menu.
/// </summary>
/// <param name="command">Set Visible and Enabled properties.</param>
protected override void ProcessOnStatusDeleteCommand (MenuCommand command)
{
  // Default settings from the base method.
  base.ProcessOnStatusDeleteCommand(command);
  if (this.CurrentSelection.Count > 1)
  {
    // If user has selected more than one item, Delete is greyed out.
    command.Enabled = false;
  }
}
```

 最佳做法是先调用基方法，以处理所有你无需考虑的用例和设置。

 ProcessOnStatus 方法不应在“存储”中创建、删除或更新元素。

### <a name="to-change-the-behavior-of-the-command"></a>更改命令的行为
 Override the ProcessOnMenu... method. 以下示例将阻止用户一次删除多个元素，即使使用 Delete 键也是如此。

```
/// <summary>
/// Called when user presses Delete key
/// or clicks the Delete command on a menu.
/// </summary>
protected override void ProcessOnMenuDeleteCommand()
{
  // Allow users to delete only one thing at a time.
  if (this.CurrentSelection.Count <= 1)
  {
    base.ProcessOnMenuDeleteCommand();
  }
}
```

 如果你的代码将对“存储”进行更改（例如创建、删除或更新元素或链接），则必须在事务内进行这些更改。 For more information, see [How to Create and Update model elements](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

### <a name="writing-the-code-of-the-methods"></a>编写方法的代码
 以下片段通常在这些方法内十分有用：

- `this.CurrentSelection` 用户右键单击的形状始终包含在此形状和连接符列表中。 如果用户单击关系图的空白部分，则“关系图”是该列表中的唯一成员。

- `this.IsDiagramSelected()` - `true` if the user clicked a blank part of the diagram.

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()` - 用户未选择多个形状

- `this.SingleSelection` - 用户右键单击的形状或关系图

- `shape.ModelElement as MyLanguageElement` - 由形状表示的模型元素。

  For more information about how to navigate from element to element and about how to create objects and links, see [Navigating and Updating a Model in Program Code](../modeling/navigating-and-updating-a-model-in-program-code.md).

## <a name="see-also"></a>请参阅
 <xref:System.ComponentModel.Design.MenuCommand> [Writing Code to Customise a Domain-Specific Language](../modeling/writing-code-to-customise-a-domain-specific-language.md) [How to: Add a Command to the Shortcut Menu](../modeling/how-to-add-a-command-to-the-shortcut-menu.md) [Walkthrough: Getting Information from a Selected Link](../misc/walkthrough-getting-information-from-a-selected-link.md) [How VSPackages Add User Interface Elements](../extensibility/internals/how-vspackages-add-user-interface-elements.md) [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md) [VSCT XML Schema Reference](../extensibility/vsct-xml-schema-reference.md)
