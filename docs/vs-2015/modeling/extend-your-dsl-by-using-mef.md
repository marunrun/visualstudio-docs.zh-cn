---
title: 通过使用 MEF 扩展 DSL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: 3e7be79a-53ab-4d79-863a-bef8d27839bd
caps.latest.revision: 16
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: a1b90f37dcdadc53b6f2a81b9b4e9a860dd6a529
ms.sourcegitcommit: 7fbfb2a1d43ce72545096c635df2b04496b0be71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/09/2019
ms.locfileid: "67692522"
---
# <a name="extend-your-dsl-by-using-mef"></a>使用 MEF 扩展 DSL
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以通过使用 Managed Extensibility Framework (MEF) 扩展你的域特定语言 (DSL)。 您或其他开发人员将能够编写的 DSL 的扩展，而无需更改 DSL 定义和程序代码。 此类扩展包括菜单命令、 拖放处理程序和验证。 用户将能够安装 DSL，，然后根据需要为其安装扩展。  
  
 此外，启用时 MEF 在 DSL 中，可能会更轻松地编写的一些功能 DSL，即使它们是与 DSL。  
  
 有关 MEF 的详细信息，请参阅[Managed Extensibility Framework (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)。  
  
### <a name="to-enable-your-dsl-to-be-extended-by-mef"></a>若要启用由 MEF 扩展 DSL  
  
1. 创建一个名为的新文件夹**MefExtension**内**DslPackage**项目。 将以下文件添加到它：  
  
    文件名： `CommandExtensionVSCT.tt`  
  
   > [!IMPORTANT]
   > 在此文件以 GUID CommandSetId DslPackage\GeneratedCode\Constants.tt 中定义的相同设置 GUID  
  
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
  
    如果将此文件的添加，则必须启用验证在 DSL 中使用至少一个中的交换机**EditorValidation**在 DSL 资源管理器。  
  
   ```  
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
   <#@ include file="DslPackage\ValidationExtensionRegistrar.tt" #>  
   ```  
  
    文件名： `PackageExtensionEnablement.tt`  
  
   ```  
   <#@ Dsl processor="DslDirectiveProcessor" requires="fileName='..\..\Dsl\DslDefinition.dsl'" #>  
   <#@ include file="DslPackage\PackageExtensionEnablement.tt" #>  
   ```  
  
2. 创建一个名为的新文件夹**MefExtension**内**Dsl**项目。 将以下文件添加到它：  
  
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
  
3. 将以下行添加到名为现有文件**DslPackage\Commands.vsct**:  
  
   ```  
   <Include href="MefExtension\CommandExtensionVSCT.vsct"/>  
   ```  
  
    在现有之后插入行`<Include>`指令。  
  
4. `Open DslDefinition.dsl.`  
  
5. 在 DSL 资源管理器中选择**编辑器 \ 验证**。  
  
6. 在属性窗口中，请确保至少一个属性名为**使用...** 是`true`。  
  
7. 在解决方案资源管理器工具栏中，单击**转换所有模板**。  
  
    下面的每个文件添加显示附属文件。  
  
8. 生成并运行解决方案，以验证仍然正常工作。  
  
   你的 DSL 现已启用 MEF 的。 您可以编写作为 MEF 扩展的菜单命令、 笔势处理程序和验证约束。 您可以在 DSL 解决方案以及其他自定义代码中编写这些扩展。 此外，您或其他开发人员可以编写单独[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展 DSL 的扩展。  
  
## <a name="creating-an-extension-for-a-mef-enabled-dsl"></a>创建适用于启用了 MEF 的 DSL 扩展  
 如果你有权访问由自己或其他人创建的启用 MEF 的 DSL，你可以为其编写扩展。 扩展可用于添加菜单命令、 笔势处理程序或验证约束。 若要创作这些扩展，请使用[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]扩展 (VSIX) 解决方案。 该解决方案由两部分组成： 一个类库项目的生成代码的程序集，并打包程序集的 VSIX 项目。  
  
#### <a name="to-create-a-dsl-extension-vsix"></a>若要创建 DSL 扩展 VSIX  
  
1. 创建一个新类库项目。 若要执行此操作，在**新的项目**对话框中，选择**Visual Basic**或**Visual C#** ，然后选择**类库**。  
  
2. 新类库项目中，将添加到 DSL 的程序集的引用。  
  
   - 此程序集通常具有文件名结尾"。Dsl.dll"。  
  
   - 如果你有权访问 DSL 项目，可以找到程序集文件的目录下**Dsl\\bin\\\***  
  
   - 如果你有权访问的 DSL 的 VSIX 文件，您可以通过 VSIX 文件的文件扩展名更改为".zip"找到程序集。 解压缩.zip 文件。  
  
3. 添加以下.NET 程序集的引用：  
  
   - Microsoft.VisualStudio.Modeling.Sdk.11.0.dll  
  
   - Microsoft.VisualStudio.Modeling.Sdk.Diagrams.11.0.dll  
  
   - Microsoft.VisualStudio.Modeling.Sdk.Shell.11.0.dll  
  
   - System.ComponentModel.Composition.dll  
  
   - System.Windows.Forms.dll  
  
4. 在同一解决方案中创建一个 VSIX 项目。 若要执行此操作，在**新的项目**对话框框中，展开**Visual Basic**或**Visual C#** ，单击**扩展性**，然后选择**VSIX 项目**。  
  
5. 在解决方案资源管理器，右键单击 VSIX 项目，然后单击**设为启动项目**。  
  
6. 在新的项目中，打开**source.extension.vsixmanifest**。  
  
7. 单击**添加内容**。 在对话框中，将**内容类型**到**MEF 组件**，并**源项目**到你的类库项目。  
  
8. 添加到 DSL 的 VSIX 引用。  
  
   1. 在中**source.extension.vsixmanifest**，单击**添加引用**  
  
   2. 在对话框中，单击**添加负载**，然后查找的 DSL 的 VSIX 文件。 在 DSL 解决方案中生成的 VSIX 文件**DslPackage\\bin\\\*** 。  
  
       这允许用户在同时安装 DSL 和扩展。 如果用户已安装 DSL，则将安装你的扩展。  
  
9. 查看和更新的其他字段**source.extension.vsixmanifest**。 单击**选择版本**，并验证正确[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]设置版本。  
  
10. 将代码添加到类库项目。 下一节中使用这些示例作为指南。  
  
     可以添加任意数量的命令、 笔势和验证类。  
  
11. 若要测试此扩展，按**F5**。 在实验实例中的[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]，创建或打开的 DSL 的文件的示例。  
  
## <a name="writing-mef-extensions-for-dsls"></a>编写 MEF 扩展 Dsl  
 您可以在单独的 DSL 扩展解决方案的程序集代码项目中编写扩展。 此外可以在 DslPackage 项目中，使用 MEF，作为写入作为 DSL 的一部分的命令、 笔势和验证代码的简便方法。  
  
### <a name="menu-commands"></a>菜单命令  
 若要编写菜单命令，定义一个类，实现<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement.ICommandExtension>，并添加前缀具有名为在 DSL 中定义的属性的类*YourDsl*`CommandExtension`。 您可以编写多个菜单命令类。  
  
 `QueryStatus()` 每当用户右键单击关系图时调用。 它应检查当前所选内容和设置`command.Enabled`以指示该命令时适用。  
  
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
 笔势处理程序可以处理对象拖动到关系图上从任何位置，内部或外部[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 下面的示例使用户可以将文件从 Windows 资源管理器拖动到关系图上。 它将创建包含文件名称的元素。  
  
 可以编写处理程序来处理来自其他 DSL 模型和 UML 模型拖动的。 有关详细信息，请参阅[如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)。  
  
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
 验证方法被标记为通过`ValidationExtension`属性是由而生成的 DSL，还通过<xref:Microsoft.VisualStudio.Modeling.Validation.ValidationMethodAttribute>。 该方法可以出现在通过某个属性未标记任何类。  
  
 有关详细信息，请参阅[特定于域的语言中的验证](../modeling/validation-in-a-domain-specific-language.md)。  
  
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
 [传送 Visual Studio 扩展](../extensibility/shipping-visual-studio-extensions.md)   
 [托管可扩展性框架 (MEF)](https://msdn.microsoft.com/library/6c61b4ec-c6df-4651-80f1-4854f8b14dde)   
 [如何：添加拖放处理程序](../modeling/how-to-add-a-drag-and-drop-handler.md)   
 [域特定语言中的验证](../modeling/validation-in-a-domain-specific-language.md)
