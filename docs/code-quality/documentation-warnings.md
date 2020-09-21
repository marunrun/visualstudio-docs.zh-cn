---
title: 文档规则
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation rules
- managed code analysis rules, documentation rules
- rules, documentation
author: mavasani
ms.author: mavasani
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5f4ec6a0dd154dae89145add26c60a8b1322a444
ms.sourcegitcommit: 566144d59c376474c09bbb55164c01d70f4b621c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/19/2020
ms.locfileid: "90808647"
---
# <a name="documentation-rules"></a>文档规则

文档规则支持通过对外部可见 Api 使用正确的 [XML 文档注释](/dotnet/csharp/codedoc) 来编写正确的库。

## <a name="in-this-section"></a>在本节中

| 规则 | 描述 |
| - | - |
| [CA1200:不要使用带前缀的 cref 标记](../code-quality/ca1200.md) | XML 文档标记中的 [cref](/dotnet/csharp/programming-guide/xmldoc/cref-attribute) 特性表示 "代码引用"。 它指定标记的内部文本是一个代码元素，例如类型、方法或属性。 避免使用 `cref` 带有前缀的标记，因为这会阻止编译器验证引用。 它还可防止 Visual Studio 集成开发环境 (IDE) 在重构期间查找和更新这些符号引用。 |

## <a name="see-also"></a>另请参阅

- [代码分析规则](../code-quality/code-analysis-for-managed-code-warnings.md)
