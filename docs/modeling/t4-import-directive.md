---
title: T4 导入指令
ms.date: 11/04/2016
ms.topic: reference
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2a28bedd01e3a4f6a7a87b025ac9a9a6184da9b2
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/01/2020
ms.locfileid: "75591861"
---
# <a name="t4-import-directive"></a>T4 导入指令

在 Visual Studio T4 文本模板的代码块中，`import` 指令允许你引用另一个命名空间中的元素，而无需提供完全限定的名称。 它等效于 C# 中的 `using` 或 `imports` 中的 [!INCLUDE[vb_current_short](../debugger/includes/vb_current_short_md.md)]。

有关编写 T4 文本模板的一般概述，请参阅[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)。

## <a name="using-the-import-directive"></a>使用 Import 指令

```
<#@ import namespace="namespace" #>
```

 在此示例中，模板代码可为 System.IO 的成员省略显式命名空间：

```
<#@ import namespace="System.IO" #>
<#
   string fileContent = File.ReadAllText("C:\x.txt"); // System.IO.File
#>
The file contains: <#=  fileContent #>
```

## <a name="standard-imports"></a>标准导入
 将自动导入以下命名空间，您无需为其编写导入指令：

- `System`

  另外，如果您使用自定义指令，则指令处理器可能会自动导入一些命名空间。

  例如，如果您为域特定语言 (DSL) 编写模板，则无需为下列命名空间编写导入指令：

- `Microsoft.VisualStudio.Modeling`

- DSL 的命名空间

## <a name="see-also"></a>另请参阅

- [T4 程序集指令](../modeling/t4-assembly-directive.md)
