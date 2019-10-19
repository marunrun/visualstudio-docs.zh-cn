---
title: 如何：基于 XSD 架构创建 XML 文档
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 193b195f-e918-4c79-a1a1-8096a1433bde
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 1f423af7dc4fae7a116acbaf8497c5ee4268653e
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645977"
---
# <a name="how-to-create-an-xml-document-based-on-an-xsd-schema"></a>如何：基于 XSD 架构创建 XML 文档

"**生成示例 xml** " 功能根据 xml 架构（XSD）文件生成一个示例 xml 文件。

可以在下列情况下使用此选项：

- 了解架构中各个构造的使用情况。

- 确认架构发挥了应有的作用。

"**生成示例 XML** " 功能仅适用于全局元素，需要一个有效的 XML 架构集。

此功能通常会生成有效的 XML 文档。 但是，如果架构包含下列一项或多项内容，示例可能无效：

- `xs:key`、`xs:keyref` 和 `xs:unique` 标识约束。

- `xs:pattern` 方面。

- `xs:QName` 类型的枚举。

- `xs:ENTITY`、`xs:ENTITIES` 和 `xs:NOTATION` 类型。

另请注意，只有当架构中发生 `xs:base64Binary` 类型的枚举时，才会生成同类型的内容。

## <a name="to-generate-an-xml-instance-document-based-on-the-xsd-file"></a>基于 XSD 文件生成 XML 实例文档

1. 按照[如何：创建和编辑 XSD 架构文件](../xml-tools/how-to-create-and-edit-an-xsd-schema-file.md)中的步骤操作。

2. 在[XML 架构资源管理器](../xml-tools/xml-schema-explorer.md)中，右键单击 `PurchaseOrder` 全局元素。 选择 "**生成示例 XML**"。

     选择此选项时，PurchaseOrder。将在 XML 编辑器中生成并打开包含以下示例 XML 内容的*xml*文件：

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