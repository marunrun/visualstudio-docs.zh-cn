---
title: 如何：创建基于 XSD 架构的 XML 文档 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 193b195f-e918-4c79-a1a1-8096a1433bde
caps.latest.revision: 9
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 623da37807e0fd61041bfeb9ab411ce0cb96d4b5
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68164487"
---
# <a name="how-to-create-an-xml-document-based-on-an-xsd-schema"></a>如何：基于 XSD 架构创建 XML 文档
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**生成示例 XML**功能生成基于 XML 架构 (XSD) 文件的示例 XML 文件。  
  
 可以在下列情况下使用此选项：  
  
- 了解架构中各个构造的使用情况。  
  
- 确认架构发挥了应有的作用。  
  
  **生成示例 XML**功能仅对全局元素可用，并且需要有效的 XML 架构集。  
  
  此功能通常会生成有效的 XML 文档。 但是，如果架构包含下列一项或多项内容，示例可能无效：  
  
- `xs:key`、`xs:keyref` 和 `xs:unique` 标识约束。  
  
- `xs:pattern` 方面。  
  
- `xs:QName` 类型的枚举。  
  
- `xs:ENTITY`、`xs:ENTITIES` 和 `xs:NOTATION` 类型。  
  
  另请注意，只有当架构中发生 `xs:base64Binary` 类型的枚举时，才会生成同类型的内容。  
  
### <a name="to-generate-an-xml-instance-document-based-on-the-xsd-file"></a>基于 XSD 文件生成 XML 实例文档  
  
1. 按照中的步骤[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)。  
  
2. 在中[XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)，右键单击`PurchaseOrder`全局元素。 选择**生成示例 XML**。  
  
     在您选择此选项后，将生成使用以下示例 XML 内容的 PurchaseOrder.xml 文件并在“XML 编辑器”中打开该文件：  
  
    ```  
    <?xml version="1.0" encoding="utf-8"?>  
    <PurchaseOrder OrderDate="1900-01-01" xmlns="http://tempuri.org/PurchaseOrderSchema.xsd">  
      <ShipTo country="US">  
        <name>name1</name>  
        <street>street1</street>  
        <city>city1</city>  
        <state>state1</state>  
        <zip>1</zip>  
      </ShipTo>  
      <ShipTo country="US">  
        <name>name2</name>  
        <street>street2</street>  
        <city>city2</city>  
        <state>state2</state>  
        <zip>-79228162514264337593543950335</zip>  
      </ShipTo>  
      <BillTo country="US">  
        <name>name1</name>  
        <street>street1</street>  
        <city>city1</city>  
        <state>state1</state>  
        <zip>1</zip>  
      </BillTo>  
    </PurchaseOrder>  
    ```  
  
## <a name="see-also"></a>请参阅  
 [使用 XML 数据](../xml-tools/working-with-xml-data.md)
