---
title: XML 代码段 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 348dbf64-3f09-4fff-b47a-a7ecdf3221cc
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 5bc8946d62f47291a6e0e3f26032589bfdf0de16
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72669361"
---
# <a name="xml-snippets"></a>XML 代码片断
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML 编辑器提供了一个称为*xml 代码段*的功能，使您能够更快地生成 xml 文件。 XML 代码段可以通过插入文件反复使用。 您还可以根据 XML 架构定义语言 (XSD) 架构生成 XML 数据。

## <a name="reusable-xml-snippets"></a>可反复使用的 XML 代码段
 “XML 编辑器”包括许多代码段，用于执行一些常见的任务。 这样，您更容易创建 XML 文件。 例如，如果编写 XML 架构，使用“复杂类型序列元素”和“简单类型元素”代码段将以下 XML 文本插入文件。 然后，根据您的需要更改 `name` 值。

```
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

 可以通过两种方法插入代码段。 "**插入代码段**" 命令将 XML 代码段插入到光标位置。 "**环绕**" 命令环绕所选文本周围的 XML 代码段。 这两个命令都可以通过 "**编辑**" 菜单下的 " **IntelliSense** " 子菜单或编辑器快捷菜单。

 有关详细信息，请参阅[如何：使用 XML 代码段](../xml-tools/how-to-use-xml-snippets.md)。

## <a name="schema-generated-xml-snippets"></a>从架构生成的 XML 代码段
 “XML 编辑器”还可以从 XML 架构生成 XML 代码段。 通过此功能可以使用从该元素的架构信息生成的 XML 元素来填充元素。

 有关详细信息，请参阅[如何：从 Xml 架构生成 Xml 代码段](../xml-tools/how-to-generate-an-xml-snippet-from-an-xml-schema.md)。

## <a name="create-new-xml-snippets"></a>新建 XML 代码段
 除了默认情况下随 [!INCLUDE[msCoName](../includes/msconame-md.md)] Visual Studio 提供的代码段之外，您还可以创建并使用自己的 XML 代码段。

 有关详细信息，请参阅[如何：创建 XML 代码段](../xml-tools/how-to-create-xml-snippets.md)。

## <a name="see-also"></a>请参阅
 [XML 编辑器](../xml-tools/xml-editor.md)
