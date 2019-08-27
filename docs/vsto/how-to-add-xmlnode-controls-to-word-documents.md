---
title: 如何：向 Word 文档添加 XMLNode 控件
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XMLNode control, adding to documents
- controls [Office development in Visual Studio], adding to documents
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f0f849088a2c3cc726adc6054aef1ff7a7c1c52f
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63427410"
---
# <a name="how-to-add-xmlnode-controls-to-word-documents"></a>如何：向 Word 文档添加 XMLNode 控件
  **重要**设置 Microsoft Word 有关本主题中的信息是提供的以独占方式适合的权益和使用个人和组织用户位于美国州和其领土的外部或使用，或开发运行的程序，在 2010 年 1 月，Microsoft 中删除的特定功能实现的时间之前已由 Microsoft 许可的 Microsoft Word 产品被与 Microsoft Word 中的自定义 XML。 有关 Microsoft Word 此信息可能不读取或使用的个人或组织在美国或其区域使用，或开发在 Microsoft Word 2010 年 1 月 10 日之后，由 Microsoft 已许可的产品运行的程序中;这些产品不将行为与相同产品许可在该日期之前或购买，美国以外的使用许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 当非重复的 XML 架构元素映射到 Microsoft Office Word 文档时，Visual Studio 会自动添加<xref:Microsoft.Office.Tools.Word.XMLNode>到你的文档的控件。 有关映射重复的 XML 架构元素的信息，请参阅[如何：向 Word 文档添加 XMLNodes 控件](../vsto/how-to-add-xmlnodes-controls-to-word-documents.md)。

> [!NOTE]
> <xref:Microsoft.Office.Tools.Word.XMLNode>控件不是从可用**工具箱**或**数据源**不能以编程方式创建窗口中，和它。

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-add-an-xmlnode-control-to-a-document"></a>若要向文档添加 XMLNode 控件

1. 在 Visual Studio 设计器中，在功能区中，在文档中，单击**开发人员**选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅[如何：功能区上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

2. 在中**XML**组中，单击**架构**。

     **模板和外接程序**对话框随即打开。

3. 单击**XML 架构**选项卡。

4. 单击**将架构添加**。

     **添加架构**对话框随即打开。

5. 选择包含中的非重复架构元素的 XML 架构**添加架构**对话框中，单击**打开**。

     **架构设置**对话框随即出现。

6. 分配一个别名，或单击**确定**添加不带别名的架构。

     该架构添加到**添加架构**对话框。

7. 在中**添加架构**对话框中，单击**确定**。

8. **XML 结构**任务窗格随即打开。

9. 单击的非重复架构元素**XML 结构**任务窗格，以将其添加到文档。

     <xref:Microsoft.Office.Tools.Word.XMLNode>控件被创建并添加到项目。

## <a name="see-also"></a>请参阅
- [XMLNode 控件](../vsto/xmlnode-control.md)
- [通过使用扩展的对象自动化 Word](../vsto/automating-word-by-using-extended-objects.md)
- [主机项和主机控件概述](../vsto/host-items-and-host-controls-overview.md)
- [主机项和主机控件的编程限制](../vsto/programmatic-limitations-of-host-items-and-host-controls.md)
