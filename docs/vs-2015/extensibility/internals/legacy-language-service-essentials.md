---
title: 旧版语言服务基本知识 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "90840344"
---
# <a name="legacy-language-service-essentials"></a>旧版语言服务基础知识
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

必须提供语言服务才能将编程语言集成到 Visual Studio 中。 本主题介绍旧版语言服务中的可用功能。  
  
 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解有关实现语言服务的新方法的详细信息，请参阅 [编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。  
  
> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。  
  
 旧版语言服务提供以下功能：  
  
|Feature|说明|  
|-------------|-----------------|  
|语法着色|使编辑器视图为语言的不同元素显示不同的颜色和字体样式。 这种差异可以更轻松地读取和编辑文件。<br /><br /> 有关一般信息，请参阅 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。<br /><br /> 有关 (MPF) 的托管包框架中此功能的信息，请参阅 [旧版语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。|  
|语句结束|完成用户已开始键入的语句或关键字。 语句完成可帮助用户更轻松地输入困难的语句，但键入的内容更少，并且出错的几率更少。<br /><br /> 有关一般信息，请参阅 [旧版语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。<br /><br /> 有关 MPF 中此功能的信息，请参阅 [旧版语言服务中的 Word 完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)。|  
|大括号匹配|突出显示成对字符，如大括号。 当用户键入一个结束字符（如 "}"）时，大括号匹配会突出显示相应的开始字符，如 "{"。 当存在多个级别的封闭字符时，此功能可帮助用户确认封闭字符是否配对正确。<br /><br /> 有关 MPF 中此功能的信息，请参阅 [旧版语言服务中的大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)。|  
|参数信息工具提示|显示用户当前正在键入的重载方法的可能签名列表。<br /><br /> 有关一般信息，请参阅 [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。<br /><br /> 有关 MPF 中此功能的信息，请参阅 [旧版语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)。|  
|错误标记|在语法不正确的文本下显示红色波浪下划线（也称为曲线）。 错误标记通常用于使用户了解拼写错误的关键字、未闭合的括号、无效字符和类似错误。<br /><br /> 在多功能进纸器类中，在类的方法中自动处理错误标记 <xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A> <xref:Microsoft.VisualStudio.Package.AuthoringSink> 。|  
  
 其中许多功能都需要语言服务来分析源代码。 通常可以重复使用编译器或解释器的词汇切分和分析代码。  
  
 以下功能与对编程语言的支持相关，但并不是语言服务的一部分：  
  
|Feature|说明|  
|-------------|-----------------|  
|表达式计算器|[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]通过验证断点并提供要在 "自动调试" 窗口中显示的表达式的**Autos**列表来支持调试器。<br /><br /> 有关详细信息，请参阅 [语言服务支持以进行调试](../../extensibility/internals/language-service-support-for-debugging.md)。|  
|符号浏览工具|支持 **对象浏览器**、 **类视图**、 **调用浏览器**和 **查找符号结果**。|
