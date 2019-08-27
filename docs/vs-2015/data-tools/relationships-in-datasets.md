---
title: 数据集中的关系 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
f1_keywords:
- vbData.Microsoft.VSDesigner.DataSource.DesignRelation
- vbdata.Microsoft.VSDesigner.DataSource.DesignRelation
dev_langs:
- VB
- CSharp
- C++
- aspx
helpviewer_keywords:
- relationships, about relationships
- datasets [Visual Basic], relationships
- relationships, datasets
ms.assetid: cfe274f0-71fe-40f6-994e-7c7f6273c9ba
caps.latest.revision: 18
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 7f6aba4076f7532d5eab5d47515b734c4c312b99
ms.sourcegitcommit: 08fc78516f1107b83f46e2401888df4868bb1e40
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2019
ms.locfileid: "65692531"
---
# <a name="relationships-in-datasets"></a>数据集中的关系
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

包含相关的数据的数据集表，表使用<xref:System.Data.DataRelation>对象来表示表之间的父/子关系，并从另一个返回相关的记录。 通过将相关的表添加到数据集**数据源配置向导**，或**数据集设计器**下创建并配置<xref:System.Data.DataRelation>为您的对象。  
  
 <xref:System.Data.DataRelation>对象执行两个功能：  
  
- 它可以提供与你正在使用的记录相关的记录。 它提供了子记录，如果你在父记录 (<xref:System.Data.DataRow.GetChildRows%2A>)，如果你正在使用子记录的父记录 (<xref:System.Data.DataRow.GetParentRow%2A>)。  
  
- 它可以强制执行约束的引用完整性，例如当删除父记录中删除相关的子记录。  
  
  务必要了解真正的联接的函数之间的区别<xref:System.Data.DataRelation>对象。 在真正的联接，记录处于取自父和子表，将放入单个的平面记录集。 当你使用<xref:System.Data.DataRelation>对象，创建新的记录集。 相反，DataRelation 跟踪的表之间的关系，并使父和子记录保持同步。  
  
## <a name="datarelation-objects-and-constraints"></a>DataRelation 对象和约束  
 一个<xref:System.Data.DataRelation>对象还用于创建和强制实施以下限制：  
  
- 唯一约束，这可确保表中的列包含没有重复项。  
  
- Foreign key 约束，可用于在数据集中的父和子表之间维护引用完整性。  
  
  在中指定的约束<xref:System.Data.DataRelation>对象实现通过自动创建相应的对象或设置属性。 如果您通过使用创建 foreign key 约束<xref:System.Data.DataRelation>对象、 实例的<xref:System.Data.ForeignKeyConstraint>类添加到<xref:System.Data.DataRelation>对象的<xref:System.Data.DataRelation.ChildKeyConstraint%2A>属性。  
  
  唯一约束实现只需设置<xref:System.Data.DataColumn.Unique%2A>数据列到属性`true`或通过添加的实例<xref:System.Data.UniqueConstraint>类来<xref:System.Data.DataRelation>对象的<xref:System.Data.DataRelation.ParentKeyConstraint%2A>属性。 在数据集中挂起约束的信息，请参阅[填充数据集时关闭约束](../data-tools/turn-off-constraints-while-filling-a-dataset.md)。  
  
### <a name="referential-integrity-rules"></a>引用完整性规则  
 作为外键约束的一部分，可以指定应用于三个点的引用完整性规则：  
  
- 更新父记录时  
  
- 删除父记录时  
  
- 当接受或拒绝更改  
  
  可在规则中指定<xref:System.Data.Rule>枚举并列出在下表中。  
  
|外键约束规则|操作|  
|----------------------------------|------------|  
|<xref:System.Data.Rule>|对父记录所做的更改 （更新或删除） 也由子表中的相关记录中。|  
|<xref:System.Data.Rule>|不删除子记录，但子记录中的外键设置为<xref:System.DBNull>。 可以使用此设置，保留子记录作为"孤立"— 即，它们具有与父记录没有关系。 **注意：** 使用此规则可以导致子表中的数据无效。|  
|<xref:System.Data.Rule>|相关的子记录中的外键设置为其默认值 (由列的建立<xref:System.Data.DataColumn.DefaultValue%2A>属性)。|  
|<xref:System.Data.Rule>|相关的子记录到不进行任何更改。 使用此设置时，子记录可以包含对无效的父记录的引用。|  
  
 数据集表中的更新的详细信息，请参阅[将数据保存回数据库](../data-tools/save-data-back-to-the-database.md)。  
  
### <a name="constraint-only-relations"></a>仅限约束的关系  
 当你创建<xref:System.Data.DataRelation>对象，你必须指定，关系仅用于强制执行约束的选项，即，它将不也用于访问相关的记录。 此选项可用于生成数据集略有更有效且包含较少的方法比具有相关记录功能。 但是，您将不能访问相关的记录。 例如，约束关系阻止你删除父记录仍包含子记录，并且不能通过父访问子记录。  
  
## <a name="manually-creating-a-data-relation-in-the-dataset-designer"></a>手动创建数据集设计器中的数据关系  
 当在 Visual Studio 中使用数据设计工具创建数据的表时，会自动创建关系如果可以从你的数据源收集的信息。 如果你手动添加从数据表**数据集**选项卡**工具箱**，可能需要手动创建关系。 有关创建信息<xref:System.Data.DataRelation>对象以编程方式，请参阅[添加 Datarelation](https://msdn.microsoft.com/library/a4a564fb-c1c4-4135-b6c2-b030e51195e4)。  
  
 数据的表之间的关系显示为行中**数据集设计器**，用来描述一个多方面的关系的键和无穷大标志符号。 默认情况下，relationshipCommentEnd Id 名称 ="1c8c78e19b7fa441"未显示在设计图面上。  
  
 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]  
  
#### <a name="to-create-a-relationship-between-two-data-tables"></a>若要创建的两个数据表之间的关系  
  
1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 拖动**关系**对象从**数据集**工具箱拖到关系中子数据的表。  
  
     **关系**对话框将打开，填充**子表**与您拖动表框**关系**拖到对象。  
  
3. 选择从父表**父表**框。 父表包含一个对多关系的"一"方上的记录。  
  
4. 验证正确的子表显示在**子表**框。 子表包含一个对多关系的"多"方上的记录。  
  
5. 键入的名称中的关系**名称**框中，或保留默认名称基于所选的表。 这是实际的名称<xref:System.Data.DataRelation>在代码中的对象。  
  
6. 选择联接中的表的列**键列**并**外键列**列出。  
  
7. 选择是否创建一个关系、 约束，或这两者。 有关信息，请参阅[DataRelation 对象介绍](https://msdn.microsoft.com/library/89d8a881-8265-41f2-a88b-61311ab06192)。  
  
8. 选中或清除**嵌套关系**框。 选择此选项设置<xref:System.Data.DataRelation.Nested%2A>属性设置为`true`，这将导致子行要以 XML 数据形式编写或与同步这些行时嵌套在父列的关系的<xref:System.Xml.XmlDataDocument>。 有关详细信息，请参阅[嵌套 Datarelation](https://msdn.microsoft.com/library/9530f9c9-dd98-4b93-8cdb-40d7f1e8d0ab)。  
  
9. 设置对这些表中的记录进行更改时要强制实施的规则。 有关详细信息，请参阅 <xref:System.Data.Rule>。  
  
10. 单击**确定**来创建关系。 在两个表之间的设计器中显示的关系线。  
  
#### <a name="to-display-a-relation-name-in-the-dataset-designer"></a>若要在数据集设计器中显示的关系名称  
  
1. 在“数据集设计器”中打开数据集。 有关详细信息，请参阅[如何：在数据集设计器中打开数据集](https://msdn.microsoft.com/library/36fc266f-365b-42cb-aebb-c993dc2c47c3)。  
  
2. 从**数据**菜单中，选择**显示关系标签**命令以显示该关系名称。 清除该命令，以隐藏关系名称。
