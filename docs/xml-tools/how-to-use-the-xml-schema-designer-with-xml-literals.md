---
title: 如何：将 XML 架构设计器用于 XML 文本
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: TerryGLee
ms.author: tglee
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: b4001e705cc69e07242abeeef5919573b264c5e8
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592654"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>如何：将 XML 架构设计器用于 XML 文本

本主题描述如何查看与 Visual Basic 项目中的 XML 文本关联的架构。

## <a name="create-a-new-visual-basic-project"></a>创建新的 Visual Basic 项目

1. 打开 Visual Studio。

2. 创建一个名为**XMLLiterals**的新 Visual Basic**控制台应用**项目。

     新项目包含一个 Visual Basic 源文件， *Module1*。

## <a name="add-an-existing-xsd-file"></a>添加现有的 XSD 文件

1. 在记事本中打开一个新的文本文件。 从[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)中复制 XML 架构示例代码，并将其粘贴到文件中。

2. 将该文件保存在一个名为*PurchaseOrderSchema*的位置。

3. 在**解决方案资源管理器**中，右键单击项目的名称，选择 "**添加**"，然后选择 "**现有项**"。 此时将显示 "**添加现有项**" 对话框。 浏览到*PurchaseOrderSchema*文件，选择它，然后单击 "**添加**"。

     XMLLiterals 项目现在包含两个文件： *Module1*和*PurchaseOrderSchema*。

## <a name="add-code"></a>添加代码

使用 XML 文本添加 Visual Basic 代码，基于项目中包含的 XSD 文件：

1. 将*Module1*文件中的代码替换为以下代码：

   ```vb
   Imports <xmlns:ns="http://tempuri.org/PurchaseOrderSchema.xsd">

   Module Module1
      Sub Main()

          Dim XMLLiteral = <ns:PurchaseOrder OrderDate="1900-01-01">
                               <ns:ShipTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:ShipTo>
                               <ns:BillTo country="US">
                                   <ns:name>name1</ns:name>
                                   <ns:street>street1</ns:street>
                                   <ns:city>city1</ns:city>
                                   <ns:state>state1</ns:state>
                                   <ns:zip>1</ns:zip>
                               </ns:BillTo>
                           </ns:PurchaseOrder>

      End Sub
   End Module
   ```

2. 右键单击 XML 文本或 XML 命名空间导入中的任何 XML 节点，然后选择 **"在架构资源管理器中显示"** 。

   **Xml 架构资源管理器**与具有与 xml 架构集关联的 xml 文本的 Visual Basic 文件并行显示。
