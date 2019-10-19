---
title: 创建 XML 架构
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 1d6700a9-fd67-4794-8997-399589e99bec
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 73563d732aab48192892794c15750bc9e5d3eb6a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2019
ms.locfileid: "72645965"
---
# <a name="how-to-create-an-xml-schema-from-an-xml-document"></a>如何：从 XML 文档创建 XML 架构

使用 "XML 编辑器" 可以从 XML 文档创建 XML 架构定义语言（XSD）架构。 该 XML 文件通过以下方式确定如何生成架构：

- 如果 XML 文档没有关联的架构或文档类型定义 (DTD)，将使用 XML 文档中的数据推断新的 XML 架构。

- 如果 XML 文档包含关联的 DTD，外部 DTD 和内部子集将转换为相应的 XML 架构。

- 如果 XML 文档包含内联的 XML 数据简化 (XDR) 架构，XDR 架构将转换为相应的 XML 架构。

然后，将使用创建的架构为 XML 文件提供 IntelliSense。

有关架构推断引擎的详细信息，请参阅[推断 XML 架构](/dotnet/standard/data/xml/inferring-an-xml-schema)。

## <a name="to-create-an-xml-schema"></a>若要创建 XML 架构

1. 在 Visual Studio 中打开 XML 文件。

2. 在菜单栏上，选择 " **XML**  > **创建架构**"。

   将为 XML 文件中找到的每个命名空间创建并打开 XML 架构文档。 每个架构作为临时的杂项文件打开。 架构可以保存到磁盘中、添加到项目中或丢弃。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)