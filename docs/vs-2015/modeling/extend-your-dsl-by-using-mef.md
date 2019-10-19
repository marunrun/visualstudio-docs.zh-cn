---
title: 使用 MEF 扩展 DSL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 3e7be79a-53ab-4d79-863a-bef8d27839bd
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: d3257acde8d3c62aca64e3401ec18134601973e5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669651"
---
# <a name="extend-your-dsl-by-using-mef"></a>使用 MEF 扩展 DSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

你可以使用 Managed Extensibility Framework （MEF）扩展域特定语言（DSL）。 你或其他开发人员将能够在不更改 DSL 定义和程序代码的情况下，为 DSL 编写扩展。 此类扩展包括菜单命令、拖放处理程序和验证。 用户可以安装 DSL，然后根据需要安装它的扩展。

 此外，当你在 DSL 中启用 MEF 时，你可以更轻松地编写 DSL 的某些功能，即使它们都与 DSL 一起生成。

 有关 MEF 的详细信息，请参阅[Managed Extensibility Framework （MEF）](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)。

### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>若要使 DSL 能够由 MEF 扩展

1. 在**DslPackage**项目中创建名为**MefExtension**的新文件夹。 将以下文件添加到其中：

    文件名： `CommandExtensionVSCT.tt`

   > [!IMPORTANT]
   > 将此文件中的 GUID 设置为与在 DslPackage\GeneratedCode\Constants.tt 中定义的 GUID CommandSetId 相同。

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#
   // CmdSet Guid must be defined before master template is included
   // This Guid must be kept synchronized with the CommandSetId Guid in Constants.tt
   Guid guidCmdSet = new Guid ("00000000-0000-0000-0000-000000000000");
   string menuidCommandsExtensionBaseId="0x4000";
   #>
   <#@ include file="DslPackage\CommandExtensionVSCT.tt" #>
   ```

    文件名： `CommandExtensionRegistrar.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="DslPackage\CommandExtensionRegistrar.tt" #>
   ```

    文件名： `ValidationExtensionEnablement.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="DslPackage\ValidationExtensionEnablement.tt" #>
   ```

    文件名： `ValidationExtensionRegistrar.tt`

    如果添加此文件，则必须在 dsl 资源管理器中使用**EditorValidation**中的至少一个开关在 dsl 中启用验证。

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>
   ```

    文件名： `PackageExtensionEnablement.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>
   ```

2. 在**Dsl**项目中创建名为**MefExtension**的新文件夹。 将以下文件添加到其中：

    文件名： `DesignerExtensionMetaDataAttribute.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="Dsl\DesignerExtensionMetadataAttribute.tt" #>
   ```

    文件名： `GestureExtensionEnablement.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="Dsl\GestureExtensionEnablement.tt" #>
   ```

    文件名： `GestureExtensionController.tt`

   ```
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>
   <#@ include file="Dsl\GestureExtensionController.tt" #>
   ```

3. 将以下行添加到名为**DslPackage\Commands.vsct**的现有文件：

   ```
   <Include href="MefExtension\CommandExtensionVSCT.vsct"/>
   ```

    在现有 `<Include>` 指令的后面插入行。

4. `Open DslDefinition.dsl.`

5. 在 DSL 资源管理器中，选择**编辑器 \ 验证**。

6. 在属性窗口中，确保至少有一个名为 "**使用 ...** " 的属性被 `true`。

7. 在解决方案资源管理器工具栏中，单击 "**转换所有模板**"。

    附属文件显示在你添加的每个文件的下方。

8. 生成并运行解决方案，验证它是否仍然正常工作。

   DSL 现在已启用 MEF。 可以将菜单命令、笔势处理程序和验证约束作为 MEF 扩展来编写。 可以在 DSL 解决方案中将这些扩展与其他自定义代码一起编写。 此外，你或其他开发人员可以编写扩展 DSL 的单独 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展。

## <a name="creating-an-extension-for-a-mef-enabled-dsl"></a>为启用 MEF 的 DSL 创建扩展
 如果有权访问自己或其他人创建的支持 MEF 的 DSL，可以为其编写扩展。 扩展可用于添加菜单命令、笔势处理程序或验证约束。 若要创作这些扩展，请使用 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 扩展（VSIX）解决方案。 此解决方案包含两部分：生成代码程序集的类库项目，以及打包程序集的 VSIX 项目。

#### <a name="to-create-a-dsl-extension-vsix"></a>创建 DSL 扩展 VSIX

1. 创建一个新类库项目。 为此，请在 "**新建项目**" 对话框中选择**Visual Basic**或**视觉C#对象**，然后选择 **"类库"。**

2. 在新的类库项目中，添加对 DSL 的程序集的引用。

   - 此程序集通常具有以 "结尾的名称。Dsl .dll "。

   - 如果有权访问 DSL 项目，可以在目录**DSL \\bin \\** 中找到程序集文件 \*

   - 如果有权访问 DSL VSIX 文件，可以通过将 VSIX 文件的文件扩展名更改为 ".zip" 来找到该程序集。 解压缩 .zip 文件。

3. 添加对以下 .NET 程序集的引用：

   - VisualStudio （& e）

   - VisualStudio. 11.0. 11.0。

   - VisualStudio. 11.0. 11.0。

   - System.ComponentModel.Composition.dll

   - System.Windows.Forms.dll

4. 在同一解决方案中创建 VSIX 项目。 为此，请在 "**新建项目**" 对话框中展开**Visual Basic**或**视觉C#对象**，单击 "**扩展性**"，然后选择 " **VSIX 项目**"。

5. 在解决方案资源管理器中，右键单击 VSIX 项目，然后单击 "**设为启动项目**"。

6. 在新项目中，打开**source.extension.vsixmanifest**。

7. 单击 "**添加内容**"。 在对话框中，将 "**内容类型**" 设置为 " **MEF 组件**"，将 "**源项目**" 设置为类库项目。

8. 向 DSL 添加 VSIX 引用。

   1. 在**source.extension.vsixmanifest**中，单击 "**添加引用**"

   2. 在对话框中，单击 "**添加有效负载**"，然后找到 DSL 的 VSIX 文件。 VSIX 文件是在 DSL 解决方案中构建的，在**DslPackage \\bin \\ \*** 。

       这允许用户同时安装 DSL 和你的扩展。 如果用户已安装 DSL，则仅安装你的扩展。

9. 查看并更新**source.extension.vsixmanifest**的其他字段。 单击 "**选择版本**" 并验证是否设置了正确的 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 版本。

10. 将代码添加到类库项目。 使用下一部分中的示例作为指南。

     可以添加任意数量的命令、笔势和验证类。

11. 若要测试扩展，请按**F5**。 在 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 的实验实例中，创建或打开 DSL 的示例文件。

## <a name="writing-mef-extensions-for-dsls"></a>编写 Dsl 的 MEF 扩展
 可以在单独的 DSL 扩展解决方案的程序集代码项目中编写扩展。 你还可以在 DslPackage 项目中使用 MEF，作为 DSL 的一部分，一种简便的方式来编写命令、手势和验证代码。

### <a name="menu-commands"></a>菜单命令
 若要编写菜单命令，请定义一个实现 <xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension> 的类，并为该类提供在 DSL 中定义的属性的前缀，名为*yourdsl 可*`CommandExtension`。 可以写入多个菜单命令类。

 只要用户右键单击关系图，就会调用 `QueryStatus()`。 它应检查当前所选内容，并将 `command.Enabled` 设置为指示命令的适用时间。

```
using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl; // My DSL
using Company.MyDsl.ExtensionEnablement; // My DSL
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement; // IVsSelectionContext
using Microsoft.VisualStudio.Modeling.ExtensionEnablement; // ICommandExtension

namespace MyMefExtension
{
  // Defined in Dsl\MefExtension\DesignerExtensionMetaDataAttribute.cs:
  [MyDslCommandExtension]
  public class MyCommandClass : ICommandExtension
  {
    /// <summary>
    /// Provides access to current document and selection.
    /// </summary>
    [Import]
    IVsSelectionContext SelectionContext { get; set; }

    /// <summary>
    /// Called when the user selects this command.
    /// </summary>
    /// <param name="command"></param>
    public void Execute(IMenuCommand command)
    {
      // Transaction is required if you want to update elements.
      using (Transaction t = SelectionContext.CurrentStore
              .TransactionManager.BeginTransaction("fix names"))
      {
        foreach (ExampleShape shape in SelectionContext.CurrentSelection)
        {
          ExampleElement element = shape.ModelElement as ExampleElement;
          element.Name = element.Name + " !";
        }
        t.Commit();
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines whether the command should appear.
    /// This method should set command.Enabled and command.Visible.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled =
        command.Visible = (SelectionContext.CurrentSelection.OfType<ExampleShape>().Count() > 0);
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Determines the text of the command in the menu.
    /// </summary>
    public string Text
    {
      get { return "My menu command"; }
    }
  }
}

```

### <a name="gesture-handlers"></a>笔势处理程序
 笔势处理程序可处理从 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 中的任何位置拖到关系图上的对象。 以下示例允许用户将文件从 Windows 资源管理器拖到关系图上。 它创建包含文件名的元素。

 您可以编写处理程序来处理其他 DSL 模型和 UML 模型中的拖动。 有关详细信息，请参阅[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)。

```

using System.ComponentModel.Composition;
using System.Linq;
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling; // Transactions
using Microsoft.VisualStudio.Modeling.Diagrams;
using Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.ExtensionEnablement;

namespace MefExtension
{
  [MyDslGestureExtension]
  class MyGestureExtension : IGestureExtension
  {
    public void OnDoubleClick(ShapeElement targetElement, DiagramPointEventArgs diagramPointEventArgs)
    {
      System.Windows.Forms.MessageBox.Show("double click!");
    }

    /// <summary>
    /// Called when the user drags anything over the diagram.
    /// Return true if the dragged object can be dropped on the current target.
    /// </summary>
    /// <param name="targetMergeElement">The shape or diagram that the mouse is currently over</param>
    /// <param name="diagramDragEventArgs">Data about the dragged element.</param>
    /// <returns></returns>
    public bool CanDragDrop(ShapeElement targetMergeElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      // This handler only allows items to be dropped onto the diagram:
      return targetMergeElement is MefDsl2Diagram &&
      // And only accepts files dragged from Windows Explorer:
        diagramDragEventArgs.Data.GetFormats().Contains("FileNameW");
    }

    /// <summary>
    /// Called when the user drops an item onto the diagram.
    /// </summary>
    /// <param name="targetDropElement"></param>
    /// <param name="diagramDragEventArgs"></param>
    public void OnDragDrop(ShapeElement targetDropElement, DiagramDragEventArgs diagramDragEventArgs)
    {
      MefDsl2Diagram diagram = targetDropElement as MefDsl2Diagram;
      if (diagram == null) return;

      // This handler only accepts files dragged from Windows Explorer:
      string[] draggedFileNames = diagramDragEventArgs.Data.GetData("FileNameW") as string[];
      if (draggedFileNames == null || draggedFileNames.Length == 0) return;

      using (Transaction t = diagram.Store.TransactionManager.BeginTransaction("file names"))
      {
        // Create an element to represent each file:
        foreach (string fileName in draggedFileNames)
        {
          ExampleElement element = new ExampleElement(diagram.ModelElement.Partition);
          element.Name = fileName;

          // This method of adding the new element allows the position
          // of the shape to be specified:
          ElementGroup group = new ElementGroup(element);
          diagram.ElementOperations.MergeElementGroupPrototype(
            diagram, group.CreatePrototype(), PointD.ToPointF(diagramDragEventArgs.MousePosition));
        }
        t.Commit();
      }
    }
  }
}

```

### <a name="validation-constraints"></a>验证约束
 验证方法由 DSL 生成的 `ValidationExtension` 特性标记，还由 <xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute> 标记。 方法可以出现在未由特性标记的任何类中。

 有关详细信息，请参阅[以域特定语言进行验证](../modeling/validation-in-a-domain-specific-language.md)。

```
using Company.MyDsl;
using Company.MyDsl.ExtensionEnablement;
using Microsoft.VisualStudio.Modeling.Validation;

namespace MefExtension
{
  class MyValidationExtension // Can be any class.
  {
    // SAMPLE VALIDATION METHOD.
    // All validation methods have the following attributes.

    // Specific to the extended DSL:
    [MyDslValidationExtension]

    // Determines when validation is applied:
    [ValidationMethod(
       ValidationCategories.Save
     | ValidationCategories.Open
     | ValidationCategories.Menu)]

    /// <summary>
    /// When validation is executed, this method is invoked
    /// for every element in the model that is an instance
    /// of the second parameter type.
    /// </summary>
    /// <param name="context">For reporting errors</param>
    /// <param name="elementToValidate"></param>
    private void ValidateClassNames
      (ValidationContext context,
       // Type determines to what elements this will be applied:
       ExampleElement elementToValidate)
    {
      // Write code here to test values and links.
      if (elementToValidate.Name.IndexOf(' ') >= 0)
      {
        // Log any unacceptable values:
        context.LogError(
          // Description:
          "Name must not contain spaces"
          // Error code unique to this type of error:
          , "MyDsl001"
          // Element to highlight when user double-clicks error:
          , elementToValidate);
} } } }

```

## <a name="see-also"></a>请参阅
 [随附 Visual Studio extension](../extensibility/shipping-visual-studio-extensions.md) [Managed Extensibility Framework （MEF）](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)如何：[在域特定语言中](../modeling/validation-in-a-domain-specific-language.md)[添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)验证
