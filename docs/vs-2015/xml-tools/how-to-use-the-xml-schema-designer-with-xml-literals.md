---
title: 如何：将 XML 架构设计器与 XML 文本一起使用 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a9e82cf8387756cb4a4abe8b4c41d082485cdcdc
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72656296"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>如何：将 XML 架构设计器用于 XML 文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题描述如何查看与 Visual Basic 项目中的 XML 文本关联的架构。

### <a name="to-create-a-new-visual-basic-console-application-project"></a>创建新的 Visual Basic 控制台应用程序项目

1. 启动 Visual Studio 2010。

2. 从 "**文件**" 菜单中选择 "**新建**"，然后选择 "**项目**"。 此时将出现“新建项目”对话框。 对于 "**项目类型**"，请选择 **"其他语言"，** 然后选择 " **Visual Basic**"。 对于 "**模板**"，选择 "控制台应用程序"。 然后，在 "**名称**" 字段中键入 `XMLLiterals`，并在 "**位置**" 字段中键入项目位置。 单击“确定”。

     新项目创建完成。 XMLLiterals 项目包含一个 Visual Basic 源文件：Module1.vb。

### <a name="to-add-an-existing-xsd-file-to-the-project"></a>向项目中添加现有的 XSD 文件

1. 在记事本中打开一个新的文本文件。从[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)中复制 XML 架构示例代码，并将其粘贴到文件中。

2. 使用文件名 PurchaseOrderSchema.xsd 将文件保存到某个位置。

3. 在解决方案资源管理器中，右键单击项目的名称，选择 "**添加**"，然后选择 "**现有项 ...** "。 此时将显示 "**添加现有项**" 对话框。 浏览到 PurchaseOrderSchema 文件，选择它，然后单击 "**添加**"。

     XMLLiterals 项目现在包含两个文件：Module1.vb 和 PurchaseOrderSchema.xsd。

### <a name="to-add-visual-basic-code-with-an-xml-literal-based-on-the-xsd-file-included-in-the-project"></a>基于项目中包含的 XSD 文件添加带 XML 文本的 Visual Basic 代码

1. 用下面的代码替换 Module1.vb 文件中的代码：

    ```
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

     此时将并排显示 XML 架构资源管理器和带有与 XML 架构集关联的 XML 文本的 Visual Basic 文件。
