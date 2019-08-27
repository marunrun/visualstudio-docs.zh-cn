---
title: 在旧版语言服务中的断完成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], IntelliSense Complete Word
- IntelliSense, Complete Word
- Complete Word
ms.assetid: 0ace5ac3-f9e1-4e6d-add4-42967b1f96a6
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 26495f909d815b32ff8a75c2529ba30eabf3b5c8
ms.sourcegitcommit: 40d612240dc5bea418cd27fdacdf85ea177e2df3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/29/2019
ms.locfileid: "66309716"
---
# <a name="word-completion-in-a-legacy-language-service"></a>旧版语言服务中的文字完成
文字自动完成填充在未完全键入单词上缺少的字符。 如果只有一个可能的完成，完成字符输入时完成单词。 如果部分单词与匹配多个可能性，显示可能的完成列表。 完成字符可以是标识符不使用任何字符。

 旧版语言服务实现 VSPackage 的一部分，但实现语言服务功能的较新方法是使用 MEF 扩展。 若要获取详细信息，请参阅[扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 我们建议在开始尽可能快地使用新编辑器 API。 这将提高您的语言服务的性能，让您充分利用新的编辑器功能。

## <a name="implementation-steps"></a>实现步骤

1. 当用户选择**完成单词**从**IntelliSense**菜单中，<xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID>命令发送到语言服务。

2. <xref:Microsoft.VisualStudio.Package.ViewFilter>类用于捕获命令以及调用<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法，分析原因为<xref:Microsoft.VisualStudio.Package.ParseReason>。

3. <xref:Microsoft.VisualStudio.Package.Source>然后类调用<xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A>方法以获取可能的单词补全和显示工具提示中的单词列表使用的列表<xref:Microsoft.VisualStudio.Package.CompletionSet>类。

    如果只有一个匹配的单词，<xref:Microsoft.VisualStudio.Package.Source>类完成单词。

   或者，如果扫描程序返回触发器值<xref:Microsoft.VisualStudio.Package.TokenTriggers>标识符的第一个字符键入时，<xref:Microsoft.VisualStudio.Package.Source>检测到此类，并调用<xref:Microsoft.VisualStudio.Package.Source.Completion%2A>方法，分析原因为<xref:Microsoft.VisualStudio.Package.ParseReason>。 在这种情况下分析器必须检测存在成员选择字符，并提供成员的列表。

## <a name="enabling-support-for-the-complete-word"></a>启用了完整的字词的支持
 若要启用对 word 完成项集合的支持`CodeSense`名为参数传递给<xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute>与语言包相关联的用户属性。 这将设置<xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A>属性上的<xref:Microsoft.VisualStudio.Package.LanguagePreferences>类。

 您的分析程序必须返回声明的列表，以响应分析原因值<xref:Microsoft.VisualStudio.Package.ParseReason>，对于文字自动完成操作。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>ParseSource 方法中实现完成单词
 对于文字自动完成<xref:Microsoft.VisualStudio.Package.Source>类调用<xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A>方法<xref:Microsoft.VisualStudio.Package.AuthoringScope>类来获取可能的字匹配项的列表。 必须在从派生类中实现列表<xref:Microsoft.VisualStudio.Package.Declarations>类。 请参阅<xref:Microsoft.VisualStudio.Package.Declarations>类必须实现的方法的详细信息。

 如果列表包含仅一个词，则<xref:Microsoft.VisualStudio.Package.Source>类自动插入这个词来代替部分单词。 如果列表包含多个词语，<xref:Microsoft.VisualStudio.Package.Source>类显示一个工具提示列表，用户可以从中选择适当的选择。

 此外看的示例<xref:Microsoft.VisualStudio.Package.Declarations>中的类实现[旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)。