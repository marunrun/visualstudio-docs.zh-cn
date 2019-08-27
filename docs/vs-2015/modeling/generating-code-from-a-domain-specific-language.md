---
title: 从域特定语言生成代码 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
ms.assetid: e3706cc9-2afd-456a-a879-68425a248ebc
caps.latest.revision: 15
author: gewarren
ms.author: gewarren
manager: jillfra
ms.openlocfilehash: 63e1b48a7582294c200b1e30147d85a9b26165d4
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "68182807"
---
# <a name="generating-code-from-a-domain-specific-language"></a>从域特定语言生成代码
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Microsoft[!INCLUDE[dsl](../includes/dsl-md.md)]提供了一种强大方法从模型中表示的数据生成代码、 文档、 配置文件和其他项目。 使用[!INCLUDE[dsl](../includes/dsl-md.md)]，可以创建一组类，表示数据，可以编写文本模板中的类名称和属性反映了该数据。  
  
 例如，Fabrikam 有客户名称和电子邮件地址的一个 XML 文件。 其开发人员创建一个模型中的客户是一个类，使用属性名称和电子邮件。 他们编写多个文本模板来处理数据，包括此代码段的 HTML 页的一部分生成的所有客户表：  
  
```  
<table>  
<# foreach (Customer c in ContactList) {  #>  
  <tr><td> <#= c.FullName #> </td>   
      <td> <#= c.EmailAddress #> </td> </tr>  
<# } #>  </table>  
```  
  
 处理客户数据库时，XML 文件读取到模型存储区中。 一个*指令处理器*、 创建使用[!INCLUDE[dsl](../includes/dsl-md.md)]，使客户类可供代码中的文本模板。 可以针对相同的存储区运行多个文本模板。  
  
 文本模板对至关重要[!INCLUDE[dsl](../includes/dsl-md.md)]。 它们用于生成的 VSPackage 和用于将与工具集成的控件以及在域模型元素的源代码[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]。  
  
 本部分讨论的一些方法来创建、 修改和调试文本模板中使用[!INCLUDE[dsl](../includes/dsl-md.md)]。  
  
## <a name="in-this-section"></a>本节内容  
 [从文本模板访问模型](../modeling/accessing-models-from-text-templates.md)  
  
 提供有关特定于域的语言在文本模板中引用的基本信息。  
  
 [演练：调试访问模型的文本模板](../modeling/walkthrough-debugging-a-text-template-that-accesses-a-model.md)  
  
 描述如何进行故障排除和调试特定于域的语言是指在文本模板。  
  
 [演练：将主机连接到所生成的指令处理器](../modeling/walkthrough-connecting-a-host-to-a-generated-directive-processor.md)  
  
 介绍如何连接到生成的指令处理器自定义主机。  
  
 [DslTextTransform 命令](../modeling/the-dsltexttransform-command.md)  
  
 介绍引用域特定语言的文本模板在命令行执行的 TextTransform 可执行文件的命令文件。  
  
## <a name="reference"></a>参考  
 [编写 T4 文本模板](../modeling/writing-a-t4-text-template.md)  
  
 提供文本模板指令和控制块的语法。  
  
## <a name="related-sections"></a>相关章节  
 [使用 T4 文本模板生成设计时代码](../modeling/design-time-code-generation-by-using-t4-text-templates.md)  
  
 说明文本模板转换过程。  
  
 [生成过程中的代码生成](../modeling/code-generation-in-a-build-process.md)  
  
 如果要从生成服务器上的 DSL 生成的文件，请阅读本主题。
