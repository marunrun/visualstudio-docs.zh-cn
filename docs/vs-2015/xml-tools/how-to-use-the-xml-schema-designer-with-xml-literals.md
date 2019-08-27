---
title: 如何：用于 XML 文本使用 XML 架构设计器 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: d11803e7-f81a-41a2-a145-ba494a45cc93
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 05c32bfc6c3220739c433ef519b696953bc8b1b4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68190318"
---
# <a name="how-to-use-the-xml-schema-designer-with-xml-literals"></a>如何：将 XML 架构设计器用于 XML 文本
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

本主题描述如何查看与 Visual Basic 项目中的 XML 文本关联的架构。  
  
### <a name="to-create-a-new-visual-basic-console-application-project"></a>创建新的 Visual Basic 控制台应用程序项目  
  
1. 启动 Visual Studio 2010。  
  
2. 从**文件**菜单中，选择**新建**，然后选择**项目**。 此时将出现“新建项目”  对话框。 有关**项目类型**，选择**其他语言**，然后选择**Visual Basic**。 有关**模板**，选择控制台应用程序。 然后键入`XMLLiterals`中**名称**字段和中的项目位置**位置**字段。 单击 **“确定”** 。  
  
     新项目创建完成。 XMLLiterals 项目包含一个 Visual Basic 源文件：Module1.vb。  
  
### <a name="to-add-an-existing-xsd-file-to-the-project"></a>向项目中添加现有的 XSD 文件  
  
1. 打开一个新文本文件中 Notepad.Copy 中的 XML 架构示例代码[采购订单架构](../xml-tools/sample-xsd-file-simple-schema.md)并将其粘贴到该文件。  
  
2. 使用文件名 PurchaseOrderSchema.xsd 将文件保存到某个位置。  
  
3. 在解决方案资源管理器，右键单击项目的名称，选择**外**，然后选择**现有项...** . **添加现有项**对话框随即出现。 浏览到 PurchaseOrderSchema.xsd 文件，选择它，，然后单击**添加**。  
  
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
  
2. 右键单击 XML 文本或导入的 XML 命名空间中的任何 XML 节点并选择**在架构资源管理器中显示**。  
  
     此时将并排显示 XML 架构资源管理器和带有与 XML 架构集关联的 XML 文本的 Visual Basic 文件。
