---
title: XML 代码片断
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c261893b50a217d888300ca01f3bc190bc065c94
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72658761"
---
# <a name="xml-snippets"></a>XML 代码片断

XML 编辑器提供了一个称为*xml 代码段*的功能，使您能够更快地生成 xml 文件。 XML 代码段可以通过插入文件反复使用。 您还可以根据 XML 架构定义语言（XSD）架构生成 XML 数据。

## <a name="reusable-xml-snippets"></a>可重用的 XML 代码段

XML 编辑器包含许多涵盖一些常见任务的代码段。 这样，您更容易创建 XML 文件。 例如，如果您正在创作 XML 架构，则使用 "复杂类型序列元素" 和 "简单类型元素" 代码段将以下 XML 文本插入到您的文件中。 然后，根据您的需要更改 `name` 值。

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

可以通过两种方法插入代码段。 "**插入代码段**" 命令将 XML 代码段插入到光标位置。 "**环绕**" 命令环绕所选文本周围的 XML 代码段。 通过 "**编辑**" 菜单下的 " **IntelliSense** " 子菜单或编辑器中的右键单击菜单，可以使用这两个命令。

有关详细信息，请参阅[如何：使用 XML 代码段](../xml-tools/how-to-use-xml-snippets.md)。

## <a name="schema-generated-xml-snippets"></a>架构生成的 XML 代码段

"XML 编辑器" 还可以从 XML 架构生成 XML 代码段。 通过此功能可以使用从该元素的架构信息生成的 XML 元素来填充元素。 有关详细信息，请参阅[如何：从 xml 架构生成 xml 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)。

## <a name="create-new-xml-snippets"></a>创建新的 XML 代码段

除了默认情况下随 Visual Studio 提供的代码段之外，你还可以创建并使用自己的 XML 代码段。 有关详细信息，请参阅[如何：创建 XML 代码段](../xml-tools/how-to-create-xml-snippets.md)。

## <a name="see-also"></a>请参阅

- [Visual Studio 中的代码片段](../ide/code-snippets.md)
- [XML 编辑器](../xml-tools/xml-editor.md)