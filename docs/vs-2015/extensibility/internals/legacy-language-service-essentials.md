---
title: 旧版语言服务基础知识 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
caps.latest.revision: 22
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a3926ff84f3b2e6415df1ca7333409c05d839685
ms.sourcegitcommit: 47eeeeadd84c879636e9d48747b615de69384356
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63436267"
---
# <a name="legacy-language-service-essentials"></a>旧版语言服务基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

必须提供要集成到 Visual Studio 编程语言的语言服务。 本主题介绍在旧版语言服务中提供的功能。  
  
 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。  
  
> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。  
  
 旧版语言服务提供以下功能：  
  
|功能|描述|  
|-------------|-----------------|  
|语法着色|将导致编辑器视图以显示不同颜色和字体样式的一种语言的不同元素。 此优势使其更易于阅读和编辑文件。<br /><br /> 有关常规信息，请参阅[语法突出显示旧版语言服务中](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。<br /><br /> 有关在托管的包框架 (MPF) 此功能的信息，请参阅[旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。|  
|语句结束|完成的语句或用户已开始键入关键字。 语句完成可帮助用户更轻松地输入困难的语句，减少键入和更少的出错机会。<br /><br /> 有关常规信息，请参阅[旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。<br /><br /> MPF 中此功能的信息，请参阅[旧版语言服务中的文字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)。|  
|大括号匹配|突出显示成对大括号等字符。 当用户键入结束字符如"}"，大括号匹配突出显示相应的开始字符，如"{"。 当存在多个级别的封闭字符时，此功能可帮助用户确认正确配对的封闭字符。<br /><br /> MPF 中此功能的信息，请参阅[旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。|  
|参数信息工具提示|显示可能的用户当前正在键入的重载方法签名中的列表。<br /><br /> 有关常规信息，请参阅[旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。<br /><br /> MPF 中此功能的信息，请参阅[旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)。|  
|错误标记|显示红色的波浪下划线，也称为波浪线下语法不正确的文本。 错误标记通常用于使用户意识到拼错的关键字、 不完整的括号、 无效字符和类似的错误。<br /><br /> 错误标记中自动处理 MPF 类中<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A>方法的<xref:Microsoft.VisualStudio.Package.AuthoringSink>类。|  
  
 许多这些功能需要语言服务以分析源代码。 您通常可以重复使用词汇切分和分析你的编译器或解释器的代码。  
  
 以下功能与相关的编程语言的支持，但不语言服务的一部分：  
  
|功能|描述|  
|-------------|-----------------|  
|表达式计算器|支持[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]要显示在通过验证断点并提供一系列表达式调试器**自动**调试窗口。<br /><br /> 有关详细信息，请参阅[以便进行调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)。|  
|符号浏览工具|支持**对象浏览器**，**类视图**，**调用浏览器**，以及**查找符号结果**。|
