---
title: 将 UML 关系图导出到图像文件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: b29ce2a5-0ee3-4ab7-9aa3-13ca9c6b37a2
caps.latest.revision: 10
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 782d5da27898de7a332824e6fb07842710ab0656
ms.sourcegitcommit: 2da366ba9ad124366f6502927ecc720985fc2f9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68871845"
---
# <a name="export-uml-diagrams-to-image-files"></a>将 UML 关系图导出至图像文件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

可以将 UML 文档从[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]导出到程序控制下的映像。 例如，你可能希望将此操作作为自动文档生成的一部分加以执行。

 如果想要手动将文档导出为图像，则可以将一个关系图中的形状复制并粘贴到诸如 Word 这样的其他程序中。 还可以将文档打印为 XPS 格式。 有关详细信息, 请参阅将[关系图导出为图像](../modeling/export-diagrams-as-images.md)。

## <a name="saving-an-image"></a>保存图像
 下面的代码定义了一个用于将图像保存到文件的快捷菜单命令（也称为上下文菜单命令）。

> [!NOTE]
> 若要使此代码以菜单命令方式工作，必须将其合并到 MEF 组件。 有关详细信息, 请参阅[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)。

 代码优先使用[IShape](/previous-versions/ee789371(v=vs.140))获取<xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram>基础实现的。 此类型具有 <xref:Microsoft.VisualStudio.Modeling.Diagrams.Diagram.CreateBitmap%2A> 方法。

```
namespace SaveToImage
{
  using System.ComponentModel.Composition; // for [Import], [Export]
  using System.Drawing; // for Bitmap
  using System.Drawing.Imaging; // for ImageFormat
  using System.Linq; // for collection extensions
  using System.Windows.Forms; // for SaveFileDialog
  using Microsoft.VisualStudio.Modeling.Diagrams;
    // for Diagram
  using Microsoft.VisualStudio.Modeling.ExtensionEnablement;
    // for IGestureExtension, ICommandExtension, ILinkedUndoContext
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Presentation;
    // for IDiagramContext
  using Microsoft.VisualStudio.ArchitectureTools.Extensibility.Uml;
    // for designer extension attributes

  /// <summary>
  /// Called when the user clicks the menu item.
  /// </summary>
  // Context menu command applicable to any UML diagram
  [Export(typeof(ICommandExtension))]
  [ClassDesignerExtension]
  [UseCaseDesignerExtension]
  [SequenceDesignerExtension]
  [ComponentDesignerExtension]
  [ActivityDesignerExtension]
  class CommandExtension : ICommandExtension
  {
    [Import]
    IDiagramContext Context { get; set; }

    public void Execute(IMenuCommand command)
    {
      // Get the diagram of the underlying implementation.
      Diagram dslDiagram = Context.CurrentDiagram.GetObject<Diagram>();
      if (dslDiagram != null)
      {
        string imageFileName = FileNameFromUser();
        if (!string.IsNullOrEmpty(imageFileName))
        {
          Bitmap bitmap = dslDiagram.CreateBitmap(
           dslDiagram.NestedChildShapes,
           Diagram.CreateBitmapPreference.FavorClarityOverSmallSize);
          bitmap.Save(imageFileName, GetImageType(imageFileName));
        }
      }
    }

    /// <summary>
    /// Called when the user right-clicks the diagram.
    /// Set Enabled and Visible to specify the menu item status.
    /// </summary>
    /// <param name="command"></param>
    public void QueryStatus(IMenuCommand command)
    {
      command.Enabled = Context.CurrentDiagram != null
        && Context.CurrentDiagram.ChildShapes.Count() > 0;
    }

    /// <summary>
    /// Menu text.
    /// </summary>
    public string Text
    {
      get { return "Save To Image..."; }
    }

    /// <summary>
    /// Ask the user for the path of an image file.
    /// </summary>
    /// <returns>image file path, or null</returns>
    private string FileNameFromUser()
    {
      SaveFileDialog dialog = new SaveFileDialog();
      dialog.AddExtension = true;
      dialog.DefaultExt = "image.bmp";
      dialog.Filter = "Bitmap ( *.bmp )|*.bmp|JPEG File ( *.jpg )|*.jpg|Enhanced Metafile (*.emf )|*.emf|Portable Network Graphic ( *.png )|*.png";
      dialog.FilterIndex = 1;
      dialog.Title = "Save Diagram to Image";
      return dialog.ShowDialog() == DialogResult.OK ? dialog.FileName : null;
    }

    /// <summary>
    /// Return the appropriate image type for a file extension.
    /// </summary>
    /// <param name="fileName"></param>
    /// <returns></returns>
    private ImageFormat GetImageType(string fileName)
    {
      string extension = System.IO.Path.GetExtension(fileName).ToLowerInvariant();
      ImageFormat result = ImageFormat.Bmp;
      switch (extension)
      {
        case ".jpg":
          result = ImageFormat.Jpeg;
          break;
        case ".emf":
          result = ImageFormat.Emf;
          break;
        case ".png":
          result = ImageFormat.Png;
          break;
      }
      return result;
    }
  }
}
```

## <a name="see-also"></a>请参阅
 将[关系图导出为图像](../modeling/export-diagrams-as-images.md)[在建模图上定义菜单命令](../modeling/define-a-menu-command-on-a-modeling-diagram.md)
