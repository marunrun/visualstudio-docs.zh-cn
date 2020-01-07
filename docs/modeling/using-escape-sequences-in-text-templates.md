---
title: 在文本模板中使用转义序列
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- text templates, escape sequences
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 83e6e5cf163037077d0517e5f7ea460f9124f27c
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75594040"
---
# <a name="use-escape-sequences-in-text-templates"></a>在文本模板中使用转义序列

您可以在文本模板中使用转义序列来生成文本模板标记和（ C#仅在代码中）以转义控制字符和引号。

若要将标准代码块的打开和关闭标记打印到输出文件，请按如下所示对标记进行转义：

```
\<# ... \#>
```

您可以对其他文本模板指令和代码块标记执行相同的操作。

如果文本块包含用于转义文本模板标记的字符串，则可以使用以下转义序列：

- 如果文本模板标记前面有偶数个转义符（\\）字符，则模板分析器将包含一半转义符，并将序列作为文本模板标记包含在内。 例如，如果文本模板中有四个转义符，则生成的文件中将有两个 "\\" 字符。

- 如果文本模板标记前面有奇数个转义符（\\）字符，则模板分析器将包含一半的 "\\" 字符以及标记本身（\<# 或 # >）。 标记不被视为文本模板标记。

- 如果转义（\\）字符出现在除转义控制字符或引号（仅在中C# ）的任何序列中的任何其他位置，则将直接输出该字符。

## <a name="see-also"></a>另请参阅

- [如何：使用转义序列基于模板生成模板](../modeling/how-to-generate-templates-from-templates-by-using-escape-sequences.md)
