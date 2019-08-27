---
title: 如何：将 XML 架构设计器用于 XML 文本
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
- VB
ms.workload:
- multiple
ms.openlocfilehash: 9e92cbdca3ac2c5c366ec054ba79f2e7324986c1
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001815"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>如何：结合使用 XML 架构设计器和 XML 文本

本主题描述如何查看与 Visual Basic 项目中的 XML 文本关联的架构。

## <a name="create-a-new-visual-basic-project"></a>创建新的 Visual Basic 项目

1. 打开 Visual Studio。

2. 创建一个新的 Visual Basic**控制台应用程序**名为项目**XMLLiterals**。

     新项目包含一个 Visual Basic 源文件*Module1.vb*。

## <a name="add-an-existing-xsd-file"></a>添加现有的 XSD 文件

1. 在记事本中打开新的文本文件。 中的 XML 架构示例代码复制[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)并将其粘贴到该文件。

2. 将文件保存在某个位置具有名称*PurchaseOrderSchema.xsd*。

3. 在中**解决方案资源管理器**，右键单击项目的名称，选择**添加**，然后选择**现有项**。 **添加现有项**对话框随即出现。 浏览到*PurchaseOrderSchema.xsd*文件中，选择它，，然后单击**添加**。

     XMLLiterals 项目现在包含两个文件：*Module1.vb*并*PurchaseOrderSchema.xsd*。

## <a name="add-code"></a>添加代码

若要添加 Visual Basic 代码与 XML 文本，基于项目中包含的 XSD 文件：

1. 中的代码替换*Module1.vb*文件使用以下代码：

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

2. 右键单击 XML 文本或导入的 XML 命名空间中的任何 XML 节点并选择**在架构资源管理器中显示**。

   **XML 架构资源管理器**具有 XML 文本与 XML 架构集相关联的 Visual Basic 文件将并排显示。