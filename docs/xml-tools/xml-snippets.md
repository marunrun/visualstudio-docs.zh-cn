---
title: XML 代码片断
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 66736431b295f974bda1ca855d88cd5f5f868e7d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807710"
---
# <a name="xml-snippets"></a>XML 代码片断

XML 编辑器提供一种功能，称为*XML 代码段*，这样可以更快地生成 XML 文件。 XML 代码段可以通过插入文件反复使用。 此外可以生成基于 XML 架构定义语言 (XSD) 架构的 XML 数据。

## <a name="reusable-xml-snippets"></a>可重复使用的 XML 代码段

XML 编辑器包括很多代码段，用于某些常见任务。 这样，您更容易创建 XML 文件。 例如，如果编写 XML 架构，使用"复杂类型序列元素"和"简单类型元素"代码段插入到你的文件的以下 XML 文本。 然后，根据您的需要更改 `name` 值。

```xml
<xs:element name="name">
  <xs:complexType>
    <xs:sequence>
      <xs:element name="name">
        <xs:simpleType>
          <xs:restriction base="xs:string"></xs:restriction>
        </xs:simpleType>
      </xs:element>
    </xs:sequence>
  </xs:complexType>
</xs:element>
```

可以通过两种方法插入代码段。 **插入代码段**命令将在光标位置处插入 XML 代码段。 **Surround With**命令包装所选文本环绕 XML 代码段。 这两个命令均可以从**智能感知**子菜单下的**编辑**菜单中，或在编辑器中右键单击菜单。

有关详细信息，请参阅[如何：使用 XML 代码段](../xml-tools/how-to-use-xml-snippets.md)。

## <a name="schema-generated-xml-snippets"></a>架构生成 XML 代码段

XML 编辑器还具有从 XML 架构生成 XML 代码段的功能。 通过此功能可以使用从该元素的架构信息生成的 XML 元素来填充元素。 有关详细信息，请参阅[如何：从 XML 架构生成 XML 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)。

## <a name="create-new-xml-snippets"></a>新建 XML 代码段

除了默认情况下包含在 Visual Studio 的代码段，还可以创建和使用你自己的 XML 代码段。 有关详细信息，请参阅[如何：创建 XML 代码段](../xml-tools/how-to-create-xml-snippets.md)。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码片段](../ide/code-snippets.md)
- [XML 编辑器](../xml-tools/xml-editor.md)