---
title: 传统语言服务要点 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- languages, integrating into Visual Studio
- language services, integrating programming languages
- Visual Studio, integrating programming languages
- programming languages, integrating into Visual Studio
ms.assetid: c15e0ccb-e7c5-4dbb-affb-fe3d3244debe
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 501bccf755293e86e8a9dc23fce125a10c882376
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80707422"
---
# <a name="legacy-language-service-essentials"></a>旧版语言服务基础知识
您必须提供语言服务，以便将编程语言集成到 Visual Studio 中。 本主题介绍旧语言服务中可用的功能。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解有关实现语言服务的新方法的详细信息，请参阅[编辑器和语言服务扩展](../../extensibility/editor-and-language-service-extensions.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

 传统语言服务提供以下功能：

|Feature|说明|
|-------------|-----------------|
|语法着色|使编辑器视图显示不同语言元素的不同颜色和字体样式。 这种区别可以使读取和编辑文件变得更加容易。<br /><br /> 有关一般信息，请参阅[旧语言服务中的语法着色](../../extensibility/internals/syntax-coloring-in-a-legacy-language-service.md)。<br /><br /> 有关托管包框架 （MPF） 中此功能的信息，请参阅[旧语言服务中的语法着色](../../extensibility/internals/syntax-colorizing-in-a-legacy-language-service.md)。|
|语句结束|完成用户已开始键入的语句或关键字。 语句完成可帮助用户更轻松地输入困难语句，减少键入次数和错误机会。<br /><br /> 有关一般信息，请参阅[旧语言服务中的语句完成](../../extensibility/internals/statement-completion-in-a-legacy-language-service.md)。<br /><br /> 有关 MPF 中此功能的信息，请参阅[旧语言服务中的字完成](../../extensibility/internals/word-completion-in-a-legacy-language-service.md)。|
|大括号匹配|突出显示配对的字符，如大括号。 当用户键入结束字符（如"*"）时，大括号匹配将突出显示相应的开口字符，如"*"。 当包含字符有多个级别时，此功能可帮助用户确认封闭字符正确配对。<br /><br /> 有关 MPF 中此功能的信息，请参阅[旧语言服务中的"大括号匹配](../../extensibility/internals/brace-matching-in-a-legacy-language-service.md)"。|
|参数信息工具提示|显示用户当前键入的重载方法的可能签名的列表。<br /><br /> 有关一般信息，请参阅[旧语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service1.md)。<br /><br /> 有关 MPF 中此功能的信息，请参阅[旧语言服务中的参数信息](../../extensibility/internals/parameter-info-in-a-legacy-language-service2.md)。|
|错误标记|在语法不正确的文本下显示波浪红色下划线，也称为波浪形下划线。 错误标记通常用于使用户了解拼写错误的关键字、未闭合括号、无效字符和类似的错误。<br /><br /> 在 MPF 类中，错误标记在<xref:Microsoft.VisualStudio.Package.AuthoringSink.AddError%2A><xref:Microsoft.VisualStudio.Package.AuthoringSink>类的方法中自动处理。|

 其中许多功能需要语言服务来分析源代码。 通常，您可以为编译器或解释器重用标记和解析代码。

 以下功能与对编程语言的支持相关，但不是语言服务的一部分：

| Feature | 说明 |
|-----------------------| - |
| 表达式赋值器 | 通过验证[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]断点并提供要在**Autos**调试窗口中显示的表达式列表，支持调试器。<br /><br /> 有关详细信息，请参阅[调试的语言服务支持](../../extensibility/internals/language-service-support-for-debugging.md)。 |
| 符号浏览工具 | 支持**对象浏览器**、**类视图**、**调用浏览器**和**查找符号结果**。 |
