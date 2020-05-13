---
title: 传统语言服务中的字完成 |微软文档
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 948751cde5b6b710d911a30ca26a61e5411bba4d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703164"
---
# <a name="word-completion-in-a-legacy-language-service"></a>旧版语言服务中的文字完成
单词完成将填充部分键入的单词上缺少的字符。 如果只有一个可能的完成，则输入完成字符时，该单词将完成。 如果部分单词与多个可能性匹配，将显示可能完成的列表。 完成字符可以是不用于标识符的任何字符。

 旧语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的较新方法是使用 MEF 扩展。 要了解更多信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议您尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并允许您利用新的编辑器功能。

## <a name="implementation-steps"></a>实施步骤

1. 当用户从 **"IntelliSense"** 菜单中选择 **"完整字"** 时，<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>该命令将发送到语言服务。

2. 类<xref:Microsoft.VisualStudio.Package.ViewFilter>捕获命令，用 的解析<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>原因调用 方法<xref:Microsoft.VisualStudio.Package.ParseReason>。

3. 然后<xref:Microsoft.VisualStudio.Package.Source>，<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>类调用 方法获取可能的单词完成的列表，然后使用 类<xref:Microsoft.VisualStudio.Package.CompletionSet>在工具提示列表中显示单词。

    如果只有一个匹配的单词，则<xref:Microsoft.VisualStudio.Package.Source>类将完成该单词。

   或者，如果扫描程序在键入标识符的第<xref:Microsoft.VisualStudio.Package.TokenTriggers>一个字符时返回触发器值，<xref:Microsoft.VisualStudio.Package.Source>则类将检测此值，并调用 具有<xref:Microsoft.VisualStudio.Package.Source.Completion%2A><xref:Microsoft.VisualStudio.Package.ParseReason>的解析原因的方法。 在这种情况下，解析器必须检测成员选择字符的存在并提供成员列表。

## <a name="enabling-support-for-the-complete-word"></a>启用对完整字的支持
 要启用对单词完成的支持，将`CodeSense`命名参数传递给与语言<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>包关联的用户属性。 这将在<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>类上<xref:Microsoft.VisualStudio.Package.LanguagePreferences>设置属性。

 解析器必须返回声明列表以响应解析原因值<xref:Microsoft.VisualStudio.Package.ParseReason>，以便单词完成才能操作。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>在 ParseSource 方法中实现完整单词
 对于单词完成，<xref:Microsoft.VisualStudio.Package.Source>类调用<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A><xref:Microsoft.VisualStudio.Package.AuthoringScope>类上的方法以获取可能的单词匹配的列表。 必须在派生自类的<xref:Microsoft.VisualStudio.Package.Declarations>类中实现该列表。 有关必须<xref:Microsoft.VisualStudio.Package.Declarations>实现的方法的详细信息，请参阅 该类。

 如果列表仅包含一个单词，则<xref:Microsoft.VisualStudio.Package.Source>类会自动插入该单词以代替部分单词。 如果列表包含多个单词，则<xref:Microsoft.VisualStudio.Package.Source>类将显示一个工具提示列表，用户可以从中选择适当的选项。

 还要查看<xref:Microsoft.VisualStudio.Package.Declarations>[旧语言服务中成员完成中的](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)类实现示例。
