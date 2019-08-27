---
title: 自定义属性窗口 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- Domain-Specific Language, Properties window
ms.assetid: b6658de5-4e85-4628-93b2-5cc12f63d25b
caps.latest.revision: 22
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 3e391e21ac16bdbee9fc2881b264f964a4b28cc0
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63433223"
---
# <a name="customizing-the-properties-window"></a>自定义“属性”窗口
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

您可以自定义外观和行为的属性窗口中你的域特定语言 (DSL) 中[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。 在 DSL 定义中，每个域类上定义域属性。 默认情况下，选择关系图上或在模型资源管理器中的类的实例时每个域的属性已列出在属性窗口中。 这样可以查看和编辑域属性的值即使您有不到关系图上的形状字段映射它们。  
  
## <a name="names-descriptions-and-categories"></a>名称、 说明和类别  
 **名称和显示名称**。 在域属性的定义中，该属性的显示名称是在运行时在属性窗口中显示的名称。 与此相反，编写程序代码来更新属性时使用的名称。 名称必须是正确的 CLR 字母数字名称，但显示名称可以包含空格。  
  
 当在 DSL 定义中设置属性的名称时，其显示名称是自动设置为该名称的副本。 如果要编写一个采用 Pascal 大小写格式的名称，例如"FuelGauge"，显示名称将自动包含空格："汽油表"。 但是，可以为其他值显式设置显示名称。  
  
 **说明**。 域属性的说明将显示在两个位置：  
  
- 底部的属性窗口时用户选择的属性。 可用于向用户说明该属性表示。  
  
- 在生成的程序代码中。 如果您使用的文档功能来提取 API 文档，它将显示为此属性在 API 中的说明。  
  
  **Category**。 类别是属性窗口中的标题。  
  
## <a name="exposing-style-features"></a>公开样式功能  
 可以表示某些图形元素的动态功能或*公开*作为域的属性。 可以由用户更新已以这种方式公开的功能，可以详细轻松地更新程序代码。  
  
 右键单击 DSL 定义中的形状类、 指向**公开添加**，然后选择一项功能。  
  
 在形状上可以公开**FillColor**， **OutlineColor**， **TextColor**， **OutlineDashStyle**， **OutlineThickness**并**FillGradientMode**属性。 有关连接器可以公开**颜色**`,`**TextColor**， **DashStyle**，并且**粗细**属性。 在关系图上可以公开**FillColor**并**TextColor**属性。  
  
## <a name="forwarding-displaying-properties-of-related-elements"></a>转发：显示相关元素的属性  
 时 DSL 的用户在模型中选择一个元素，该元素的属性将显示在属性窗口中。 但是，您还可以显示指定的相关元素的属性。 这是很有用，如果已定义一起工作的一组元素。 例如，可以定义主要元素和可选的插件元素。 如果主要元素映射到一个形状，另一个则不是很有用，若要查看其所有属性，就好像在上一个元素。  
  
 这种效果名为*属性转发*，并在几个情况下自动发生。 在其他情况下，可以通过定义的域类型描述符转发的属性来实现。  
  
### <a name="default-property-forwarding-cases"></a>默认属性转发情况  
 当用户在资源管理器中选择一个形状或连接器或一个元素时，在属性窗口中显示以下属性：  
  
- 模型元素，包括那些在基类中定义的域类定义的域属性。 例外情况是为其设置域属性**是可浏览**到`False`。  
  
- 通过具有多重性 0..1 关系链接的元素的名称。 这提供一种简便的方法来根据需要查看链接的元素，即使您未定义此关系的连接符映射。  
  
- 以元素为目标的嵌入关系的域属性。 由于通常不显式显示嵌入关系，这能让用户可以查看其属性。  
  
- 在所选的形状或连接线定义的域属性。  
  
### <a name="adding-property-forwarding"></a>添加属性转发  
 若要转发属性，您定义的域类型描述符。 如果您有两个域类之间的域关系，可以使用域类型描述符中的第二个域类的域属性的值的第一个类中设置域属性。 例如，如果有之间的关系**书籍**域类和一个**作者**域类，您可以使用的域类型说明符以使**名称**属性本书**作者**出现在属性窗口中，当用户选择一书。  
  
> [!NOTE]
> 当用户编辑模型时，属性转发会影响仅属性窗口。 它不接收类上定义的域属性。 如果你想要访问已转发的域属性在 DSL 定义的其他部分或在程序代码中，你必须访问转发元素。  
  
 以下过程假设已创建 DSL。 第一个几个步骤总结了系统必备组件。  
  
##### <a name="to-forward-a-property-from-another-element"></a>若要从另一个元素转发属性  
  
1. 创建[!INCLUDE[dsl](../includes/dsl-md.md)]解决方案，其中包含至少两个类，它们在此示例中称为**书籍**并**作者**。 应该有任意一种类型之间的关系**书籍**并**作者**。  
  
     源角色的重数 (站点中的角色**书籍**端) 应为 0..1 或 1..1，因此每个**书籍**有一个**作者**。  
  
2. 在中**DSL 资源管理器**，右键单击**书籍**域类，然后单击**添加新 DomainTypeDescriptor**。  
  
     一个名为节点**自定义属性描述符的路径**下显示**自定义类型描述符**节点。  
  
3. 右键单击**自定义类型描述符**节点，并单击**添加新 PropertyPath**。  
  
     新的属性路径将显示下**自定义属性描述符的路径**节点。  
  
4. 选择新的属性路径，然后在**属性**窗口中，将**属性的路径**到适当的模型元素的路径。  
  
     通过单击该属性右侧的向下箭头，可以编辑树视图中的路径。 有关域路径的详细信息，请参阅[域路径语法](../modeling/domain-path-syntax.md)。 当你对其进行编辑时，路径应类似于**BookReferencesAuthor.Author/ ！作者**。  
  
5. 设置**属性**到**名称**域属性**作者**。  
  
6. 设置**显示名称**到**创作名称**。  
  
7. 转换所有模板、 生成并运行 DSL。  
  
8. 在模型图中，创建一本书，作者，并将它们使用引用关系链接。 选择的书元素，并在属性窗口中，您应看到作者姓名以及一书的属性。 更改链接作者的名称或链接到不同的作者，该书并观察一书的作者姓名发生更改。  
  
## <a name="custom-property-editors"></a>自定义属性编辑器  
 属性窗口中提供了相应编辑体验的类型的每个域属性的默认值。 例如，对于枚举类型时，用户看到的下拉列表，并对于数值属性，用户可以输入数字。 这是仅适用于内置类型。 如果指定外部类型，用户将能够看到该属性的值，但无法编辑它。  
  
 但是，可以指定以下编辑器和类型：  
  
1. 与标准的类型一起使用的另一个编辑器。 例如，可以指定一个字符串属性的文件路径编辑器。  
  
2. 有关域属性，并为其编辑器外部类型。  
  
3. 诸如文件路径编辑器中，或您的.NET 编辑器可以创建你自己的自定义属性编辑器。  
  
    外部类型和字符串，具有一个默认编辑器，如类型之间转换。  
  
   在 DSL 中，*外部类型*是任何类型，不是简单类型 （例如布尔值或 Int32） 或字符串之一。  
  
#### <a name="to-define-a-domain-property-that-has-an-external-type"></a>若要定义一个具有外部类型的域属性  
  
1. 在中**解决方案资源管理器**，添加对程序集 (DLL) 中包含的外部类型的引用**Dsl**项目。  
  
    程序集可以是.NET 程序集或您提供的程序集。  
  
2. 添加到类型**域类型**列表中，除非你已这样做。  
  
   1. 打开 DslDefinition.dsl，然后在**DSL 资源管理器**，右键单击根节点，然后单击**添加新的外部类型**。  
  
        在下，将出现一个新项**域类型**节点。  
  
       > [!WARNING]
       > 菜单项不是在 DSL 的根节点，**域类型**节点。  
  
   2. 在属性窗口中设置的名称和新类型的命名空间。  
  
3. 将域属性添加到域类，以通常的方式。  
  
    在属性窗口中，从下拉列表中选择的外部类型**类型**字段。  
  
   在此阶段，用户可以查看的属性的值，但它们不能编辑它。 显示的值从获取`ToString()`函数。 您可以编写程序代码设置的值的属性，例如在命令窗口或规则。  
  
### <a name="setting-a-property-editor"></a>设置属性编辑器  
 将 CLR 特性添加到域属性，采用以下形式：  
  
```  
[System.ComponentModel.Editor (  
   typeof(AnEditor),  
   typeof(System.Drawing.Design.UITypeEditor))]  
  
```  
  
 可以通过使用在属性上设置属性**自定义特性**属性窗口中的条目。  
  
 类型`AnEditor`必须派生自第二个参数中指定的类型。 第二个参数应为<xref:System.Drawing.Design.UITypeEditor>或<xref:System.ComponentModel.ComponentEditor>。 有关详细信息，请参阅 <xref:System.ComponentModel.EditorAttribute>。  
  
 你可以指定自己的编辑器或编辑器中提供[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)]，如<xref:System.Windows.Forms.Design.FileNameEditor>或<xref:System.Drawing.Design.ImageEditor>。 例如，使用以下过程以用户可在其中输入文件名称的属性。  
  
##### <a name="to-define-a-file-name-domain-property"></a>若要定义的文件名称的域属性  
  
1. 将域属性添加到 DSL 定义中的域类。  
  
2. 选择新的属性。 在中**自定义特性**字段属性窗口中，输入以下属性。 若要输入此属性，单击省略号 **[...]** 然后单独输入属性名称和参数：  
  
    ```  
    [System.ComponentModel.Editor (  
       typeof(System.Windows.Forms.Design.FileNameEditor)  
       , typeof(System.Drawing.Design.UITypeEditor))]  
  
    ```  
  
3. 将保留为默认设置域属性的类型**字符串**。  
  
4. 若要测试编辑器中，验证用户可以打开要编辑域属性的文件名称编辑器。  
  
    1. 按 ctrl+f5 或 F5。 在调试解决方案中，打开一个测试文件。 创建域类的元素，并选择它。  
  
    2. 在属性窗口中，选择域属性。 值字段显示一个省略号 **[...]**.  
  
    3. 单击省略号。 文件对话框。 选择一个文件并关闭对话框。 文件路径现在是域属性的值。  
  
### <a name="defining-your-own-property-editor"></a>定义属性编辑器  
 您可以定义自己的编辑器。 您可以实现此设置以允许用户编辑已定义的类型，或以特殊方式编辑标准类型。 例如，可以允许用户输入一个字符串，表示一个公式。  
  
 通过编写的类派生自定义编辑器<xref:System.Drawing.Design.UITypeEditor>。 您的类必须重写：  
  
- <xref:System.Drawing.Design.UITypeEditor.EditValue%2A>与用户交互和更新的属性值。  
  
- <xref:System.Drawing.Design.UITypeEditor.GetEditStyle%2A>指定是否在编辑器将打开一个对话框，或提供一个下拉列表菜单。  
  
  你还可以提供的图形表示形式将在属性网格中显示的属性的值。 若要执行此操作，重写`GetPaintValueSupported`，和`PaintValue`。  有关详细信息，请参阅 <xref:System.Drawing.Design.UITypeEditor>。  
  
> [!NOTE]
> 在单独的代码文件中添加代码**Dsl**项目。  
  
 例如：  
  
```  
internal class TextFileNameEditor : System.Windows.Forms.Design.FileNameEditor  
{  
  protected override void InitializeDialog(System.Windows.Forms.OpenFileDialog openFileDialog)  
  {  
    base.InitializeDialog(openFileDialog);  
    openFileDialog.Filter = "Text files(*.txt)|*.txt|All files (*.*)|*.*";  
    openFileDialog.Title = "Select a text file";  
  }  
}  
  
```  
  
 若要使用此编辑器，将**自定义特性**到域属性：  
  
```  
[System.ComponentModel.Editor (  
   typeof(MyNamespace.TextFileNameEditor)  
   , typeof(System.Drawing.Design.UITypeEditor))]  
  
```  
  
 有关详细信息，请参阅 <xref:System.Drawing.Design.UITypeEditor>。  
  
## <a name="providing-a-drop-down-list-of-values"></a>提供值下拉的列表  
 可以提供一系列可供选择的用户的值。  
  
> [!NOTE]
> 此方法提供了一系列可以在运行时更改的值。 如果你想要提供一个列表，其中不会更改，请考虑改为使用一个枚举的类型作为域属性的类型。  
  
 若要定义的标准值的列表，您将添加到域属性的 CLR 属性，具有以下形式：  
  
```  
[System.ComponentModel.TypeConverter   
(typeof(MyTypeConverter))]  
  
```  
  
 定义一个从 <xref:System.ComponentModel.TypeConverter> 派生的类。 在一个单独的文件中添加代码**Dsl**项目。 例如：  
  
```csharp  
/// <summary>  
/// Type converter that provides a list of values   
/// to be displayed in the property grid.  
/// </summary>  
/// <remarks>This type converter returns a list   
/// of the names of all "ExampleElements" in the   
/// current store.</remarks>  
public class MyTypeConverter : System.ComponentModel.TypeConverter  
{  
  /// <summary>  
  /// Return true to indicate that we return a list of values to choose from  
  /// </summary>  
  /// <param name="context"></param>  
  public override bool GetStandardValuesSupported  
    (System.ComponentModel.ITypeDescriptorContext context)  
  {  
    return true;  
  }  
  
  /// <summary>  
  /// Returns true to indicate that the user has   
  /// to select a value from the list  
  /// </summary>  
  /// <param name="context"></param>  
  /// <returns>If we returned false, the user would   
  /// be able to either select a value from   
  /// the list or type in a value that is not in the list.</returns>  
  public override bool GetStandardValuesExclusive  
      (System.ComponentModel.ITypeDescriptorContext context)  
  {  
    return true;  
  }  
  
  /// <summary>  
  /// Return a list of the values to display in the grid  
  /// </summary>  
  /// <param name="context"></param>  
  /// <returns>A list of values the user can choose from</returns>  
  public override StandardValuesCollection GetStandardValues  
      (System.ComponentModel.ITypeDescriptorContext context)  
  {  
    // Try to get a store from the current context  
    // "context.Instance"  returns the element(s) that   
    // are currently selected i.e. whose values are being  
    // shown in the property grid.   
    // Note that the user could have selected multiple objects,   
    // in which case context.Instance will be an array.  
    Store store = GetStore(context.Instance);  
  
    List<string> values = new List<string>();  
  
    if (store != null)  
    {  
      values.AddRange(store.ElementDirectory  
        .FindElements<ExampleElement>()  
        .Select<ExampleElement, string>(e =>   
      {  
        return e.Name;  
      }));  
    }  
    return new StandardValuesCollection(values);  
  }  
  
  /// <summary>  
  /// Attempts to get to a store from the currently selected object(s)  
  /// in the property grid.  
  /// </summary>  
  private Store GetStore(object gridSelection)  
  {  
    // We assume that "instance" will either be a single model element, or   
    // an array of model elements (if multiple items are selected).  
  
    ModelElement currentElement = null;  
  
    object[] objects = gridSelection as object[];  
    if (objects != null && objects.Length > 0)  
    {  
      currentElement = objects[0] as ModelElement;  
    }  
    else  
    {  
        currentElement = gridSelection as ModelElement;  
    }  
  
    return (currentElement == null) ? null : currentElement.Store;  
  }  
  
}  
  
```  
  
## <a name="see-also"></a>请参阅  
 [在程序代码中导航和更新模型](../modeling/navigating-and-updating-a-model-in-program-code.md)
