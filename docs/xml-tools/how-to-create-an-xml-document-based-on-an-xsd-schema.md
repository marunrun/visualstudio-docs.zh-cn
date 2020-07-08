---
title: 如何：基于 XSD 架构创建 XML 文档
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 193b195f-e918-4c79-a1a1-8096a1433bde
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 424b325b244499a18077cc1df0ff9164c41763d2
ms.sourcegitcommit: ca777040ca372014b9af5e188d9b60bf56e3e36f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85815456"
---
# <a name="how-to-create-an-xml-document-based-on-an-xsd-schema"></a>如何：基于 XSD 架构创建 XML 文档

“生成示例 XML”功能基于 XML 架构 (XSD) 文件生成示例 XML 文件。

可以在下列情况下使用此选项：

- 了解架构中各个构造的使用情况。

- 确认架构发挥了应有的作用。

“生成示例 XML”功能仅对全局元素可用，而且需要有效的 XML 架构集。

此功能通常会生成有效的 XML 文档。 但是，如果架构包含下列一项或多项内容，示例可能无效：

- `xs:key`、`xs:keyref` 和 `xs:unique` 标识约束。

- `xs:pattern` Facet。

- `xs:QName` 类型的枚举。

- `xs:ENTITY`、`xs:ENTITIES` 和 `xs:NOTATION` 类型。

另请注意，只有当架构中发生 `xs:base64Binary` 类型的枚举时，才会生成同类型的内容。

## <a name="to-generate-an-xml-instance-document-based-on-the-xsd-file"></a>基于 XSD 文件生成 XML 实例文档

1. 按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 在 [XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)中，右键单击 `PurchaseOrder` 全局元素。 选择“生成示例 XML”。

     选择此选项后，将生成具有以下示例 XML 内容的 PurchaseOrder.xml 文件并在 XML 编辑器中打开该文件：

    ```xml
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
