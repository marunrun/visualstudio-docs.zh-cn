---
title: 创建 XML 架构
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 1d6700a9-fd67-4794-8997-399589e99bec
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0e93155f230ee4a564116f5d1357a97923706c36
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62783488"
---
# <a name="how-to-create-an-xml-schema-from-an-xml-document"></a>如何：基于XML 文档创建 XML 架构

XML 编辑器，可以从 XML 文档创建 XML 架构定义语言 (XSD) 架构。 XML 文件确定如何按以下方式生成架构：

- 如果 XML 文档没有关联的架构或文档类型定义 (DTD)，将使用 XML 文档中的数据推断新的 XML 架构。

- 如果 XML 文档包含关联的 DTD，外部 DTD 和内部子集将转换为相应的 XML 架构。

- 如果 XML 文档包含内联的 XML 数据简化 (XDR) 架构，XDR 架构将转换为相应的 XML 架构。

创建架构然后用于为 XML 文件提供 IntelliSense。

有关架构推断引擎的详细信息，请参阅[推断 XML 架构](/dotnet/standard/data/xml/inferring-an-xml-schema)。

## <a name="to-create-an-xml-schema"></a>若要创建 XML 架构

1. 在 Visual Studio 中打开 XML 文件。

2. 在菜单栏上依次选择**XML** > **Create Schema**。

   创建并打开 XML 文件中找到每个命名空间的 XML 架构文档。 每个架构作为临时的杂项文件打开。 架构可以保存到磁盘中、添加到项目中或丢弃。

## <a name="see-also"></a>请参阅

- [XML 编辑器](../xml-tools/xml-editor.md)