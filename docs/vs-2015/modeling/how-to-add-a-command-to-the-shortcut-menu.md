---
title: 如何：向快捷菜单添加命令 |Microsoft Docs
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
ms.openlocfilehash: 2d5ddea477aa7295c41097177265b43483b7aa45
ms.sourcegitcommit: c150d0be93b6f7ccbe9625b41a437541502560f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/10/2020
ms.locfileid: "75850413"
---
# <a name="how-to-add-a-command-to-the-shortcut-menu"></a>如何：向快捷菜单中添加命令
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将菜单命令添加到域特定语言 (DSL)，以便用户可以执行特定于 DSL 的任务。 当用户右键单击关系图时，这些命令将显示在上下文（快捷）菜单上。 你可以定义某个命令，以使它仅在特定情况下才显示在菜单中。 例如，可以使该命令仅在用户单击特定类型的元素或处于特定状态下的元素时才可见。

 总之，请在 DslPackage 项目中执行如下步骤：

1. [在 .vsct 中声明命令。](#VSCT)

2. [更新 Package.tt 中的包版本号](#version)。 只要更改 Commands.vsct，就必须执行此操作

3. [在 CommandSet 类中编写方法](#CommandSet)，使命令可见，并定义要执行的命令。

   有关示例，请参阅[可视化和建模 SDK 网站](https://www.visualstudio.com/)。

> [!NOTE]
> 通过在 CommandSet.cs 中重写方法，还可以修改某些现有命令（例如剪切、粘贴、全选和打印）的行为。 有关详细信息，请参阅[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。

## <a name="defining-a-command-using-mef"></a>使用 MEF 定义命令
 托管扩展框架 (MEF) 提供了一种定义关系图菜单上的菜单命令的替代方法。 它的主要用途是允许你或其他各方扩展 DSL。 用户可以选择只安装 DSL 或同时安装 DSL 和扩展。 但是，完成在 DSL 上启用 MEF 的初始工作后，MEF 还将减少定义快捷菜单命令的工作量。

 请在以下情况下使用本主题中的方法：

1. 你想要定义右键单击快捷菜单以外的菜单上的菜单命令。

2. 你想要在菜单中定义特定的命令分组。

3. 你不希望其他人使用自己的命令来扩展 DSL。

4. 你只想要定义一个命令。

   否则，请考虑使用 MEF 方法来定义命令。 有关详细信息，请参阅[使用 MEF 扩展 DSL](../modeling/extend-your-dsl-by-using-mef.md)。

## <a name="VSCT"></a>在 .Vsct 中声明命令。
 菜单命令将在 DslPackage\Commands.vsct 中声明。 这些定义指定菜单项的标签以及它们在菜单上显示的位置。

 所编辑的文件 .vsct 从多个 .h 文件导入定义，这些文件位于目录*Visual STUDIO SDK 安装路径*\VisualStudioIntegration\Common\Inc。它还包括从 DSL 定义生成的 GeneratedVsct. .vsct。

 有关 .vsct 文件的详细信息，请参阅[Visual Studio 命令表（.Vsct）文件](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)。

#### <a name="to-add-the-command"></a>添加命令

1. 在**解决方案资源管理器**的**DslPackage**项目下，打开 .vsct。

2. 在 `Commands` 元素中，定义一个或多个按钮和一个组。 *按钮*是菜单上的一项。 *组*是菜单中的一个部分。 若要定义这些项，请添加以下元素：

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
    > 每个按钮或组由一个 GUID 和一个整数 ID 标识。 可以使用同一 GUID 创建多个组和按钮。 但是，它们必须具有不同的 ID。 GUID 名称和 ID 名称将转换为 `<Symbols>` 节点中的实际 Guid 和数值 Id。

3. 为命令添加可见性约束，以便仅在域特定语言的上下文中加载该命令。 有关详细信息，请参阅[VisibilityConstraints 元素](../extensibility/visibilityconstraints-element.md)。

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

5. 将 `{000...000}` 替换为标识组和菜单项的 GUID。 若要获取新的 GUID，请使用 "**工具**" 菜单上的 "**创建 GUID** " 工具。

    > [!NOTE]
    > 如果添加更多组或菜单项，则可以使用同一 GUID。 但是，你必须将新值用于 `IDSymbols`。

6. 在已从此过程复制的代码中，将以下字符串的每个匹配项替换为自己的字符串：

    - `grpidMyMenuGroup`

    - `cmdidMyContextMenuCommand`

    - `guidCustomMenuCmdSet`

    - `My Context Menu Command`

## <a name="version"></a>更新 Package.tt 中的包版本
 每当添加或更改命令时，都要在发布新版本的域特定语言之前，更新应用于程序包类的 `version` 的 <xref:Microsoft.VisualStudio.Shell.ProvideMenuResourceAttribute> 参数。

 因为程序包类定义在生成的文件中，因此请在生成 Package.cs 文件的文本模板文件中更新该特性。

#### <a name="to-update-the-packagett-file"></a>更新 Package.tt 文件

1. 在**解决方案资源管理器**的 " **DslPackage** " 项目的 " **GeneratedCode** " 文件夹中，打开 Package.tt 文件。

2. 查找 `ProvideMenuResource` 特性。

3. 递增特性的 `version` 参数，它是第二个参数。 如果需要，你可以显式编写参数名称以提醒你它的用途。 例如：

     `[VSShell::ProvideMenuResource("1000.ctmenu", version: 2 )]`

## <a name="CommandSet"></a>定义命令的行为
 DSL 已具有一些在 DslPackage\GeneratedCode\CommandSet.cs 中声明的分部类中实现的命令。 若要添加新命令，你必须通过创建包含同一个类的分部声明的新文件来扩展此类。 该类的名称通常是 *\<e >* `CommandSet`。 这将有助于通过验证该类的名称以及检查其内容来开始操作。

 命令集类派生自 <xref:Microsoft.VisualStudio.Modeling.Shell.CommandSet>。

#### <a name="to-extend-the-commandset-class"></a>扩展 CommandSet 类

1. 在“解决方案资源管理器”中，在 DslPackage 项目中打开 GeneratedCode 文件夹，然后在 CommandSet.tt 下进行查找并打开其生成的文件 CommandSet.cs。 注意在此处定义的第一个类的命名空间和名称。 例如，你可能看到：

     `namespace Company.Language1`

     `{ ...  internal partial class Language1CommandSet : ...`

2. 在**DslPackage**中，创建一个名为 "**自定义代码**" 的文件夹。 在此文件夹中，创建一个名为 `CommandSet.cs`的新类文件。

3. 在该新文件中，编写具有与生成的分部类相同的命名空间和名称的分部声明。 例如：

     `namespace Company.Language1 /* Make sure this is correct */`

     `{ internal partial class Language1CommandSet { ...`

     **注意**如果使用类模板创建新文件，则必须更正命名空间和类名。

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
 对于每个命令，定义一个 `OnStatus...` 方法，该方法确定命令是否将显示在菜单上，以及是启用还是灰显。设置 `MenuCommand`的 `Visible` 和 `Enabled` 属性，如下面的示例中所示。 每次用户右键单击关系图时，都将调用此方法以构造快捷菜单，因此它必须尽快工作。

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

- `this.CurrentSelection`。 用户右键单击的形状始终包含在此列表中。 如果用户单击关系图的空白部分，则“关系图”是该列表中的唯一成员。

- 如果用户单击了关系图的空白部分，则 `this.IsDiagramSelected()` - `true`。

- `this.IsCurrentDiagramEmpty()`

- `this.IsSingleSelection()`-用户未选择多个对象

- `this.SingleSelection`-用户右键单击的形状或关系图

- `shape.ModelElement as MyLanguageElement`-形状表示的模型元素。

  一般原则是，使 `Visible` 属性依赖于所选定的内容，并使 `Enabled` 属性依赖于选定元素的状态。

  OnStatus 方法不应更改“存储”的状态。

### <a name="define-what-the-command-does"></a>定义命令可执行操作
 对于每个命令，定义在用户单击菜单命令时执行所需操作的 `OnMenu...` 方法。

 如果要对模型元素进行更改，则必须在事务内执行此操作。 有关详细信息，请参阅[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。

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

 有关如何在模型中从对象导航到对象以及如何创建对象和链接的详细信息，请参阅[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)。

### <a name="register-the-command"></a>注册命令
 在 C# 中重复在 CommandSet.vsct 的“符号”部分中进行的 GUID 和 ID 值的声明：

```
private Guid guidCustomMenuCmdSet =
    new Guid("00000000-0000-0000-0000-000000000000");
private const int grpidMyMenuGroup = 0x01001;
private const int cmdidMyContextMenuCommand = 1;
```

 使用与 **.vsct**中插入的 GUID 相同的值。

> [!NOTE]
> 如果更改 VSCT 文件的“符号”部分，还必须更改这些要匹配的声明。 还应在 Package.tt 中递增版本号

 将菜单命令注册为此命令集的一部分。 初始化关系图后，将调用 `GetMenuCommands()` 一次：

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

1. 在**解决方案资源管理器**工具栏上，单击 "**转换所有模板**"。

2. 按**F5**重新生成解决方案，并在实验生成中开始调试域特定语言。

3. 在实验性生成中，打开示例关系图。

4. 在关系图中右键单击各种项，以验证命令是否根据所选择的项正确启用或禁用，以及是否相应地显示或隐藏。

## <a name="troubleshooting"></a>故障排除
 **命令未显示在菜单中：**

- 除非安装 DSL 包，否则命令将只显示在 Visual Studio 的调试实例中。 有关详细信息，请参阅[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)。

- 确保实验性示例具有此 DSL 的正确文件扩展名。 若要检查该文件扩展名，请在 Visual Studio 的主实例中打开 DslDefinition.dsl。 随后，在 DSL 资源管理器中，右键单击“编辑器”节点，然后单击“属性”。 在“属性”窗口中，检查 FileExtension 属性。

- 是否[递增了包版本号](#version)？

- 在 OnStatus 方法的开头设置断点。 在右键单击关系图的任意部分时，应发生中断。

   **不调用 OnStatus 方法**：

  - 确保 CommandSet 代码中的 GUID 和 ID 匹配 Commands.vsct 的“符号”部分中的 GUID 和 ID。

  - 在 Commands.vsct 中，确保每个“父”节点中的 GUID 和 ID 标识正确的父“组”。

  - 在 Visual Studio 命令提示符中，键入 devenv /rootsuffix exp /setup。 然后，重新启动 Visual Studio 的调试实例。

- 逐步执行 OnStatus 方法，以验证 command.Visible 和 command.Enabled 是否设置为 True。

  **出现错误的菜单文本，或命令出现在错误的位置**：

- 确保 GUID 和 ID 的组合对此命令是唯一的。

- 确保已卸载早期版本的程序包。

## <a name="see-also"></a>请参阅
 [编写代码以定制域特定语言](../modeling/writing-code-to-customise-a-domain-specific-language.md)[如何：修改标准菜单命令](../modeling/how-to-modify-a-standard-menu-command-in-a-domain-specific-language.md)[部署域特定语言解决方案](../modeling/deploying-domain-specific-language-solutions.md)
