---
title: 从域特定语言生成代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: e3706cc9-2afd-456a-a879-68425a248ebc
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 32cafb9e68fc2535ed3b570022a59d284f4c4cae
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "72666102"
---
# <a name="generating-code-from-a-domain-specific-language"></a>从域特定语言生成代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft [!INCLUDE[dsl](../includes/dsl-md.md)] 提供了一种强大的方法，可通过模型中的数据生成代码、文档、配置文件和其他项目。 使用 [!INCLUDE[dsl](../includes/dsl-md.md)] ，你可以创建一组表示数据的类，并且可以在名称和属性反映该数据的类中编写文本模板。

 例如，Fabrikam 包含一个 XML 文件，其中包含客户名称和电子邮件地址。 他们的开发人员创建一个模型，其中 Customer 为类，具有属性名称和电子邮件。 它们写入多个文本模板用于处理数据，包括此片段，该片段会生成一个表，其中包含所有客户作为 HTML 页面的一部分：

```
<table>
<# foreach (Customer c in ContactList) {  #>
  <tr><td> <#= c.FullName #> </td>
      <td> <#= c.EmailAddress #> </td> </tr>
<# } #>  </table>
```

 处理客户数据库时，会将 XML 文件读入模型存储区。 使用创建的 *指令处理器* [!INCLUDE[dsl](../includes/dsl-md.md)] 使 Customer 类可用于文本模板中的代码。 许多文本模板可针对同一个存储区运行。

 文本模板对于是必需的 [!INCLUDE[dsl](../includes/dsl-md.md)] 。 它们用于为域模型的元素，以及用于将工具与集成的 VSPackage 和控件的源代码进行生成 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。

 本部分介绍了在中创建、修改和调试所用文本模板的一些方式 [!INCLUDE[dsl](../includes/dsl-md.md)] 。

## <a name="in-this-section"></a>本节内容
 [从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)

 提供有关在文本模板中引用域特定语言的基本信息。

 [演练：调试访问模型的文本模板](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)

 介绍如何对引用域特定语言的文本模板进行故障排除和调试。

 [演练：将主机连接至生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)

 描述如何将自定义主机连接到生成的指令处理器。

 [DslTextTransform 命令](../modeling/the-dsltexttransform-command.md)

 描述在用于引用域特定语言的文本模板的命令行上执行 TextTransform 可执行文件的命令文件。

## <a name="reference"></a>参考
 [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)

 提供文本模板指令和控制块的语法。

## <a name="related-sections"></a>相关章节
 [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)

 说明文本模板转换过程。

 [生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)

 如果要在生成服务器上从 DSL 生成文件，请阅读本主题。
