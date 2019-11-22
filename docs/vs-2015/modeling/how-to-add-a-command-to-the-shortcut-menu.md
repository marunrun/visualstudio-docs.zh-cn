---
title: 'How to: Add a Command to the Shortcut Menu | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language Tools, walkthroughs
- walkthroughs [Domain-Specific Language Tools]
ms.assetid: cd550399-05fc-4dbf-be4c-f5094bb752ce
caps.latest.revision: 24
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 8d5373ae27797aa3bfe4627fb84ce393dce9e910
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300890"
---
# <a name="how-to-add-a-command-to-the-shortcut-menu"></a>如何：向快捷菜单中添加命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将菜单命令添加到域特定语言 (DSL)，以便用户可以执行特定于 DSL 的任务。 当用户右键单击关系图时，这些命令将显示在上下文（快捷）菜单上。 你可以定义某个命令，以使它仅在特定情况下才显示在菜单中。 例如，可以使该命令仅在用户单击特定类型的元素或处于特定状态下的元素时才可见。

 总之，请在 DslPackage 项目中执行如下步骤：

1. [Declare the command in Commands.vsct](#VSCT)

2. [Update the package version number in Package.tt](#version). 只要更改 Commands.vsct，就必须执行此操作

3. [Write methods in the CommandSet class](#CommandSet) to make the command visible and to define what you want the command to do.

   For samples, see the [Visualization and Modeling SDK website](https://go.microsoft.com/fwlink/?LinkID=185579).

> [!NOTE]
> 通过在 CommandSet.cs 中重写方法，还可以修改某些现有命令（例如剪切、粘贴、全选和打印）的行为。 For more information, see [How to: Modify a Standard Menu Command](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

## <a name="defining-a-command-using-mef"></a>使用 MEF 定义命令
 托管扩展框架 (MEF) 提供了一种定义关系图菜单上的菜单命令的替代方法。 它的主要用途是允许你或其他各方扩展 DSL。 用户可以选择只安装 DSL 或同时安装 DSL 和扩展。 但是，完成在 DSL 上启用 MEF 的初始工作后，MEF 还将减少定义快捷菜单命令的工作量。

 请在以下情况下使用本主题中的方法：

1. 你想要定义右键单击快捷菜单以外的菜单上的菜单命令。

2. 你想要在菜单中定义特定的命令分组。

3. 你不希望其他人使用自己的命令来扩展 DSL。

4. 你只想要定义一个命令。

   否则，请考虑使用 MEF 方法来定义命令。 For more information, see [Extend your DSL by using MEF](../modeling/extend-your-dsl-by-using-mef.md).

## <a name="VSCT"></a> Declare the Command in Commands.Vsct
 菜单命令将在 DslPackage\Commands.vsct 中声明。 这些定义指定菜单项的标签以及它们在菜单上显示的位置。

 The file that you edit, Commands.vsct, imports definitions from several .h files, which are located in the directory *Visual Studio SDK install path*\VisualStudioIntegration\Common\Inc. It also includes GeneratedVsct.vsct, which is generated from your DSL definition.

 For more information about .vsct files, see [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md).

#### <a name="to-add-the-command"></a>添加命令

1. In **Solution Explorer**, under the **DslPackage** project, open Commands.vsct.

2. 在 `Commands` 元素中，定义一个或多个按钮和一个组。 A *button* is an item on the menu. A *group* is a section in the menu. 若要定义这些项，请添加以下元素：

    ```
    <!-- Define a group - a section in the menu -->
    <Groups>
      <Group guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup" priority="0x0100">
        <!-- These symbols are defined in GeneratedVSCT.vsct -->
        <Parent guid="guidCmdSet" id="menuidContext" />
      </Group>
    </Groups>
    <!-- Define a button - a menu item - inside the Group -->
    <Buttons>
      <Button guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"
        priority="0x0100" type="Button">
        <Parent guid="guidCustomMenuCmdSet" id="grpidMyMenuGroup"/>
        <!-- If you do not want to place the command in your own Group,
             use Parent guid="guidCmdSet" id="grpidContextMain".
             These symbols are defined in GeneratedVSCT.vsct -->
        <CommandFlag>DynamicVisibility</CommandFlag>
        <Strings>
          <ButtonText>My Context Menu Command</ButtonText>
        </Strings>
      </Button>
    </Buttons>
    ```

    > [!NOTE]
    > 每个按钮或组由一个 GUID 和一个整数 ID 标识。 可以使用同一 GUID 创建多个组和按钮。 但是，它们必须具有不同的 ID。 The GUID names and ID names are translated to actual GUIDs and numeric IDs in the `<Symbols>` node.

3. 为命令添加可见性约束，以便仅在域特定语言的上下文中加载该命令。 For more information, see [VisibilityConstraints Element](../extensibility/visibilityconstraints-element.md).

     为此，请在 `CommandTable` 元素后的 `Commands` 元素中添加以下元素。

    ```
    <VisibilityConstraints>
      <!-- Ensures the command is only loaded for this DSL -->
      <VisibilityItem guid="guidCustomMenuCmdSet" id="cmdidMyContextMenuCommand"
        context="guidEditor"/>
    </VisibilityConstraints>
    ```

4. 定义用于 GUID 和 ID 的名称。 为此，请在 `Symbols` 元素后的 `CommandTable` 元素中添加 `Commands` 元素。

    ```
    <Symbols>
      <!-- Substitute a unique GUID for the placeholder: -->
      <GuidSymbol name="guidCustomMenuCmdSet"
        value="{00000000-0000-0000-0000-000000000000}" >
        <IDSymbol name="grpidMyMenuGroup" value="0x01001"/>
        <IDSymbol name="cmdidMyContextMenuCommand" value="0x00001"/>
      </GuidSymbol>
    </Symbols>
    ```

5. 将 `{000...000}` 替换为标识组和菜单项的 GUID。 To obtain a new GUID, use the **Create GUID** tool on the **Tools** menu.

    > [!NOTE]
    > 如果添加更多组或菜单项，则可以使用同一 GUID。 但是，你必须将新值用于 `IDSymbols`。

6. 在已从此过程复制的代码中，将以下字符串的每个匹配项替换为自己的字符串：

    - `grpidMyMenuGroup`

    - `cmdidMyContextMenuCommand`

    - `guidCustomMenuCmdSet`

    - `My Context Menu Command`

## <a name="version"></a> Update the Package Version in Package.tt
 每当添加或更改命令时，都要在发布新版本的域特定语言之前，更新应用于程序包类的 `version` 的 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 参数。

 因为程序包类定义在生成的文件中，因此请在生成 Package.cs 文件的文本模板文件中更新该特性。

#### <a name="to-update-the-packagett-file"></a>更新 Package.tt 文件

1. In **Solution Explorer**, in the **DslPackage** project, in the **GeneratedCode** folder, open the Package.tt file.

2. 查找 `ProvideMenuResource` 特性。

3. 递增特性的 `version` 参数，它是第二个参数。 如果需要，你可以显式编写参数名称以提醒你它的用途。 例如:

     `[VSShell::ProvideMenuResource("1000.ctmenu", version: 2 )]`

## <a name="CommandSet"></a> Define the Behavior of the Command
 DSL 已具有一些在 DslPackage\GeneratedCode\CommandSet.cs 中声明的分部类中实现的命令。 若要添加新命令，你必须通过创建包含同一个类的分部声明的新文件来扩展此类。 The name of the class is usually *\<YourDslName>* `CommandSet`. 这将有助于通过验证该类的名称以及检查其内容来开始操作。

 命令集类派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>。

#### <a name="to-extend-the-commandset-class"></a>扩展 CommandSet 类

1. 在“解决方案资源管理器”中，在 DslPackage 项目中打开 GeneratedCode 文件夹，然后在 CommandSet.tt 下进行查找并打开其生成的文件 CommandSet.cs。 注意在此处定义的第一个类的命名空间和名称。 例如，你可能看到：

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. In **DslPackage**, create a folder that is named **Custom Code**. In this folder, create a new class file that is named `CommandSet.cs`.

3. 在该新文件中，编写具有与生成的分部类相同的命名空间和名称的分部声明。 例如:

     `namespace Company.Language1 /* Make sure this is correct */`

     `{ internal partial class Language1CommandSet { ...`

     **Note** If you used the class template to create the new file, you must correct both the namespace and the class name.

### <a name="extend-the-command-set-class"></a>扩展命令集类
 通常，命令集代码将需要导入以下命名空间：

```
using System;
using System.Collections.Generic;
using System.ComponentModel.Design;
using System.Linq;
using Microsoft.VisualStudio.Modeling;
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Shell;
```

 调整命名空间和类名，以匹配生成的 CommandSet.cs 中的命名空间和类名：

```
namespace Company.Language1 /* Make sure this is correct */
{
  // Same class as the generated class.
  internal partial class Language1CommandSet
  {
```

 必须定义两个方法：一个用于确定命令何时在上下文菜单上可见，另一个用于执行该命令。 这些方法不是重写方法；相反，在命令的列表中注册这些方法。

### <a name="define-when-the-command-will-be-visible"></a>定义命令将何时可见
 For each command, define an `OnStatus...` method that determines whether the command will appear on the menu, and whether it will be enabled or greyed out. Set the `Visible` and `Enabled` properties of the `MenuCommand`, as shown in the following example. 每次用户右键单击关系图时，都将调用此方法以构造快捷菜单，因此它必须尽快工作。

 在此示例中，该命令仅在用户已选择特定类型的形状时才可见，并且仅在至少一个选定元素处于特定状态时才启用该命令。 该示例基于类关系图 DSL 模板，并且 ClassShape 和 ModelClass 是在 DSL 中定义的类型：

```
private void OnStatusMyContextMenuCommand(object sender, EventArgs e)
{
  MenuCommand command = sender as MenuCommand;
  command.Visible = command.Enabled = false;
  foreach (object selectedObject in this.CurrentSelection)
  {
    ClassShape shape = selectedObject as ClassShape;
    if (shape != null)
    {
      // Visibility depends on what is selected.
      command.Visible = true;
      ModelClass element = shape.ModelElement as ModelClass;
      // Enabled depends on state of selection.
      if (element != null && element.Comments.Count == 0)
      {
        command.Enabled = true;
        return; // seen enough
} } } }
```

 以下片段通常在 OnStatus 方法内十分有用：

- `this.CurrentSelection` 用户右键单击的形状始终包含在此列表中。 如果用户单击关系图的空白部分，则“关系图”是该列表中的唯一成员。

- `this.IsDiagramSelected()` - `true` if the user clicked a blank part of the diagram.

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()` - 用户未选择多个对象

- `this.SingleSelection` - 用户右键单击的形状或关系图

- `shape.ModelElement as MyLanguageElement` - 由形状表示的模型元素。

  一般原则是，使 `Visible` 属性依赖于所选定的内容，并使 `Enabled` 属性依赖于选定元素的状态。

  OnStatus 方法不应更改“存储”的状态。

### <a name="define-what-the-command-does"></a>定义命令可执行操作
 对于每个命令，定义在用户单击菜单命令时执行所需操作的 `OnMenu...` 方法。

 如果要对模型元素进行更改，则必须在事务内执行此操作。 For more information, see [How to: Modify a Standard Menu Command](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

 在此示例中，`ClassShape`、`ModelClass` 和 `Comment` 是在 DSL 中定义的类型，该 DSL 派生自类关系图 DSL 模板。

```
private void OnMenuMyContextMenuCommand(object sender, EventArgs e)
{
  MenuCommand command = sender as MenuCommand;
  Store store = this.CurrentDocData.Store;
  // Changes to elements and shapes must be performed in a Transaction.
  using (Transaction transaction =
       store.TransactionManager.BeginTransaction("My command"))
  {
    foreach (object selectedObject in this.CurrentSelection)
    {
      // ClassShape is defined in my DSL.
      ClassShape shape = selectedObject as ClassShape;
      if (shape != null)
      {
        // ModelClass is defined in my DSL.
        ModelClass element = shape.ModelElement as ModelClass;
        if (element != null)
        {
          // Do required action here - for example:

          // Create a new element. Comment is defined in my DSL.
          Comment newComment = new Comment(element.Partition);
          // Every element must be the target of an embedding link.
          element.ModelRoot.Comments.Add(newComment);
          // Set properties of new element.
          newComment.Text = "This is a comment";
          // Create a reference link to existing object.
          element.Comments.Add(newComment);
        }
      }
    }
    transaction.Commit(); // Don't forget this!
  }
}
```

 For more information about how to navigate from object to object in the model, and about how to create objects and links, see [How to: Modify a Standard Menu Command](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md).

### <a name="register-the-command"></a>注册命令
 在 C# 中重复在 CommandSet.vsct 的“符号”部分中进行的 GUID 和 ID 值的声明：

```
private Guid guidCustomMenuCmdSet =
    new Guid("00000000-0000-0000-0000-000000000000");
private const int grpidMyMenuGroup = 0x01001;
private const int cmdidMyContextMenuCommand = 1;
```

 Use the same GUID value as you inserted in **Commands.vsct**.

> [!NOTE]
> 如果更改 VSCT 文件的“符号”部分，还必须更改这些要匹配的声明。 还应在 Package.tt 中递增版本号

 将菜单命令注册为此命令集的一部分。 当初始化关系图时，将调用一次 `GetMenuCommands()`：

```
protected override IList<MenuCommand> GetMenuCommands()
{
  // Get the list of generated commands.
  IList<MenuCommand> commands = base.GetMenuCommands();
  // Add a custom command:
  DynamicStatusMenuCommand myContextMenuCommand =
    new DynamicStatusMenuCommand(
      new EventHandler(OnStatusMyContextMenuCommand),
      new EventHandler(OnMenuMyContextMenuCommand),
      new CommandID(guidCustomMenuCmdSet, cmdidMyContextMenuCommand));
  commands.Add(myContextMenuCommand);
  // Add more commands here.
  return commands;
}
```

## <a name="test-the-command"></a>测试命令
 在 Visual Studio 的实验实例中生成并运行 DSL。 在已指定的情况下，该命令应显示在快捷菜单中。

#### <a name="to-exercise-the-command"></a>演练命令

1. On the **Solution Explorer** toolbar, click **Transform All Templates**.

2. Press **F5** to rebuild the solution, and start debugging the domain-specific language in the experimental build.

3. 在实验性生成中，打开示例关系图。

4. 在关系图中右键单击各种项，以验证命令是否根据所选择的项正确启用或禁用，以及是否相应地显示或隐藏。

## <a name="troubleshooting"></a>疑难解答
 **Command does not appear in menu:**

- 除非安装 DSL 包，否则命令将只显示在 Visual Studio 的调试实例中。 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。

- 确保实验性示例具有此 DSL 的正确文件扩展名。 若要检查该文件扩展名，请在 Visual Studio 的主实例中打开 DslDefinition.dsl。 随后，在 DSL 资源管理器中，右键单击“编辑器”节点，然后单击“属性”。 在“属性”窗口中，检查 FileExtension 属性。

- Did you [increment the package version number](#version)?

- 在 OnStatus 方法的开头设置断点。 在右键单击关系图的任意部分时，应发生中断。

   **OnStatus method is not called**:

  - 确保 CommandSet 代码中的 GUID 和 ID 匹配 Commands.vsct 的“符号”部分中的 GUID 和 ID。

  - 在 Commands.vsct 中，确保每个“父”节点中的 GUID 和 ID 标识正确的父“组”。

  - 在 Visual Studio 命令提示符中，键入 devenv /rootsuffix exp /setup。 然后，重新启动 Visual Studio 的调试实例。

- 逐步执行 OnStatus 方法，以验证 command.Visible 和 command.Enabled 是否设置为 True。

  **Wrong menu text appears, or command appears in the wrong place**:

- 确保 GUID 和 ID 的组合对此命令是唯一的。

- 确保已卸载早期版本的程序包。

## <a name="see-also"></a>请参阅
 [Writing Code to Customise a Domain-Specific Language](../modeling/writing-code-to-customise-a-domain-specific-language.md) [How to: Modify a Standard Menu Command](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md) [Deploying Domain-Specific Language Solutions](../modeling/deploying-domain-specific-language-solutions.md)
