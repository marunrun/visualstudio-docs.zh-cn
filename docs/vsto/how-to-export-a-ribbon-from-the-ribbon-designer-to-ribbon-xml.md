---
title: 如何：将功能区从功能区设计器导出到功能区 XML
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom Ribbon, XML
- customizing the Ribbon, XML
- Ribbon [Office development in Visual Studio], XML
- Ribbon [Office development in Visual Studio], exporting
- XML [Office development in Visual Studio], Ribbon
- Ribbon Designer [Office development in Visual Studio]
- exporting Ribbon
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 57918e8a51a3948a2c69eb0c8ab5438b147e44f0
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/30/2020
ms.locfileid: "85543463"
---
# <a name="how-to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>如何：将功能区从功能区设计器导出到功能区 XML
  "**功能区（可视化设计器）** " 项不支持所有可能的功能区自定义项。 若要以高级方式自定义功能区，可以将功能区从设计器导出到功能区 XML，并直接编辑 XML。

> [!NOTE]
> 并非所有属性值都显示在功能区 XML 文件中。 有关详细信息，请参阅[功能区概述](../vsto/ribbon-overview.md)。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

### <a name="to-export-a-ribbon-from-the-ribbon-designer-to-ribbon-xml"></a>将功能区从功能区设计器导出到功能区 XML

1. 在**解决方案资源管理器**中右键单击功能区代码文件，然后单击 "**视图设计器**"。

2. 右键单击功能区设计器，然后单击 "**将功能区导出到 XML**"。

     Visual Studio 将功能区 XML 文件和功能区 XML 代码文件添加到项目。

3. 在功能区代码类中，找到以开头的注释 `TODO:` 。

4. 根据要开发的解决方案的类型，将这些注释中的代码块复制到**ThisAddin**、 **ThisWorkbook**或**ThisDocument**类中。

     此代码使 Microsoft Office 的应用程序能够发现和加载自定义功能区。 有关更多信息，请参见 [Ribbon XML](../vsto/ribbon-xml.md)。

5. 在**ThisAddin**、 **ThisWorkbook**或**ThisDocument**类中，取消注释代码块。

     取消注释代码后，它应与下面的示例类似。 在此示例中，调用了功能区类 `MyRibbon` 。

     [!code-csharp[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/CSharp/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.cs#1)]
     [!code-vb[Trin_Ribbon_Custom_Tab_XML#1](../vsto/codesnippet/VisualBasic/Trin_Ribbon_Custom_Tab_XML_O12/ThisAddIn.vb#1)]

6. 切换到功能区 XML 代码文件并查找 `Ribbon Callbacks` 区域。

     这是编写回调方法来处理用户操作（例如单击按钮）的位置。

7. 为在功能区设计器代码中编写的每个事件处理程序创建一个回调方法。

8. 将所有事件处理程序代码从事件处理程序移动到回调方法，并修改代码以使用功能区扩展性（RibbonX）编程模型。

     有关编写回调方法和使用 RibbonX 编程模型的信息，请参阅[功能区 XML](../vsto/ribbon-xml.md)。

## <a name="see-also"></a>另请参阅
- [功能区概述](../vsto/ribbon-overview.md)
- [功能区设计器](../vsto/ribbon-designer.md)
- [Ribbon XML](../vsto/ribbon-xml.md)
- [演练：使用功能区设计器创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-the-ribbon-designer.md)
- [演练：使用功能区 XML 创建自定义选项卡](../vsto/walkthrough-creating-a-custom-tab-by-using-ribbon-xml.md)
