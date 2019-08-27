---
title: 从域特定语言生成代码
ms.date: 11/04/2016
ms.topic: conceptual
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 37c60ed42e7d4a7604dc3d99f7e0311c7000b99c
ms.sourcegitcommit: 6a19c5ece38a70731496a38f2ef20676ff18f8a4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476512"
---
# <a name="generating-code-from-a-domain-specific-language"></a>从域特定语言生成代码

Microsoft[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]提供了一种强大方法从模型中表示的数据生成代码、 文档、 配置文件和其他项目。 使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]，可以创建一组类，表示数据，可以编写文本模板中的类名称和属性反映了该数据。

例如，Fabrikam 有客户名称和电子邮件地址的一个 XML 文件。 其开发人员创建一个模型中的客户是一个类，使用属性名称和电子邮件。 他们编写多个文本模板来处理数据，包括此代码段的 HTML 页的一部分生成的所有客户表：

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

处理客户数据库时，XML 文件读取到模型存储区中。 一个*指令处理器*、 创建使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]，使客户类可供代码中的文本模板。 可以针对相同的存储区运行多个文本模板。

文本模板对至关重要[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]。 它们用于生成的 VSPackage 和用于与 Visual Studio 集成工具的控件以及在域模型元素的源代码。

本部分讨论的一些方法来创建、 修改和调试文本模板中使用[!INCLUDE[dsl](../modeling/includes/dsl_md.md)]。

## <a name="in-this-section"></a>本节内容

[从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)\
提供有关特定于域的语言在文本模板中引用的基本信息。

[演练：调试文本模板访问模型](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)\
描述如何进行故障排除和调试特定于域的语言是指在文本模板。

[演练：将主机连接到生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)\
介绍如何连接到生成的指令处理器自定义主机。

[DslTextTransform 命令](../modeling/the-dsltexttransform-command.md)\
介绍引用域特定语言的文本模板在命令行执行的 TextTransform 可执行文件的命令文件。

## <a name="reference"></a>参考

[编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)\
提供文本模板指令和控制块的语法。

## <a name="related-sections"></a>相关章节

[使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)\
说明文本模板转换过程。

[生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)\
如果要从生成服务器上的 DSL 生成的文件，请阅读本主题。