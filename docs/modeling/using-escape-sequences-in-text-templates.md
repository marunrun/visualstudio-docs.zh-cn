---
title: 在文本模板中使用转义序列
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b48748c5c5d071e724be3ff35eca457f36385baa
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476614"
---
# <a name="use-escape-sequences-in-text-templates"></a>在文本模板中使用转义序列

在文本模板生成文本模板标记并 （在 C# 仅代码），可以使用转义序列转义控制字符和引号引起来。

若要打印的标准代码块的输出文件的打开和关闭标记，请按如下所示转义标记：

```
\<# ... \#>
```

您也可以执行同样的其他文本模板指令和代码块标记。

如果文本块包括用于转义文本模板标记的字符串，则可能会使用以下的转义序列：

- 如果文本模板标记前面有偶数个转义 (\\) 字符在模板分析器将包括半转义字符，包括为文本模板标记序列。 例如，如果文本模板中有四个转义符，将有两个"\\"生成文件中的字符。

- 如果文本模板标记前面有奇数数目的转义 (\\) 字符，在模板分析器将包括的下半部分"\\"字符以及标记本身 (\<# >)。 标记不被认为是一个文本模板标记。

- 如果转义符 (\\) 字符将出现在其中将转义的控制字符或引号 （在仅限 C#) 之外的任何序列中的其他任何位置，将直接输出的字符。

## <a name="see-also"></a>请参阅

- [如何：使用转义序列基于模板生成模板](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)