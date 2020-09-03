---
title: 旧版语言服务中的单词完成 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "80703164"
---
# <a name="word-completion-in-a-legacy-language-service"></a>旧版语言服务中的文字完成
单词完成填写部分类型的单词上缺少的字符。 如果只有一个可能的完成，则在输入完成字符时将完成单词。 如果部分单词匹配多个可能的完成，则会显示一个可能的完成列表。 完成字符可以是任何不用于标识符的字符。

 旧版语言服务是作为 VSPackage 的一部分实现的，但实现语言服务功能的更新方法是使用 MEF 扩展。 若要了解详细信息，请参阅 [扩展编辑器和语言服务](../../extensibility/extending-the-editor-and-language-services.md)。

> [!NOTE]
> 建议你尽快开始使用新的编辑器 API。 这将提高语言服务的性能，并使你能够利用新的编辑器功能。

## <a name="implementation-steps"></a>实现步骤

1. 当用户从**IntelliSense**菜单中选择 "**完成单词**" 时，该 <xref:Microsoft.VisualStudio.VSConstants.VSStd2KCmdID> 命令将发送到语言服务。

2. <xref:Microsoft.VisualStudio.Package.ViewFilter>类捕获命令并调用 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 方法，分析原因为 <xref:Microsoft.VisualStudio.Package.ParseReason> 。

3. <xref:Microsoft.VisualStudio.Package.Source>然后，类调用 <xref:Microsoft.VisualStudio.Package.LanguageService.ParseSource%2A> 方法来获取可能的单词完成列表，然后使用类在工具提示列表中显示单词 <xref:Microsoft.VisualStudio.Package.CompletionSet> 。

    如果只有一个匹配的单词，则 <xref:Microsoft.VisualStudio.Package.Source> 类完成单词。

   或者，如果在 <xref:Microsoft.VisualStudio.Package.TokenTriggers> 输入标识符的第一个字符时扫描程序返回触发器值，则类会 <xref:Microsoft.VisualStudio.Package.Source> 检测到这种情况，并调用 <xref:Microsoft.VisualStudio.Package.Source.Completion%2A> 方法，分析原因为 <xref:Microsoft.VisualStudio.Package.ParseReason> 。 在这种情况下，分析器必须检测是否存在成员选择字符并提供成员列表。

## <a name="enabling-support-for-the-complete-word"></a>启用对完整单词的支持
 若要启用对 word 完成的支持，请设置 `CodeSense` 传递到 <xref:Microsoft.VisualStudio.Shell.ProvideLanguageServiceAttribute> 与语言包关联的用户属性的命名参数。 这将设置 <xref:Microsoft.VisualStudio.Package.LanguagePreferences.EnableCodeSense%2A> 类的属性 <xref:Microsoft.VisualStudio.Package.LanguagePreferences> 。

 <xref:Microsoft.VisualStudio.Package.ParseReason>要使 word 完成操作正常运行，分析器必须返回一个声明列表以响应分析原因值。

## <a name="implementing-complete-word-in-the-parsesource-method"></a>在 ParseSource 方法中实现完整的单词
 对于 word 完成， <xref:Microsoft.VisualStudio.Package.Source> 类对类调用 <xref:Microsoft.VisualStudio.Package.AuthoringScope.GetDeclarations%2A> 方法， <xref:Microsoft.VisualStudio.Package.AuthoringScope> 以获取可能的单词匹配项的列表。 必须在派生自类的类中实现列表 <xref:Microsoft.VisualStudio.Package.Declarations> 。 <xref:Microsoft.VisualStudio.Package.Declarations>有关必须实现的方法的详细信息，请参阅类。

 如果列表只包含一个单词，则 <xref:Microsoft.VisualStudio.Package.Source> 类会自动将该单词插入到部分单词的位置。 如果列表包含多个单词，则类将 <xref:Microsoft.VisualStudio.Package.Source> 显示一个工具提示列表，用户可从中选择合适的选项。

 另请查看在 <xref:Microsoft.VisualStudio.Package.Declarations> [旧版语言服务中的成员完成](../../extensibility/internals/member-completion-in-a-legacy-language-service.md)中的类实现的示例。
