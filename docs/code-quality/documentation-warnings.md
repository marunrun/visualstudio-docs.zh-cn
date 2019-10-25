---
title: 文档警告
ms.date: 09/16/2019
ms.topic: reference
f1_keywords:
- vs.codeanalysis.documentationrules
helpviewer_keywords:
- documentation warnings
- managed code analysis warnings, documentation warnings
- warnings, documentation
author: mavasani
ms.author: mavasani
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 4946c69bbbe4bf1c240967ebd93ef58cfa79e333
ms.sourcegitcommit: 8589d85cc10710ef87e6363a2effa5ee5610d46a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/23/2019
ms.locfileid: "72807108"
---
# <a name="documentation-warnings"></a>文档警告

文档警告支持通过正确使用适用于外部可见 Api 的[XML 文档注释](/dotnet/csharp/codedoc)来编写记录良好的库。

## <a name="in-this-section"></a>本节内容

| 规则 | 描述 |
| - | - |
| [CA1200：避免使用带有前缀的 cref 标记](../code-quality/ca1200.md) | XML 文档标记中的[cref](/dotnet/csharp/programming-guide/xmldoc/cref-attribute)特性表示 "代码引用"。 它指定标记的内部文本是一个代码元素，例如类型、方法或属性。 避免使用带有前缀的 `cref` 标记，因为这会阻止编译器验证引用。 它还可防止 Visual Studio 集成开发环境（IDE）在重构期间查找和更新这些符号引用。 |

## <a name="see-also"></a>请参阅

- [代码分析警告](../code-quality/code-analysis-for-managed-code-warnings.md)
