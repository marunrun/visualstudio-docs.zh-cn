---
title: 如何：将架构映射到 Visual Studio 内部的 Word 文档
titleSuffix: ''
ms.custom: seodec18
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- XML schemas [Office development in Visual Studio], mapping
- mappings [Office development in Visual Studio], XML schemas to Word documents
- Word [Office development in Visual Studio], mapping XML schemas
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 4c6f9ee9a7b636c6c12bfe2f8debcc05911e3b04
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63441757"
---
# <a name="how-to-map-schemas-to-word-documents-inside-visual-studio"></a>如何：将架构映射到 Visual Studio 内部的 Word 文档
  **重要**设置 Microsoft Word 有关本主题中的信息是提供的以独占方式适合的权益和使用个人和组织用户位于美国州和其领土的外部或使用，或开发运行的程序，在 2010 年 1 月，Microsoft 中删除的特定功能实现的时间之前已由 Microsoft 许可的 Microsoft Word 产品被与 Microsoft Word 中的自定义 XML。 有关 Microsoft Word 此信息可能不读取或使用的个人或组织在美国或其区域使用，或开发在 Microsoft Word 2010 年 1 月 10 日之后，由 Microsoft 已许可的产品运行的程序中;这些产品不将行为与相同产品许可在该日期之前或购买，美国以外的使用许可。

 [!INCLUDE[appliesto_wdalldoc](../vsto/includes/appliesto-wdalldoc-md.md)]

 在 Visual Studio 中打开文档时，可以将 XML 架构映射到文档中。 使用 Visual Studio 外部打开文档时使用的相同 Microsoft Office Word 工具。 Office 项目创建相同的对象是否将架构映射到文档之前或之后创建 Word 解决方案。

## <a name="to-map-an-xml-schema-to-a-word-document-in-visual-studio"></a>若要将 XML 架构映射到 Visual Studio 中的 Word 文档

1. 打开 Visual Studio 内部的 Word 文档或模板项目。

2. 单击要将焦点移到设计器中的文档中。

3. 在功能区中，单击**开发人员**选项卡。

    > [!NOTE]
    > 如果看不到 **“开发人员”** 选项卡，则必须首先显示它。 有关详细信息，请参阅[如何：功能区上显示开发人员选项卡](../vsto/how-to-show-the-developer-tab-on-the-ribbon.md)。

4. 在中**XML**组中，单击**架构**。

     **模板和外接程序**对话框随即打开。

5. 单击**XML 架构**选项卡。

6. 单击**将架构添加**。

     **添加架构**对话框随即打开。

7. 浏览到您的架构文件，选择它，，然后单击**打开**。

     **架构设置**对话框随即打开。

8. 分配一个别名，或单击**确定**添加不带别名的架构。

9. 单击 **“确定”**。

     **XML 结构**窗口随即打开。

10. 将元素从拖动**XML 结构**窗口到想要创建的相应控件在文档中的位置。

## <a name="see-also"></a>请参阅
- [如何：将架构映射到 Visual Studio 内部的工作表](../vsto/how-to-map-schemas-to-worksheets-inside-visual-studio.md)
- [XML 架构和文档级自定义项中的数据](../vsto/xml-schemas-and-data-in-document-level-customizations.md)
